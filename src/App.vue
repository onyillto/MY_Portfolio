<template>
  <div class="portfolio-app">
    <div class="noise-overlay"></div>

    <nav class="nav-container">
      <div class="nav-tabs">
        <button
          v-for="(tab, index) in tabs"
          :key="tab.id"
          class="nav-tab"
          :class="{ active: activeTab === index }"
          @click="activeTab = index"
          :title="tab.name"
        >
          <span v-html="tab.icon"></span>
        </button>
      </div>
    </nav>

    <div class="app-container" :class="{ 'reverse-layout': activeTab !== 0 }">
      <!-- Profile Card -->
      <aside class="profile-card">
        <div class="profile-inner">
          <div class="profile-image">
            <img src="/profile.png" alt="Jay - Full Stack Developer" />
          </div>
          <h1 class="profile-name">Onyinye Achomadu</h1>
          <div class="profile-badge"></div>
          <p class="profile-bio">
            Full Stack JavaScript Developer with 3+ years of experience
            specializing in Node.js, Express.js, and modern frontend frameworks.
          </p>
          <div class="social-links">
            <a
              v-for="social in socials"
              :key="social.name"
              :href="social.link"
              target="_blank"
              rel="noopener noreferrer"
              class="social-link"
              :title="social.name"
            >
              <span v-html="social.icon"></span>
            </a>
          </div>
        </div>
      </aside>

      <!-- Content Area -->
      <main class="content-area">
        <div class="sections-wrapper">
          <Transition name="slide" mode="out-in">
            <!-- Home Section -->
            <section v-if="activeTab === 0" key="home" class="section">
              <div class="section-title">
                <div class="main">FULL-STACK</div>
                <div class="sub">DEVELOPER</div>
              </div>
              <p class="hero-description">
                Passionate about creating intuitive and engaging user
                experiences. Specialize in transforming ideas into beautifully
                crafted, scalable applications using modern technologies.
              </p>
              <div class="stats-row">
                <div v-for="stat in stats" :key="stat.label" class="stat-item">
                  <div class="stat-number">{{ stat.value }}</div>
                  <div class="stat-label">{{ stat.label }}</div>
                </div>
              </div>
              <div class="skill-cards">
                <div
                  v-for="skill in skills"
                  :key="skill.title"
                  class="skill-card"
                  :class="skill.color"
                >
                  <span v-html="skill.icon" class="skill-icon"></span>
                  <h3>{{ skill.title }}</h3>
                  <div class="arrow">→</div>
                </div>
              </div>
            </section>

            <!-- Projects Section -->
            <section v-else-if="activeTab === 1" key="projects" class="section">
              <div class="section-title">
                <div class="main">RECENT</div>
                <div class="sub">PROJECTS</div>
              </div>
              <div class="projects-list">
                <div
                  v-for="(project, i) in projects"
                  :key="project.name"
                  class="project-item"
                  :style="{ animationDelay: `${i * 0.1}s` }"
                >
                  <div
                    class="project-thumb"
                    :style="{ background: project.gradient }"
                  >
                    {{ project.abbr }}
                  </div>
                  <div class="project-info">
                    <h3>{{ project.name }}</h3>
                    <p>{{ project.description }}</p>
                  </div>
                  <div class="project-links">
                    <a
                      v-if="project.githubLink"
                      :href="project.githubLink"
                      target="_blank"
                      class="project-link"
                      title="View Code"
                    >
                      <svg
                        viewBox="0 0 24 24"
                        fill="none"
                        stroke="currentColor"
                        stroke-width="2"
                      >
                        <path
                          d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"
                        />
                      </svg>
                    </a>
                    <a
                      v-if="project.liveLink"
                      :href="project.liveLink"
                      target="_blank"
                      class="project-link"
                      title="Live Demo"
                    >
                      <svg
                        viewBox="0 0 24 24"
                        fill="none"
                        stroke="currentColor"
                        stroke-width="2"
                      >
                        <path
                          d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"
                        />
                        <polyline points="15 3 21 3 21 9" />
                        <line x1="10" y1="14" x2="21" y2="3" />
                      </svg>
                    </a>
                  </div>
                  <div class="project-arrow">↗</div>
                </div>
              </div>
            </section>

            <!-- Tech Stack Section -->
            <section v-else-if="activeTab === 2" key="stack" class="section">
              <div class="section-title">
                <div class="main">TECH</div>
                <div class="sub">STACK</div>
              </div>
              <div class="tech-categories">
                <div class="tech-category">
                  <h3>Backend & Databases</h3>
                  <div class="tech-grid">
                    <div
                      v-for="(tech, i) in backendStack"
                      :key="tech.name"
                      class="tech-item"
                      :style="{ animationDelay: `${i * 0.1}s` }"
                    >
                      <div class="tech-icon" :class="tech.class">
                        {{ tech.icon }}
                      </div>
                      <div class="tech-info">
                        <h4>{{ tech.name }}</h4>
                        <p>{{ tech.type }}</p>
                      </div>
                    </div>
                  </div>
                </div>
                <div class="tech-category">
                  <h3>Frontend & Frameworks</h3>
                  <div class="tech-grid">
                    <div
                      v-for="(tech, i) in frontendStack"
                      :key="tech.name"
                      class="tech-item"
                      :style="{ animationDelay: `${i * 0.1}s` }"
                    >
                      <div class="tech-icon" :class="tech.class">
                        {{ tech.icon }}
                      </div>
                      <div class="tech-info">
                        <h4>{{ tech.name }}</h4>
                        <p>{{ tech.type }}</p>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </section>

            <!-- Tools Section -->
            <section v-else-if="activeTab === 3" key="tools" class="section">
              <div class="section-title">
                <div class="main">PREMIUM</div>
                <div class="sub">TOOLS</div>
              </div>
              <div class="tools-grid">
                <div
                  v-for="(tool, i) in tools"
                  :key="tool.name"
                  class="tool-item"
                  :style="{ animationDelay: `${i * 0.1}s` }"
                >
                  <div class="tool-icon" :class="tool.class">
                    {{ tool.icon }}
                  </div>
                  <div class="tool-info">
                    <h4>{{ tool.name }}</h4>
                    <p>{{ tool.type }}</p>
                  </div>
                </div>
              </div>
            </section>

            <!-- Contact Section -->
            <section v-else-if="activeTab === 4" key="contact" class="section">
              <div class="section-title">
                <div class="main">LET'S WORK</div>
                <div class="sub">TOGETHER</div>
              </div>
              <div class="contact-content">
                <p class="contact-description">
                  Ready to bring your ideas to life? I'm available for freelance
                  projects, collaborations, and full-time opportunities. Let's
                  create something amazing together.
                </p>
                <div class="contact-methods">
                  <a
                    v-for="(method, i) in contactMethods"
                    :key="method.label"
                    :href="method.href"
                    class="contact-method"
                    :style="{ animationDelay: `${i * 0.1}s` }"
                  >
                    <div class="contact-icon">
                      <span v-html="method.icon"></span>
                    </div>
                    <div class="contact-info">
                      <h4>{{ method.label }}</h4>
                      <p>{{ method.value }}</p>
                    </div>
                  </a>
                </div>
                <button class="cta-button">Get In Touch →</button>
              </div>
            </section>
          </Transition>
        </div>
      </main>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const activeTab = ref(0);

