Today I Built my Personal Portfolio Website using claude.ai 

# PROMPT GIVEN TO CLAUDE :

You are an expert full-stack web developer and personal branding designer.

Build a complete, modern, single-file personal portfolio website using HTML, Tailwind CSS (CDN), and vanilla JavaScript for this person:

=== PERSONAL INFO ===
Name: [Your Name]
Title: [e.g., 'Data Science Enthusiast | GenAI Builder']
Location: [City, Country]
Email: [email]
LinkedIn: [URL]
GitHub: [URL]
About: [2-3 sentences about yourself]

=== SKILLS ===
Technical: [Python, ML, SQL, etc.]
Tools: [VS Code, Jupyter, Power BI, etc.]
Soft Skills: [Leadership, Communication, etc.]

=== PROJECTS ===
1. [Project Name] — [1 line description] — Tech: [stack]
2. [Project Name] — [1 line description] — Tech: [stack]
3. [Project Name] — [1 line description] — Tech: [stack]

=== EXPERIENCE & ACHIEVEMENTS ===
- [Internship / Hackathon / Certification]
- [Award / Rank / Notable achievement]

=== DESIGN PREFERENCES ===
Mode: Dark/Light toggle
Style: Modern, minimal, premium
Colors: [e.g., Purple + Teal, or Blue + Orange]
Font: Clean sans-serif display font

=== REQUIREMENTS ===
Include these sections:
- Hero (name, title, typing animation, social links)
- About Me
- Skills (animated bars + tech tags)
- Projects (cards with tech tags)
- Achievements & Certifications
- Contact (form + direct links)
- Dark/Light mode toggle
- Mobile responsive
- Smooth scroll animations
- Active nav highlighting
- Single HTML file, no build step
- Tailwind via CDN
- SEO meta tags included

Optional:
- If a resume is uploaded, extract details automatically.
- If a profile photo is uploaded, use it in the portfolio.
- Generate recruiter-friendly content and project descriptions from resume data.

Return only the complete HTML code.


## HTML CODE OF THE PORTFOLIO :
<!DOCTYPE html>
<html lang="en" class="scroll-smooth">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Nandika Sharma | Full Stack & AI/ML Developer</title>
  <meta name="description" content="Nandika Sharma — MCA graduate skilled in Full Stack Development, AI/ML, Python, React.js, and Data Analytics. Based in Meerut, India." />
  <meta name="keywords" content="Nandika Sharma, Full Stack Developer, AI ML, Python, React, Flask, Portfolio, Meerut" />
  <meta name="author" content="Nandika Sharma" />
  <meta property="og:title" content="Nandika Sharma | Full Stack & AI/ML Developer" />
  <meta property="og:description" content="Motivated MCA graduate building AI-powered web solutions." />
  <meta property="og:type" content="website" />
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet" />
  <script src="https://cdn.tailwindcss.com"></script>
  <script>
    tailwind.config = {
      darkMode: 'class',
      theme: {
        extend: {
          fontFamily: {
            sans: ['Space Grotesk', 'sans-serif'],
            mono: ['JetBrains Mono', 'monospace'],
          },
          colors: {
            violet: {
              400: '#a78bfa',
              500: '#8b5cf6',
              600: '#7c3aed',
            },
            teal: {
              400: '#2dd4bf',
              500: '#14b8a6',
            },
          },
          animation: {
            'fade-in': 'fadeIn 0.6s ease forwards',
            'slide-up': 'slideUp 0.6s ease forwards',
            'pulse-slow': 'pulse 3s ease-in-out infinite',
          },
          keyframes: {
            fadeIn: { from: { opacity: 0 }, to: { opacity: 1 } },
            slideUp: { from: { opacity: 0, transform: 'translateY(30px)' }, to: { opacity: 1, transform: 'translateY(0)' } },
          },
        },
      },
    };
  </script>
  <style>
    :root {
      --violet: #8b5cf6;
      --teal: #14b8a6;
    }

    /* ---- GLOBAL ---- */
    * { box-sizing: border-box; }
    html { scroll-behavior: smooth; }

    body {
      font-family: 'Space Grotesk', sans-serif;
      transition: background 0.3s, color 0.3s;
    }

    /* DARK */
    .dark body, body.dark {
      background: #0a0a0f;
      color: #e2e8f0;
    }
    .dark { background: #0a0a0f; color: #e2e8f0; }

    /* LIGHT */
    body:not(.dark) {
      background: #f8f8fc;
      color: #1a1a2e;
    }

    /* ---- GRADIENT TEXT ---- */
    .grad {
      background: linear-gradient(135deg, var(--violet), var(--teal));
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
    }

    /* ---- GLOW EFFECT ---- */
    .glow-violet {
      box-shadow: 0 0 32px rgba(139,92,246,0.25), 0 0 0 1px rgba(139,92,246,0.15);
    }
    .glow-teal {
      box-shadow: 0 0 32px rgba(20,184,166,0.2);
    }

    /* ---- TYPING CURSOR ---- */
    #typed-text::after {
      content: '|';
      animation: blink 0.75s step-end infinite;
      color: var(--violet);
    }
    @keyframes blink { 50% { opacity: 0; } }

    /* ---- SKILL BAR ---- */
    .skill-bar-inner {
      height: 4px;
      border-radius: 2px;
      background: linear-gradient(90deg, var(--violet), var(--teal));
      width: 0;
      transition: width 1.2s cubic-bezier(.4,0,.2,1);
    }

    /* ---- CARD ---- */
    .project-card {
      transition: transform 0.25s ease, box-shadow 0.25s ease;
    }
    .project-card:hover {
      transform: translateY(-6px);
    }
    .dark .project-card:hover {
      box-shadow: 0 12px 40px rgba(139,92,246,0.2);
    }
    .light .project-card:hover {
      box-shadow: 0 12px 40px rgba(139,92,246,0.12);
    }

    /* ---- NAV PILL ---- */
    .nav-link.active { color: var(--violet); }

    /* ---- MESH BG ---- */
    .mesh-bg {
      background-image:
        radial-gradient(ellipse 60% 50% at 20% 30%, rgba(139,92,246,0.08) 0%, transparent 60%),
        radial-gradient(ellipse 50% 60% at 80% 70%, rgba(20,184,166,0.07) 0%, transparent 60%);
    }

    /* ---- SCROLL REVEAL ---- */
    .reveal {
      opacity: 0;
      transform: translateY(28px);
      transition: opacity 0.6s ease, transform 0.6s ease;
    }
    .reveal.visible {
      opacity: 1;
      transform: none;
    }

    /* ---- CONTACT INPUT ---- */
    .contact-input {
      background: transparent;
      border-bottom: 1.5px solid rgba(139,92,246,0.3);
      outline: none;
      transition: border-color 0.2s;
      width: 100%;
      padding: 8px 0;
    }
    .contact-input:focus {
      border-color: var(--violet);
    }
    .dark .contact-input { color: #e2e8f0; }
    .contact-input::placeholder { color: #94a3b8; }

    /* ---- AVATAR RING ---- */
    .avatar-ring {
      background: linear-gradient(135deg, var(--violet), var(--teal));
      padding: 3px;
      border-radius: 50%;
      display: inline-block;
    }

    /* ---- CHIP ---- */
    .chip {
      font-family: 'JetBrains Mono', monospace;
      font-size: 0.72rem;
      padding: 3px 10px;
      border-radius: 4px;
      font-weight: 500;
      letter-spacing: 0.02em;
    }
    .dark .chip {
      background: rgba(139,92,246,0.12);
      border: 1px solid rgba(139,92,246,0.25);
      color: #a78bfa;
    }
    .chip:not(.dark .chip) {
      background: rgba(139,92,246,0.08);
      border: 1px solid rgba(139,92,246,0.2);
      color: #7c3aed;
    }

    /* ---- SECTION LABEL ---- */
    .section-label {
      font-family: 'JetBrains Mono', monospace;
      font-size: 0.72rem;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      color: var(--teal);
    }

    /* ---- MOBILE MENU ---- */
    #mobile-menu {
      transition: max-height 0.3s ease, opacity 0.3s ease;
      max-height: 0;
      overflow: hidden;
      opacity: 0;
    }
    #mobile-menu.open {
      max-height: 320px;
      opacity: 1;
    }

    /* ---- TOAST ---- */
    #toast {
      transition: opacity 0.3s, transform 0.3s;
    }
  </style>
