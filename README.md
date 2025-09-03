<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ms. P's Daily Hub</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary-accent: #f72585; /* Vibrant Pink */
            --secondary-accent: #4cc9f0; /* Vibrant Blue/Cyan */
            --text-light: #f0f0f0;
            --text-secondary: #adb5bd;
            --card-bg: rgba(0, 0, 0, 0.4);
            --card-border: rgba(255, 255, 255, 0.15);
            --glow-shadow-primary: 0 0 15px rgba(247, 37, 133, 0.6);
            --glow-shadow-secondary: 0 0 15px rgba(76, 201, 240, 0.6);
            --red-accent: #e53935;
            --green-accent: #34c759;
        }

        *, *::before, *::after { box-sizing: border-box; }

        @keyframes animateBackground {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        body {
            font-family: 'Poppins', sans-serif;
            background: linear-gradient(-45deg, #000000, #1d0c33, #f72585, #4cc9f0, #3a0ca3);
            background-size: 400% 400%;
            animation: animateBackground 20s ease infinite;
            background-attachment: fixed;
            color: var(--text-light);
            margin: 0;
            padding: 0;
            line-height: 1.6;
        }
        
        .top-header-bar {
            text-align: center;
            padding: 10px 20px;
            background: rgba(0,0,0,0.3);
            backdrop-filter: blur(5px);
            -webkit-backdrop-filter: blur(5px);
            font-weight: 600;
            color: var(--text-light);
            text-shadow: 0 0 5px var(--secondary-accent);
            width: 100%;
            position: sticky;
            top: 0;
            z-index: 1001;
        }

        .container { max-width: 1400px; margin: 0 auto; padding: 20px; position: relative; }

        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding-bottom: 20px;
            margin-bottom: 30px;
            position: relative;
            flex-wrap: wrap;
            gap: 20px;
        }
        .header-left { text-align: center; flex-grow: 1; }
        .header .subtitle { color: var(--text-light); margin: 0 0 15px 0; font-size: 1.8em; font-weight: 700; text-shadow: 0 0 8px #fff, 0 0 20px var(--primary-accent), 0 0 30px var(--primary-accent); }

        #class-selector {
            -webkit-appearance: none; -moz-appearance: none; appearance: none;
            background-color: var(--card-bg);
            color: var(--text-light);
            border: 1px solid var(--card-border);
            border-radius: 8px;
            padding: 10px 40px 10px 20px;
            font-family: inherit;
            font-size: 1.1em;
            font-weight: 600;
            cursor: pointer;
            background-image: url("data:image/svg+xml;charset=UTF-8,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='none' stroke='%23adb5bd' stroke-width='2' stroke-linecap='round' stroke-linejoin='round'%3e%3cpolyline points='6 9 12 15 18 9'%3e%3c/polyline%3e%3c/svg%3e");
            background-repeat: no-repeat;
            background-position: right 1rem center;
            background-size: 1em;
        }

        .navbar { display: flex; justify-content: center; margin-bottom: 30px; flex-wrap: wrap; gap: 15px; }
        .nav-link { padding: 12px 28px; text-decoration: none; color: var(--text-light); background-color: transparent; border: 1px solid var(--card-border); border-radius: 50px; transition: all 0.3s ease; cursor: pointer; font-weight: 600; }
        .nav-link:hover { transform: translateY(-3px); box-shadow: var(--glow-shadow-primary); border-color: var(--primary-accent); color: var(--primary-accent); }
        .nav-link.active { background: linear-gradient(90deg, var(--primary-accent), var(--secondary-accent)); color: white; border-color: transparent; font-weight: 700; box-shadow: 0 0 15px rgba(247, 37, 133, 0.5); }
        
        .tab-content { display: none; }
        .tab-content.active { display: block; }
        
        .grid-container { display: grid; gap: 25px; grid-template-columns: repeat(auto-fit, minmax(350px, 1fr)); }
        
        .card { background: var(--card-bg); backdrop-filter: blur(12px); -webkit-backdrop-filter: blur(12px); padding: 24px; border-radius: 16px; border: 1px solid var(--card-border); transition: transform 0.3s ease, box-shadow 0.3s ease; display: flex; flex-direction: column; }
        .card:not(.timer-widget-base):hover { transform: translateY(-8px) scale(1.02); box-shadow: var(--glow-shadow-secondary); }
        .card h2 { margin-top: 0; border-bottom: 2px solid; border-image: linear-gradient(to right, var(--primary-accent), var(--secondary-accent)) 1; padding-bottom: 12px; margin-bottom: 18px; color: var(--text-light); font-weight: 600; display: flex; align-items: center; justify-content: space-between; gap: 10px; }
        .card h2 .title-text { display: flex; align-items: center; flex-grow: 1; min-width: 0; }
        .card h2 .emoji-icon { font-size: 1.2em; margin-right: 12px; }
        .card h2 a { color: inherit; text-decoration: none; transition: color 0.3s ease; }
        .card h2 a:hover { color: var(--secondary-accent); }
        .card textarea { width: 100%; min-height: 150px; padding: 12px; background-color: rgba(0, 0, 0, 0.2); color: var(--text-light); border: 1px solid var(--card-border); border-radius: 8px; resize: vertical; font-family: inherit; }
        .connect-link { display: block; background: linear-gradient(90deg, var(--primary-accent), #c03089); color: white; padding: 12px 24px; border-radius: 50px; text-decoration: none; transition: all 0.3s ease; font-weight: 600; border: none; text-align: center; }
        .connect-link:hover { transform: translateY(-2px); box-shadow: var(--glow-shadow-primary); }

        .calculator { display: grid; grid-template-columns: repeat(4, 1fr); gap: 10px; }
        .calc-display { grid-column: 1 / -1; background-color: rgba(0,0,0,0.3); color: var(--text-light); font-size: 2.5em; padding: 15px; text-align: right; border-radius: 8px; margin-bottom: 10px; word-wrap: break-word; word-break: break-all; }
        .calc-btn { background-color: rgba(255,255,255,0.1); border: 1px solid var(--card-border); color: var(--text-light); font-size: 1.5em; padding: 20px; border-radius: 8px; cursor: pointer; transition: all 0.2s ease; }
        .calc-btn:hover { background-color: rgba(255,255,255,0.2); transform: scale(1.05); }
        .calc-btn.operator { background-color: rgba(76, 201, 240, 0.5); }
        .calc-btn.equals { background-color: rgba(247, 37, 133, 0.5); grid-column: span 2; }

        .link-list a { display: block; background: rgba(0,0,0,0.2); padding: 15px; margin-bottom: 10px; border-radius: 8px; text-decoration: none; color: var(--text-secondary); font-weight: 600; transition: all 0.3s ease; }
        .link-list a:hover { color: var(--text-light); background: var(--primary-accent); transform: translateX(10px); }

        .image-placeholder { width: 100%; height: 200px; border: 2px dashed var(--card-border); border-radius: 8px; display: flex; flex-direction: column; justify-content: center; align-items: center; color: var(--text-secondary); cursor: pointer; transition: all 0.3s ease; }
        .image-placeholder:hover { border-color: var(--primary-accent); color: var(--primary-accent); }
        .image-placeholder.has-image { border: none; padding: 0; overflow: hidden; }
        .image-placeholder.has-image img { width: 100%; height: 100%; object-fit: contain; border-radius: 8px; }
        .remove-btn { background-color: var(--red-accent); color: white; border: none; padding: 8px 16px; border-radius: 50px; cursor: pointer; font-size: 14px; margin-top: 10px; display: none; transition: all 0.3s ease; }
        .remove-btn:hover { transform: translateY(-2px); box-shadow: 0 0 10px var(--red-accent); }

        .card-footer-action { margin-top: auto; padding-top: 15px; border-top: 1px solid var(--card-border); }
        .action-input-group { display: flex; gap: 10px; align-items: center; }
        .action-input { flex-grow: 1; background-color: rgba(0,0,0,0.2); border: 1px solid var(--card-border); color: var(--text-light); border-radius: 8px; padding: 10px; font-family: 'Poppins', sans-serif; font-size: 1em; }
        select.action-input { -webkit-appearance: none; -moz-appearance: none; appearance: none; background-image: url("data:image/svg+xml;charset=UTF-8,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='none' stroke='%23adb5bd' stroke-width='2' stroke-linecap='round' stroke-linejoin='round'%3e%3cpolyline points='6 9 12 15 18 9'%3e%3c/polyline%3e%3c/svg%3e"); background-repeat: no-repeat; background-position: right 1rem center; background-size: 1em; padding-right: 2.5rem; }
        .action-btn { background: linear-gradient(90deg, var(--green-accent), #2a9d8f); color: white; border: none; padding: 10px 15px; border-radius: 8px; cursor: pointer; font-weight: 600; transition: all 0.3s ease; }
        .action-btn:hover { transform: translateY(-2px); box-shadow: 0 0 10px rgba(52, 199, 89, 0.5); }
        .gemini-result-box { background-color: rgba(0,0,0,0.2); border: 1px solid var(--card-border); border-radius: 8px; padding: 15px; margin-top: 10px; min-height: 50px; white-space: pre-wrap; }
        .loader { text-align: center; padding: 10px; display: none; }
        #generate-prompt-btn { display: none; margin-top: 10px; width: 100%; }

        .agenda-item { background-color: rgba(0,0,0,0.2); border: 1px solid var(--card-border); border-radius: 8px; padding: 10px 15px; margin-bottom: 10px; display: flex; justify-content: space-between; align-items: center; }
        .agenda-item-content img { max-width: 100%; border-radius: 8px; margin-top: 5px; }
        .delete-item-btn { background-color: transparent; color: var(--text-secondary); border: none; cursor: pointer; font-size: 1.2em; padding: 5px; }
        .delete-item-btn:hover { color: var(--red-accent); }
        #custom-agenda-group { display: none; margin-top: 10px; }
        
        .clear-btn { background: transparent; border: 1px solid var(--card-border); color: var(--text-secondary); font-size: 0.7em; padding: 4px 8px; border-radius: 50px; cursor: pointer; transition: all 0.3s ease; flex-shrink: 0; }
        .clear-btn:hover { color: var(--red-accent); border-color: var(--red-accent); }
        
        /* --- Dynamic Timer Widget --- */
        .timer-widget-base { transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1); }
        .timer-widget-static { width: 160px; padding: 12px; }
        .timer-widget-static .timer-display { font-size: 1.8em; }
        .timer-widget-static .timer-controls, .timer-widget-static .timer-progress-bar { display: none; }

        .timer-widget-active { width: 280px; padding: 20px; box-shadow: var(--glow-shadow-secondary), 0 8px 32px rgba(0, 0, 0, 0.4) !important; }
        .timer-widget-active .timer-display { font-size: 2.2em; }
        .timer-widget-active .timer-controls { display: flex; }
        .timer-widget-active .timer-progress-bar { display: block; }
        
        .timer-widget-base .timer-display { font-weight: 700; margin-bottom: 12px; text-align: center; color: var(--text-light); text-shadow: 0 0 10px var(--secondary-accent); }
        .timer-presets { display: flex; flex-wrap: wrap; gap: 6px; margin-bottom: 10px; justify-content: center; }
        .timer-widget-base .timer-controls { flex-wrap: wrap; gap: 6px; margin-bottom: 10px; justify-content: center; }
        .timer-widget-base .timer-progress-bar { width: 100%; height: 4px; background-color: rgba(255, 255, 255, 0.2); border-radius: 2px; overflow: hidden; margin-top: 10px; }
        .timer-widget-base .progress { height: 100%; width: 0%; background: linear-gradient(90deg, var(--primary-accent), var(--secondary-accent)); border-radius: 2px; transition: width 1s linear; }
        
        .timer-btn, .timer-control-btn { padding: 6px 12px; font-size: 0.8em; background: rgba(255, 255, 255, 0.1); color: var(--text-light); border: 1px solid var(--card-border); border-radius: 6px; cursor: pointer; transition: all 0.2s ease; font-weight: 500; }
        .timer-btn:hover, .timer-control-btn:hover { background: var(--secondary-accent); color: #111; transform: translateY(-1px); }
        .timer-btn.active { background: var(--primary-accent); color: white; border-color: var(--primary-accent); }
        
        .rss-item { margin-bottom: 15px; padding-bottom: 15px; border-bottom: 1px solid var(--card-border); }
        .rss-item:last-child { border-bottom: none; }
        .rss-item a { text-decoration: none; color: var(--secondary-accent); font-weight: 600; transition: color 0.3s ease; }
        .rss-item a:hover { color: var(--primary-accent); }
        .rss-feed p { margin: 5px 0 0; color: var(--text-secondary); font-size: 0.9em; }

        /* --- Archive Styles --- */
        #archive-display h2 { border-bottom: 2px solid var(--primary-accent); padding-bottom: 10px; margin-top: 20px; }
        .archive-class-grid { display: grid; gap: 20px; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); }
        .archive-entry { padding: 15px; font-size: 0.9em; }
        .archive-entry h4 { margin-top: 0; color: var(--primary-accent); font-size: 1.1em; }
        .archive-entry h5 { color: var(--secondary-accent); border-bottom: 1px solid var(--secondary-accent); padding-bottom: 3px; margin-top: 10px; margin-bottom: 5px; font-size: 1em; }
        .archive-entry p, .archive-entry ul { margin-top: 0; font-size: 0.95em; word-wrap: break-word; }
        .archive-entry ul { list-style-type: disc; padding-left: 20px; }
        .archive-entry img { max-width: 100%; border-radius: 8px; margin-top: 10px; }
        #github-publish-section { margin-top: 40px; padding-top: 20px; border-top: 2px solid var(--card-border); }
        #github-publish-section textarea { width: 100%; min-height: 250px; font-family: monospace; font-size: 0.9em; }
        
        /* --- Notification Styles --- */
        .notification {
            position: fixed;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            background: linear-gradient(90deg, var(--green-accent), #2a9d8f);
            color: white;
            padding: 15px 25px;
            border-radius: 50px;
            z-index: 2000;
            opacity: 0;
            visibility: hidden;
            transition: opacity 0.5s, visibility 0.5s, bottom 0.5s;
            font-weight: 600;
            box-shadow: 0 5px 15px rgba(0,0,0,0.3);
        }

        .notification.show {
            opacity: 1;
            visibility: visible;
            bottom: 40px;
        }
    </style>
</head>
<body>
    <div class="top-header-bar" id="top-header-bar"></div>

    <div class="container">
        <div class="header">
            <div class="header-left">
                <h2 class="subtitle">Ms. P's Daily Hub</h2>
                <select id="class-selector">
                    <option value="Lit Basics">Lit Basics</option>
                    <option value="Study Skills">Study Skills</option>
                    <option value="Math Essentials 2/3">Math Essentials 2/3</option>
                    <option value="Advocacy">Advocacy</option>
                </select>
            </div>
            <div class="card timer-widget-base timer-widget-static" id="timer-widget">
                <h2 style="font-size: 0.9em; margin: 0 0 8px 0; border: none; padding: 0;"><span class="title-text"><span class="emoji-icon">⏱️</span>Timer</span></h2>
                <div class="timer-display" id="timerDisplay">00:00</div>
                <div class="timer-presets">
                    <button class="timer-btn" data-time="300">5min</button>
                    <button class="timer-btn" data-time="600">10min</button>
                    <button class="timer-btn" data-time="900">15min</button>
                </div>
                <div class="timer-controls">
                    <button class="timer-control-btn" id="start-btn">Start</button>
                    <button class="timer-control-btn" id="pause-btn">Pause</button>
                    <button class="timer-control-btn" id="reset-btn">Reset</button>
                </div>
                <div class="timer-progress-bar">
                    <div class="progress" id="progressBar"></div>
                </div>
            </div>
        </div>

        <nav class="navbar">
            <a href="#" class="nav-link active" data-tab="home">Home</a>
            <a href="#" class="nav-link" data-tab="resources">Resources</a>
            <a href="#" class="nav-link" data-tab="game-links">Game Links</a>
            <a href="#" class="nav-link" data-tab="teacher-tools">Teacher Tools</a>
            <a href="#" class="nav-link" data-tab="archive">Daily Archive</a>
        </nav>

        <!-- Home Tab -->
        <div id="home" class="tab-content active">
            <div class="grid-container">
                <div class="card">
                    <h2><span class="title-text"><span class="emoji-icon">📋</span>Today's Agenda</span></h2>
                    <div id="agenda-list" style="flex-grow: 1;"></div>
                    <div class="card-footer-action">
                        <div class="action-input-group">
                            <select id="agenda-preset-select" class="action-input">
                                <option value="" disabled selected>Add an item...</option>
                                <option value="Do Now: Math Warm-ups">Do Now: Math Warm-ups</option>
                                <option value="Do Now: Weekly Word Wizard">Do Now: Weekly Word Wizard</option>
                                <option value="Direct Instruction">Direct Instruction</option>
                                <option value="Group Work">Group Work</option>
                                <option value="Independent Practice">Independent Practice</option>
                                <option value="Exit Ticket">Exit Ticket</option>
                                <option value="custom">Custom Item...</option>
                            </select>
                            <button id="add-agenda-item-btn" class="action-btn">Add</button>
                        </div>
                        <div id="custom-agenda-group">
                            <input type="text" id="custom-agenda-input" class="action-input" placeholder="Enter custom text...">
                        </div>
                        <div class="action-input-group" style="margin-top: 10px;">
                             <button id="add-agenda-image-btn" class="action-btn" style="width:100%; background: var(--secondary-accent);">Add Image</button>
                             <input type="file" id="agenda-image-input" style="display: none;" accept="image/*">
                        </div>
                    </div>
                </div>
                <div class="card">
                    <h2><span class="title-text"><span class="emoji-icon">🧠</span>Learning Objective</span> <button id="clear-objective-btn" class="clear-btn">Clear</button></h2>
                    <textarea id="learningObjective" placeholder="Type or generate..."></textarea>
                    <div class="card-footer-action">
                        <div class="action-input-group">
                            <input type="text" id="objective-topic" class="action-input" placeholder="Enter a topic...">
                            <button id="generate-objective-btn" class="action-btn gemini-btn">✨ Generate</button>
                        </div>
                    </div>
                </div>
                <div class="card">
                    <h2><span class="title-text"><span class="emoji-icon">🤝</span>Check and Connect</span> <button id="clear-donow-btn" class="clear-btn">Clear</button></h2>
                    <textarea id="doNow" placeholder="Enter or generate a 'Do Now'..."></textarea>
                    <div class="card-footer-action">
                         <button id="generate-donow-btn" class="action-btn gemini-btn" style="width: 100%;">✨ Generate Daily Question</button>
                    </div>
                </div>
                <div class="card">
                    <h2><span class="title-text"><span class="emoji-icon">😂</span> Daily Drop</span></h2>
                    <div class="image-placeholder" id="daily-drop-placeholder">
                        <input type="file" id="daily-drop-input" style="display: none;" accept="image/*">
                        <p>Click to upload a photo!</p>
                    </div>
                    <button id="remove-daily-drop-btn" class="remove-btn">Remove Photo</button>
                    <div class="card-footer-action">
                        <button id="generate-prompt-btn" class="action-btn gemini-btn">✨ Generate Writing Prompt</button>
                        <div class="loader" id="prompt-loader">Analyzing...</div>
                        <div class="gemini-result-box" id="prompt-result" style="display: none;"></div>
                    </div>
                </div>
                <div class="card">
                    <h2><span class="title-text"><span class="emoji-icon">🏛️</span>On This Day</span></h2>
                    <div style="margin-bottom: auto;">
                        <a href="https://www.britannica.com/on-this-day" target="_blank" class="connect-link">On This Day</a>
                        <a href="https://www.britannica.com/one-good-fact" target="_blank" class="connect-link" style="background: linear-gradient(90deg, #4cc9f0, #2575fc); margin-top: 10px;">One Good Fact</a>
                    </div>
                    <p style="margin-top: 20px; color: var(--text-secondary);">Explore historical events and interesting facts for today's date from Britannica.</p>
                </div>
                 <div class="card">
                    <h2><span class="title-text"><span class="emoji-icon">📰</span><a href="https://thekidshouldseethis.com/" target="_blank">The Kids Should See This</a></span></h2>
                    <div class="link-list" style="margin-top:auto;">
                        <a href="https://thekidshouldseethis.com/music" target="_blank">Music</a>
                        <a href="https://thekidshouldseethis.com/art" target="_blank">Art</a>
                        <a href="https://thekidshouldseethis.com/tagged/humor" target="_blank">Funny</a>
                        <a href="https://thekidshouldseethis.com/tagged/stop-motion" target="_blank">Stop-Motion</a>
                    </div>
                </div>
                <div class="card">
                    <h2><span class="title-text"><span class="emoji-icon">🎓</span>TED-Ed Videos</span></h2>
                    <p>Explore engaging educational videos covering science, history, literature, and more.</p>
                    <div class="link-list" style="margin-top:auto;">
                        <a href="https://ed.ted.com/?popular=1" target="_blank">Popular Lessons</a>
                        <a href="https://ed.ted.com/?category=mathematics" target="_blank">Mathematics</a>
                        <a href="https://ed.ted.com/?category=literature-language" target="_blank">Literature & Language</a>
                        <a href="https://ed.ted.com/?category=thinking-learning" target="_blank">Thinking & Learning</a>
                    </div>
                </div>
                <div class="card">
                    <h2><span class="title-text"><span class="emoji-icon">🗞️</span>NYT Learning Network</span></h2>
                    <div class="link-list" style="margin-top:auto;">
                        <a href="https://www.nytimes.com/column/learning-student-opinion" target="_blank">Student Opinion Questions</a>
                        <a href="https://www.nytimes.com/spotlight/accessible-activities" target="_blank">Picture Prompts</a>
                        <a href="https://www.nytimes.com/column/learning-word-of-the-day" target="_blank">Word of the Day</a>
                        <a href="https://www.nytimes.com/spotlight/learning-contests" target="_blank">Contests</a>
                    </div>
                </div>
            </div>
            <!-- Action Buttons -->
            <div class="grid-container" style="margin-top: 25px; grid-template-columns: 1fr 1fr;">
                <div class="card">
                    <h2><span class="title-text"><span class="emoji-icon">📤</span>Export Today's Plan</span></h2>
                    <p>Copy a formatted version of today's plan to paste into Google Classroom, a doc, or a slide.</p>
                    <button id="copy-for-sharing-btn" class="action-btn" style="width: 100%; margin-top: auto;">Copy for Sharing</button>
                </div>
                 <div class="card">
                    <h2><span class="title-text"><span class="emoji-icon">✅</span>Submit for the Record</span></h2>
                    <p>Post today's plan to the Daily Archive for students to view later.</p>
                    <button id="submit-to-archive-btn" class="action-btn" style="width: 100%; background: var(--primary-accent); margin-top: auto;">Submit Today's Plan to Archive</button>
                </div>
            </div>
        </div>

        <div id="resources" class="tab-content"><div class="grid-container"><div class="card"><h2><span class="title-text"><span class="emoji-icon">📚</span>Helpful Links</span></h2><div class="link-list"><a href="https://www.khanacademy.org/" target="_blank">Khan Academy</a><a href="https://www.virtualnerd.com/" target="_blank">Virtual Nerd</a><a href="https://mathantics.com/" target="_blank">Math Antics</a><a href="https://www.ixl.com/" target="_blank">IXL</a><a href="https://www.wewillwrite.com/" target="_blank">WeWillWrite</a><a href="https://www.merriam-webster.com/" target="_blank">Merriam-Webster Dictionary</a><a href="https://newsela.com/" target="_blank">Newsela</a></div></div><div class="card"><h2><span class="title-text"><span class="emoji-icon">🧮</span>Calculator</span></h2><div class="calculator"><div id="calc-display" class="calc-display">0</div><button class="calc-btn operator">C</button><button class="calc-btn operator">+/-</button><button class="calc-btn operator">%</button><button class="calc-btn operator">/</button><button class="calc-btn">7</button><button class="calc-btn">8</button><button class="calc-btn">9</button><button class="calc-btn operator">*</button><button class="calc-btn">4</button><button class="calc-btn">5</button><button class="calc-btn">6</button><button class="calc-btn operator">-</button><button class="calc-btn">1</button><button class="calc-btn">2</button><button class="calc-btn">3</button><button class="calc-btn operator">+</button><button class="calc-btn" style="grid-column: span 2;">0</button><button class="calc-btn">.</button><button class="calc-btn equals">=</button></div></div></div></div>
        <div id="game-links" class="tab-content"><div class="card"><h2><span class="title-text"><span class="emoji-icon">🎮</span>Game Links</span></h2><div class="link-list"><a href="https://kahoot.it/" target="_blank">Kahoot!</a><a href="https://quizizz.com/join" target="_blank">Quizizz</a><a href="https://www.blooket.com/play" target="_blank">Blooket</a><a href="https://quizlet.com/live" target="_blank">Quizlet Live</a><a href="https://www.gimkit.com/join" target="_blank">Gimkit</a><a href="https://www.99math.com/join" target="_blank">99math</a></div></div></div>
        <div id="teacher-tools" class="tab-content">
            <div class="card">
                <h2><span class="title-text"><span class="emoji-icon">📝</span>Document Generator</span></h2>
                <p>Select a document type, generate a template, and download it as a text file.</p>
                <select id="doc-type-select" class="action-input" style="margin-bottom: 10px;">
                    <option value="behavior">Behavior Log</option>
                    <option value="parent">Parent Communication</option>
                    <option value="notes">Miscellaneous Notes</option>
                </select>
                <textarea id="doc-generator-textarea" style="min-height: 250px;"></textarea>
                <div class="card-footer-action">
                    <div class="action-input-group">
                        <button id="generate-doc-btn" class="action-btn gemini-btn">✨ Generate Template</button>
                        <button id="download-doc-btn" class="action-btn" style="background: var(--secondary-accent);">📥 Download .txt</button>
                    </div>
                </div>
            </div>
        </div>
        <div id="archive" class="tab-content">
            <div class="card">
                <h2><span class="title-text"><span class="emoji-icon">🗄️</span>Daily Archive</span></h2>
                <p>This is a view-only archive of past lessons. This archive is saved in your browser. New entries are added daily and will remain here unless you clear your browser's cache.</p>
                <div id="archive-display"></div>
                <div id="github-publish-section">
                     <h2><span class="title-text"><span class="emoji-icon">🚀</span>Publish Archive</span></h2>
                    <p>Generate a complete HTML file of the archive to upload to a static website for students and parents to view.</p>
                    <div class="action-input-group" style="margin-bottom: 15px;">
                        <button id="generate-archive-html-btn" class="action-btn" style="width: 50%;">Generate Archive HTML</button>
                        <button id="clear-archive-btn" class="action-btn" style="width: 50%; background: var(--red-accent);">Clear Entire Archive</button>
                    </div>
                    <textarea id="archive-for-github" readonly placeholder="Generated HTML code will appear here..."></textarea>
                </div>
            </div>
        </div>
    </div>
    
    <div id="notification-box" class="notification"></div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const elements = {
                classSelector: document.getElementById('class-selector'),
                notificationBox: document.getElementById('notification-box'),
                topHeaderBar: document.getElementById('top-header-bar'),
                navLinks: document.querySelectorAll('.nav-link'),
                tabContents: document.querySelectorAll('.tab-content'),
                timer: {
                    widget: document.getElementById('timer-widget'),
                    display: document.getElementById('timerDisplay'),
                    startBtn: document.getElementById('start-btn'),
                    pauseBtn: document.getElementById('pause-btn'),
                    resetBtn: document.getElementById('reset-btn'),
                    presets: document.querySelectorAll('.timer-btn'),
                    progressBar: document.getElementById('progressBar')
                },
                agenda: {
                    list: document.getElementById('agenda-list'),
                    presetSelect: document.getElementById('agenda-preset-select'),
                    customGroup: document.getElementById('custom-agenda-group'),
                    customInput: document.getElementById('custom-agenda-input'),
                    addBtn: document.getElementById('add-agenda-item-btn'),
                    addImageBtn: document.getElementById('add-agenda-image-btn'),
                    imageInput: document.getElementById('agenda-image-input')
                },
                objective: {
                    textarea: document.getElementById('learningObjective'),
                    topicInput: document.getElementById('objective-topic'),
                    generateBtn: document.getElementById('generate-objective-btn'),
                    clearBtn: document.getElementById('clear-objective-btn')
                },
                doNow: {
                    textarea: document.getElementById('doNow'),
                    generateBtn: document.getElementById('generate-donow-btn'),
                    clearBtn: document.getElementById('clear-donow-btn')
                },
                dailyDrop: {
                    placeholder: document.getElementById('daily-drop-placeholder'),
                    input: document.getElementById('daily-drop-input'),
                    removeBtn: document.getElementById('remove-daily-drop-btn'),
                    generatePromptBtn: document.getElementById('generate-prompt-btn'),
                    promptLoader: document.getElementById('prompt-loader'),
                    promptResult: document.getElementById('prompt-result')
                },
                actions: {
                    copyBtn: document.getElementById('copy-for-sharing-btn'),
                    submitBtn: document.getElementById('submit-to-archive-btn')
                },
                archive: {
                    display: document.getElementById('archive-display'),
                    generateHtmlBtn: document.getElementById('generate-archive-html-btn'),
                    clearBtn: document.getElementById('clear-archive-btn'),
                    githubTextarea: document.getElementById('archive-for-github')
                },
                teacherTools: {
                    docTypeSelect: document.getElementById('doc-type-select'),
                    textarea: document.getElementById('doc-generator-textarea'),
                    generateBtn: document.getElementById('generate-doc-btn'),
                    downloadBtn: document.getElementById('download-doc-btn')
                },
                 calculator: {
                    display: document.getElementById('calc-display'),
                    buttons: document.querySelectorAll('.calculator .calc-btn')
                }
            };

            let state = {
                currentClass: elements.classSelector.value,
                archives: [],
                timerInterval: null,
                totalSeconds: 0,
                remainingSeconds: 0,
                isTimerRunning: false
            };
            
            // NOTE: The API_URL should not have the key directly in it.
            // The key is provided by the execution environment.
            const API_KEY = ""; // This should be empty.
            const API_URL_BASE = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-05-20:generateContent?key=${API_KEY}`;

            function showNotification(message, isError = false) {
                elements.notificationBox.textContent = message;
                elements.notificationBox.style.background = isError ? 'var(--red-accent)' : 'var(--green-accent)';
                elements.notificationBox.classList.add('show');
                setTimeout(() => {
                    elements.notificationBox.classList.remove('show');
                }, 3000);
            }

            function updateTime() {
                const now = new Date();
                const timeOptions = { hour: '2-digit', minute: '2-digit', second: '2-digit' };
                const dateOptions = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
                elements.topHeaderBar.textContent = `${now.toLocaleDateString([], dateOptions)} | ${now.toLocaleTimeString([], timeOptions)}`;
            }
            setInterval(updateTime, 1000);
            updateTime();
            
            elements.navLinks.forEach(link => {
                link.addEventListener('click', (e) => {
                    e.preventDefault();
                    elements.navLinks.forEach(item => item.classList.remove('active'));
                    elements.tabContents.forEach(content => content.classList.remove('active'));
                    
                    link.classList.add('active');
                    const tabId = link.getAttribute('data-tab');
                    document.getElementById(tabId).classList.add('active');
                });
            });

            function formatTime(seconds) {
                const mins = Math.floor(seconds / 60);
                const secs = seconds % 60;
                return `${String(mins).padStart(2, '0')}:${String(secs).padStart(2, '0')}`;
            }

            function updateTimerDisplay() {
                elements.timer.display.textContent = formatTime(state.remainingSeconds);
                const progress = state.totalSeconds > 0 ? ((state.totalSeconds - state.remainingSeconds) / state.totalSeconds) * 100 : 0;
                elements.timer.progressBar.style.width = `${progress}%`;
            }

            function startTimer() {
                if (state.isTimerRunning || state.remainingSeconds <= 0) return;
                state.isTimerRunning = true;
                elements.timer.widget.classList.add('timer-widget-active');
                elements.timer.widget.classList.remove('timer-widget-static');
                state.timerInterval = setInterval(() => {
                    state.remainingSeconds--;
                    updateTimerDisplay();
                    if (state.remainingSeconds <= 0) {
                        clearInterval(state.timerInterval);
                        state.isTimerRunning = false;
                        showNotification("Time's up!");
                        elements.timer.display.textContent = "Done!";
                    }
                }, 1000);
            }

            function pauseTimer() {
                clearInterval(state.timerInterval);
                state.isTimerRunning = false;
            }

            function resetTimer() {
                clearInterval(state.timerInterval);
                state.isTimerRunning = false;
                state.remainingSeconds = state.totalSeconds;
                updateTimerDisplay();
                 elements.timer.widget.classList.remove('timer-widget-active');
                elements.timer.widget.classList.add('timer-widget-static');
            }
            
            elements.timer.presets.forEach(btn => {
                btn.addEventListener('click', () => {
                    elements.timer.presets.forEach(p => p.classList.remove('active'));
                    btn.classList.add('active');
                    pauseTimer();
                    state.totalSeconds = parseInt(btn.dataset.time, 10);
                    state.remainingSeconds = state.totalSeconds;
                    updateTimerDisplay();
                    startTimer();
                });
            });

            elements.timer.startBtn.addEventListener('click', startTimer);
            elements.timer.pauseBtn.addEventListener('click', pauseTimer);
            elements.timer.resetBtn.addEventListener('click', resetTimer);

            elements.agenda.presetSelect.addEventListener('change', () => {
                if (elements.agenda.presetSelect.value === 'custom') {
                    elements.agenda.customGroup.style.display = 'block';
                    elements.agenda.customInput.focus();
                } else {
                    elements.agenda.customGroup.style.display = 'none';
                }
            });

            // NEW: Image resizing helper function
            async function resizeImage(file, maxWidth = 800, maxHeight = 800) {
                return new Promise((resolve, reject) => {
                    const reader = new FileReader();
                    reader.onload = (event) => {
                        const img = new Image();
                        img.onload = () => {
                            const canvas = document.createElement('canvas');
                            let width = img.width;
                            let height = img.height;

                            if (width > height) {
                                if (width > maxWidth) {
                                    height *= maxWidth / width;
                                    width = maxWidth;
                                }
                            } else {
                                if (height > maxHeight) {
                                    width *= maxHeight / height;
                                    height = maxHeight;
                                }
                            }
                            canvas.width = width;
                            canvas.height = height;
                            const ctx = canvas.getContext('2d');
                            ctx.drawImage(img, 0, 0, width, height);
                            resolve({
                                dataUrl: canvas.toDataURL(file.type),
                                mimeType: file.type
                            });
                        };
                        img.onerror = reject;
                        img.src = event.target.result;
                    };
                    reader.onerror = reject;
                    reader.readAsDataURL(file);
                });
            }

            function addAgendaItem(content, type = 'text') {
                 if (!content) return;
                const itemDiv = document.createElement('div');
                itemDiv.className = 'agenda-item';
                
                const contentDiv = document.createElement('div');
                contentDiv.className = 'agenda-item-content';

                if (type === 'text') {
                    contentDiv.textContent = content;
                } else if (type === 'image') {
                    const img = document.createElement('img');
                    img.src = content;
                    contentDiv.appendChild(img);
                }

                const deleteBtn = document.createElement('button');
                deleteBtn.className = 'delete-item-btn';
                deleteBtn.innerHTML = '&times;';
                deleteBtn.onclick = () => itemDiv.remove();

                itemDiv.appendChild(contentDiv);
                itemDiv.appendChild(deleteBtn);
                elements.agenda.list.appendChild(itemDiv);
            }

            elements.agenda.addBtn.addEventListener('click', () => {
                let value = elements.agenda.presetSelect.value;
                if (value === 'custom') {
                    value = elements.agenda.customInput.value;
                    elements.agenda.customInput.value = '';
                    elements.agenda.customGroup.style.display = 'none';
                }
                if (value) {
                    addAgendaItem(value);
                }
                elements.agenda.presetSelect.value = '';
            });

            elements.agenda.addImageBtn.addEventListener('click', () => elements.agenda.imageInput.click());
            elements.agenda.imageInput.addEventListener('change', async (event) => {
                const file = event.target.files[0];
                if (file) {
                    try {
                        const { dataUrl } = await resizeImage(file);
                        addAgendaItem(dataUrl, 'image');
                    } catch (error) {
                        showNotification('Error resizing image. Please try another file.', true);
                        console.error('Image resize error:', error);
                    }
                }
            });

            elements.objective.clearBtn.addEventListener('click', () => elements.objective.textarea.value = '');
            elements.doNow.clearBtn.addEventListener('click', () => elements.doNow.textarea.value = '');

            async function callGemini(prompt) {
                const payload = { contents: [{ parts: [{ text: prompt }] }] };
                try {
                    const response = await fetch(API_URL_BASE, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify(payload)
                    });
                    if (!response.ok) throw new Error(`HTTP error! status: ${response.status}`);
                    const data = await response.json();
                    if (data.candidates && data.candidates.length > 0) {
                        return data.candidates[0].content.parts[0].text.trim();
                    }
                    throw new Error("No candidates returned from API.");
                } catch (error) {
                    console.error("Gemini API Error:", error);
                    showNotification("Error generating content. See console.", true);
                    return null;
                }
            }
            
            async function callGeminiWithImage(prompt, base64Image, mimeType, loader, resultEl) {
                loader.style.display = 'block';
                resultEl.style.display = 'none';
                resultEl.textContent = '';
                
                const payload = {
                    contents: [{
                        parts: [
                            { text: prompt },
                            { inlineData: { mimeType: mimeType, data: base64Image } }
                        ]
                    }]
                };

                try {
                    const response = await fetch(API_URL_BASE, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify(payload)
                    });
                    if (!response.ok) throw new Error(`HTTP error! status: ${response.status}`);
                    const data = await response.json();
                    if (data.candidates && data.candidates.length > 0) {
                        const text = data.candidates[0].content.parts[0].text;
                        resultEl.textContent = text.trim();
                        resultEl.style.display = 'block';
                    } else {
                         throw new Error("No candidates returned from API for image prompt.");
                    }
                } catch (error) {
                    console.error("Gemini Vision API Error:", error);
                    showNotification("Error generating prompt. See console.", true);
                } finally {
                    loader.style.display = 'none';
                }
            }


            elements.objective.generateBtn.addEventListener('click', async () => {
                const topic = elements.objective.topicInput.value.trim();
                if (!topic) {
                    showNotification("Please enter a topic for the objective.", true);
                    return;
                }
                const prompt = `Generate a clear, concise 7th-grade student-friendly learning objective for the topic: "${topic}". Start with "Students will be able to...".`;
                elements.objective.generateBtn.disabled = true;
                const result = await callGemini(prompt);
                 elements.objective.generateBtn.disabled = false;
                if (result) elements.objective.textarea.value = result;
            });

            elements.doNow.generateBtn.addEventListener('click', async () => {
                const topic = elements.objective.topicInput.value.trim();
                if (!topic) {
                    showNotification("Please enter a topic in the objective box first.", true);
                    return;
                }
                const prompt = `Generate a fun, engaging warm-up question for a 7th-grade class about to learn: "${topic}". Make it high-interest and relevant.`;
                elements.doNow.generateBtn.disabled = true;
                const result = await callGemini(prompt);
                elements.doNow.generateBtn.disabled = false;
                if (result) elements.doNow.textarea.value = result;
            });
            
            elements.dailyDrop.placeholder.addEventListener('click', () => elements.dailyDrop.input.click());
            elements.dailyDrop.input.addEventListener('change', async (event) => {
                const file = event.target.files[0];
                if (file) {
                    try {
                         const { dataUrl, mimeType } = await resizeImage(file);
                        const img = document.createElement('img');
                        img.src = dataUrl;
                        img.alt = "Daily Drop Image";
                        img.dataset.mimeType = mimeType;
                        elements.dailyDrop.placeholder.innerHTML = '';
                        elements.dailyDrop.placeholder.appendChild(img);

                        elements.dailyDrop.placeholder.classList.add('has-image');
                        elements.dailyDrop.removeBtn.style.display = 'block';
                        elements.dailyDrop.generatePromptBtn.style.display = 'block';
                    } catch (error) {
                        showNotification('Error processing image. Please try another file.', true);
                        console.error('Daily Drop image error:', error);
                    }
                }
            });

            elements.dailyDrop.removeBtn.addEventListener('click', () => {
                elements.dailyDrop.placeholder.innerHTML = '<p>Click to upload a photo!</p>';
                elements.dailyDrop.placeholder.classList.remove('has-image');
                elements.dailyDrop.input.value = '';
                elements.dailyDrop.removeBtn.style.display = 'none';
                elements.dailyDrop.generatePromptBtn.style.display = 'none';
                elements.dailyDrop.promptResult.style.display = 'none';
            });
            
            elements.dailyDrop.generatePromptBtn.addEventListener('click', () => {
                const img = elements.dailyDrop.placeholder.querySelector('img');
                if (img && img.src) {
                    const base64Image = img.src.split(',')[1];
                    const mimeType = img.dataset.mimeType || 'image/jpeg';
                    const prompt = "Generate a short, creative writing prompt for a middle school student based on this image.";
                    callGeminiWithImage(prompt, base64Image, mimeType, elements.dailyDrop.promptLoader, elements.dailyDrop.promptResult);
                } else {
                    showNotification("Please upload an image first.", true);
                }
            });
            
             elements.actions.copyBtn.addEventListener('click', () => {
                const className = state.currentClass;
                const date = new Date().toLocaleDateString([], { weekday: 'long', month: 'long', day: 'numeric' });
                const objective = elements.objective.textarea.value.trim();
                const doNow = elements.doNow.textarea.value.trim();
                const agendaItems = Array.from(elements.agenda.list.querySelectorAll('.agenda-item-content')).map((item, index) => {
                    const img = item.querySelector('img');
                    return img ? `${index + 1}. (Image attached)` : `${index + 1}. ${item.textContent}`;
                }).join('\n');

                const formattedText = `**Class:** ${className}\n**Date:** ${date}\n\n**Learning Objective:**\n${objective}\n\n**Check and Connect (Do Now):**\n${doNow}\n\n**Today's Agenda:**\n${agendaItems}`;

                navigator.clipboard.writeText(formattedText).then(() => {
                    showNotification('Copied to clipboard!');
                }, () => {
                    showNotification('Failed to copy.', true);
                });
            });

            function saveState() {
                try {
                    const dataToSave = {
                        objective: elements.objective.textarea.value,
                        doNow: elements.doNow.textarea.value,
                        agenda: Array.from(elements.agenda.list.querySelectorAll('.agenda-item-content')).map(item => {
                            const img = item.querySelector('img');
                            return { type: img ? 'image' : 'text', content: img ? img.src : item.textContent };
                        }),
                        dailyDrop: elements.dailyDrop.placeholder.classList.contains('has-image') ? elements.dailyDrop.placeholder.querySelector('img').src : null
                    };
                    localStorage.setItem(`teacherHubState_${state.currentClass}`, JSON.stringify(dataToSave));
                } catch(e) {
                     if (e.name === 'QuotaExceededError') {
                        showNotification('Could not save session. Storage is full. Clear archive or remove large images.', true);
                    } else {
                        showNotification('Error saving session.', true);
                    }
                }
            }

            function loadState() {
                const savedState = localStorage.getItem(`teacherHubState_${state.currentClass}`);
                elements.objective.textarea.value = '';
                elements.doNow.textarea.value = '';
                elements.agenda.list.innerHTML = '';
                elements.dailyDrop.removeBtn.click(); 

                if (savedState) {
                    const data = JSON.parse(savedState);
                    elements.objective.textarea.value = data.objective || '';
                    elements.doNow.textarea.value = data.doNow || '';
                    if (data.agenda) {
                        data.agenda.forEach(item => addAgendaItem(item.content, item.type));
                    }
                    
                    if (data.dailyDrop) {
                        const img = document.createElement('img');
                        img.src = data.dailyDrop;
                        img.alt = "Daily Drop Image";
                        elements.dailyDrop.placeholder.innerHTML = '';
                        elements.dailyDrop.placeholder.appendChild(img);
                        elements.dailyDrop.placeholder.classList.add('has-image');
                        elements.dailyDrop.removeBtn.style.display = 'block';
                        elements.dailyDrop.generatePromptBtn.style.display = 'block';
                    }
                }
            }

            elements.classSelector.addEventListener('change', () => {
                saveState(); 
                state.currentClass = elements.classSelector.value;
                loadState();
                loadArchives();
            });

            window.addEventListener('beforeunload', saveState);

            function loadArchives() {
                const savedArchives = localStorage.getItem('teacherHubArchives');
                state.archives = savedArchives ? JSON.parse(savedArchives) : [];
                renderArchive();
            }

            function saveArchives() {
                try {
                    localStorage.setItem('teacherHubArchives', JSON.stringify(state.archives));
                } catch(e) {
                    showNotification('Could not save to archive. Storage may be full.', true);
                }
            }

            function renderArchive() {
                elements.archive.display.innerHTML = '';
                const groupedByDate = state.archives.reduce((acc, entry) => {
                    (acc[entry.date] = acc[entry.date] || []).push(entry);
                    return acc;
                }, {});

                Object.keys(groupedByDate).sort((a,b) => new Date(b) - new Date(a)).forEach(date => {
                    const dateHeader = document.createElement('h2');
                    dateHeader.textContent = new Date(date).toLocaleDateString([], { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' });
                    elements.archive.display.appendChild(dateHeader);

                    const grid = document.createElement('div');
                    grid.className = 'archive-class-grid';
                    
                    groupedByDate[date].forEach(entry => {
                        const dailyDropHTML = entry.dailyDrop ? `<h5>Daily Drop</h5><img src="${entry.dailyDrop}" alt="Daily Drop from ${entry.date}">` : '';
                        const entryDiv = document.createElement('div');
                        entryDiv.className = 'card archive-entry';
                        entryDiv.innerHTML = `
                            <h4>${entry.className}</h4>
                            <h5>Learning Objective</h5>
                            <p>${entry.objective || 'N/A'}</p>
                            <h5>Check and Connect</h5>
                            <p>${entry.doNow || 'N/A'}</p>
                            <h5>Agenda</h5>
                            <ul>${entry.agenda.map(item => `<li>${item.type === 'image' ? '<img src="'+item.content+'" alt="Agenda image">' : item.textContent}</li>`).join('')}</ul>
                            ${dailyDropHTML}
                        `;
                        grid.appendChild(entryDiv);
                    });
                    elements.archive.display.appendChild(grid);
                });
            }

            elements.actions.submitBtn.addEventListener('click', () => {
                const dailyDropImg = elements.dailyDrop.placeholder.querySelector('img');
                const entry = {
                    id: Date.now(),
                    date: new Date().toISOString().split('T')[0],
                    className: state.currentClass,
                    objective: elements.objective.textarea.value.trim(),
                    doNow: elements.doNow.textarea.value.trim(),
                    agenda: Array.from(elements.agenda.list.querySelectorAll('.agenda-item-content')).map(item => {
                        const img = item.querySelector('img');
                        return { type: img ? 'image' : 'text', content: img ? img.src : item.textContent };
                    }),
                    dailyDrop: dailyDropImg ? dailyDropImg.src : null
                };

                if (!entry.objective && !entry.doNow && entry.agenda.length === 0 && !entry.dailyDrop) {
                    showNotification("Cannot submit an empty plan to the archive.", true);
                    return;
                }

                state.archives.push(entry);
                saveArchives();
                renderArchive();
                showNotification("Today's plan has been archived!");
            });

            elements.archive.clearBtn.addEventListener('click', () => {
                if (confirm("Are you sure you want to permanently delete the entire archive? This cannot be undone.")) {
                    state.archives = [];
                    saveArchives();
                    renderArchive();
                    showNotification("Archive cleared.");
                }
            });
            
             elements.archive.generateHtmlBtn.addEventListener('click', () => {
                let html = `<!DOCTYPE html><html lang="en"><head><meta charset="UTF-8"><title>Class Archive</title><style>body{font-family:sans-serif;background:#f0f2f5;color:#333;padding:20px;max-width:900px;margin:auto;} h1,h2{color:#005a9c;} .date-group{margin-bottom:20px;border-bottom:2px solid #ccc;padding-bottom:10px;}.class-entry{background:#fff;border:1px solid #ddd;border-radius:5px;padding:15px;margin-bottom:10px;} h3{color:#d6336c;margin-top:0;} img{max-width:100%;height:auto;border-radius:4px;}</style></head><body><h1>Daily Learning Archive</h1>`;
                const groupedByDate = state.archives.reduce((acc, entry) => {
                    (acc[entry.date] = acc[entry.date] || []).push(entry);
                    return acc;
                }, {});

                Object.keys(groupedByDate).sort((a, b) => new Date(b) - new Date(a)).forEach(date => {
                    html += `<div class="date-group"><h2>${new Date(date).toLocaleDateString([], { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' })}</h2>`;
                    groupedByDate[date].forEach(entry => {
                         const dailyDropHTML = entry.dailyDrop ? `<strong>Daily Drop:</strong><div><img src="${entry.dailyDrop}" alt="Daily Drop"></div>` : '';
                        html += `<div class="class-entry"><h3>${entry.className}</h3><strong>Objective:</strong><p>${entry.objective || 'N/A'}</p><strong>Do Now:</strong><p>${entry.doNow || 'N/A'}</p><strong>Agenda:</strong><ul>${entry.agenda.map(i => `<li>${i.type === 'image' ? `<img src="${i.content}" alt="Agenda Image">` : i.content}</li>`).join('')}</ul>${dailyDropHTML}</div>`;
                    });
                    html += `</div>`;
                });

                html += `</body></html>`;
                elements.archive.githubTextarea.value = html;
                showNotification("Archive HTML generated!");
            });
            
            elements.teacherTools.generateBtn.addEventListener('click', async () => {
                const docType = elements.teacherTools.docTypeSelect.value;
                let prompt = '';
                if(docType === 'behavior') {
                    prompt = 'Generate a simple, professional template for a student behavior log. Include fields for Date, Student Name, Behavior Observed, and Action Taken.';
                } else if(docType === 'parent') {
                    prompt = 'Generate a friendly, professional template for a parent communication log. Include fields for Date, Student Name, Parent Contacted, Method (Phone/Email), Reason for Contact, and Summary of Conversation.';
                } else {
                    prompt = 'Generate a flexible template for miscellaneous classroom notes. Include a section for Date, Topic, Key Points, and Action Items.';
                }
                elements.teacherTools.generateBtn.disabled = true;
                const result = await callGemini(prompt);
                elements.teacherTools.generateBtn.disabled = false;
                if (result) elements.teacherTools.textarea.value = result;
            });

            elements.teacherTools.downloadBtn.addEventListener('click', () => {
                const text = elements.teacherTools.textarea.value;
                if (!text) {
                    showNotification("Nothing to download.", true);
                    return;
                }
                const blob = new Blob([text], { type: 'text/plain' });
                const a = document.createElement('a');
                a.href = URL.createObjectURL(blob);
                a.download = `${elements.teacherTools.docTypeSelect.value}_template.txt`;
                document.body.appendChild(a);
                a.click();
                document.body.removeChild(a);
                showNotification("Template downloaded!");
            });
            
            elements.calculator.buttons.forEach(button => {
                button.addEventListener('click', () => {
                    const value = button.textContent;
                    let current = elements.calculator.display.textContent;

                    if (value === 'C') {
                        elements.calculator.display.textContent = '0';
                    } else if (value === '=') {
                        try {
                            elements.calculator.display.textContent = eval(current.replace(/--/g, '+').replace(/(\d)%/g, '($1/100)'));
                        } catch {
                            elements.calculator.display.textContent = 'Error';
                        }
                    } else if (value === '+/-') {
                         if (current !== '0') {
                            elements.calculator.display.textContent = current.startsWith('-') ? current.slice(1) : '-' + current;
                        }
                    } else {
                        if (current === '0' || current === 'Error') {
                            elements.calculator.display.textContent = value;
                        } else {
                            elements.calculator.display.textContent += value;
                        }
                    }
                });
            });
            
            // --- INITIAL LOAD ---
            loadState();
            loadArchives();
        });
    </script>
</body>
</html>