const tabs = [
  {
    id: "home",
    name: "Home",
    icon: '<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"/><polyline points="9 22 9 12 15 12 15 22"/></svg>',
  },
  {
    id: "projects",
    name: "Projects",
    icon: '<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="2" y="3" width="20" height="14" rx="2"/><line x1="8" y1="21" x2="16" y2="21"/><line x1="12" y1="17" x2="12" y2="21"/></svg>',
  },
  {
    id: "stack",
    name: "Tech Stack",
    icon: '<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><line x1="4" y1="21" x2="4" y2="14"/><line x1="4" y1="10" x2="4" y2="3"/><line x1="12" y1="21" x2="12" y2="12"/><line x1="12" y1="8" x2="12" y2="3"/><line x1="20" y1="21" x2="20" y2="16"/><line x1="20" y1="12" x2="20" y2="3"/></svg>',
  },
  {
    id: "tools",
    name: "Tools",
    icon: '<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M14.7 6.3a1 1 0 0 0 0 1.4l1.6 1.6a1 1 0 0 0 1.4 0l3.77-3.77a6 6 0 0 1-7.94 7.94l-6.91 6.91a2.12 2.12 0 0 1-3-3l6.91-6.91a6 6 0 0 1 7.94-7.94l-3.76 3.76z"/></svg>',
  },
  {
    id: "contact",
    name: "Contact",
    icon: '<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M11 4H4a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7"/><path d="M18.5 2.5a2.121 2.121 0 0 1 3 3L12 15l-4 1 1-4 9.5-9.5z"/></svg>',
  },
];