</head>

<body class="dark">

<!-- ═══════════════════════ NAVBAR ═══════════════════════ -->
<nav id="navbar" class="fixed top-0 left-0 right-0 z-50 transition-all duration-300">
  <div class="max-w-6xl mx-auto px-6 h-16 flex items-center justify-between">

    <!-- Logo -->
    <a href="#hero" class="font-mono text-sm font-semibold grad">nandika.dev</a>

    <!-- Desktop nav -->
    <ul class="hidden md:flex items-center gap-8 text-sm font-medium">
      <li><a class="nav-link transition-colors hover:text-violet-400" href="#about">About</a></li>
      <li><a class="nav-link transition-colors hover:text-violet-400" href="#skills">Skills</a></li>
      <li><a class="nav-link transition-colors hover:text-violet-400" href="#projects">Projects</a></li>
      <li><a class="nav-link transition-colors hover:text-violet-400" href="#achievements">Achievements</a></li>
      <li><a class="nav-link transition-colors hover:text-violet-400" href="#contact">Contact</a></li>
    </ul>

    <!-- Right controls -->
    <div class="flex items-center gap-3">
      <!-- Dark/Light toggle -->
      <button id="theme-toggle" aria-label="Toggle theme"
        class="w-9 h-9 rounded-lg flex items-center justify-center transition hover:bg-white/10">
        <svg id="sun-icon" class="hidden w-5 h-5 text-yellow-300" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <circle cx="12" cy="12" r="5"/><path stroke-linecap="round" d="M12 2v2M12 20v2M4.22 4.22l1.42 1.42M18.36 18.36l1.42 1.42M2 12h2M20 12h2M4.22 19.78l1.42-1.42M18.36 5.64l1.42-1.42"/>
        </svg>
        <svg id="moon-icon" class="w-5 h-5 text-slate-300" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 12.79A9 9 0 1111.21 3a7 7 0 009.79 9.79z"/>
        </svg>
      </button>

      <!-- Hamburger -->
      <button id="hamburger" class="md:hidden w-9 h-9 flex flex-col justify-center items-center gap-1.5 rounded-lg hover:bg-white/10 transition" aria-label="Menu">
        <span class="w-5 h-0.5 bg-current transition-all" id="hb1"></span>
        <span class="w-5 h-0.5 bg-current transition-all" id="hb2"></span>
        <span class="w-5 h-0.5 bg-current transition-all" id="hb3"></span>
      </button>
    </div>
  </div>

  <!-- Mobile menu -->
  <div id="mobile-menu" class="md:hidden px-6 pb-4 dark:bg-[#0a0a0f]/95 bg-white/95 backdrop-blur-md border-t dark:border-white/5 border-slate-200">
    <ul class="flex flex-col gap-3 pt-3 text-sm font-medium">
      <li><a class="nav-link block py-1 hover:text-violet-400 transition" href="#about" onclick="closeMobileMenu()">About</a></li>
      <li><a class="nav-link block py-1 hover:text-violet-400 transition" href="#skills" onclick="closeMobileMenu()">Skills</a></li>
      <li><a class="nav-link block py-1 hover:text-violet-400 transition" href="#projects" onclick="closeMobileMenu()">Projects</a></li>
      <li><a class="nav-link block py-1 hover:text-violet-400 transition" href="#achievements" onclick="closeMobileMenu()">Achievements</a></li>
      <li><a class="nav-link block py-1 hover:text-violet-400 transition" href="#contact" onclick="closeMobileMenu()">Contact</a></li>
    </ul>
  </div>
</nav>

