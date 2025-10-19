<!DOCTYPE html>
<html lang="en" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jonathan Bheri | Principal Controls Engineer</title>
    
    <!-- Tailwind CSS via CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Google Fonts: Inter -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;900&family=Fira+Code:wght@400;500&display=swap" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Oswald:wght@400;700&family=Playfair+Display:wght@700;900&display=swap" rel="stylesheet">
    
    <!-- Custom Tailwind Configuration -->
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        'sans': ['Inter', 'sans-serif'],
                        'mono': ['Fira Code', 'monospace'],
                        'serif': ['Playfair Display', 'serif'],
                        'sans-alt': ['Oswald', 'sans-serif'],
                    },
                    colors: {
                        'dark-navy': '#020c1b', // Main background
                        'navy': '#0a192f',      // Lighter background for elements
                        'light-navy': '#112240', // Card, nav background
                        'slate': '#8892b0',      // Default text
                        'light-slate': '#a8b2d1', // Lighter text
                        'lightest-slate': '#ccd6f6', // Headings
                        'accent': '#facc15',     // Accent color (yellow)
                    },
                    animation: {
                        'fade-in-up': 'fadeInUp 0.5s ease-out forwards',
                        'loader-fade-out': 'loaderFadeOut 0.5s 1.5s forwards',
                        'content-fade-in': 'contentFadeIn 0.5s 1.8s forwards',
                        'marquee': 'marquee 15s linear infinite',
                    },
                    keyframes: {
                        fadeInUp: {
                            '0%': { opacity: '0', transform: 'translateY(20px)' },
                            '100%': { opacity: '1', transform: 'translateY(0)' },
                        },
                        loaderFadeOut: {
                            '0%': { opacity: '1' },
                            '100%': { opacity: '0', visibility: 'hidden' },
                        },
                        contentFadeIn: {
                            '0%': { opacity: '0' },
                            '100%': { opacity: '1' },
                        },
                        marquee: {
                            '0%': { transform: 'translateX(0%)' },
                            '100%': { transform: 'translateX(-100%)' },
                        },
                    }
                }
            }
        }
    </script>
    
    <!-- Custom Styles -->
    <style type="text/tailwindcss">
        /* Apply base styles */
        body {
            @apply bg-dark-navy font-sans text-slate;
        }
        
        /* Section heading style */
        .section-heading {
            @apply flex items-center w-full text-2xl md:text-3xl font-bold font-mono text-lightest-slate mb-10 whitespace-nowrap;
        }
        .section-heading::before {
            @apply text-accent font-mono text-xl md:text-2xl mr-3 relative top-0.5;
            counter-increment: section;
            content: '0' counter(section) '.';
        }
        .section-heading::after {
            @apply block w-full h-px bg-light-navy ml-4;
            content: '';
        }
        
        /* Loader styles */
        #loader-ring {
            @apply rounded-full border-4 border-accent;
            border-top-color: transparent;
            animation: spin 1s linear infinite;
        }
        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        /* Classic blinking cursor for the new typewriter effect */
        .blinking-cursor::after {
            content: '|';
            color: theme('colors.accent');
            animation: blink 1s step-end infinite;
        }
        @keyframes blink {
            from, to { color: transparent; }
            50% { color: theme('colors.accent'); }
        }
        
        /* Scroll-triggered fade-in sections */
        .fade-in-section {
            opacity: 0;
            transform: translateY(20px);
            transition: opacity 0.6s ease-out, transform 0.6s ease-out;
            will-change: opacity, transform;
            visibility: hidden;
        }
        .fade-in-section.is-visible {
            opacity: 1;
            transform: translateY(0);
            visibility: visible;
        }
        
        /* Experience tabs */
        .tab-button {
            @apply transition-all duration-300 py-3 px-4 md:px-5 md:border-l-2 border-b-2 md:border-b-0 border-light-navy text-slate whitespace-nowrap;
        }
        .tab-button:hover {
            @apply bg-navy/50 text-accent;
        }
        .tab-button.active {
            @apply text-accent border-accent bg-navy/50;
        }
        
        /* Project card hover */
        .project-card {
            @apply transition-all duration-300 hover:-translate-y-2;
        }
        .project-card:hover .project-title {
            @apply text-accent;
        }
        .project-card:hover {
            box-shadow: 0 0 25px -5px theme('colors.accent / 20%');
        }

        /* Sticky social/email links */
        .side-link-container {
            @apply hidden md:flex fixed bottom-0 z-10 flex-col items-center;
        }
        .side-link-container::after {
            @apply content-[''] w-px h-24 bg-light-slate mt-5;
        }

        /* Carousel Styles */
        .carousel-container { @apply relative; }
        .carousel-viewport { @apply overflow-hidden rounded-lg; }
        .carousel-track {
            @apply flex transition-transform duration-500 ease-in-out;
        }
        .carousel-card {
            @apply flex-shrink-0 w-full md:w-[50%] lg:w-[33.3333%] p-2;
        }
        .carousel-button {
            @apply absolute top-1/2 -translate-y-1/2 z-10 bg-light-navy/50 text-lightest-slate rounded-full w-10 h-10 flex items-center justify-center backdrop-blur-sm hover:bg-light-navy hover:text-accent transition-all duration-300 disabled:opacity-0 disabled:cursor-not-allowed;
        }
        .carousel-dots {
            @apply flex justify-center items-center gap-2 mt-6;
        }
        .carousel-dot {
            @apply w-2 h-2 bg-light-navy rounded-full transition-all duration-300 cursor-pointer hover:bg-navy;
        }
        .carousel-dot.is-active {
            @apply bg-accent w-4;
        }

        /* Skills Marquee */
        .skill-item {
            @apply mx-6 text-base font-mono text-light-slate;
        }
        .skill-item-separator {
            @apply mx-6 text-base font-mono text-accent;
        }

    </style>
