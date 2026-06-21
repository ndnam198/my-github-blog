+++
draft = false
title = 'About Me'
aliases = [
  "/about",
]
+++

<div style="text-align: center; margin: 3rem 0;">
  <img src="/images/avatar.jpeg" alt="Nam Nguyen - Software Engineer" width="" height="350" style="border-radius: 3%; object-fit: contain; display: block; margin: 0 auto 2rem auto;">
</div>

# Nam Nguyen

Software Engineer

<div class="hero-badges">
  <span>📍 Hanoi, Vietnam</span>
  <span>💼 7 years experience</span>
</div>

## About

<div>
  <p>
    Passionate technologist with extensive experience in developing scalable applications across various industries. Accomplished in building and working within cross-functional teams, as well as managing products from conception to deployment, delivering robust and maintainable applications that enhances business efficiency and user satisfaction.</p><p>Driven by curiosity and a continuous desire to learn, constantly seeks to refine processes through the adoption of innovative technologies, patterns, and emerging methodologies.
  </p>
</div>

## Experience

### Sun* Vietnam

**Software Engineer** · Full-time · Hanoi Capital Region · Hybrid · Sep 2024 – Present

- Engineered and deployed feature enhancements for a B2B wound management mobile platform which heavily used Flutter and Clean Architecture with Bloc state management.
- Conversational AI: Developed and deployed Bank Jago's Conversational Banking bot using LangChain and RAG. Participated in the success of both the mobile app and the backend service that serves the RAG.

### FPT Software

**Mobile Software Engineer** · Full-time · Hanoi Capital Region · Hybrid · Dec 2020 – Aug 2024

- Developed a high-fidelity driving simulation suite to standardize and accelerate closed-course test preparation. Successfully lowered the learning curve for novice drivers by providing a realistic, zero-risk environment for mastering vehicle controls.
- Contributed to the development of a flagship mobile application for Europe's leading heating solutions provider. Architected the integration of complex, proprietary communication protocols while maintaining a seamless and intuitive user experience. Utilising Clean Architecture and a comprehensive testing strategy—ranging from unit to end-to-end—to ensure maximum system reliability.

### VinFast

**Software QA Intern** · Full-time · Hanoi Capital Region · On-site · Jul 2020 – Nov 2020

- Interned as a QA Tester, participating in building a charging station for motorcycles following IEC 61851.
- Wrote and maintained test cases.
- Verified product quality through thorough testing and validation processes.

### Makipos

**Embedded System Engineer Intern** · Internship · Hanoi Capital Region · On-site · Apr 2020 – Jul 2020

- PCB engineering process: layout, manufacture, and testing.
- Built a communication library in C to serve temperature/humidity/PM2.5 dust sensor data collection via I2C and USART protocols.

## Education

### Bachelor's degree, Electronics & Automation Control Engineering

**Hanoi University of Science and Technology** · 2016 – 2020

- Studied electronics, hardware circuitry, and embedded design
- Programmed low-level hardware using embedded C and Linux
- Achieved Hands-on experience by engineering and building many IoT projects from scratch involving many layers of software: Embedded, Web server by ExpressJS

### Physics

**Hanoi Amsterdam High School**

- Physics-specialized class

## Certifications

### Certified LeSS Practitioner (Large-Scale Scrum)

**[The LeSS Company](https://less.works/courses/less-practitioner)** · 11/2025

## Technical Skills

### Languages

Dart, Python, Typescript, C, C#, Bash scripting

### Frameworks

Flutter, ReactJS, React Native, Unity, FastAPI, LangChain, LangGraph

### Databases

PostgreSQL, Redis, Supabase, RealmDB

### CI/CD automation

Fastlane, Harness, Azure DevOps, Github Actions

### Cloud platforms and monitoring tools

GCP, Langfuse, Growthbook, Firebase, nginx

## Languages

- **Vietnamese** — Mother tongue
- **English** — Working Proficiency

## Interests

- Build software that improves productivity
- Experimenting with emerging technologies, understanding how they work in-depth
- Get to understand the inner workings of the software I use

## Current Goal
<p style="margin-bottom: 1.5rem;">Build meaningful software that improves lives</p>

  <a href="#" id="blog-button" class="cta-primary">📝 Check out my blog</a></br>
  <a href="/projects" class="cta-secondary">🚀 View my projects</a>

<script>
document.addEventListener('DOMContentLoaded', function() {
  const blogButton = document.getElementById('blog-button');
  if (blogButton) {
    blogButton.addEventListener('click', function(e) {
      e.preventDefault();

      if (window.location.hostname === 'localhost' || window.location.hostname === '127.0.0.1') {
        window.location.href = '/posts/';
      } else {
        const pathParts = window.location.pathname.split('/').filter(part => part);
        const repoName = pathParts[0] || '';
        window.location.href = repoName ? `/${repoName}/posts/` : '/posts/';
      }
    });
  }
});
</script>