const socials = [
  {
    name: "GitHub",
    link: "https://github.com/onyillto",
    icon: '<svg viewBox="0 0 24 24" fill="currentColor"><path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0024 12c0-6.63-5.37-12-12-12z"/></svg>',
  },
  {
    name: "X",
    link: "https://x.com/OnyinyeAchomadu",
    icon: '<svg viewBox="0 0 24 24" fill="currentColor"><path d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24H16.17l-5.214-6.817L4.99 21.75H1.68l7.73-8.835L1.254 2.25H8.08l4.713 6.231zm-1.161 17.52h1.833L7.084 4.126H5.117z"/></svg>',
  },
  {
    name: "LinkedIn",
    link: "https://www.linkedin.com/in/achomadu-onyinye20/",
    icon: '<svg viewBox="0 0 24 24" fill="currentColor"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>',
  },
  {
    name: "Instagram",
    link: "https://www.instagram.com/brit_teck/",
    icon: '<svg viewBox="0 0 24 24" fill="currentColor"><path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zm0-2.163c-3.259 0-3.667.014-4.947.072-4.358.2-6.78 2.618-6.98 6.98-.059 1.281-.073 1.689-.073 4.948 0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.058 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98-1.281-.059-1.69-.073-4.949-.073zm0 5.838a6.162 6.162 0 100 12.324 6.162 6.162 0 000-12.324zm0 10.162a3.999 3.999 0 110-7.998 3.999 3.999 0 010 7.998zm6.406-11.845a1.44 1.44 0 100 2.881 1.44 1.44 0 000-2.881z"/></svg>',
  },
];

const stats = [
  { value: "+3", label: "Years of Experience" },
  { value: "+20", label: "Projects Completed" },
  { value: "+10", label: "Happy Clients" },
];

const skills = [
  {
    title: "Backend Development",
    color: "orange",
    icon: '<svg viewBox="0 0 24 24" fill="currentColor"><path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5"/></svg>',
  },
  {
    title: "Frontend & React, Vue, Next.js",
    color: "lime",
    icon: '<svg viewBox="0 0 24 24" fill="currentColor"><rect x="3" y="3" width="7" height="7"/><rect x="14" y="3" width="7" height="7"/><rect x="3" y="14" width="7" height="7"/><rect x="14" y="14" width="7" height="7"/></svg>',
  },
  {
    title: "Database & RESTful APIs",
    color: "purple",
    icon: '<svg viewBox="0 0 24 24" fill="currentColor"><circle cx="12" cy="12" r="3"/><path d="M12 1v6m0 6v10M4.22 4.22l4.24 4.24m7.08 7.08l4.24 4.24M1 12h6m6 0h10M4.22 19.78l4.24-4.24m7.08-7.08l4.24-4.24"/></svg>',
  },
  {
    title: "DevOps & Cloud (GCP, Docker)",
    color: "dark",
    icon: '<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M21 16V8a2 2 0 0 0-1-1.73l-7-4a2 2 0 0 0-2 0l-7 4A2 2 0 0 0 3 8v8a2 2 0 0 0 1 1.73l7 4a2 2 0 0 0 2 0l7-4A2 2 0 0 0 21 16z"/><polyline points="3.27 6.96 12 12.01 20.73 6.96"/><line x1="12" y1="22.08" x2="12" y2="12"/></svg>',
  },
];

