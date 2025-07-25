---
layout: page
title: Resume
icon: fas fa-file-alt
order: 2
---

{% raw %}

<!-- <!DOCTYPE html> -->
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .neumorphic {
            border-radius: 20px;
            padding: 30px;
            margin: 2rem auto;
            max-width: 850px;
            transition: all 0.3s ease;
            border: 0.5px solid #ccc;
        }
        :root[data-theme="light"] .neumorphic {
            background: #f0f0f3;
            box-shadow:
                8px 8px 15px rgba(0, 0, 0, 0.1),
                -4px -4px 10px rgba(255, 255, 255, 0.9);
        }
        :root[data-theme="dark"] .neumorphic {
            background: #1e1e1e;
            box-shadow:
                8px 8px 15px rgba(0, 0, 0, 0.6),
                -4px -4px 10px rgba(255, 255, 255, 0.02);
        }
        .neumorphic:hover {
            transform: translateY(-2px);
            box-shadow:
                10px 10px 20px rgba(0, 0, 0, 0.15),
                -5px -5px 15px rgba(255, 255, 255, 0.6);
        }
        table thead {
            border-bottom: 1px solid black !important;
        }
        thead, tbody, tr, th, td {
            border: 1px solid black !important;
            padding: 0 !important;
        }
    </style>
