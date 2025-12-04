<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Comprehensive Web Page Example</title>
    <style>
        /* Basic inline CSS for better visibility */
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            line-height: 1.6;
        }
        header, section, footer {
            padding: 15px;
            margin-bottom: 20px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 10px;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: left;
        }
        th {
            background-color: #f2f2f2;
        }
        form {
            background-color: #f9f9f9;
            padding: 20px;
        }
        .form-group {
            margin-bottom: 15px;
        }
        .form-group label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }
        .form-group input[type="text"],
        .form-group input[type="email"],
        .form-group textarea {
            width: calc(100% - 16px);
            padding: 8px;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
        .image-container {
            text-align: center;
        }
    </style>
</head>
<body>

    <header>
        <h1>Welcome to the Comprehensive HTML Example Page</h1>
        <p>This page showcases various essential HTML elements used in modern web development.</p>
        <nav>
            <h2>Navigation Menu</h2>
            <ul>
                <li><a href="#about">About Us</a></li>
                <li><a href="#services">Our Services</a></li>
                <li><a href="#data">Data Table</a></li>
                <li><a href="#contact">Contact Form</a></li>
            </ul>
        </nav>
    </header>

    <section id="about">
        <h2>1. About Us Section</h2>
        <div class="image-container">
            <img src="https://via.placeholder.com/400x150?text=Web+Development+Image" alt="Placeholder Image for Web Development" width="400" height="150">
        </div>
        <p>This is the first main paragraph. We focus on providing high-quality educational resources for learning web technologies like HTML, CSS, and JavaScript.</p>
        <p>Here is a blockquote for emphasis:</p>
        <blockquote>
            "The best way to predict the future is to create it." - Peter Drucker
        </blockquote>
        <p>We believe in continuous learning and hands-on practice.</p>
    </section>

    <section id="services">
        <h2>2. Our Services & Lists</h2>
        <h3>Key Offerings (Ordered List)</h3>
        <ol>
            <li>Front-end Development Workshops</li>
            <li>Back-end System Architecture Consulting</li>
            <li>Database Management Training</li>
            <li>Full-stack Project Mentorship</li>
        </ol>

        <h3>Technology Stack (Description List)</h3>
        <dl>
            <dt>HTML5</dt>
            <dd>The latest standard for structuring web content.</dd>
            <dt>CSS3</dt>
            <dd>Used for styling the presentation of the document.</dd>
            <dt>JavaScript</dt>
            <dd>The programming language for dynamic web behavior.</dd>
        </dl>
    </section>

    <section id="data">
        <h2>3. Sample Data Table</h2>
        <table>
            <thead>
                <tr>
                    <th>Feature</th>
                    <th>Availability</th>
                    <th>Priority</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>User Authentication</td>
                    <td>Available</td>
                    <td>High</td>
                </tr>
                <tr>
                    <td>Payment Gateway Integration</td>
                    <td>In Development</td>
                    <td>Medium</td>
                </tr>
                <tr>
                    <td>Advanced Analytics</td>
                    <td>Planned</td>
                    <td>Low</td>
                </tr>
            </tbody>
            <tfoot>
                <tr>
                    <td colspan="3">Data last updated: December 2025</td>
                </tr>
            </tfoot>
        </table>
    </section>

    <section id="contact">
        <h2>4. Contact Form</h2>
        <form action="/submit-form" method="POST">
            <div class="form-group">
                <label for="name">Your Name:</label>
                <input type="text" id="name" name="user_name" required>
            </div>

            <div class="form-group">
                <label for="email">Your Email:</label>
                <input type="email" id="email" name="user_email" required>
            </div>

            <div class="form-group">
                <label for="subject">Subject:</label>
                <select id="subject" name="enquiry_subject">
                    <option value="general">General Inquiry</option>
                    <option value="support">Technical Support</option>
                    <option value="feedback">Feedback</option>
                </select>
            </div>
            
            <div class="form-group">
                <label for="message">Message:</label>
                <textarea id="message" name="user_message" rows="5" required></textarea>
            </div>

            <div class="form-group">
                <input type="checkbox" id="subscribe" name="subscribe_newsletter">
                <label for="subscribe">Subscribe to our newsletter</label>
            </div>
            
            <button type="submit">Send Message</button>
            <button type="reset">Clear Form</button>
        </form>
    </section>

    <footer>
        <p>&copy; 2025 Comprehensive HTML Example. All rights reserved.</p>
        <p>Follow us on <a href="https://example.com/social" target="_blank">Social Media</a>.</p>
    </footer>

</body>
</html>