<!-- ═══════════════════════ HERO ═══════════════════════ -->
<section id="hero" class="relative min-h-screen flex items-center justify-center mesh-bg overflow-hidden pt-16">

  <!-- Decorative orbs -->
  <div class="absolute top-1/4 left-1/4 w-64 h-64 rounded-full blur-3xl opacity-20 animate-pulse-slow" style="background: radial-gradient(circle, #8b5cf6, transparent)"></div>
  <div class="absolute bottom-1/4 right-1/4 w-64 h-64 rounded-full blur-3xl opacity-15 animate-pulse-slow" style="background: radial-gradient(circle, #14b8a6, transparent); animation-delay:1.5s"></div>

  <div class="relative max-w-6xl mx-auto px-6 flex flex-col lg:flex-row items-center gap-12 lg:gap-20">

    <!-- Text side -->
    <div class="flex-1 text-center lg:text-left">
      <p class="section-label mb-4 animate-fade-in">Hello, I'm</p>
      <h1 class="text-5xl sm:text-6xl lg:text-7xl font-bold tracking-tight mb-4 leading-none">
        <span class="grad">Nandika</span><br/>
        <span class="dark:text-white text-slate-900">Sharma</span>
      </h1>
      <div class="text-lg sm:text-xl font-mono mb-6 dark:text-slate-400 text-slate-600 min-h-[1.8em]">
        <span id="typed-text"></span>
      </div>
      <p class="text-base dark:text-slate-400 text-slate-600 max-w-lg mx-auto lg:mx-0 leading-relaxed mb-8">
        MCA graduate turning complex problems into elegant, AI-powered web solutions. From skin-disease detection to real-time fitness AI — I build things that matter.
      </p>

      <!-- CTA -->
      <div class="flex flex-wrap gap-3 justify-center lg:justify-start mb-10">
        <a href="#projects" class="px-6 py-3 rounded-lg text-sm font-semibold text-white transition hover:opacity-90 hover:scale-105" style="background: linear-gradient(135deg, #8b5cf6, #14b8a6)">
          View Projects
        </a>
        <a href="#contact" class="px-6 py-3 rounded-lg text-sm font-semibold border transition hover:bg-violet-500/10 dark:border-violet-400/30 border-violet-500/30 dark:text-violet-300 text-violet-700">
          Get in Touch
        </a>
      </div>

      <!-- Social links -->
      <div class="flex items-center gap-4 justify-center lg:justify-start">
        <span class="text-xs dark:text-slate-500 text-slate-400 font-mono uppercase tracking-widest">Find me on</span>
        <a href="https://github.com/Nandikas00" target="_blank" rel="noopener" aria-label="GitHub"
          class="w-9 h-9 rounded-lg flex items-center justify-center dark:bg-white/5 bg-slate-100 hover:bg-violet-500/20 transition">
          <svg class="w-4 h-4" fill="currentColor" viewBox="0 0 24 24"><path d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112 6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0022 12.017C22 6.484 17.522 2 12 2z"/></svg>
        </a>
        <a href="https://www.linkedin.com/in/nandika-sharma-743560202/" target="_blank" rel="noopener" aria-label="LinkedIn"
          class="w-9 h-9 rounded-lg flex items-center justify-center dark:bg-white/5 bg-slate-100 hover:bg-teal-500/20 transition">
          <svg class="w-4 h-4" fill="currentColor" viewBox="0 0 24 24"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 01-2.063-2.065 2.064 2.064 0 112.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>
        </a>
        <a href="mailto:nandikasharma0@gmail.com" aria-label="Email"
          class="w-9 h-9 rounded-lg flex items-center justify-center dark:bg-white/5 bg-slate-100 hover:bg-violet-500/20 transition">
          <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"/></svg>
        </a>
      </div>
    </div>

    <!-- Avatar side -->
    <div class="flex-shrink-0 reveal">
      <div class="avatar-ring">
        <div class="w-52 h-52 sm:w-64 sm:h-64 rounded-full dark:bg-slate-900 bg-slate-100 flex items-center justify-center overflow-hidden">
          <!-- Initials avatar -->
          <div class="flex flex-col items-center justify-center select-none">
            <span class="text-6xl font-bold grad leading-none">N</span>
            <span class="text-xs font-mono dark:text-slate-500 text-slate-400 mt-2 tracking-widest uppercase">Full Stack · AI/ML</span>
          </div>
        </div>
      </div>
      <!-- Location badge -->
      <div class="mt-4 flex items-center justify-center gap-2 dark:text-slate-400 text-slate-500 text-sm">
        <svg class="w-4 h-4 text-teal-400 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"/><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"/></svg>
        Meerut, India
      </div>
    </div>

  </div>

  <!-- Scroll indicator -->
  <div class="absolute bottom-8 left-1/2 -translate-x-1/2 flex flex-col items-center gap-2 animate-bounce opacity-50">
    <span class="text-xs font-mono uppercase tracking-widest">scroll</span>
    <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"/></svg>
  </div>
</section>

<!-- ═══════════════════════ ABOUT ═══════════════════════ -->
<section id="about" class="py-24 px-6">
  <div class="max-w-6xl mx-auto">
    <div class="reveal">
      <p class="section-label mb-3">Who I am</p>
      <h2 class="text-3xl sm:text-4xl font-bold mb-12 dark:text-white text-slate-900">About Me</h2>
    </div>

    <div class="grid md:grid-cols-2 gap-12 items-center">
      <!-- Text -->
      <div class="reveal space-y-5">
        <p class="dark:text-slate-300 text-slate-700 leading-relaxed">
          I'm a motivated <strong class="dark:text-white text-slate-900 font-semibold">MCA graduate</strong> passionate about building products at the intersection of full-stack engineering and artificial intelligence. I love turning real-world challenges into clean, scalable software — whether that's a neural network diagnosing skin conditions or a platform coaching your fitness goals.
        </p>
        <p class="dark:text-slate-300 text-slate-700 leading-relaxed">
          My technical range spans Python, React.js, Flask, Angular, and SQL, with hands-on experience architecting ML prediction systems and deploying production-grade web applications. I care deeply about code quality, user experience, and the stories data can tell.
        </p>
        <p class="dark:text-slate-300 text-slate-700 leading-relaxed">
          When I'm not building, I'm exploring the latest in AI research, contributing to open-source, or mentoring peers through complex technical concepts — leadership is a skill I treat as seriously as any framework.
        </p>
      </div>

      <!-- Stats cards -->
      <div class="reveal grid grid-cols-2 gap-4">
        <div class="dark:bg-white/4 bg-white rounded-xl p-5 border dark:border-white/8 border-slate-200 glow-violet">
          <div class="text-3xl font-bold grad mb-1">3+</div>
          <div class="text-sm dark:text-slate-400 text-slate-500">AI/ML Projects Shipped</div>
        </div>
        <div class="dark:bg-white/4 bg-white rounded-xl p-5 border dark:border-white/8 border-slate-200">
          <div class="text-3xl font-bold grad mb-1">10+</div>
          <div class="text-sm dark:text-slate-400 text-slate-500">Technologies Mastered</div>
        </div>
        <div class="dark:bg-white/4 bg-white rounded-xl p-5 border dark:border-white/8 border-slate-200">
          <div class="text-3xl font-bold grad mb-1">MCA</div>
          <div class="text-sm dark:text-slate-400 text-slate-500">Master's in Computer Applications</div>
        </div>
        <div class="dark:bg-white/4 bg-white rounded-xl p-5 border dark:border-white/8 border-slate-200 glow-teal">
          <div class="text-3xl font-bold grad mb-1">IIT</div>
          <div class="text-sm dark:text-slate-400 text-slate-500">Bombay Certified</div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ═══════════════════════ SKILLS ═══════════════════════ -->