</head>
<body style="width: 100vw; height: 100vh;">
    <div class="neumorphic" style="
        width: 100%; 
        height: 100%; 
        margin-top: 20px;
    ">
        <!-- Header -->
        <div id="header" style="
            display: flex;
            justify-content: space-between;
            align-items: center;
            height: 130px;
            font-family: 'Times New Roman', Times, serif;
            padding: 0 20px;
        ">
            <!-- Left Logo -->
            <div id="logo-container" style="flex-shrink: 0;">
                <img src="/assets/img/resume/dtu-circle-cropped-image.png" alt="DTU Logo" style="height: 100px;">
            </div>
            <!-- Middle Text (Name + Degree) -->
            <div id="middle-text" style="display: flex; flex-direction: column; justify-content: center; padding: 0 40px; text-align: left; flex: 1; line-height: 1.3;">
                <h1 style="margin: 0; font-size: 22px; font-weight: bold; font-variant: small-caps;">Kartik Walia</h1>
                <p style="margin: 2px 0; font-size: 15px;">2K22/CO/236</p>
                <p style="margin: 2px 0; font-size: 15px;">Bachelor of Technology</p>
                <p style="margin: 2px 0; font-size: 15px;">Computer Science Engineering</p>
                <p style="margin: 2px 0; font-size: 15px;">Delhi Technological University, formerly DCE</p>
            </div>
            <!-- Right Text (Contact Info) -->
            <div id="right-text" style="display: flex; flex-direction: column; justify-content: center; text-align: right; font-size: 15px; line-height: 1.3;">
                <p style="margin: 2px 0;">+91-9717090525</p>
                <p style="margin: 2px 0;">
                    <a href="mailto:business.kartikwalia@gmail.com" style="text-decoration: none; color: inherit;">
                        business.kartikwalia@gmail.com
                    </a>
                </p>
                <p style="margin: 2px 0;">
                    <a href="mailto:kartikwalia_co22a4_66@dtu.ac.in" style="text-decoration: none; color: inherit;">
                        kartikwalia_co22a4_66@dtu.ac.in
                    </a>
                </p>
                <p style="margin: 2px 0;">
                    <a href="https://github.com/thekartikwalia" target="_blank" style="text-decoration: none; color: inherit;">
                        GitHub
                    </a>
                </p>
                <p style="margin: 2px 0;">
                    <a href="https://www.linkedin.com/in/thekartikwalia" target="_blank" style="text-decoration: none; color: inherit;">
                        LinkedIn
                    </a>
                </p>
            </div>
        </div>
        <!-- Education -->
        <div id="education" style="padding: 0 20px;">
            <div id="education" style="border-bottom: 1px solid black; padding-bottom: 4px; margin-top: 6px; margin-bottom: 6px;">
                <h2 style="
                    font-size: 22px; 
                    font-weight: bold; 
                    font-variant: small-caps; 
                    margin: 0 auto 4px auto; 
                    text-align: center;
                    display: inline-block;
                    padding: 0 10px;
                    position: relative;
                    top: 6px;
                ">
                    Education
                </h2>
            </div>
            <table style="width: 100%; border-collapse: collapse; font-family: 'Times New Roman', Times, serif; font-size: 15px; border: 1px solid black !important; text-align: center;">
                <thead>
                    <tr>
                        <th style="border: 1px solid black; padding: 0;">Degree</th>
                        <th style="border: 1px solid black; padding: 0;">Institute</th>
                        <th style="border: 1px solid black; padding: 0;">Board / University</th>
                        <th style="border: 1px solid black; padding: 0;">CGPA / Percentage</th>
                        <th style="border: 1px solid black; padding: 0;">Year</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td style="border: 1px solid black; padding: 0;">B.Tech CSE</td>
                        <td style="border: 1px solid black; padding: 0;">Delhi Technological University</td>
                        <td style="border: 1px solid black; padding: 0;">DTU</td>
                        <td style="border: 1px solid black; padding: 0;">8.39 (Till 5th Sem)</td>
                        <td style="border: 1px solid black; padding: 0;">2022 - 2026</td>
                    </tr>
                    <tr>
                        <td style="border: 1px solid black; padding: 0;">Class XII</td>
                        <td style="border: 1px solid black; padding: 0;">N K Bagrodia Public School, New Delhi</td>
                        <td style="border: 1px solid black; padding: 0;">CBSE</td>
                        <td style="border: 1px solid black; padding: 0;">92%</td>
                        <td style="border: 1px solid black; padding: 0;">2021</td>
                    </tr>
                    <tr>
                        <td style="border: 1px solid black; padding: 0;">Class X</td>
                        <td style="border: 1px solid black; padding: 0;">N K Bagrodia Public School, New Delhi</td>
                        <td style="border: 1px solid black; padding: 0;">CBSE</td>
                        <td style="border: 1px solid black; padding: 0;">91%</td>
                        <td style="border: 1px solid black; padding: 0;">2019</td>
                    </tr>
                </tbody>
            </table>
        </div>
        <div id="experience" style="padding: 0 20px; font-size: 15px; line-height: 1.3;">
            <div id="experience" style="border-bottom: 1px solid black; padding-bottom: 4px; margin-top: 6px; margin-bottom: 6px;">
                <h2 style="
                    font-size: 22px; 
                    font-weight: bold; 
                    font-variant: small-caps; 
                    margin: 0 auto 4px auto; 
                    text-align: center;
                    display: inline-block;
                    padding: 0 10px;
                    position: relative;
                    top: 6px;
                ">
                    Experience
                </h2>
            </div>
            <ul style="list-style-type: disc; padding-left: 20px; margin-top: 8px;">
                <li>
                    <div style="display: flex; justify-content: space-between;">
                        <strong>Training & Placement Department, DTU</strong>
                        <span style="font-style: italic;">Feb 2025 - Present</span>
                    </div>
                    <div style="display: flex; justify-content: space-between;">
                        <em>Web Development</em>
                        <span>New Delhi</span>
                    </div>
                    <ul style="list-style-type: '- '; padding-left: 15px; margin-top: 4px;">
                        <li>Built a polyglot, microservices-based placement portal for 9,000+ DTU students.</li>
                        <li>Architected the system into 3 services: Node.js API (Clark), Python parser (Excelsior), Go cron (Janitor).</li>
                        <li>Offloaded Excel parsing to Python (Excelsior) for async handling and smooth Node.js performance.</li>
                        <li>Ensured type-safe inter-service gRPC communication using Protocol Buffers across all languages.</li>
                    </ul>
                </li>
                <li style="margin-top: 8px;">
                    <div style="display: flex; justify-content: space-between;">
                        <strong>Algozenith</strong>
                        <span style="font-style: italic;">Jan - Apr 2025</span>
                    </div>
                    <div style="display: flex; justify-content: space-between;">
                        <em>Subject Matter Expert</em>
                        <span>Remote</span>
                    </div>
                    <ul style="list-style-type: '- '; padding-left: 15px; margin-top: 4px;">
                        <li>Developed STL and Mathematics courses taken by 7,900+ students, with 1,260+ completing over 50%.</li>
                        <li>Created structured notes, step-by-step guides, and progressive modules to enhance clarity and engagement.</li>
                    </ul>
                </li>
            </ul>
        </div>
        <div id="projects" style="padding: 0 20px; font-size: 15px; line-height: 1.3;">
            <div id="projects" style="border-bottom: 1px solid black; padding-bottom: 4px; margin-top: 6px; margin-bottom: 6px;">
                <h2 style="
                    font-size: 22px; 
                    font-weight: bold; 
                    font-variant: small-caps; 
                    margin: 0 auto 4px auto; 
                    text-align: center;
                    display: inline-block;
                    padding: 0 10px;
                    position: relative;
                    top: 6px;
                ">
                    Projects
                </h2>
            </div>
            <ul style="list-style-type: disc; padding-left: 20px; margin-top: 8px;">
                <li>
                    <div style="display: flex; justify-content: space-between;">
                        <strong>Hybrid Dask-Based Music Recommender System</strong>
                        <span style="font-style: italic;">Jul 2025</span>
                    </div>
                    <div style="display: flex; justify-content: space-between;">
                        <em>Python, Dask, Streamlit, DVC, Docker, CI/CD, AWS</em>
                        <a href="https://github.com/thekartikwalia/hybrid-recommender-system" style="text-decoration: none; color: inherit;">GitHub</a>
                    </div>
                    <ul style="list-style-type: '- '; padding-left: 15px; margin-top: 4px;">
                        <li>Built a hybrid music recommender using Dask & scikit-learn for scalable content-collab filtering.</li>
                        <li>Designed CI/CD with DVC & GitHub Actions to automate model versioning and container deployments.</li>
                        <li>Used Docker & ECR to deploy on AWS EC2 with a custom blue-green strategy for zero-downtime rollout.</li>
                    </ul>
                </li>
                <li style="margin-top: 8px;">
                    <div style="display: flex; justify-content: space-between;">
                        <strong>AI-Powered Coding Assistant</strong>
                        <span style="font-style: italic;">Feb 2025</span>
                    </div>
                    <div style="display: flex; justify-content: space-between;">
                        <em>JavaScript, Marked.js, DOMPurify, highlight.js, GitHub Markdown CSS, html2pdf.js </em>
                        <a href="https://github.com/thekartikwalia/AI-Powered-Coding-Assitant" style="text-decoration: none; color: inherit;">GitHub</a>
                    </div>
                    <ul style="list-style-type: '- '; padding-left: 15px; margin-top: 4px;">
                        <li>Developed a Chrome extension to auto-extract problem & code context from SPA using MutationObserver.</li>
                        <li>Hooked into in-memory JS by overriding XMLHttpRequest to access non-DOM problem metadata.</li>
                        <li>Integrated Gemini API to offer context-aware coding suggestions based on live user code and problem data.</li>
                    </ul>
                </li>
                <li style="margin-top: 8px;">
                    <div style="display: flex; justify-content: space-between;">
                        <strong>Terrain-Traversing Autonomous Rover</strong>
                        <span style="font-style: italic;">Jan - Aug 2024</span>
                    </div>
                    <div style="display: flex; justify-content: space-between;">
                        <em>Python, ROS Noetic, Arduino, RTK-GPS, 2D LiDAR, MoveBase, RViz, React.js</em>
                        <a href="https://github.com/thekartikwalia/ugvc2024_ws" style="text-decoration: none; color: inherit;">GitHub</a>
                    </div>
                    <ul style="list-style-type: '- '; padding-left: 15px; margin-top: 4px;">
                        <li>Designed a navigation system using 2D LiDAR and RTK-GPS for precise localization and obstacle avoidance.</li>
                        <li>Employed ROS MoveBase with DWA planner on a pre-built SLAM map for dynamic waypoint path planning.</li>
                        <li>Developed modular branches: Arduino for sensors, React GUI for interface, and ROS Noetic for autonomy.</li>
                    </ul>
                </li>
            </ul>
        </div>
        <div id="technical-skills" style="padding: 0 20px; font-size: 15px; line-height: 1.3;">
            <div id="technical-skills" style="border-bottom: 1px solid black; padding-bottom: 4px; margin-top: 6px; margin-bottom: 6px;">
                <h2 style="
                    font-size: 22px; 
                    font-weight: bold; 
                    font-variant: small-caps; 
                    margin: 0 auto 4px auto; 
                    text-align: center;
                    display: inline-block;
                    padding: 0 10px;
                    position: relative;
                    top: 6px;
                ">
                    Technical Skills
                </h2>
            </div>
            <ul style="list-style-type: disc; padding-left: 20px; margin-top: 8px;">
                <li><strong>Programming Languages:</strong> C, C++, JavaScript, TypeScript, Python, SQL, HTML, CSS, LaTeX, Markdown</li>
                <li><strong>Software & Web Technologies:</strong> React.js, Next.js, Node.js, Express.js, Prisma, RESTful API</li>
                <li><strong>Robotics & Scientific Computing:</strong> NumPy, Pandas, Streamlit, ROS Noetic, ROS2 Humble, Gazebo, Dask</li>
                <li><strong>DevOps & Deployment:</strong> Docker, AWS EC2, AWS ECR, AWS S3, CI/CD, GitHub Actions</li>
                <li><strong>Developer Tools:</strong> Git, GitHub, VS Code, Jupyter, Google Colab, Postman, Bash, DVC</li>
                <li><strong>Soft Skills:</strong> Leadership, Strategic Planning, Logical Thinking, Teamwork</li>
                <li><strong>Relevant Coursework:</strong> Machine Learning, OOPs, Operating System, DBMS, Computer Networks</li>
            </ul>
        </div>
        <div id="achievements" style="padding: 0 20px; font-size: 15px; line-height: 1.3;">
            <div id="achievements" style="border-bottom: 1px solid black; padding-bottom: 4px; margin-top: 6px; margin-bottom: 6px;">
                <h2 style="
                    font-size: 22px; 
                    font-weight: bold; 
                    font-variant: small-caps; 
                    margin: 0 auto 4px auto; 
                    text-align: center;
                    display: inline-block;
                    padding: 0 10px;
                    position: relative;
                    top: 6px;
                ">
                    Achievements
                </h2>
            </div>
            <ul style="list-style-type: disc; padding-left: 20px; margin-top: 8px;">
                <li>
                    <div style="display: flex; justify-content: space-between;">
                        <span><strong>4th Position International</strong>, UGVC, Military Technical College, Cairo, Egypt</span>
                        <span style="font-style: italic;">2024</span>
                    </div>
                </li>
                <li style="margin-top: 4px;">
                    <div style="display: flex; justify-content: space-between;">
                        <span><strong>2nd Position National</strong>, Mernifier, IIT Bombay, India</span>
                        <span style="font-style: italic;">2023</span>
                    </div>
                </li>
            </ul>
        </div>
        <div id="positions-of-responsibility" style="padding: 0 20px; font-size: 15px; line-height: 1.3;">
            <div id="positions-of-responsibility" style="border-bottom: 1px solid black; padding-bottom: 4px; margin-top: 6px; margin-bottom: 6px;">
                <h2 style="
                    font-size: 22px; 
                    font-weight: bold; 
                    font-variant: small-caps; 
                    margin: 0 auto 4px auto; 
                    text-align: center;
                    display: inline-block;
                    padding: 0 10px;
                    position: relative;
                    top: 6px;
                ">
                    Positions of Responsibility
                </h2>
            </div>
            <ul style="list-style-type: disc; padding-left: 20px; margin-top: 8px;">
                <li>
                    <div style="display: flex; justify-content: space-between;">
                        <span><strong>Placement Coordinator</strong>, DTU</span>
                        <span style="font-style: italic;">Mar 2025 - Present</span>
                    </div>
                </li>
                <li style="margin-top: 4px;">
                    <div style="display: flex; justify-content: space-between;">
                        <span><strong>Team Leader</strong>, DTU T&P Recruitment Manager Team</span>
                        <span style="font-style: italic;">Feb 2025 - Present</span>
                    </div>
                </li>
                <li style="margin-top: 4px;">
                    <div style="display: flex; justify-content: space-between;">
                        <span><strong>Team Captain</strong>, UGV-DTU</span>
                        <span style="font-style: italic;">Feb 2025 - Present</span>
                    </div>
                </li>
            </ul>
        </div>
    </div>
</body>
</html>


{% endraw %}
