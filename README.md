# Desicoder
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Desicoder - AI-Powered Coding for the Next Billion</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;700;900&family=Poppins:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #05070D;
            color: #EAEAEA;
        }

        :lang(hi) {
            font-family: 'Poppins', sans-serif;
        }

        .main-container {
            height: 100vh;
            overflow-x: hidden;
            overflow-y: auto;
            scroll-behavior: smooth;
        }
        
        #interactive-hero {
            height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: grab;
            perspective: 1500px;
            background: radial-gradient(circle, rgba(16,185,129,0.1) 0%, rgba(5,7,13,0) 60%);
        }
        #interactive-hero:grabbing {
            cursor: grabbing;
        }

        #tech-render {
            transition: transform 0.2s cubic-bezier(0, .5, .5, 1);
            transform-style: preserve-3d;
            animation: float 4s ease-in-out infinite;
        }
        
        @keyframes float {
            0% { transform: translateY(0px); }
            50% { transform: translateY(-20px); }
            100% { transform: translateY(0px); }
        }
        
        .fade-in {
            opacity: 0;
            transform: translateY(30px);
            transition: opacity 0.8s ease-out, transform 0.8s ease-out;
        }
        .fade-in.visible {
            opacity: 1;
            transform: translateY(0);
        }
        
        .accent-color { color: #10B981; }
        .bg-accent-color { background-color: #10B981; }

        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: #0D1117; }
        ::-webkit-scrollbar-thumb {
            background-color: #10B981;
            border-radius: 10px;
            border: 2px solid #0D1117;
        }
        
        .lang-switcher .dropdown {
            display: none;
            position: absolute;
            right: 0;
            top: 120%;
            background-color: #0D1117;
            border-radius: 8px;
            padding: 8px;
            border: 1px solid #333;
        }
        .lang-switcher:hover .dropdown {
            display: block;
        }
        .lang-switcher .dropdown a {
            display: block;
            padding: 8px 12px;
            border-radius: 4px;
            white-space: nowrap;
        }
        .lang-switcher .dropdown a:hover {
            background-color: #10B981;
        }
        
        .highlight-card, .track-card, .project-card {
            background-color: #0D1117;
            border: 1px solid #21262d;
            border-radius: 16px;
            padding: 2rem;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            display: flex;
            flex-direction: column;
        }
        .highlight-card:hover, .track-card:hover, .project-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 20px 30px rgba(0,0,0,0.2);
        }

        .mic-button.listening {
            animation: pulse 1.5s infinite;
        }
        @keyframes pulse {
            0% { box-shadow: 0 0 0 0 rgba(16, 185, 129, 0.7); }
            70% { box-shadow: 0 0 0 20px rgba(16, 185, 129, 0); }
            100% { box-shadow: 0 0 0 0 rgba(16, 185, 129, 0); }
        }
        .code-editor {
            background-color: #010409;
            border-radius: 8px;
            padding: 1rem;
            font-family: 'Courier New', Courier, monospace;
            min-height: 100px;
        }
        .demo-container.listening-glow {
            box-shadow: 0 0 25px rgba(16, 185, 129, 0.3);
        }
        
        .section-bg {
             background-color: #0D1117;
             padding-top: 10rem;
             padding-bottom: 10rem;
        }
    </style>
</head>
<body>

    <div class="main-container">

        <header class="fixed top-0 left-0 right-0 z-20 p-6 flex justify-between items-center">
            <h1 class="text-2xl font-black tracking-wider" data-lang-key="title">Desicoder</h1>
            <nav class="hidden md:flex gap-8 font-medium text-sm items-center">
                <a href="#demo" data-lang-key="nav_demo" class="hover:text-accent-color transition-colors">Live Demo</a>
                <a href="#highlights" data-lang-key="nav_highlights" class="hover:text-accent-color transition-colors">Highlights</a>
                <a href="#tracks" data-lang-key="nav_tracks" class="hover:text-accent-color transition-colors">Career Tracks</a>
                <a href="#community" data-lang-key="nav_community" class="hover:text-accent-color transition-colors">Community</a>
                <div class="relative lang-switcher">
                    <button class="flex items-center gap-2 border border-white/50 px-3 py-1.5 rounded-full">
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16"><path d="M0 8a8 8 0 1 1 16 0A8 8 0 0 1 0 8zm11.5 0a.5.5 0 0 0-.5-.5h-2a.5.5 0 0 0 0 1h2a.5.5 0 0 0 .5-.5zM8 1a.5.5 0 0 0-.5.5v2a.5.5 0 0 0 1 0v-2A.5.5 0 0 0 8 1zm0 14a.5.5 0 0 0 .5-.5v-2a.5.5 0 0 0-1 0v2a.5.5 0 0 0 .5.5zM4.5 8a.5.5 0 0 0-.5-.5h-2a.5.5 0 0 0 0 1h2a.5.5 0 0 0 .5-.5z"/></svg>
                        <span id="current-lang">EN</span>
                    </button>
                    <div class="dropdown">
                        <a href="#" onclick="changeLanguage('en')">English</a>
                        <a href="#" onclick="changeLanguage('hi')">हिंदी</a>
                    </div>
                </div>
            </nav>
            <button data-lang-key="btn_signup" class="bg-accent-color text-white px-5 py-2 rounded-full text-sm font-bold hover:scale-105 transition-transform">
                Sign Up
            </button>
        </header>

        <section id="interactive-hero">
            <img id="tech-render" src="https://img.icons8.com/3d-fluency/512/bot.png" 
                 alt="Friendly 3D robot assistant" 
                 class="w-full h-full max-w-lg object-contain"
                 onerror="this.onerror=null;this.src='https://placehold.co/512x512/05070D/eeeeee?text=3D+Model+Error&font=inter';">
            <p id="drag-instruction" data-lang-key="drag_instruction" class="absolute bottom-10 text-gray-500 text-sm animate-pulse">Click and Drag to Rotate</p>
        </section>

        <section class="bg-transparent -mt-32 pb-32 text-center relative z-10">
             <div class="max-w-4xl mx-auto px-10">
                <h2 data-lang-key="hero_title" class="text-4xl md:text-5xl font-black leading-tight">
                    Learn to Code with AI, in Native
                </h2>
                <div class="mt-8 flex flex-col sm:flex-row gap-4 justify-center">
                    <button data-lang-key="btn_start_learning" class="bg-accent-color text-white font-bold py-4 px-10 rounded-full text-lg hover:scale-105 transition-transform">
                        Start Learning
                    </button>
                    <button data-lang-key="btn_explore_paths" class="bg-gray-700/50 text-white font-bold py-4 px-10 rounded-full text-lg hover:bg-gray-600/50 transition-colors">
                        Explore Career Paths
                    </button>
                </div>
            </div>
        </section>

        <section id="demo" class="section-bg">
             <div class="max-w-4xl mx-auto text-center">
                <h2 class="text-4xl font-bold mb-2" data-lang-key="demo_title">Experience the Magic</h2>
                <p class="text-gray-400 mb-10" data-lang-key="demo_subtitle">Click the mic and speak your command.</p>
                <div id="demo-container" class="demo-container bg-[#05070D] border border-[#21262d] rounded-2xl p-4 md:p-8 grid md:grid-cols-2 gap-4 md:gap-8 items-center transition-shadow duration-300">
                    <div class="text-left">
                        <label class="font-semibold" data-lang-key="demo_label_speak">1. Speak your command</label>
                        <div class="mt-2 flex items-center gap-4">
                            <button id="mic-button" class="mic-button bg-accent-color p-4 rounded-full transition-transform hover:scale-110">
                                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="white" viewBox="0 0 16 16"><path d="M5 3a3 3 0 0 1 6 0v5a3 3 0 0 1-6 0V3z"/><path d="M3.5 6.5A.5.5 0 0 1 4 7v1a4 4 0 0 0 8 0V7a.5.5 0 0 1 1 0v1a5 5 0 0 1-4.5 4.975V15h3a.5.5 0 0 1 0 1h-7a.5.5 0 0 1 0-1h3v-2.025A5 5 0 0 1 3 8V7a.5.5 0 0 1 .5-.5z"/></svg>
                            </button>
                            <p id="transcribed-text" class="text-gray-400 italic"></p>
                        </div>
                    </div>
                    <div class="text-left">
                        <label class="font-semibold" data-lang-key="demo_label_code">2. See the generated code</label>
                        <div id="code-output" class="code-editor mt-2 text-gray-300"></div>
                        <button id="explain-button" class="mt-4 w-full bg-gray-700/50 text-white font-bold py-2 px-4 rounded-lg flex items-center justify-center gap-2 opacity-50 cursor-not-allowed" disabled>
                            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" viewBox="0 0 16 16"><path d="M11.536 14.01A8.473 8.473 0 0 0 14.026 8a8.473 8.473 0 0 0-2.49-6.01l.484-.485A.5.5 0 0 0 11.535 1h-1a.5.5 0 0 0-.465.3l-.22.44a.5.5 0 0 0 .13.553L11 3.5l-1.964 1.964A.5.5 0 0 0 9.5 6v1.5a.5.5 0 0 0 .5.5h1.5a.5.5 0 0 0 .354-.854L11 7.146V6.5l1.5 1.5a.5.5 0 0 0 .854-.353V6a.5.5 0 0 0-.3-.464l-.44-.22a.5.5 0 0 0-.553.13l-.485.484A7.475 7.475 0 0 1 8 5.5a7.475 7.475 0 0 1-3.516 1.026l.485.484a.5.5 0 0 0 .553.13l.44-.22a.5.5 0 0 0 .3-.464v-.646l.5-.5a.5.5 0 0 0-.854-.353L6.5 6.5v.646a.5.5 0 0 0 .3.464l.44.22a.5.5 0 0 0 .553-.13l.485-.484A6.47 6.47 0 0 0 8 7.5a6.47 6.47 0 0 0 1.964 4.536L8.5 10.5v.646a.5.5 0 0 0 .3.464l.44.22a.5.5 0 0 0 .553-.13l.485-.484A7.475 7.475 0 0 1 8 10.5a7.475 7.475 0 0 1-3.516-1.026l.485-.484a.5.5 0 0 0 .553-.13l.44.22a.5.5 0 0 0 .3-.464v-.646l.5-.5a.5.5 0 0 0-.854-.353L6.5 8.5v.646a.5.5 0 0 0 .3.464l.44.22a.5.5 0 0 0 .553-.13l.485-.484A6.47 6.47 0 0 0 8 9.5a6.47 6.47 0 0 0 1.964 4.536L8.5 12.5v.646a.5.5 0 0 0 .3.464l.44.22a.5.5 0 0 0 .553-.13l.485-.484A7.475 7.475 0 0 1 8 12.5a7.475 7.475 0 0 1-3.516-1.026l.485-.484a.5.5 0 0 0 .553-.13l.44.22a.5.5 0 0 0 .3-.464v-.646l.5-.5a.5.5 0 0 0-.854-.353L6.5 10.5v.646a.5.5 0 0 0 .3.464l.44.22a.5.5 0 0 0 .553-.13l.485-.484A6.47 6.47 0 0 0 8 11.5a6.47 6.47 0 0 0 1.964 4.536L8.5 14.5v.646a.5.5 0 0 0 .3.464l.44.22a.5.5 0 0 0 .553-.13l.485-.484A8.478 8.478 0 0 0 11.5 16a8.478 8.478 0 0 0 2.526-6.01l-.484.485a.5.5 0 0 0 .485.515h.5a.5.5 0 0 0 .5-.5v-1a.5.5 0 0 0-.5-.5h-.5a.5.5 0 0 0-.485.515l.484.485A7.475 7.475 0 0 1 12.5 8a7.475 7.475 0 0 1-1.026-3.516l.484-.485a.5.5 0 0 0 .13-.553l-.22-.44a.5.5 0 0 0-.465-.3h-1a.5.5 0 0 0-.485.515l.484.485A8.473 8.473 0 0 0 8 1.5a8.473 8.473 0 0 0-6.01 2.49l.485.484A.5.5 0 0 0 3 4.5v1a.5.5 0 0 0 .5.5h1a.5.5 0 0 0 .354-.854L4.5 4.854V5.5l-1.5-1.5a.5.5 0 0 0-.354-.146H2a.5.5 0 0 0-.5.5v1a.5.5 0 0 0 .5.5h.5a.5.5 0 0 0 .465-.3l.22.44a.5.5 0 0 0-.13.553l-.485.484A7.475 7.475 0 0 1 5.5 8a7.475 7.475 0 0 1 1.026 3.516l-.484.485a.5.5 0 0 0-.13.553l.22.44a.5.5 0 0 0 .465.3h1a.5.5 0 0 0 .485-.515l-.484-.485A8.473 8.473 0 0 0 8 14.5a8.473 8.473 0 0 0 6.01-2.49l-.485-.484a.5.5 0 0 0-.354-.146H12a.5.5 0 0 0-.5.5v1a.5.5 0 0 0 .5.5h.5a.5.5 0 0 0 .5-.5v-1a.5.5 0 0 0-.5-.5h-.5a.5.5 0 0 0-.465.3l-.22-.44a.5.5 0 0 0 .13-.553l.485-.484z"/></svg>
                            <span data-lang-key="demo_btn_explain">Explain Code</span>
                        </button>
                    </div>
                </div>
            </div>
        </section>

        <section id="highlights" class="section-bg">
             <div class="max-w-6xl mx-auto">
                <div class="grid md:grid-cols-3 gap-8">
                    <div class="highlight-card fade-in">
                        <h3 class="text-2xl font-bold accent-color" data-lang-key="card1_title">AI Explains Code</h3>
                        <p class="mt-2 text-gray-400" data-lang-key="card1_desc">Stuck on a problem? Our AI tutor breaks down complex code into simple, easy-to-understand explanations in your chosen language.</p>
                    </div>
                    <div class="highlight-card fade-in" style="animation-delay: 0.2s;">
                        <h3 class="text-2xl font-bold accent-color" data-lang-key="card2_title">Voice to Code</h3>
                        <p class="mt-2 text-gray-400" data-lang-key="card2_desc">Speak your logic in Hindi or English, and watch our AI convert your thoughts into functional code. The future of coding is here.</p>
                    </div>
                    <div class="highlight-card fade-in" style="animation-delay: 0.4s;">
                        <h3 class="text-2xl font-bold accent-color" data-lang-key="card3_title">Career Tracks</h3>
                        <p class="mt-2 text-gray-400" data-lang-key="card3_desc">Go beyond basics with guided learning paths for Frontend, Backend, and Full Stack development, designed to get you job-ready.</p>
                    </div>
                </div>
            </div>
        </section>

        <section id="tracks" class="section-bg">
             <div class="max-w-6xl mx-auto text-center">
                <h2 class="text-4xl font-bold mb-2" data-lang-key="tracks_title">Choose Your Path</h2>
                <p class="text-gray-400 mb-12" data-lang-key="tracks_subtitle">From beginner to pro, with gamified learning.</p>
                <div class="grid md:grid-cols-3 gap-8">
                    <div class="track-card fade-in">
                        <h3 class="text-2xl font-bold" data-lang-key="track_web_title">Web Developer</h3>
                        <p class="text-gray-400 mt-2" data-lang-key="track_web_desc">Build beautiful and functional websites from scratch.</p>
                        <div class="my-6 flex-grow flex items-center justify-center gap-4 text-xs text-gray-400">
                            <span>HTML</span> <span class="accent-color">&rarr;</span> <span>CSS</span> <span class="accent-color">&rarr;</span> <span>JS</span> <span class="accent-color">&rarr;</span> <span data-lang-key="track_project">Project</span>
                        </div>
                        <p class="text-sm font-semibold" data-lang-key="track_web_final">Final Project: Personal Portfolio Site</p>
                        <button class="w-full mt-6 bg-accent-color/20 text-accent-color font-bold py-3 rounded-lg hover:bg-accent-color hover:text-white transition-colors" data-lang-key="btn_start_track">Start Track</button>
                    </div>
                    <div class="track-card fade-in" style="animation-delay: 0.2s;">
                        <h3 class="text-2xl font-bold" data-lang-key="track_app_title">App Developer</h3>
                        <p class="text-gray-400 mt-2" data-lang-key="track_app_desc">Create modern applications for any device.</p>
                        <div class="my-6 flex-grow flex items-center justify-center gap-2 text-xs text-gray-400">
                            <span>React</span> <span class="accent-color">&rarr;</span> <span>Components</span> <span class="accent-color">&rarr;</span> <span>API</span> <span class="accent-color">&rarr;</span> <span data-lang-key="track_project">Project</span>
                        </div>
                        <p class="text-sm font-semibold" data-lang-key="track_app_final">Final Project: Weather App</p>
                        <button class="w-full mt-6 bg-accent-color/20 text-accent-color font-bold py-3 rounded-lg hover:bg-accent-color hover:text-white transition-colors" data-lang-key="btn_start_track">Start Track</button>
                    </div>
                    <div class="track-card fade-in" style="animation-delay: 0.4s;">
                        <h3 class="text-2xl font-bold" data-lang-key="track_game_title">Game Developer</h3>
                        <p class="text-gray-400 mt-2" data-lang-key="track_game_desc">Bring your own interactive worlds to life.</p>
                        <div class="my-6 flex-grow flex items-center justify-center gap-2 text-xs text-gray-400">
                            <span>JS Canvas</span> <span class="accent-color">&rarr;</span> <span>Sprites</span> <span class="accent-color">&rarr;</span> <span>Physics</span> <span class="accent-color">&rarr;</span> <span data-lang-key="track_project">Project</span>
                        </div>
                        <p class="text-sm font-semibold" data-lang-key="track_game_final">Final Project: 2D Pong Game</p>
                        <button class="w-full mt-6 bg-accent-color/20 text-accent-color font-bold py-3 rounded-lg hover:bg-accent-color hover:text-white transition-colors" data-lang-key="btn_start_track">Start Track</button>
                    </div>
                </div>
            </div>
        </section>

        <!-- NEW Community Section -->
        <section id="community" class="section-bg">
            <div class="max-w-6xl mx-auto text-center">
                <h2 class="text-4xl font-bold mb-2" data-lang-key="community_title">Learn and Grow Together</h2>
                <p class="text-gray-400 mb-12" data-lang-key="community_subtitle">You're not alone. Code with peers and showcase your work.</p>
                <div class="grid md:grid-cols-2 gap-8 text-left">
                    <!-- Pair Programming -->
                    <div class="bg-[#05070D] p-8 rounded-2xl border border-[#21262d]">
                        <h3 class="text-2xl font-bold" data-lang-key="pair_title">Pair Programming</h3>
                        <p class="text-gray-400 mt-2" data-lang-key="pair_desc">Team up with another student in a live, shared code editor. Solve problems together, learn from each other, and get instant feedback in a collaborative environment.</p>
                        <button class="mt-6 bg-accent-color/20 text-accent-color font-bold py-2 px-5 rounded-lg hover:bg-accent-color hover:text-white transition-colors" data-lang-key="btn_find_partner">Find a Partner</button>
                    </div>
                    <!-- Project Showcase -->
                    <div class="bg-[#05070D] p-8 rounded-2xl border border-[#21262d]">
                        <h3 class="text-2xl font-bold" data-lang-key="showcase_title">Project Showcase Wall</h3>
                        <p class="text-gray-400 mt-2" data-lang-key="showcase_desc">Get inspired by top projects from the community. Submit your own work, get recognized, and build a portfolio that stands out to recruiters.</p>
                        <button class="mt-6 bg-gray-700/50 text-white font-bold py-2 px-5 rounded-lg hover:bg-gray-600/50 transition-colors" data-lang-key="btn_view_projects">View Projects</button>
                    </div>
                </div>
            </div>
        </section>
        
        <footer class="bg-[#0D1117] py-8">
             <div class="max-w-6xl mx-auto px-10 flex justify-between items-center text-gray-500">
                <h3 class="font-bold text-lg" data-lang-key="title_footer">Desicoder</h3>
                <div class="flex gap-6 text-sm">
                    <a href="#" class="hover:text-white transition-colors" data-lang-key="footer_about">About</a>
                    <a href="#" class="hover:text-white transition-colors" data-lang-key="footer_contact">Contact</a>
                </div>
            </div>
        </footer>

    </div>

    <script>
        const translations = {
            en: {
                title: "Desicoder",
                nav_demo: "Live Demo",
                nav_highlights: "Highlights",
                nav_tracks: "Career Tracks",
                nav_community: "Community",
                btn_signup: "Sign Up",
                drag_instruction: "Click and Drag to Rotate",
                hero_title: "Learn to Code with AI, in  Native",
                btn_start_learning: "Start Learning",
                btn_explore_paths: "Explore Career Paths",
                demo_title: "Experience the Magic",
                demo_subtitle: "Click the mic and speak your command.",
                demo_label_speak: "1. Speak your command",
                demo_label_code: "2. See the generated code",
                demo_btn_explain: "Explain Code",
                card1_title: "AI Explains Code",
                card1_desc: "Stuck on a problem? Our AI tutor breaks down complex code into simple, easy-to-understand explanations in your chosen language.",
                card2_title: "Voice to Code",
                card2_desc: "Speak your logic in Hindi or English, and watch our AI convert your thoughts into functional code. The future of coding is here.",
                card3_title: "Career Tracks",
                card3_desc: "Go beyond basics with guided learning paths for Frontend, Backend, and Full Stack development, designed to get you job-ready.",
                tracks_title: "Choose Your Path",
                tracks_subtitle: "From beginner to pro, with gamified learning.",
                track_web_title: "Web Developer",
                track_web_desc: "Build beautiful and functional websites from scratch.",
                track_app_title: "App Developer",
                track_app_desc: "Create modern applications for any device.",
                track_game_title: "Game Developer",
                track_game_desc: "Bring your own interactive worlds to life.",
                track_project: "Project",
                track_web_final: "Final Project: Personal Portfolio Site",
                track_app_final: "Final Project: Weather App",
                track_game_final: "Final Project: 2D Pong Game",
                btn_start_track: "Start Track",
                community_title: "Learn and Grow Together",
                community_subtitle: "You're not alone. Code with peers and showcase your work.",
                pair_title: "Pair Programming",
                pair_desc: "Team up with another student in a live, shared code editor. Solve problems together, learn from each other, and get instant feedback in a collaborative environment.",
                btn_find_partner: "Find a Partner",
                showcase_title: "Project Showcase Wall",
                showcase_desc: "Get inspired by top projects from the community. Submit your own work, get recognized, and build a portfolio that stands out to recruiters.",
                btn_view_projects: "View Projects",
                title_footer: "Desicoder",
                footer_about: "About",
                footer_contact: "Contact"
            },
            hi: {
                title: "देसीकोडर",
                nav_demo: "लाइव डेमो",
                nav_highlights: "मुख्य बातें",
                nav_tracks: "करियर ट्रैक्स",
                nav_community: "समुदाय",
                btn_signup: "साइन अप करें",
                drag_instruction: "घुमाने के लिए क्लिक और ड्रैग करें",
                hero_title: "AI के साथ कोडिंग सीखें, हिंदी और अंग्रेज़ी में",
                btn_start_learning: "सीखना शुरू करें",
                btn_explore_paths: "करियर के रास्ते देखें",
                demo_title: "जादू का अनुभव करें",
                demo_subtitle: "माइक पर क्लिक करें और अपनी कमांड बोलें।",
                demo_label_speak: "1. अपनी कमांड बोलें",
                demo_label_code: "2. जेनरेट किया गया कोड देखें",
                demo_btn_explain: "कोड समझाओ",
                card1_title: "AI कोड समझाएगा",
                card1_desc: "किसी समस्या में फंस गए हैं? हमारा AI ट्यूटर जटिल कोड को आपकी चुनी हुई भाषा में सरल, आसानी से समझ में आने वाले स्पष्टीकरणों में तोड़ देता है।",
                card2_title: "आवाज़ से कोड",
                card2_desc: "अपनी लॉजिक हिंदी या अंग्रेजी में बोलें, और देखें कि हमारा AI आपके विचारों को कार्यात्मक कोड में कैसे परिवर्तित करता है। कोडिंग का भविष्य यहाँ है।",
                card3_title: "करियर ट्रैक्स",
                card3_desc: "फ्रंटएंड, बैकएंड और फुल स्टैक डेवलपमेंट के लिए निर्देशित शिक्षण पथों के साथ मूल बातों से आगे बढ़ें, जो आपको नौकरी के लिए तैयार करने के लिए डिज़ाइन किए गए हैं।",
                tracks_title: "अपना रास्ता चुनें",
                tracks_subtitle: "गेमिफाइड लर्निंग के साथ, शुरुआती से प्रो तक।",
                track_web_title: "वेब डेवलपर",
                track_web_desc: "शून्य से सुंदर और कार्यात्मक वेबसाइटें बनाएं।",
                track_app_title: "ऐप डेवलपर",
                track_app_desc: "किसी भी डिवाइस के लिए आधुनिक एप्लिकेशन बनाएं।",
                track_game_title: "गेम डेवलपर",
                track_game_desc: "अपनी खुद की इंटरैक्टिव दुनिया को जीवंत करें।",
                track_project: "प्रोजेक्ट",
                track_web_final: "अंतिम प्रोजेक्ट: व्यक्तिगत पोर्टफोलियो साइट",
                track_app_final: "अंतिम प्रोजेक्ट: मौसम ऐप",
                track_game_final: "अंतिम प्रोजेक्ट: 2डी पोंग गेम",
                btn_start_track: "ट्रैक शुरू करें",
                community_title: "एक साथ सीखें और बढ़ें",
                community_subtitle: "आप अकेले नहीं हैं। साथियों के साथ कोड करें और अपना काम प्रदर्शित करें।",
                pair_title: "पेयर प्रोग्रामिंग",
                pair_desc: "एक लाइव, साझा कोड संपादक में दूसरे छात्र के साथ टीम बनाएं। समस्याओं को एक साथ हल करें, एक-दूसरे से सीखें, और एक सहयोगी वातावरण में तत्काल प्रतिक्रिया प्राप्त करें।",
                btn_find_partner: "एक साथी खोजें",
                showcase_title: "प्रोजेक्ट शोकेस वॉल",
                showcase_desc: "समुदाय की शीर्ष परियोजनाओं से प्रेरणा लें। अपना काम जमा करें, मान्यता प्राप्त करें, और एक ऐसा पोर्टफोलियो बनाएं जो नियोक्ताओं को आकर्षित करे।",
                btn_view_projects: "प्रोजेक्ट देखें",
                title_footer: "देसीकोडर",
                footer_about: "हमारे बारे में",
                footer_contact: "संपर्क करें"
            }
        };

        function changeLanguage(lang) {
            document.documentElement.lang = lang;
            document.getElementById('current-lang').textContent = lang.toUpperCase();
            
            const elements = document.querySelectorAll('[data-lang-key]');
            elements.forEach(el => {
                const key = el.getAttribute('data-lang-key');
                if (translations[lang] && translations[lang][key]) {
                    el.innerHTML = translations[lang][key];
                }
            });
        }

        document.addEventListener('DOMContentLoaded', () => {
            changeLanguage('en');

            const hero = document.getElementById('interactive-hero');
            const render = document.getElementById('tech-render');
            const instruction = document.getElementById('drag-instruction');

            let isDragging = false;
            let startX, startY;
            let currentX = 0, currentY = 0;
            let rotationX = 0, rotationY = 0;
            let animationFrameId;

            const updateRotation = () => {
                render.style.transform = `rotateX(${-rotationX}deg) rotateY(${rotationY}deg)`;
                animationFrameId = requestAnimationFrame(updateRotation);
            };
            
            hero.addEventListener('mousedown', (e) => {
                cancelAnimationFrame(animationFrameId);
                isDragging = true;
                hero.classList.add('grabbing');
                instruction.style.opacity = '0';
                startX = e.pageX - hero.offsetLeft;
                startY = e.pageY - hero.offsetTop;
                currentX = rotationY;
                currentY = rotationX;
                updateRotation();
            });

            hero.addEventListener('mouseup', () => {
                isDragging = false;
                hero.classList.remove('grabbing');
                cancelAnimationFrame(animationFrameId);
            });

            hero.addEventListener('mouseleave', () => {
                isDragging = false;
                hero.classList.remove('grabbing');
            });

            hero.addEventListener('mousemove', (e) => {
                if (!isDragging) return;
                e.preventDefault();
                const x = e.pageX - hero.offsetLeft;
                const y = e.pageY - hero.offsetTop;
                const dx = x - startX;
                const dy = y - startY;
                rotationY = currentX + dx / 4; 
                rotationX = currentY + dy / 4;
            });

            const fadeInElements = document.querySelectorAll('.fade-in');
            const observer = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) entry.target.classList.add('visible');
                });
            }, { threshold: 0.1 });
            fadeInElements.forEach(el => observer.observe(el));

            const micButton = document.getElementById('mic-button');
            const transcribedText = document.getElementById('transcribed-text');
            const codeOutput = document.getElementById('code-output');
            const explainButton = document.getElementById('explain-button');
            const demoContainer = document.getElementById('demo-container');

            micButton.addEventListener('click', () => {
                transcribedText.textContent = '';
                codeOutput.textContent = '';
                explainButton.classList.add('opacity-50', 'cursor-not-allowed');
                explainButton.disabled = true;

                micButton.classList.add('listening');
                demoContainer.classList.add('listening-glow');
                transcribedText.textContent = document.documentElement.lang === 'hi' ? 'सुन रहा हूँ...' : 'Listening...';

                setTimeout(() => {
                    micButton.classList.remove('listening');
                    demoContainer.classList.remove('listening-glow');
                    const exampleText = document.documentElement.lang === 'hi' ? 'एक बटन बनाओ जो ‘Submit’ लिखा हो और दबाने पर alert aaye' : "Make a button that says 'Submit' and shows an alert on click";
                    transcribedText.textContent = `“${exampleText}”`;
                }, 2000);

                setTimeout(() => {
                    const exampleCode = '<button onclick="alert(\'Submitted\')">Submit</button>';
                    codeOutput.innerHTML = `<span class="text-gray-500">&lt;</span><span class="text-red-400">button</span> <span class="text-blue-400">onclick</span>=<span class="text-green-400">"alert('Submitted')"</span><span class="text-gray-500">&gt;</span>Submit<span class="text-gray-500">&lt;/</span><span class="text-red-400">button</span><span class="text-gray-500">&gt;</span>`;
                    explainButton.classList.remove('opacity-50', 'cursor-not-allowed');
                    explainButton.disabled = false;
                }, 3500);
            });

            explainButton.addEventListener('click', () => {
                const originalText = explainButton.innerHTML;
                const speakingText = document.documentElement.lang === 'hi' ? 'समझा रहा हूँ...' : 'Explaining...';
                explainButton.innerHTML = speakingText;
                explainButton.classList.add('bg-accent-color');

                setTimeout(() => {
                    explainButton.innerHTML = originalText;
                    explainButton.classList.remove('bg-accent-color');
                }, 2000);
            });
        });
    </script>

</body>
</html>