<section id="skills" class="py-24 px-6 dark:bg-white/[0.02] bg-slate-50">
  <div class="max-w-6xl mx-auto">
    <div class="reveal">
      <p class="section-label mb-3">What I work with</p>
      <h2 class="text-3xl sm:text-4xl font-bold mb-12 dark:text-white text-slate-900">Skills & Tools</h2>
    </div>

    <div class="grid md:grid-cols-2 gap-12">

      <!-- Skill bars -->
      <div class="reveal">
        <h3 class="text-sm font-mono uppercase tracking-widest text-violet-400 mb-6">Technical Proficiency</h3>
        <div class="space-y-5" id="skill-bars">

          <div class="skill-item">
            <div class="flex justify-between mb-2 text-sm font-medium dark:text-slate-300 text-slate-700">
              <span>Python & ML</span><span class="font-mono text-xs text-violet-400">90%</span>
            </div>
            <div class="h-1 dark:bg-white/10 bg-slate-200 rounded-full">
              <div class="skill-bar-inner" data-width="90"></div>
            </div>
          </div>

          <div class="skill-item">
            <div class="flex justify-between mb-2 text-sm font-medium dark:text-slate-300 text-slate-700">
              <span>React.js</span><span class="font-mono text-xs text-violet-400">85%</span>
            </div>
            <div class="h-1 dark:bg-white/10 bg-slate-200 rounded-full">
              <div class="skill-bar-inner" data-width="85"></div>
            </div>
          </div>

          <div class="skill-item">
            <div class="flex justify-between mb-2 text-sm font-medium dark:text-slate-300 text-slate-700">
              <span>Flask & Node.js</span><span class="font-mono text-xs text-violet-400">82%</span>
            </div>
            <div class="h-1 dark:bg-white/10 bg-slate-200 rounded-full">
              <div class="skill-bar-inner" data-width="82"></div>
            </div>
          </div>

          <div class="skill-item">
            <div class="flex justify-between mb-2 text-sm font-medium dark:text-slate-300 text-slate-700">
              <span>SQL & Databases</span><span class="font-mono text-xs text-violet-400">80%</span>
            </div>
            <div class="h-1 dark:bg-white/10 bg-slate-200 rounded-full">
              <div class="skill-bar-inner" data-width="80"></div>
            </div>
          </div>

          <div class="skill-item">
            <div class="flex justify-between mb-2 text-sm font-medium dark:text-slate-300 text-slate-700">
              <span>Deep Learning / CNNs</span><span class="font-mono text-xs text-violet-400">78%</span>
            </div>
            <div class="h-1 dark:bg-white/10 bg-slate-200 rounded-full">
              <div class="skill-bar-inner" data-width="78"></div>
            </div>
          </div>

          <div class="skill-item">
            <div class="flex justify-between mb-2 text-sm font-medium dark:text-slate-300 text-slate-700">
              <span>Angular</span><span class="font-mono text-xs text-violet-400">72%</span>
            </div>
            <div class="h-1 dark:bg-white/10 bg-slate-200 rounded-full">
              <div class="skill-bar-inner" data-width="72"></div>
            </div>
          </div>

          <div class="skill-item">
            <div class="flex justify-between mb-2 text-sm font-medium dark:text-slate-300 text-slate-700">
              <span>HTML / CSS / JS</span><span class="font-mono text-xs text-violet-400">88%</span>
            </div>
            <div class="h-1 dark:bg-white/10 bg-slate-200 rounded-full">
              <div class="skill-bar-inner" data-width="88"></div>
            </div>
          </div>

        </div>
      </div>

      <!-- Tech tags + tools -->
      <div class="reveal space-y-8">
        <div>
          <h3 class="text-sm font-mono uppercase tracking-widest text-violet-400 mb-4">Technology Stack</h3>
          <div class="flex flex-wrap gap-2">
            <span class="chip dark:bg-violet-500/15 dark:border-violet-400/20 dark:text-violet-300 bg-violet-50 border-violet-200 text-violet-700">Python</span>
            <span class="chip dark:bg-violet-500/15 dark:border-violet-400/20 dark:text-violet-300 bg-violet-50 border-violet-200 text-violet-700">React.js</span>
            <span class="chip dark:bg-violet-500/15 dark:border-violet-400/20 dark:text-violet-300 bg-violet-50 border-violet-200 text-violet-700">Flask</span>
            <span class="chip dark:bg-violet-500/15 dark:border-violet-400/20 dark:text-violet-300 bg-violet-50 border-violet-200 text-violet-700">Angular</span>
            <span class="chip dark:bg-violet-500/15 dark:border-violet-400/20 dark:text-violet-300 bg-violet-50 border-violet-200 text-violet-700">Node.js</span>
            <span class="chip dark:bg-violet-500/15 dark:border-violet-400/20 dark:text-violet-300 bg-violet-50 border-violet-200 text-violet-700">SQL</span>
            <span class="chip dark:bg-violet-500/15 dark:border-violet-400/20 dark:text-violet-300 bg-violet-50 border-violet-200 text-violet-700">PostgreSQL</span>
            <span class="chip dark:bg-violet-500/15 dark:border-violet-400/20 dark:text-violet-300 bg-violet-50 border-violet-200 text-violet-700">TensorFlow</span>
            <span class="chip dark:bg-violet-500/15 dark:border-violet-400/20 dark:text-violet-300 bg-violet-50 border-violet-200 text-violet-700">CNN</span>
            <span class="chip dark:bg-violet-500/15 dark:border-violet-400/20 dark:text-violet-300 bg-violet-50 border-violet-200 text-violet-700">OpenCV</span>
            <span class="chip dark:bg-violet-500/15 dark:border-violet-400/20 dark:text-violet-300 bg-violet-50 border-violet-200 text-violet-700">REST APIs</span>
            <span class="chip dark:bg-violet-500/15 dark:border-violet-400/20 dark:text-violet-300 bg-violet-50 border-violet-200 text-violet-700">HTML/CSS/JS</span>
          </div>
        </div>

        <div>
          <h3 class="text-sm font-mono uppercase tracking-widest text-teal-400 mb-4">Tools & Platforms</h3>
          <div class="flex flex-wrap gap-2">
            <span class="chip dark:bg-teal-500/15 dark:border-teal-400/20 dark:text-teal-300 bg-teal-50 border-teal-200 text-teal-700">VS Code</span>
            <span class="chip dark:bg-teal-500/15 dark:border-teal-400/20 dark:text-teal-300 bg-teal-50 border-teal-200 text-teal-700">Jupyter Notebook</span>
            <span class="chip dark:bg-teal-500/15 dark:border-teal-400/20 dark:text-teal-300 bg-teal-50 border-teal-200 text-teal-700">Power BI</span>
            <span class="chip dark:bg-teal-500/15 dark:border-teal-400/20 dark:text-teal-300 bg-teal-50 border-teal-200 text-teal-700">Microsoft Suite</span>
            <span class="chip dark:bg-teal-500/15 dark:border-teal-400/20 dark:text-teal-300 bg-teal-50 border-teal-200 text-teal-700">Git & GitHub</span>
          </div>
        </div>

        <div>
          <h3 class="text-sm font-mono uppercase tracking-widest mb-4" style="color:#f472b6">Soft Skills</h3>
          <div class="flex flex-wrap gap-2">
            <span class="chip" style="background:rgba(244,114,182,0.1);border-color:rgba(244,114,182,0.2);color:#f472b6">Leadership</span>
            <span class="chip" style="background:rgba(244,114,182,0.1);border-color:rgba(244,114,182,0.2);color:#f472b6">Communication</span>
            <span class="chip" style="background:rgba(244,114,182,0.1);border-color:rgba(244,114,182,0.2);color:#f472b6">Problem Solving</span>
            <span class="chip" style="background:rgba(244,114,182,0.1);border-color:rgba(244,114,182,0.2);color:#f472b6">Team Collaboration</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ═══════════════════════ PROJECTS ═══════════════════════ -->
