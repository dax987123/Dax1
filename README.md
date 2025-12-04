<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Simple To‑Do App</title>
  <style>
    :root{--bg:#f7f9fc;--card:#ffffff;--accent:#2563eb;--muted:#6b7280}
    *{box-sizing:border-box}
    body{font-family:Inter, system-ui, -apple-system, Arial; margin:0;background:var(--bg);color:#0f1724}
    .wrap{max-width:900px;margin:28px auto;padding:20px}
    header{display:flex;align-items:center;justify-content:space-between}
    h1{margin:0;font-size:20px}
    .card{background:var(--card);border-radius:12px;padding:18px;box-shadow:0 6px 20px rgba(15,23,36,0.06)}

    .input-row{display:flex;gap:10px;margin-top:14px}
    input[type="text"]{flex:1;padding:10px;border:1px solid #e6eef6;border-radius:8px;font-size:15px}
    button{background:var(--accent);color:white;border:none;padding:10px 14px;border-radius:8px;font-weight:700;cursor:pointer}
    button.secondary{background:transparent;border:1px solid rgba(15,23,36,0.06);color:var(--muted);font-weight:600}

    .filters{display:flex;gap:8px;flex-wrap:wrap;margin-top:12px}
    .filters button{background:transparent;border:1px solid #e6eef6;padding:6px 10px;border-radius:999px}

    .todo-list{margin-top:14px;display:grid;gap:8px}
    .todo{display:flex;align-items:center;justify-content:space-between;padding:10px;border-radius:10px;border:1px solid rgba(15,23,36,0.04)}
    .left{display:flex;gap:10px;align-items:center}
    .todo input[type="checkbox"]{transform:scale(1.15)}
    .text{font-size:15px}
    .text.done{text-decoration:line-through;opacity:0.6}
    .meta{font-size:12px;color:var(--muted)}
    .actions{display:flex;gap:8px;align-items:center}
    .icon-btn{background:transparent;border:0;padding:6px;border-radius:6px;cursor:pointer}

    footer{margin-top:16px;display:flex;justify-content:space-between;color:var(--muted);font-size:13px}

    @media (max-width:600px){.input-row{flex-direction:column}button{width:100%}.filters{gap:6px}}
  </style>
</head>
<body>
  <div class="wrap">
    <header>
      <h1>Simple To‑Do App</h1>
      <div class="meta">Stores tasks in Local Storage</div>
    </header>

    <section class="card" aria-labelledby="app-desc">
      <p id="app-desc" class="meta">Add tasks, mark complete, edit, delete, and filter. Works offline in your browser.</p>

      <div class="input-row">
        <input id="taskInput" type="text" placeholder="Add a new task and press Add or Enter" aria-label="Task description" />
        <button id="addBtn">Add</button>
        <button id="clearBtn" class="secondary">Clear All</button>
      </div>

      <div class="filters" role="tablist" aria-label="Filters">
        <button data-filter="all" class="filter active">All</button>
        <button data-filter="active" class="filter">Active</button>
        <button data-filter="completed" class="filter">Completed</button>
      </div>

      <div class="todo-list" id="todoList" aria-live="polite"></div>

      <footer>
        <div id="count">0 tasks</div>
        <div class="muted">Tip: double‑click a task to edit it.</div>
      </footer>
    </section>
  </div>

  <script>
    // Simple To-Do app with Local Storage
    const taskInput = document.getElementById('taskInput');
    const addBtn = document.getElementById('addBtn');
    const clearBtn = document.getElementById('clearBtn');
    const todoList = document.getElementById('todoList');
    const count = document.getElementById('count');
    const filterBtns = document.querySelectorAll('.filter');

    let tasks = JSON.parse(localStorage.getItem('tasks') || '[]');
    let currentFilter = 'all';

    function save(){ localStorage.setItem('tasks', JSON.stringify(tasks)); }

    function render(){
      // filter tasks
      const shown = tasks.filter(t => {
        if(currentFilter === 'all') return true;
        if(currentFilter === 'active') return !t.done;
        if(currentFilter === 'completed') return t.done;
      });

      todoList.innerHTML = '';
      shown.forEach(task => {
        const el = document.createElement('div');
        el.className = 'todo';
        el.innerHTML = `
          <div class="left">
            <input type="checkbox" ${task.done? 'checked':''} data-id="${task.id}" />
            <div>
              <div class="text ${task.done? 'done':''}" data-id="${task.id}">${escapeHtml(task.text)}</div>
              <div class="meta">Created: ${new Date(task.created).toLocaleString()}</div>
            </div>
          </div>
          <div class="actions">
            <button class="icon-btn" title="Edit" data-edit="${task.id}">✏️</button>
            <button class="icon-btn" title="Delete" data-delete="${task.id}">🗑️</button>
          </div>
        `;
        // event handlers
        el.querySelector('input[type="checkbox"]').addEventListener('change', e => {
          toggleDone(task.id, e.target.checked);
        });
        el.querySelector('[data-delete]').addEventListener('click', () => removeTask(task.id));
        el.querySelector('[data-edit]').addEventListener('click', () => startEdit(task.id));
        // double click to edit text
        el.querySelector('.text').addEventListener('dblclick', () => startEdit(task.id));

        todoList.appendChild(el);
      });

      count.textContent = `${tasks.length} task${tasks.length!==1?'s':''}`;
    }

    function escapeHtml(str){ return str.replaceAll('&','&amp;').replaceAll('<','&lt;').replaceAll('>','&gt;'); }

    function addTask(text){
      const t = { id: Date.now().toString(), text: text.trim(), done:false, created: Date.now() };
      tasks.unshift(t);
      save(); render();
    }

    function removeTask(id){
      if(!confirm('Delete this task?')) return;
      tasks = tasks.filter(t => t.id !== id);
      save(); render();
    }

    function toggleDone(id, done){
      const t = tasks.find(x=>x.id===id); if(!t) return; t.done = done; save(); render();
    }

    function startEdit(id){
      const t = tasks.find(x=>x.id===id); if(!t) return;
      const newText = prompt('Edit task', t.text);
      if(newText === null) return; // cancelled
      const trimmed = newText.trim();
      if(trimmed === ''){ alert('Task cannot be empty'); return; }
      t.text = trimmed; save(); render();
    }

    // UI actions
    addBtn.addEventListener('click', () => {
      const val = taskInput.value;
      if(!val.trim()) return taskInput.focus();
      addTask(val); taskInput.value = '';
    });

    taskInput.addEventListener('keydown', e => { if(e.key === 'Enter'){ addBtn.click(); } });

    clearBtn.addEventListener('click', () => {
      if(!confirm('Clear all tasks?')) return;
      tasks = []; save(); render();
    });

    filterBtns.forEach(b => b.addEventListener('click', () => {
      filterBtns.forEach(x=>x.classList.remove('active'));
      b.classList.add('active');
      currentFilter = b.dataset.filter;
      render();
    }));

    // initialize
    render();

    // Accessibility: reduce motion
    if(window.matchMedia('(prefers-reduced-motion: reduce)').matches){
      document.documentElement.style.scrollBehavior = 'auto';
    }
  </script>
</body>
</html>
