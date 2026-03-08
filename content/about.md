+++
draft = false
title = 'About'
aliases = [
  "/about",
]
+++

<div style="text-align: center; margin: 3rem 0;">
  <img src="https://ndnam198.github.io/my-github-blog/images/avatar.jpeg" alt="Nam Nguyen - Fullstack Engineer" width="180" height="180" style="border-radius: 50%; object-fit: cover; display: block; margin: 0 auto 2rem auto;">
</div>

# Nam Nguyen

Fullstack Engineer

<div class="hero-badges">
  <span>📍 Hanoi, Vietnam</span>
  <span>💼 6 years experience</span>
</div>

## Professional Summary

<div class="summary-block">
  <p>
    Full-stack software engineer with <strong>6 years of experience</strong>, focused on frontend and mobile—especially <strong>Flutter</strong>. I've built and shipped <strong>5+ apps</strong> used by over <strong>100,000 people</strong>.
  </p>

  - **Clean Architecture** — Maintainable & Scalable
  - **Performance** — Speed & Efficiency
  - **Security** — User & Data Protection
</div>

## Education

### Bachelor's degree, Electronics & Automation Control Engineering

**Hanoi University of Science and Technology**

- Electronics, hardware circuitry, and embedded design
- Low-level hardware programming with embedded C and Linux
- Industrial product design and development

### Physics Specialization

**Hanoi Amsterdam High School**

- Advanced Physics studies with talented peers

## Technical Skills

### Languages

Dart, JavaScript, TypeScript, Python, Bash Scripting, Embedded C

### Frameworks

Flutter, React Native, ExpressJS, FastAPI, LangChain, LangGraph

### Cloud & Tools

GCP, Docker, Fastlane, Firebase, Supabase

## Languages

- **Vietnamese** — Native
- **English** — Working Proficiency
- **Japanese** — Basic

## Interests

- Using automation tools to improve productivity
- Experimenting with emerging technologies
- Understanding how things work in-depth

## Current Goal

<div class="cta-block">
  <p style="margin-bottom: 1.5rem;">Build meaningful software that improves lives</p>
  <a href="#" id="blog-button" class="cta-primary">📝 Check out my blog →</a>
  <a href="/projects" class="cta-secondary">🚀 View my projects →</a>
</div>

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