<section id="projects" class="py-24 px-6">
  <div class="max-w-6xl mx-auto">
    <div class="reveal">
      <p class="section-label mb-3">Things I've built</p>
      <h2 class="text-3xl sm:text-4xl font-bold mb-12 dark:text-white text-slate-900">Projects</h2>
    </div>

    <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-6">

      <!-- FitBot -->
      <div class="project-card reveal dark:bg-white/[0.04] bg-white rounded-2xl p-6 border dark:border-white/8 border-slate-200 flex flex-col">
        <div class="w-10 h-10 rounded-lg flex items-center justify-center mb-4 text-lg" style="background:linear-gradient(135deg,rgba(139,92,246,0.2),rgba(20,184,166,0.2))">
          🏋️
        </div>
        <div class="flex items-start justify-between gap-2 mb-3">
          <h3 class="text-lg font-semibold dark:text-white text-slate-900">FitBot</h3>
          <span class="text-xs font-mono dark:bg-violet-500/15 bg-violet-50 dark:text-violet-300 text-violet-700 px-2 py-0.5 rounded border dark:border-violet-400/20 border-violet-200 flex-shrink-0">AI Platform</span>
        </div>
        <p class="text-sm dark:text-slate-400 text-slate-600 leading-relaxed mb-5 flex-1">
          A full-stack fitness platform delivering <strong class="dark:text-slate-200 text-slate-800">personalized workout plans and dietary recommendations</strong> through AI. Processes user biometrics and goals to generate adaptive fitness programs in real time, backed by a scalable REST API layer.
        </p>
        <div class="flex flex-wrap gap-1.5 mb-5">
          <span class="chip dark:bg-violet-500/10 dark:border-violet-400/15 dark:text-violet-400 bg-violet-50 border-violet-100 text-violet-600">React.js</span>
          <span class="chip dark:bg-violet-500/10 dark:border-violet-400/15 dark:text-violet-400 bg-violet-50 border-violet-100 text-violet-600">Node.js</span>
          <span class="chip dark:bg-violet-500/10 dark:border-violet-400/15 dark:text-violet-400 bg-violet-50 border-violet-100 text-violet-600">PostgreSQL</span>
          <span class="chip dark:bg-violet-500/10 dark:border-violet-400/15 dark:text-violet-400 bg-violet-50 border-violet-100 text-violet-600">REST APIs</span>
        </div>
        <a href="https://github.com/Nandikas00" target="_blank" rel="noopener"
          class="flex items-center gap-2 text-sm font-medium text-violet-400 hover:text-violet-300 transition">
          <svg class="w-4 h-4" fill="currentColor" viewBox="0 0 24 24"><path d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112 6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0022 12.017C22 6.484 17.522 2 12 2z"/></svg>
          View on GitHub
          <svg class="w-3 h-3" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14"/></svg>
        </a>
      </div>

      <!-- DermCare -->
      <div class="project-card reveal dark:bg-white/[0.04] bg-white rounded-2xl p-6 border dark:border-white/8 border-slate-200 flex flex-col" style="transition-delay:0.1s">
        <div class="w-10 h-10 rounded-lg flex items-center justify-center mb-4 text-lg" style="background:linear-gradient(135deg,rgba(20,184,166,0.2),rgba(139,92,246,0.2))">
          🔬
        </div>
        <div class="flex items-start justify-between gap-2 mb-3">
          <h3 class="text-lg font-semibold dark:text-white text-slate-900">DermCare Solutions</h3>
          <span class="text-xs font-mono dark:bg-teal-500/15 bg-teal-50 dark:text-teal-300 text-teal-700 px-2 py-0.5 rounded border dark:border-teal-400/20 border-teal-200 flex-shrink-0">ML · Healthcare</span>
        </div>
        <p class="text-sm dark:text-slate-400 text-slate-600 leading-relaxed mb-5 flex-1">
          A clinically-inspired ML web app that analyzes <strong class="dark:text-slate-200 text-slate-800">skin lesion images via CNN</strong> to predict potential dermatological conditions. Built with TensorFlow and Flask, it bridges the gap between deep learning research and accessible diagnostic tools.
        </p>
        <div class="flex flex-wrap gap-1.5 mb-5">
          <span class="chip dark:bg-teal-500/10 dark:border-teal-400/15 dark:text-teal-400 bg-teal-50 border-teal-100 text-teal-600">Angular</span>
          <span class="chip dark:bg-teal-500/10 dark:border-teal-400/15 dark:text-teal-400 bg-teal-50 border-teal-100 text-teal-600">TensorFlow</span>
          <span class="chip dark:bg-teal-500/10 dark:border-teal-400/15 dark:text-teal-400 bg-teal-50 border-teal-100 text-teal-600">Flask</span>
          <span class="chip dark:bg-teal-500/10 dark:border-teal-400/15 dark:text-teal-400 bg-teal-50 border-teal-100 text-teal-600">CNN</span>
          <span class="chip dark:bg-teal-500/10 dark:border-teal-400/15 dark:text-teal-400 bg-teal-50 border-teal-100 text-teal-600">Python</span>
        </div>
        <a href="https://github.com/Nandikas00" target="_blank" rel="noopener"
          class="flex items-center gap-2 text-sm font-medium text-teal-400 hover:text-teal-300 transition">
          <svg class="w-4 h-4" fill="currentColor" viewBox="0 0 24 24"><path d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112 6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0022 12.017C22 6.484 17.522 2 12 2z"/></svg>
          View on GitHub
          <svg class="w-3 h-3" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14"/></svg>
        </a>
      </div>

      <!-- Signature Verification -->
      <div class="project-card reveal dark:bg-white/[0.04] bg-white rounded-2xl p-6 border dark:border-white/8 border-slate-200 flex flex-col" style="transition-delay:0.2s">
        <div class="w-10 h-10 rounded-lg flex items-center justify-center mb-4 text-lg" style="background:linear-gradient(135deg,rgba(244,114,182,0.2),rgba(139,92,246,0.2))">
          ✍️
        </div>
        <div class="flex items-start justify-between gap-2 mb-3">
          <h3 class="text-lg font-semibold dark:text-white text-slate-900">Signature Verifier</h3>
          <span class="text-xs font-mono px-2 py-0.5 rounded border flex-shrink-0" style="background:rgba(244,114,182,0.1);border-color:rgba(244,114,182,0.2);color:#f472b6">Deep Learning</span>
        </div>
        <p class="text-sm dark:text-slate-400 text-slate-600 leading-relaxed mb-5 flex-1">
          A binary classification system that <strong class="dark:text-slate-200 text-slate-800">authenticates handwritten signatures</strong> by distinguishing genuine from forged samples. Uses a custom CNN trained on signature image datasets, with OpenCV preprocessing for enhanced feature extraction and robustness.
        </p>
        <div class="flex flex-wrap gap-1.5 mb-5">
          <span class="chip" style="background:rgba(244,114,182,0.1);border-color:rgba(244,114,182,0.15);color:#f472b6">Python</span>
          <span class="chip" style="background:rgba(244,114,182,0.1);border-color:rgba(244,114,182,0.15);color:#f472b6">CNN</span>
          <span class="chip" style="background:rgba(244,114,182,0.1);border-color:rgba(244,114,182,0.15);color:#f472b6">OpenCV</span>
          <span class="chip" style="background:rgba(244,114,182,0.1);border-color:rgba(244,114,182,0.15);color:#f472b6">Deep Learning</span>
        </div>
        <a href="https://github.com/Nandikas00" target="_blank" rel="noopener"
          class="flex items-center gap-2 text-sm font-medium hover:opacity-70 transition" style="color:#f472b6">
          <svg class="w-4 h-4" fill="currentColor" viewBox="0 0 24 24"><path d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112 6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0022 12.017C22 6.484 17.522 2 12 2z"/></svg>
          View on GitHub
          <svg class="w-3 h-3" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14"/></svg>
        </a>
      </div>

    </div>
  </div>