const projects = [
  {
    name: "CredNow Admin Dashboard",
    description:
      "Admin dashboard with role-based access control using React.js & Next.js",
    gradient: "linear-gradient(135deg, #10b981, #059669)",
    abbr: "CN",
    githubLink: "https://github.com/onyillto/crednow",
    liveLink: "https://crednow.ng/",
  },
  {
    name: "Ngbuka Vendor Dashboard",
    description: "Vendor management system with inventory & order tracking",
    gradient: "linear-gradient(135deg, #f59e0b, #d97706)",
    abbr: "NV",
    githubLink: "https://github.com/onyillto/ngbuka-web",
    liveLink: "https://staging-app.ngbuka.com/Onboarding",
  },
  {
    name: "Moja Realestate",
    description:
      "Sustainable farm estates & residential real estate development in Nigeria",
    gradient: "linear-gradient(135deg, #1e40af, #3b82f6)",
    abbr: "MR",
    githubLink: null,
    liveLink: "https://www.mojarealestate.net/",
  },
  {
    name: "Mayas Consulting",
    description:
      "Strategy, operations and growth consulting for African businesses",
    gradient: "linear-gradient(135deg, #1e40af, #3b82f6)",
    abbr: "MC", // changed from NC to avoid confusion with Ngbuka
    githubLink: null,
    liveLink: "https://www.mayyasconsulting.com/",
  },
  {
    name: "Ngbuka Admin Dashboard",
    description: "Admin panel for marketplace management & analytics",
    gradient: "linear-gradient(135deg, #ef4444, #dc2626)",
    abbr: "NA",
    githubLink: "https://github.com/onyillto/jenny-ngbuka-admin",
    liveLink: "https://staging-dashboard9spla.ngbuka.com/dashboard",
  },
  {
    name: "Ngbuka User App",
    description: "E-commerce app with secure escrow & Paystack integration",
    gradient: "linear-gradient(135deg, #8b5cf6, #7c3aed)",
    abbr: "NU",
    githubLink: "https://github.com/onyillto/ngbuka-web",
    liveLink: "https://staging-app.ngbuka.com/",
  },
  {
    name: "Ngbuka Forum",
    description:
      "Next.js discussion platform with SSR + backend (Node.js/Express) for spare parts community",
    gradient: "linear-gradient(135deg, #06b6d4, #0891b2)",
    abbr: "NF",
    githubLink: "https://github.com/onyillto/ngbuka-blog-forum",
    liveLink: "https://forum-staging.ngbuka.com/",
  },
  {
    name: "The Kliners OP",
    description: "Home services platform with OAuth 2.0 & GCP deployment",
    gradient: "linear-gradient(135deg, #3b82f6, #2563eb)",
    abbr: "TK",
    githubLink: "https://github.com/onyillto/UK_KLINNER",
    liveLink: "https://klinner-web-app.vercel.app/auth/signin",
  },
  {
    name: "Bloomrydes Dashboard",
    description: "Data visualization dashboard serving 10K+ users with Vue.js",
    gradient: "linear-gradient(135deg, #ec4899, #db2777)",
    abbr: "BR",
    githubLink: "#",
    liveLink: "#",
  },
  {
    name: "Bloomrydes API",
    description:
      "RESTful API with 15+ features, WebSocket & real-time updates\n\nLinks available upon request due to security reasons",
    gradient: "linear-gradient(135deg, #f43f5e, #e11d48)",
    abbr: "BA",
    githubLink: null,
    liveLink: null,
  },
];

const backendStack = [
  { name: "Node.js", type: "Runtime Environment", icon: "N", class: "node" },
  { name: "Express.js", type: "Web Framework", icon: "Ex", class: "express" },
  { name: "MongoDB", type: "NoSQL Database", icon: "M", class: "mongo" },
  { name: "PostgreSQL", type: "SQL Database", icon: "Pg", class: "postgres" },
  { name: "OAuth/JWT", type: "Authentication", icon: "🔐", class: "auth" },
];

const frontendStack = [
  {
    name: "JavaScript",
    type: "Programming Language",
    icon: "JS",
    class: "javascript",
  },
  {
    name: "TypeScript",
    type: "Typed JavaScript",
    icon: "TS",
    class: "typescript",
  },
  { name: "Next.js", type: "React Framework", icon: "N", class: "next" },
  { name: "React", type: "UI Library", icon: "R", class: "react" },
  { name: "Vue.js", type: "Progressive Framework", icon: "V", class: "vue" },
  { name: "Tailwind CSS", type: "Utility CSS", icon: "T", class: "tailwind" },
];