</head>

<body class="antialiased">

    <!-- Loader -->
    <div id="loader" class="fixed inset-0 z-50 flex items-center justify-center bg-dark-navy animate-loader-fade-out">
        <div class="relative w-16 h-16">
            <!-- The spinning ring -->
            <div id="loader-ring" class="absolute inset-0"></div>
            <!-- The initials in the center -->
            <div class="absolute inset-0 flex items-center justify-center">
                 <span class="text-accent text-xl font-mono font-bold" style="transform: translateY(-1px);">JB</span>
            </div>
        </div>
    </div>

    <!-- Main Content -->
    <div id="main-content" class="opacity-0 animate-content-fade-in px-6 sm:px-10 md:px-16 lg:px-24">

        <!-- Header / Navigation -->
        <header id="main-nav" class="fixed top-0 left-0 right-0 z-30 bg-dark-navy/80 backdrop-blur-md shadow-lg -translate-y-full transition-transform duration-300">
            <nav class="container mx-auto max-w-screen-xl px-6 py-4">
                <div class="flex justify-between items-center">
                    <a href="#" class="text-accent text-2xl font-bold font-mono border-2 border-accent w-10 h-10 flex items-center justify-center rounded-sm">
                        JB
                    </a>
                    <ol class="hidden md:flex items-center space-x-8 list-none font-mono text-sm">
                        <li><a href="#about" class="text-lightest-slate hover:text-accent transition-colors duration-300"><span class="text-accent mr-1.5">01.</span>About</a></li>
                        <li><a href="#experience" class="text-lightest-slate hover:text-accent transition-colors duration-300"><span class="text-accent mr-1.5">02.</span>Experience</a></li>
                        <li><a href="#projects" class="text-lightest-slate hover:text-accent transition-colors duration-300"><span class="text-accent mr-1.5">03.</span>Projects</a></li>
                        <li><a href="#contact" class="text-lightest-slate hover:text-accent transition-colors duration-300"><span class="text-accent mr-1.5">04.</span>Contact</a></li>
                    </ol>
                    <div class="md:hidden text-accent">
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-8 h-8">
                          <path stroke-linecap="round" stroke-linejoin="round" d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25h16.5" />
                        </svg>
                    </div>
                </div>
            </nav>
        </header>

        <!-- Social Links (Sticky Side) -->
        <div class="side-link-container left-6 lg:left-10">
            <ul class="flex flex-col space-y-6">
                <li>
                    <a href="https://www.linkedin.com/in/jonathanbheri" target="_blank" rel="noopener noreferrer" class="group block">
                        <span class="sr-only">LinkedIn</span>
                        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" class="w-6 h-6 fill-slate group-hover:fill-accent transition-all duration-300 group-hover:-translate-y-0.5">
                            <path d="M19 0h-14c-2.761 0-5 2.239-5 5v14c0 2.761 2.239 5 5 5h14c2.762 0 5-2.239 5-5v-14c0-2.761-2.238-5-5-5zm-11 19h-3v-11h3v11zm-1.5-12.268c-.966 0-1.75-.79-1.75-1.764s.784-1.764 1.75-1.764 1.75.79 1.75 1.764-.783 1.764-1.75 1.764zm13.5 12.268h-3v-5.604c0-3.368-4-3.113-4 0v5.604h-3v-11h3v1.765c1.396-2.586 7-2.777 7 2.476v6.759z"/>
                        </svg>
                    </a>
                </li>
                <li>
                    <a href="https://github.com/JonathanBheri" target="_blank" rel="noopener noreferrer" class="group block">
                         <span class="sr-only">GitHub</span>
                        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" class="w-6 h-6 fill-slate group-hover:fill-accent transition-all duration-300 group-hover:-translate-y-0.5">
                            <path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/>
                        </svg>
                    </a>
                </li>
            </ul>
        </div>

        <!-- Email (Sticky Side) -->
        <div class="side-link-container right-6 lg:right-10">
            <a href="mailto:jonubheri@yahoo.com" class="font-mono text-sm text-slate hover:text-accent transition-all duration-300 tracking-widest hover:-translate-y-1" style="writing-mode: vertical-rl;">
                jonubheri@yahoo.com
            </a>
        </div>

        <!-- Main Content Area -->
        <main class="container mx-auto max-w-screen-lg">

            <!-- Hero Section -->
            <section id="hero" class="min-h-screen flex flex-col justify-center items-start">
                <p class="text-accent font-mono text-base md:text-lg mb-4">Hi, my name is</p>
                <h1 class="text-4xl sm:text-6xl lg:text-7xl font-bold font-serif text-lightest-slate">Jonathan Bheri.</h1>
                <h2 class="text-4xl sm:text-5xl lg:text-6xl font-bold font-sans-alt uppercase text-slate mt-2 tracking-wide">I build things for the physical world.</h2>
                <p class="mt-6 max-w-xl text-light-slate">
                    I'm a <span id="typewriter" class="text-accent font-semibold blinking-cursor"></span> specialist based in the San Francisco Bay Area, with a passion for leading complex automation and equipment engineering projects in high-tech manufacturing.
                </p>
            </section>

            <!-- About Section -->
            <section id="about" class="py-24 fade-in-section" style="counter-reset: section 0;">
                <h2 class="section-heading">About Me</h2>
                <div class="max-w-3xl">
                    <div class="space-y-4 text-light-slate text-base md:text-lg">
                        <p>
                            As a results-driven Principal Controls Engineer, I have extensive experience leading complex automation and equipment engineering projects within the high-tech manufacturing sector. My passion lies in architecting and commissioning state-of-the-art production lines that redefine industry standards.
                        </p>
                        <p>
                            I have a proven expertise in designing advanced fire safety systems, and establishing robust data pipelines for quality control. I am deeply passionate about improving OEE, quality, and cycle time through innovative control systems, robotics, and data analytics.
                        </p>
                        
                    </div>
                    <!-- Tech Skills Marquee -->
                    <div class="relative w-full overflow-hidden bg-navy py-4 group mt-12">
                        <div class="flex animate-marquee group-hover:[animation-play-state:paused] whitespace-nowrap">
                            <div class="flex items-center flex-shrink-0">
                                <span class="skill-item">Python</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">C++</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">MATLAB</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">Ladder logic (Allen-Bradley, Siemens)</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">Structured Text</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">AutoCAD</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">ANSYS</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">CATIA</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">Unigraphics NX</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">Solidworks</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">SQL</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">Karel (Fanuc)</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">Scikit-learn</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">TensorFlow</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">Pytorch</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">Keras</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">OpenCV</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">CUDA</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">HTML</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">CSS</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">REST API</span><span class="skill-item-separator">|</span>

                            </div>
                             <div class="flex items-center flex-shrink-0" aria-hidden="true">
                                <span class="skill-item">Python</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">C++</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">MATLAB</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">Ladder logic (Allen-Bradley, Siemens)</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">Structured Text</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">SQL</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">Karel (Fanuc)</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">Scikit-learn</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">TensorFlow</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">Pytorch</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">Keras</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">OpenCV</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">CUDA</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">HTML</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">CSS</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">REST API</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">AutoCAD</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">ANSYS</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">CATIA</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">Unigraphics NX</span><span class="skill-item-separator">|</span>
                                <span class="skill-item">Solidworks</span><span class="skill-item-separator">|</span>
                            </div>
                        </div>
                    </div>
                </div>
            </section>

            <!-- Experience Section -->
            <section id="experience" class="py-24 fade-in-section" style="counter-reset: section 1;">
                <h2 class="section-heading">Work Experience</h2>
                <div class="flex flex-col md:flex-row min-h-[300px]">
                    <div class="flex flex-row md:flex-col overflow-x-auto whitespace-nowrap md:overflow-x-visible md:whitespace-normal font-mono text-sm">
                        <button class="tab-button active" data-tab="sigray">Sigray</button>
                        <button class="tab-button" data-tab="enovix">Enovix</button>
                        <button class="tab-button" data-tab="tesla">Tesla</button>
                        <button class="tab-button" data-tab="vizag">Vizag Steel</button>
                    </div>
                    <div id="tab-panels-container" class="flex-1 p-1 pt-4 md:p-2 md:pl-8">
                        <div id="tab-panel-sigray" class="tab-panel">
                            <h3 class="text-xl font-medium font-mono text-lightest-slate">
                                <span>Principal Controls Engineer</span>
                                
                            </h3>
                            <p class="font-mono text-sm text-light-slate mt-1 mb-5">Jan 2025 - Present</p>
                            <ul class="space-y-3 list-none">
                                <li class="flex"><span class="text-accent mr-3 mt-1">›</span>Owner for all controls activities across the company, encompassing integration and infrastructure for all the X-ray product lines.</li>
                                <li class="flex"><span class="text-accent mr-3 mt-1">›</span>Architected and implemented infrastructure design for system management and provisioning using Red Hat Enterprise Linux company-wide using Satellite.</li>
                                <li class="flex"><span class="text-accent mr-3 mt-1">›</span>Designed a high precision timing system with Piezo stages (PI USA) and timing/signal controller (Zebra-Quantum detector) for X-ray tomography imaging.</li>
                                <li class="flex"><span class="text-accent mr-3 mt-1">›</span>Engineered a highly sensitive leak detection system with comprehensive traceability for the XRM product line, enhancing product reliability.</li>
                            </ul>
                        </div>
                        <div id="tab-panel-enovix" class="tab-panel hidden">
                            <h3 class="text-xl font-medium font-mono text-lightest-slate">
                                <span>Principal Equipment and Controls Engineer</span>
                                
                            </h3>
                            <p class="font-mono text-sm text-light-slate mt-1 mb-5">Aug 2022 - Nov 2025</p>
                            <ul class="space-y-3 list-none">
                                <li class="flex"><span class="text-accent mr-3 mt-1">›</span>Managed critical equipment and control systems for Degas, Formation, and Testing lines, overseeing installation, configuration, and commissioning.</li>
                                <li class="flex"><span class="text-accent mr-3 mt-1">›</span>Led multiple teams in constructing a state-of-the-art production line for battery formation, achieving a throughput of 250 units per hour (UPH).</li>
                                <li class="flex"><span class="text-accent mr-3 mt-1">›</span>Designed and implemented advanced fire safety systems specifically tailored for battery-related hazards, deploying a 7-fold fire detection and control system.</li>
                                <li class="flex"><span class="text-accent mr-3 mt-1">›</span>Pioneered the design of an ASRS system for efficient battery management, increasing throughput by 12% and achieving 37% labor savings.</li>
                                <li class="flex"><span class="text-accent mr-3 mt-1">›</span>Established robust data pipelines from diverse charging and testing equipment to ensure adherence to performance and quality standards.</li>
                                <li class="flex"><span class="text-accent mr-3 mt-1">›</span>Collaborated closely with cross-functional teams to achieve ambitious production targets while maintaining safety and reliability as guiding principles.</li>
                            </ul>
                        </div>
                        <div id="tab-panel-tesla" class="tab-panel hidden">
                             <h3 class="text-xl font-medium font-mono text-lightest-slate flex items-center">
                                <span>Manufacturing Equipment Engineer at</span>
                                
                            </h3>
                            <p class="font-mono text-sm text-light-slate mt-1 mb-5">Nov 2018 – July 2022</p>
                            <ul class="space-y-3 list-none">
                                <li class="flex"><span class="text-accent mr-3 mt-1">›</span>Led projects improving OEE, Quality, and Safety on Battery pack and Enclosure lines using Allen Bradley PLCs and Ignition SCADA.</li>
                                <li class="flex"><span class="text-accent mr-3 mt-1">›</span>Decreased machine Tact time by 15 seconds on the pack line, resulting in an additional throughput of 147,000 packs per annum (a 37% increase).</li>
                                <li class="flex"><span class="text-accent mr-3 mt-1">›</span>Developed and updated logic for product development and continuous improvement projects, creating complementary HMI UI and scripts on Ignition.</li>
                                <li class="flex"><span class="text-accent mr-3 mt-1">›</span>Sustained and improved Battery pack and BMS system End of Line (EOL) Testers, designing connectors with better modularity for mass manufacturing.</li>
                                <li class="flex"><span class="text-accent mr-3 mt-1">›</span>Collaborated with cross-functional teams on DOEs, feasibility analysis, and data analytics to optimize line parameters using Python, Minitab, and Tableau.</li>
                                <li class="flex"><span class="text-accent mr-3 mt-1">›</span>Designed and prototyped custom equipment and tools using CAD and various machining techniques.</li>
                            </ul>
                        </div>
                        <div id="tab-panel-vizag" class="tab-panel hidden">
                            <h3 class="text-xl font-medium font-mono text-lightest-slate">
                                <span>Automation Intern</span>
                                
                            </h3>
                            <p class="font-mono text-sm text-light-slate mt-1 mb-5">May 2014 – June 2014</p>
                            <ul class="space-y-3 list-none">
                                <li class="flex"><span class="text-accent mr-3 mt-1">›</span>Performed inspection of the fuel and raw material delivery system for the blast furnace.</li>
                                <li class="flex"><span class="text-accent mr-3 mt-1">›</span>Assessed and developed a system model to improve blast furnace performance.</li>
                                <li class="flex"><span class="text-accent mr-3 mt-1">›</span>Developed a Failure Tolerant control system to manage the flow of fuel and raw materials into the system.</li>
                                <li class="flex"><span class="text-accent mr-3 mt-1">›</span>Reported the assessment on the control system to the Instrumentation Engineer for implementation.</li>
                            </ul>
                        </div>
                    </div>
                </div>
            </section>

            <!-- Projects Section -->
            <section id="projects" class="py-24 fade-in-section" style="counter-reset: section 2;">
                <h2 class="section-heading">Personal Projects</h2>
                <div class="carousel-container">
                    <div class="carousel-viewport">
                        <div id="project-carousel-track" class="carousel-track -ml-2">
                            <!-- Project cards will be injected here by JavaScript -->
                        </div>
                    </div>
                    
                    <!-- Carousel Navigation -->
                    <button id="prev-btn" aria-label="Previous Project" class="carousel-button left-0 md:-left-5">
                        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7"></path></svg>
                    </button>
                    <button id="next-btn" aria-label="Next Project" class="carousel-button right-0 md:-right-5">
                        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"></path></svg>
                    </button>
                </div>
                <!-- Dot navigation -->
                <div id="carousel-dots-container" class="carousel-dots"></div>
            </section>
            
            <!-- Contact Section -->
            <section id="contact" class="py-24 text-center fade-in-section" style="counter-reset: section 3;">
                <h2 class="text-accent font-mono mb-3 text-lg">04. What's Next?</h2>
                <h3 class="text-4xl md:text-5xl font-bold font-mono text-lightest-slate mb-4">Get In Touch</h3>
                <p class="text-light-slate max-w-lg mx-auto mb-10 text-base md:text-lg">
                    I'm currently seeking new opportunities and am always open to discussing new projects, creative ideas, or ways to contribute to your vision. My inbox is always open, so please feel free to reach out.
                </p>
                <a href="mailto:jonubheri@yahoo.com" class="text-accent border border-accent rounded px-8 py-4 font-mono text-sm transition duration-300 hover:bg-accent/10">
                    Say Hello
                </a>
            </section>

        </main>

        <!-- Footer -->
        <footer class="text-center text-slate text-xs font-mono py-8">
            <p>Designed & Built by Jonathan Bheri</p>
        </footer>

    </div>

    <!-- JavaScript -->
    <script>
        document.addEventListener('DOMContentLoaded', () => {

            const isReducedMotion = window.matchMedia(`(prefers-reduced-motion: reduce)`).matches === true;

            // --- 1. Typewriter Effect ---
            if (!isReducedMotion) {
                const typewriterElement = document.getElementById('typewriter');
                const words = [
                    'Principal Controls Engineer',
                    'Automation Specialist',
                    'Robotics Enthusiast',
                    'Problem Solver',
                    'AI Vision Engineer'
                ];
                let wordIndex = 0;
                let charIndex = 0;
                let isDeleting = false;

                function type() {
                    const currentWord = words[wordIndex];
                    let typeSpeed = isDeleting ? 60 : 120;

                    if (isDeleting) {
                        // Deleting characters
                        typewriterElement.textContent = currentWord.substring(0, charIndex - 1);
                        charIndex--;
                    } else {
                        // Typing characters
                        typewriterElement.textContent = currentWord.substring(0, charIndex + 1);
                        charIndex++;
                    }

                    // Logic to switch states
                    if (!isDeleting && charIndex === currentWord.length) {
                        // Pause at the end of a word, then start deleting
                        typeSpeed = 2000;
                        isDeleting = true;
                    } else if (isDeleting && charIndex === 0) {
                        // Finished deleting, move to the next word
                        isDeleting = false;
                        wordIndex = (wordIndex + 1) % words.length;
                        typeSpeed = 500; // Pause before typing new word
                    }

                    setTimeout(type, typeSpeed);
                }
                // Start the effect after a delay
                setTimeout(type, 1800);
            } else {
                 // For reduced motion, just show the first title
                 document.getElementById('typewriter').textContent = 'Principal Controls Engineer';
            }

            // --- 2. Sticky Nav on Scroll ---
            const nav = document.getElementById('main-nav');
            
            window.addEventListener('scroll', () => {
                if (window.scrollY > 100) {
                    nav.classList.remove('-translate-y-full');
                } else {
                    nav.classList.add('-translate-y-full');
                }
            });
            
            // --- 3. Intersection Observer for Fade-in Sections ---
            if (!isReducedMotion) {
                const sections = document.querySelectorAll('.fade-in-section');
                const observerOptions = {
                    root: null, rootMargin: '0px', threshold: 0.1
                };

                const observer = new IntersectionObserver((entries, observer) => {
                    entries.forEach(entry => {
                        if (entry.isIntersecting) {
                            entry.target.classList.add('is-visible');
                            observer.unobserve(entry.target);
                        }
                    });
                }, observerOptions);

                sections.forEach(section => {
                    observer.observe(section);
                });
            } else {
                 document.querySelectorAll('.fade-in-section').forEach(section => {
                    section.classList.add('is-visible');
                 });
            }

            // --- 4. Experience Tabs ---
            const tabButtons = document.querySelectorAll('.tab-button');
            const tabPanelsContainer = document.getElementById('tab-panels-container');

            tabButtons.forEach(button => {
                button.addEventListener('click', () => {
                    const targetTab = button.getAttribute('data-tab');
                    const targetPanel = document.getElementById(`tab-panel-${targetTab}`);
                    
                    tabButtons.forEach(btn => btn.classList.remove('active'));
                    button.classList.add('active');

                    // Simple animation for the panel switch
                    tabPanelsContainer.style.opacity = '0';
                    setTimeout(() => {
                        document.querySelectorAll('.tab-panel').forEach(p => p.classList.add('hidden'));
                        targetPanel.classList.remove('hidden');
                        tabPanelsContainer.style.opacity = '1';
                    }, 150);
                });
            });

            // --- 5. Project Carousel ---
            const projectTrack = document.getElementById('project-carousel-track');
            const dotsContainer = document.getElementById('carousel-dots-container');
            const prevButton = document.getElementById('prev-btn');
            const nextButton = document.getElementById('next-btn');

            const projectData = [
                { title: 'Video Description Generation', desc: 'Used ViBe, StAR, VGG, and EKF to separate, identify, label, and track objects in video frames to generate descriptions based on relative motion.', tech: ['OpenCV', 'Python', 'TensorFlow'] },
                { title: 'Feature Importance Analysis', desc: 'Analyzed feature importance for a 15-joint robot using SVR with sequential feature selection and Random Forest with Gini impurity for ranking.', tech: ['MATLAB', 'Python', 'Scikit-learn'] },
                { title: 'Raspberry Pi Parking Assistance', desc: 'Developed a parking assistance system using Simulink for signal processing and a Raspberry Pi for deployment, providing proximity alerts.', tech: ['Simulink', 'MATLAB', 'Raspberry Pi'] },
                { title: 'FMCW Synthetic Aperture Radar', desc: 'Developed an algorithm for target detection using FMCW and constructed a MATLAB simulation to swath the target using a Synthetic Aperture Radar.', tech: ['MATLAB'] },
                { title: 'SnakeBot: Vertebral Robot', desc: 'Designed a vertebral-structured robot to demonstrate snake slithering mechanics, controlled by an Arduino and servo motors.', tech: ['3D printing', 'Creo', 'Arduino', 'C'] },
                { title: 'Image Texture Transfer', desc: 'Used Image Quilting and Fast Texture Transfer algorithms to transfer artistic textures to photographic images for photo-realistic renderings.', tech: ['MATLAB'] },
            ];

            // Populate carousel
            projectTrack.innerHTML = projectData.map(p => {
                const techList = p.tech.map(t => `<li class="mr-4">${t}</li>`).join('');
                return `
                    <div class="carousel-card">
                        <div class="project-card bg-light-navy rounded-lg p-6 flex flex-col h-full shadow-lg">
                             <div class="flex-grow">
                                <h3 class="project-title text-lg font-bold font-mono text-lightest-slate mb-3 transition-colors">${p.title}</h3>
                                <p class="text-sm text-light-slate">${p.desc}</p>
                            </div>
                            <footer class="mt-auto pt-4">
                                <ul class="flex flex-wrap font-mono text-xs text-slate">${techList}</ul>
                            </footer>
                        </div>
                    </div>
                `;
            }).join('');

            // Carousel Logic
            const slides = Array.from(projectTrack.children);
            const slideWidth = slides[0].getBoundingClientRect().width;
            let currentIndex = 0;

            const setSlidePosition = (slide, index) => {
                // Not needed for flexbox, but good practice if not using it
            };
            slides.forEach(setSlidePosition);

            const moveToSlide = (track, currentSlide, targetSlide) => {
                const targetIndex = slides.findIndex(slide => slide === targetSlide);
                track.style.transform = 'translateX(-' + targetSlide.getBoundingClientRect().width * targetIndex + 'px)';
                currentSlide.classList.remove('is-active');
                targetSlide.classList.add('is-active');
                currentIndex = targetIndex;
            };

            const updateDots = (currentDot, targetDot) => {
                currentDot.classList.remove('is-active');
                targetDot.classList.add('is-active');
            };
            
            const updateNavButtons = () => {
                prevButton.disabled = currentIndex === 0;
                nextButton.disabled = currentIndex === slides.length - 1;
            };

            // Create dots
            slides.forEach((_, index) => {
                const button = document.createElement('button');
                button.classList.add('carousel-dot');
                if (index === 0) button.classList.add('is-active');
                dotsContainer.appendChild(button);
            });
            const dots = Array.from(dotsContainer.children);

            // Button listeners
            prevButton.addEventListener('click', () => {
                if(currentIndex === 0) return;
                moveToSlide(projectTrack, slides[currentIndex], slides[currentIndex - 1]);
                updateDots(dots[currentIndex + 1], dots[currentIndex]);
                updateNavButtons();
            });

            nextButton.addEventListener('click', () => {
                if(currentIndex === slides.length - 1) return;
                moveToSlide(projectTrack, slides[currentIndex], slides[currentIndex + 1]);
                updateDots(dots[currentIndex - 1], dots[currentIndex]);
                updateNavButtons();
            });

            dotsContainer.addEventListener('click', e => {
                const targetDot = e.target.closest('button');
                if (!targetDot) return;
                
                const currentDot = dotsContainer.querySelector('.is-active');
                const targetIndex = dots.findIndex(dot => dot === targetDot);
                
                moveToSlide(projectTrack, slides[currentIndex], slides[targetIndex]);
                updateDots(currentDot, targetDot);
                updateNavButtons();
            });
            
            updateNavButtons();

        });
    </script>
</body>
</html>