</section>

<!-- ═══════════════════════ ACHIEVEMENTS ═══════════════════════ -->
<section id="achievements" class="py-24 px-6 dark:bg-white/[0.02] bg-slate-50">
  <div class="max-w-6xl mx-auto">
    <div class="reveal">
      <p class="section-label mb-3">Milestones</p>
      <h2 class="text-3xl sm:text-4xl font-bold mb-12 dark:text-white text-slate-900">Achievements & Certifications</h2>
    </div>

    <div class="grid sm:grid-cols-2 lg:grid-cols-3 gap-6">

      <!-- IIT Bombay Certification -->
      <div class="reveal dark:bg-white/[0.04] bg-white rounded-2xl p-6 border dark:border-white/8 border-slate-200 hover:border-violet-400/30 transition">
        <div class="flex items-center gap-3 mb-4">
          <div class="w-10 h-10 rounded-lg flex items-center justify-center text-xl" style="background:linear-gradient(135deg,rgba(139,92,246,0.2),rgba(20,184,166,0.2))">
            🏅
          </div>
          <span class="text-xs font-mono text-violet-400 uppercase tracking-widest">Certification</span>
        </div>
        <h3 class="font-semibold dark:text-white text-slate-900 mb-2">C Programming Certification</h3>
        <p class="text-sm dark:text-slate-400 text-slate-600 mb-3">Completed through the Spoken Tutorial Project at IIT Bombay — India's premier technical institute.</p>
        <div class="flex items-center gap-2">
          <span class="w-2 h-2 rounded-full bg-teal-400 flex-shrink-0"></span>
          <span class="text-xs font-mono dark:text-slate-400 text-slate-500">IIT Bombay · Spoken Tutorial Project</span>
        </div>
      </div>

      <!-- MCA -->
      <div class="reveal dark:bg-white/[0.04] bg-white rounded-2xl p-6 border dark:border-white/8 border-slate-200 hover:border-teal-400/30 transition" style="transition-delay:0.1s">
        <div class="flex items-center gap-3 mb-4">
          <div class="w-10 h-10 rounded-lg flex items-center justify-center text-xl" style="background:linear-gradient(135deg,rgba(20,184,166,0.2),rgba(139,92,246,0.2))">
            🎓
          </div>
          <span class="text-xs font-mono text-teal-400 uppercase tracking-widest">Education</span>
        </div>
        <h3 class="font-semibold dark:text-white text-slate-900 mb-2">Master of Computer Applications (MCA)</h3>
        <p class="text-sm dark:text-slate-400 text-slate-600 mb-3">Postgraduate degree with specialization in Software Development, AI/ML, and Data Analytics.</p>
        <div class="flex items-center gap-2">
          <span class="w-2 h-2 rounded-full bg-violet-400 flex-shrink-0"></span>
          <span class="text-xs font-mono dark:text-slate-400 text-slate-500">Graduated · Meerut, India</span>
        </div>
      </div>

      <!-- AI ML Projects -->
      <div class="reveal dark:bg-white/[0.04] bg-white rounded-2xl p-6 border dark:border-white/8 border-slate-200 hover:border-pink-400/30 transition" style="transition-delay:0.2s">
        <div class="flex items-center gap-3 mb-4">
          <div class="w-10 h-10 rounded-lg flex items-center justify-center text-xl" style="background:rgba(244,114,182,0.15)">
            🤖
          </div>
          <span class="text-xs font-mono uppercase tracking-widest" style="color:#f472b6">Achievement</span>
        </div>
        <h3 class="font-semibold dark:text-white text-slate-900 mb-2">3 AI/ML Production Systems</h3>
        <p class="text-sm dark:text-slate-400 text-slate-600 mb-3">Built and deployed end-to-end AI systems spanning healthcare diagnostics, fitness AI, and security — all solo-engineered.</p>
        <div class="flex items-center gap-2">
          <span class="w-2 h-2 rounded-full flex-shrink-0" style="background:#f472b6"></span>
          <span class="text-xs font-mono dark:text-slate-400 text-slate-500">Full-stack · Python · Deep Learning</span>
        </div>
      </div>

    </div>
  </div>
</section>