const tools = [
  { name: "Git", type: "Version Control", icon: "G", class: "git" },
  { name: "Docker", type: "Containerization", icon: "D", class: "docker" },
  { name: "Google Cloud", type: "Cloud Platform", icon: "GC", class: "gcloud" },
  { name: "VS Code", type: "Code Editor", icon: "VS", class: "vscode" },
  { name: "Postman", type: "API Testing", icon: "P", class: "postman" },
  { name: "Jenkins", type: "CI/CD Pipeline", icon: "J", class: "jenkins" },
];

const contactMethods = [
  {
    label: "Email",
    value: "Achomaduonyinye@gmail.com",
    href: "mailto:Achomaduonyinye@gmail.com",
    icon: '<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>',
  },
  {
    label: "Phone",
    value: "+234 701 113 6719",
    href: "tel:+2347011136719",
    icon: '<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z"/></svg>',
  },
  {
    label: "Location",
    value: "Lagos, Nigeria",
    href: "#",
    icon: '<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z"/><circle cx="12" cy="10" r="3"/></svg>',
  },
  {
    label: "Availability",
    value: "Open for Opportunities",
    href: "#",
    icon: '<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/></svg>',
  },
];
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Syne:wght@400;500;600;700;800&family=Space+Mono:wght@400;700&display=swap");

.portfolio-app {
  --bg-dark: #0a0a0a;
  --bg-card: #141414;
  --accent-orange: #ff6b35;
  --accent-lime: #c8ff00;
  --accent-purple: #a855f7;
  --text-primary: #ffffff;
  --text-secondary: #888888;
  --text-muted: #555555;
  font-family: "Syne", sans-serif;
  background: var(--bg-dark);
  color: var(--text-primary);
  min-height: 100vh;
  overflow-x: hidden;
}

.slide-enter-active,
.slide-leave-active {
  transition: all 0.5s cubic-bezier(0.16, 1, 0.3, 1);
}
.slide-enter-from {
  opacity: 0;
  transform: translateX(80px);
}
.slide-leave-to {
  opacity: 0;
  transform: translateX(-80px);
}

.noise-overlay {
  position: fixed;
  inset: 0;
  pointer-events: none;
  z-index: 9999;
  opacity: 0.03;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
}

.nav-container {
  position: fixed;
  top: 24px;
  left: 50%;
  transform: translateX(-50%);
  z-index: 1000;
}

.nav-tabs {
  display: flex;
  gap: 8px;
  background: rgba(30, 30, 30, 0.9);
  backdrop-filter: blur(20px);
  padding: 8px;
  border-radius: 50px;
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.nav-tab {
  width: 44px;
  height: 44px;
  border-radius: 50%;
  border: none;
  background: transparent;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);
  color: var(--text-secondary);
}

.nav-tab:hover {
  background: rgba(255, 255, 255, 0.1);
  color: var(--text-primary);
}
.nav-tab.active {
  background: var(--text-primary);
  color: var(--bg-dark);
}
.nav-tab :deep(svg) {
  width: 20px;
  height: 20px;
}

.app-container {
  display: flex;
  min-height: 100vh;
  padding: 100px 40px 40px;
  gap: 40px;
  max-width: 1400px;
  margin: 0 auto;
  transition: all 0.5s cubic-bezier(0.16, 1, 0.3, 1);
}

/* Reverse layout for non-home tabs - profile moves to right side */
.app-container.reverse-layout {
  flex-direction: row-reverse;
}

.profile-card {
  position: sticky;
  top: 100px;
  width: 340px;
  height: fit-content;
  flex-shrink: 0;
  transition: all 0.5s cubic-bezier(0.16, 1, 0.3, 1);
}

.profile-inner {
  background: var(--bg-card);
  border-radius: 24px;
  padding: 24px;
  position: relative;
  overflow: hidden;
}