<!-- ═══════════════════════ CONTACT ═══════════════════════ -->
<section id="contact" class="py-24 px-6">
  <div class="max-w-6xl mx-auto">
    <div class="reveal">
      <p class="section-label mb-3">Let's work together</p>
      <h2 class="text-3xl sm:text-4xl font-bold mb-4 dark:text-white text-slate-900">Get in Touch</h2>
      <p class="dark:text-slate-400 text-slate-600 mb-12 max-w-lg">
        I'm open to full-time roles, freelance projects, and research collaborations. Drop a message — I respond within 24 hours.
      </p>
    </div>

    <div class="grid md:grid-cols-2 gap-12">

      <!-- Form -->
      <div class="reveal">
        <div class="space-y-8">
          <div>
            <label class="text-xs font-mono uppercase tracking-widest dark:text-slate-400 text-slate-500 block mb-2">Your Name</label>
            <input id="cf-name" type="text" placeholder="Jane Smith" class="contact-input dark:text-white text-slate-900" />
          </div>
          <div>
            <label class="text-xs font-mono uppercase tracking-widest dark:text-slate-400 text-slate-500 block mb-2">Email Address</label>
            <input id="cf-email" type="email" placeholder="jane@company.com" class="contact-input dark:text-white text-slate-900" />
          </div>
          <div>
            <label class="text-xs font-mono uppercase tracking-widest dark:text-slate-400 text-slate-500 block mb-2">Message</label>
            <textarea id="cf-message" rows="4" placeholder="Tell me about your project or opportunity..." class="contact-input resize-none dark:text-white text-slate-900"></textarea>
          </div>
          <button onclick="sendMessage()"
            class="px-8 py-3 rounded-lg text-sm font-semibold text-white transition hover:opacity-90 hover:scale-105 active:scale-95"
            style="background: linear-gradient(135deg, #8b5cf6, #14b8a6)">
            Send Message →
          </button>
        </div>
      </div>

      <!-- Direct links -->
      <div class="reveal space-y-4">
        <h3 class="text-sm font-mono uppercase tracking-widest dark:text-slate-500 text-slate-400 mb-6">Or reach me directly</h3>

        <a href="mailto:nandikasharma0@gmail.com"
          class="flex items-center gap-4 p-4 rounded-xl dark:bg-white/4 bg-white border dark:border-white/8 border-slate-200 hover:border-violet-400/40 transition group">
          <div class="w-10 h-10 rounded-lg flex items-center justify-center flex-shrink-0" style="background:rgba(139,92,246,0.15)">
            <svg class="w-5 h-5 text-violet-400" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"/></svg>
          </div>
          <div>
            <div class="text-xs font-mono dark:text-slate-500 text-slate-400 uppercase tracking-widest mb-0.5">Email</div>
            <div class="text-sm font-medium dark:text-white text-slate-900 group-hover:text-violet-400 transition">nandikasharma0@gmail.com</div>
          </div>
        </a>

        <a href="https://www.linkedin.com/in/nandika-sharma-743560202/" target="_blank" rel="noopener"
          class="flex items-center gap-4 p-4 rounded-xl dark:bg-white/4 bg-white border dark:border-white/8 border-slate-200 hover:border-teal-400/40 transition group">
          <div class="w-10 h-10 rounded-lg flex items-center justify-center flex-shrink-0" style="background:rgba(20,184,166,0.15)">
            <svg class="w-5 h-5 text-teal-400" fill="currentColor" viewBox="0 0 24 24"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 01-2.063-2.065 2.064 2.064 0 112.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>
          </div>
          <div>
            <div class="text-xs font-mono dark:text-slate-500 text-slate-400 uppercase tracking-widest mb-0.5">LinkedIn</div>
            <div class="text-sm font-medium dark:text-white text-slate-900 group-hover:text-teal-400 transition">Nandika Sharma</div>
          </div>
        </a>

        <a href="https://github.com/Nandikas00" target="_blank" rel="noopener"
          class="flex items-center gap-4 p-4 rounded-xl dark:bg-white/4 bg-white border dark:border-white/8 border-slate-200 hover:border-violet-400/40 transition group">
          <div class="w-10 h-10 rounded-lg flex items-center justify-center flex-shrink-0" style="background:rgba(139,92,246,0.15)">
            <svg class="w-5 h-5 text-violet-400" fill="currentColor" viewBox="0 0 24 24"><path d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112 6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0022 12.017C22 6.484 17.522 2 12 2z"/></svg>
          </div>
          <div>
            <div class="text-xs font-mono dark:text-slate-500 text-slate-400 uppercase tracking-widest mb-0.5">GitHub</div>
            <div class="text-sm font-medium dark:text-white text-slate-900 group-hover:text-violet-400 transition">Nandikas00</div>
          </div>
        </a>

        <div class="flex items-center gap-4 p-4 rounded-xl dark:bg-white/4 bg-white border dark:border-white/8 border-slate-200">
          <div class="w-10 h-10 rounded-lg flex items-center justify-center flex-shrink-0" style="background:rgba(244,114,182,0.15)">
            <svg class="w-5 h-5" style="color:#f472b6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"/><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"/></svg>
          </div>
          <div>
            <div class="text-xs font-mono dark:text-slate-500 text-slate-400 uppercase tracking-widest mb-0.5">Location</div>
            <div class="text-sm font-medium dark:text-white text-slate-900">Meerut, Uttar Pradesh, India</div>
          </div>
        </div>

      </div>
    </div>
  </div>
</section>

<!-- ═══════════════════════ FOOTER ═══════════════════════ -->
<footer class="py-8 px-6 border-t dark:border-white/5 border-slate-200">
  <div class="max-w-6xl mx-auto flex flex-col sm:flex-row items-center justify-between gap-4">
    <span class="font-mono text-sm grad">nandika.dev</span>
    <p class="text-xs dark:text-slate-500 text-slate-400 font-mono">
      © 2025 Nandika Sharma · Built with passion & Python
    </p>
    <div class="flex items-center gap-3">
      <a href="https://github.com/Nandikas00" target="_blank" rel="noopener" class="text-xs font-mono dark:text-slate-500 text-slate-400 hover:text-violet-400 transition">GitHub</a>
      <span class="dark:text-slate-700 text-slate-300">·</span>
      <a href="https://www.linkedin.com/in/nandika-sharma-743560202/" target="_blank" rel="noopener" class="text-xs font-mono dark:text-slate-500 text-slate-400 hover:text-teal-400 transition">LinkedIn</a>
      <span class="dark:text-slate-700 text-slate-300">·</span>
      <a href="mailto:nandikasharma0@gmail.com" class="text-xs font-mono dark:text-slate-500 text-slate-400 hover:text-violet-400 transition">Email</a>
    </div>
  </div>
</footer>

<!-- Toast notification -->
<div id="toast" class="fixed bottom-8 right-8 z-50 px-5 py-3 rounded-xl text-sm font-medium text-white pointer-events-none opacity-0 -translate-y-2"
  style="background: linear-gradient(135deg, #8b5cf6, #14b8a6)">
  ✅ Message sent — I'll be in touch!
</div>

<!-- ═══════════════════════ SCRIPTS ═══════════════════════ -->
<script>
// ─── THEME TOGGLE ───────────────────────────────────────────
const html = document.documentElement;
const body = document.body;
const sunIcon = document.getElementById('sun-icon');
const moonIcon = document.getElementById('moon-icon');
let isDark = true;

function applyTheme(dark) {
  if (dark) {
    html.classList.add('dark');
    body.classList.add('dark');
    sunIcon.classList.remove('hidden');
    moonIcon.classList.add('hidden');
  } else {
    html.classList.remove('dark');
    body.classList.remove('dark');
    sunIcon.classList.add('hidden');
    moonIcon.classList.remove('hidden');
  }
}