.profile-inner::before {
  content: "";
  position: absolute;
  top: -50%;
  right: -50%;
  width: 200px;
  height: 200px;
  border: 2px dashed var(--accent-orange);
  border-radius: 50%;
  opacity: 0.3;
  animation: rotate 30s linear infinite;
}

@keyframes rotate {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

.profile-image {
  width: 100%;
  height: auto;
  background: linear-gradient(135deg, var(--accent-orange), #ff8c5a);
  border-radius: 16px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 80px;
  font-weight: 800;
  color: var(--bg-dark);
  position: relative;
  overflow: hidden;
}

.profile-image img {
  width: 100%;
  height: auto;
  display: block;
  object-fit: cover;
}

.profile-image::after {
  content: "";
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 40%;
  background: linear-gradient(to top, rgba(0, 0, 0, 0.6), transparent);
}

.profile-name {
  font-size: 28px;
  font-weight: 700;
  text-align: center;
  margin-bottom: 8px;
  margin-top: 20px;
}

.profile-badge {
  display: flex;
  justify-content: center;
  margin-bottom: 16px;
}

.flame-icon {
  width: 32px;
  height: 32px;
  background: rgba(255, 107, 53, 0.2);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 14px;
}

.profile-bio {
  text-align: center;
  color: var(--text-secondary);
  font-size: 14px;
  line-height: 1.6;
  padding: 16px 0;
  border-top: 1px dashed rgba(255, 255, 255, 0.1);
}

.social-links {
  display: flex;
  justify-content: center;
  gap: 12px;
  margin-top: 16px;
}

.social-link {
  width: 40px;
  height: 40px;
  border-radius: 12px;
  background: rgba(255, 107, 53, 0.1);
  border: none;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--accent-orange);
  transition: all 0.3s ease;
  text-decoration: none;
}

.social-link:hover {
  background: var(--accent-orange);
  color: var(--bg-dark);
  transform: translateY(-2px);
}
.social-link :deep(svg) {
  width: 18px;
  height: 18px;
}

.content-area {
  flex: 1;
}
.sections-wrapper {
  min-height: 600px;
}

.section-title {
  margin-bottom: 40px;
}
.section-title .main {
  font-size: clamp(48px, 8vw, 80px);
  font-weight: 800;
  text-transform: uppercase;
  letter-spacing: -2px;
  line-height: 0.9;
}
.section-title .sub {
  font-size: clamp(48px, 8vw, 80px);
  font-weight: 800;
  text-transform: uppercase;
  letter-spacing: -2px;
  line-height: 0.9;
  -webkit-text-stroke: 2px var(--text-muted);
  color: transparent;
}

.hero-description {
  color: var(--text-secondary);
  font-size: 16px;
  line-height: 1.8;
  max-width: 500px;
  margin-bottom: 40px;
}

.stats-row {
  display: flex;
  gap: 40px;
  margin-bottom: 40px;
}
.stat-number {
  font-size: 48px;
  font-weight: 800;
  font-family: "Space Mono", monospace;
}
.stat-label {
  font-size: 12px;
  color: var(--text-secondary);
  text-transform: uppercase;
  letter-spacing: 1px;
}

.skill-cards {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 16px;
}

.skill-card {
  padding: 24px;
  border-radius: 16px;
  position: relative;
  transition: all 0.4s ease;
  cursor: pointer;
}

.skill-card:hover {
  transform: translateY(-4px);
}
.skill-card.orange {
  background: linear-gradient(135deg, var(--accent-orange), #ff8c5a);
}
.skill-card.lime {
  background: linear-gradient(135deg, var(--accent-lime), #a8d900);
}
.skill-card.purple {
  background: linear-gradient(135deg, var(--accent-purple), #c084fc);
}
.skill-card.dark {
  background: var(--bg-card);
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.skill-card :deep(.skill-icon) {
  display: block;
  width: 40px;
  height: 40px;
  margin-bottom: 16px;
}
.skill-card :deep(.skill-icon svg) {
  width: 100%;
  height: 100%;
}
.skill-card.orange :deep(.skill-icon),
.skill-card.lime :deep(.skill-icon) {
  color: var(--bg-dark);
}
.skill-card.purple :deep(.skill-icon) {
  color: white;
}
.skill-card.dark :deep(.skill-icon) {
  color: var(--accent-orange);
}

.skill-card h3 {
  font-size: 14px;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 1px;
  color: var(--bg-dark);
}
.skill-card.dark h3 {
  color: var(--text-primary);
}
.skill-card.purple h3 {
  color: white;
}

.skill-card .arrow {
  position: absolute;
  bottom: 16px;
  right: 16px;
  width: 32px;
  height: 32px;
  border-radius: 8px;
  background: rgba(0, 0, 0, 0.2);
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--bg-dark);
}

.skill-card.dark .arrow {
  background: rgba(255, 255, 255, 0.1);
  color: var(--text-primary);
}
.skill-card.purple .arrow {
  background: rgba(255, 255, 255, 0.2);
  color: white;
}

.projects-list {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.project-item {
  display: flex;
  align-items: center;
  gap: 20px;
  padding: 20px;
  background: var(--bg-card);
  border-radius: 16px;
  border: 1px solid rgba(255, 255, 255, 0.05);
  transition: all 0.4s ease;
  cursor: pointer;
  animation: fadeInUp 0.5s ease forwards;
  opacity: 0;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.project-item:hover {
  border-color: var(--accent-orange);
  transform: translateX(8px);
}

.project-thumb {
  width: 100px;
  height: 70px;
  border-radius: 8px;
  flex-shrink: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 700;
  font-size: 14px;
  color: white;
}

.project-info {
  flex: 1;
}
.project-info h3 {
  font-size: 18px;
  font-weight: 600;
  margin-bottom: 4px;
}
.project-info p {
  color: var(--text-secondary);
  font-size: 14px;
}

.project-links {
  display: flex;
  gap: 8px;
  margin-right: 12px;
}

.project-link {
  width: 36px;
  height: 36px;
  border-radius: 10px;
  background: rgba(255, 255, 255, 0.05);
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--text-secondary);
  transition: all 0.3s ease;
  text-decoration: none;
}

.project-link:hover {
  background: var(--accent-orange);
  color: var(--bg-dark);
  transform: scale(1.1);
}

.project-link svg {
  width: 18px;
  height: 18px;
}

.project-arrow {
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--text-secondary);
  font-size: 20px;
  transition: all 0.3s ease;
}

.project-item:hover .project-arrow {
  color: var(--accent-orange);
  transform: translateX(4px);
}

.tech-categories {
  display: flex;
  flex-direction: column;
  gap: 32px;
}
.tech-category h3 {
  font-size: 14px;
  color: var(--text-secondary);
  text-transform: uppercase;
  letter-spacing: 2px;
  margin-bottom: 16px;
}
.tech-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 12px;
}

.tech-item {
  display: flex;
  align-items: center;
  gap: 16px;
  padding: 16px 20px;
  background: var(--bg-card);
  border-radius: 12px;
  border: 1px solid rgba(255, 255, 255, 0.05);
  transition: all 0.3s ease;
  animation: fadeInUp 0.5s ease forwards;
  opacity: 0;
}

.tech-item:hover {
  border-color: var(--accent-orange);
  background: rgba(255, 107, 53, 0.05);
}

.tech-icon {
  width: 40px;
  height: 40px;
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 14px;
  font-weight: 700;
  color: white;
}

.tech-icon.node {
  background: linear-gradient(135deg, #68a063, #3c873a);
}
.tech-icon.express {
  background: #000;
}
.tech-icon.mongo {
  background: linear-gradient(135deg, #4db33d, #3fa037);
}
.tech-icon.postgres {
  background: linear-gradient(135deg, #336791, #2f5b8a);
}
.tech-icon.auth {
  background: linear-gradient(135deg, #fbbf24, #f59e0b);
}
.tech-icon.javascript {
  background: linear-gradient(135deg, #f7df1e, #e5cd00);
  color: #000;
}
.tech-icon.typescript {
  background: linear-gradient(135deg, #3178c6, #235a97);
}
.tech-icon.next {
  background: #000;
}
.tech-icon.vue {
  background: linear-gradient(135deg, #42b883, #35495e);
}
.tech-icon.react {
  background: linear-gradient(135deg, #61dafb, #21a9d8);
  color: #000;
}
.tech-icon.tailwind {
  background: linear-gradient(135deg, #38bdf8, #0ea5e9);
}

.tech-info h4 {
  font-size: 16px;
  font-weight: 600;
  margin-bottom: 2px;
}
.tech-info p {
  font-size: 12px;
  color: var(--text-secondary);
}

.tools-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 16px;
}

.tool-item {
  display: flex;
  align-items: center;
  gap: 16px;
  padding: 20px;
  background: var(--bg-card);
  border-radius: 16px;
  border: 1px solid rgba(255, 255, 255, 0.05);
  transition: all 0.3s ease;
  animation: fadeInUp 0.5s ease forwards;
  opacity: 0;
}

.tool-item:hover {
  transform: translateY(-2px);
  border-color: rgba(255, 255, 255, 0.1);
}

.tool-icon {
  width: 48px;
  height: 48px;
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 16px;
  font-weight: 700;
  color: white;
}

.tool-icon.git {
  background: #f05032;
}
.tool-icon.docker {
  background: #2496ed;
}
.tool-icon.gcloud {
  background: linear-gradient(135deg, #4285f4, #34a853, #fbbc05, #ea4335);
}
.tool-icon.vscode {
  background: #007acc;
}
.tool-icon.postman {
  background: #ff6c37;
}
.tool-icon.jenkins {
  background: linear-gradient(135deg, #d33833, #ef3d3d);
}

.tool-info h4 {
  font-size: 16px;
  font-weight: 600;
}
.tool-info p {
  font-size: 13px;
  color: var(--text-secondary);
}

.contact-content {
  max-width: 600px;
}
.contact-description {
  color: var(--text-secondary);
  font-size: 18px;
  line-height: 1.8;
  margin-bottom: 40px;
}
.contact-methods {
  display: flex;
  flex-direction: column;
  gap: 16px;
  margin-bottom: 40px;
}

.contact-method {
  display: flex;
  align-items: center;
  gap: 16px;
  padding: 20px 24px;
  background: var(--bg-card);
  border-radius: 16px;
  border: 1px solid rgba(255, 255, 255, 0.05);
  transition: all 0.3s ease;
  text-decoration: none;
  color: inherit;
  animation: fadeInUp 0.5s ease forwards;
  opacity: 0;
}

.contact-method:hover {
  border-color: var(--accent-orange);
  transform: translateX(8px);
}

.contact-icon {
  width: 48px;
  height: 48px;
  border-radius: 12px;
  background: rgba(255, 107, 53, 0.1);
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--accent-orange);
}

.contact-icon :deep(svg) {
  width: 24px;
  height: 24px;
}

.contact-info h4 {
  font-size: 14px;
  color: var(--text-secondary);
  margin-bottom: 4px;
}
.contact-info p {
  font-size: 16px;
  font-weight: 600;
}

.cta-button {
  display: inline-flex;
  align-items: center;
  gap: 12px;
  padding: 16px 32px;
  background: var(--accent-orange);
  color: var(--bg-dark);
  border: none;
  border-radius: 50px;
  font-size: 16px;
  font-weight: 700;
  font-family: "Syne", sans-serif;
  cursor: pointer;
  transition: all 0.3s ease;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.cta-button:hover {
  transform: scale(1.05);
  box-shadow: 0 10px 40px rgba(255, 107, 53, 0.3);
}

/* Mobile Responsive */
@media (max-width: 1024px) {
  .app-container {
    flex-direction: column;
    padding: 100px 20px 40px;
  }

  /* On mobile, profile goes to bottom for non-home tabs */
  .app-container.reverse-layout {
    flex-direction: column;
  }

  .app-container.reverse-layout .profile-card {
    order: 2;
  }

  .app-container.reverse-layout .content-area {
    order: 1;
  }

  .profile-card {
    position: relative;
    top: 0;
    width: 100%;
    max-width: 400px;
    margin: 0 auto;
  }

  .skill-cards,
  .tech-grid,
  .tools-grid {
    grid-template-columns: 1fr;
  }
  .stats-row {
    flex-wrap: wrap;
    gap: 24px;
  }
}
</style>