document.getElementById('theme-toggle').addEventListener('click', () => {
  isDark = !isDark;
  applyTheme(isDark);
  localStorage.setItem('theme', isDark ? 'dark' : 'light');
});

// Load saved theme
const saved = localStorage.getItem('theme');
if (saved) { isDark = saved === 'dark'; applyTheme(isDark); }

// ─── NAVBAR SCROLL EFFECT ───────────────────────────────────
const navbar = document.getElementById('navbar');
window.addEventListener('scroll', () => {
  if (window.scrollY > 20) {
    navbar.classList.add('dark:bg-[#0a0a0f]/90', 'bg-white/90', 'backdrop-blur-md', 'border-b', 'dark:border-white/5', 'border-slate-200/80');
  } else {
    navbar.classList.remove('dark:bg-[#0a0a0f]/90', 'bg-white/90', 'backdrop-blur-md', 'border-b', 'dark:border-white/5', 'border-slate-200/80');
  }
}, { passive: true });

// ─── MOBILE MENU ────────────────────────────────────────────
const hamburger = document.getElementById('hamburger');
const mobileMenu = document.getElementById('mobile-menu');
let menuOpen = false;

hamburger.addEventListener('click', () => {
  menuOpen = !menuOpen;
  mobileMenu.classList.toggle('open', menuOpen);
  document.getElementById('hb1').style.transform = menuOpen ? 'rotate(45deg) translate(4px,4px)' : '';
  document.getElementById('hb2').style.opacity = menuOpen ? '0' : '1';
  document.getElementById('hb3').style.transform = menuOpen ? 'rotate(-45deg) translate(4px,-4px)' : '';
});

function closeMobileMenu() {
  menuOpen = false;
  mobileMenu.classList.remove('open');
  document.getElementById('hb1').style.transform = '';
  document.getElementById('hb2').style.opacity = '1';
  document.getElementById('hb3').style.transform = '';
}

// ─── TYPING ANIMATION ───────────────────────────────────────
const phrases = [
  'Full Stack Developer',
  'AI/ML Enthusiast',
  'Deep Learning Explorer',
  'Problem Solver',
  'React & Flask Builder',
];
let phraseIndex = 0, charIndex = 0, deleting = false;
const typedEl = document.getElementById('typed-text');

function type() {
  const phrase = phrases[phraseIndex];
  if (!deleting) {
    typedEl.textContent = phrase.slice(0, charIndex + 1);
    charIndex++;
    if (charIndex === phrase.length) { deleting = true; setTimeout(type, 1800); return; }
  } else {
    typedEl.textContent = phrase.slice(0, charIndex - 1);
    charIndex--;
    if (charIndex === 0) {
      deleting = false;
      phraseIndex = (phraseIndex + 1) % phrases.length;
    }
  }
  setTimeout(type, deleting ? 55 : 90);
}
setTimeout(type, 600);

// ─── ACTIVE NAV HIGHLIGHTING ────────────────────────────────
const sections = document.querySelectorAll('section[id]');
const navLinks = document.querySelectorAll('.nav-link');

const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      navLinks.forEach(link => {
        link.classList.remove('active');
        if (link.getAttribute('href') === '#' + entry.target.id) {
          link.classList.add('active');
        }
      });
    }
  });
}, { rootMargin: '-40% 0px -55% 0px' });

sections.forEach(s => observer.observe(s));

// ─── SCROLL REVEAL ──────────────────────────────────────────
const reveals = document.querySelectorAll('.reveal');
const revealObserver = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.classList.add('visible');
      revealObserver.unobserve(entry.target);
    }
  });
}, { rootMargin: '0px 0px -60px 0px', threshold: 0.1 });
reveals.forEach(el => revealObserver.observe(el));

// ─── SKILL BARS ─────────────────────────────────────────────
const skillBars = document.querySelectorAll('.skill-bar-inner');
const barObserver = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      const bar = entry.target;
      setTimeout(() => { bar.style.width = bar.dataset.width + '%'; }, 150);
      barObserver.unobserve(bar);
    }
  });
}, { threshold: 0.3 });
skillBars.forEach(b => barObserver.observe(b));

// ─── CONTACT FORM ────────────────────────────────────────────
function sendMessage() {
  const name = document.getElementById('cf-name').value.trim();
  const email = document.getElementById('cf-email').value.trim();
  const message = document.getElementById('cf-message').value.trim();
  if (!name || !email || !message) {
    alert('Please fill in all fields before sending.');
    return;
  }
  const mailto = `mailto:nandikasharma0@gmail.com?subject=Portfolio Contact from ${encodeURIComponent(name)}&body=${encodeURIComponent(`Name: ${name}\nEmail: ${email}\n\n${message}`)}`;
  window.location.href = mailto;
  showToast();
  document.getElementById('cf-name').value = '';
  document.getElementById('cf-email').value = '';
  document.getElementById('cf-message').value = '';
}

function showToast() {
  const toast = document.getElementById('toast');
  toast.style.opacity = '1';
  toast.style.transform = 'translateY(0)';
  setTimeout(() => {
    toast.style.opacity = '0';
    toast.style.transform = 'translateY(-8px)';
  }, 3500);
}
</script>

</body>
</html>


### Key Learnings :

- Learned how to use AI-assisted development to rapidly create and iterate on a portfolio website.
- Improved prompt engineering skills by refining prompts to achieve better UI/UX results.
- Understood the importance of clear project requirements and detailed instructions when working with AI tools.
- Learned how to structure a professional portfolio with sections for skills, projects, experience, and contact information.
- Gained experience in reviewing, customizing, and improving AI-generated code instead of relying on the initial output.
- Improved understanding of responsive design, modern layouts, and user-friendly interfaces.
- Learned the value of combining AI-generated solutions with human creativity and critical thinking.

 <img width="1920" height="1080" alt="Screenshot (129)" src="https://github.com/user-attachments/assets/e39d955b-1bff-485b-81e8-f3a9597b70fa" />
<img width="1920" height="1080" alt="Screenshot (128)" src="https://github.com/user-attachments/assets/a09e19ea-0165-4485-bffd-9964c747445f" />
<img width="1920" height="1080" alt="Screenshot (127)" src="https://github.com/user-attachments/assets/cf78c893-1392-4dc2-9427-3550da68d983" />
<img width="1920" height="1080" alt="Screenshot (126)" src="https://github.com/user-attachments/assets/f2a99766-a77e-4784-a155-15a2d6fe7df8" />
<img width="1920" height="1080" alt="Screenshot (125)" src="https://github.com/user-attachments/assets/dae23631-ac3a-44e3-b6bb-5dac6d3de958" />
<img width="1920" height="1080" alt="Screenshot (124)" src="https://github.com/user-attachments/assets/92281956-8940-4fcc-bcda-c0967f0b2f70" />

