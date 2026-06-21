+++
draft = false
title = 'Homepage'
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
  <span>💼 6 years experience</span>
</div>

## About

<div>
  <p>
    Passionate technologist with extensive experience in developing scalable applications across various industries. Accomplished in building and working within cross-functional teams, as well as managing products from conception to deployment, delivering robust and maintainable applications that significantly enhance business efficiency and user satisfaction.</p><p>Driven by curiosity and a continuous desire to learn, constantly seeks to refine processes through the adoption of innovative technologies, patterns, and emerging methodologies.
  </p>
</div>

## Experience

### Sun* Asterisk

**Software Engineer** · Hanoi · 9/2024 – Now

- Developed a B2B medical software solution using Flutter while driving major infrastructure upgrades, including a shift to a monorepo that significantly cut down on management overhead.
- Streamlined the CI/CD pipeline by removing redundant processes, saving the team both development time and operational costs.
- Designed an automation workflow for code reviews that made team collaboration smoother and faster.
- Acted as a full-stack engineer for an AI chat app, leveraging Flutter, Python, and the LangChain ecosystem (LangGraph, Langfuse) to integrate various Google LLMs.
- Built modular, highly testable features by coordinating closely across the entire stack to ensure seamless data flow and performance.

### FPT Software

**Software Engineer** · Hanoi · 01/2021 – 07/2024

- Built all-stack IoT products from the ground up, handling everything from embedded firmware to the frontend and backend infrastructure.
- Engineered, developed and shipped a reliable React Native app for enterprise clients from idea, giving users a smooth way to monitor and control their smart home devices in real-time.
- Built a bridge between Flutter and native module to facilitate Diagnostics over Internet Protocol (DoIP), standardized as ISO 13400-2, over a Wi-Fi connection, that enables in-depth device configuration and monitoring.
- Kept the codebase clean and accessible by establishing clear coding conventions and thorough documentation, making it easy for the team to test and collaborate.

### Vinfast

**Quality Assurance Intern** · Hanoi · 07/2020 – 11/2020

- Built the testing environment and ran hands-on trials for motorcycle charging stations to ensure everything worked as expected.
- Designed and maintained a regression test suite to catch bugs early and keep the software stable during every development cycle.
- Tested motorcycle durability in real-world conditions to verify long-term performance and reliability.

### Makipos

**Embedded Engineer Intern** · Hanoi · 03/2020 – 06/2020

- Developed a custom C library to streamline data collection from sensors using I2C, SPI, and UART protocols.
- Handled the physical assembly of electronic circuits through precision soldering and managed the firmware flashing process for all hardware.

## Education

### Bachelor's degree, Electronics & Automation Control Engineering

**Hanoi University of Science and Technology**

- Studied electronics, hardware circuitry, and embedded design
- Programmed low-level hardware using embedded C and Linux
- Achieved Hands-on experience by engineering and building many IoT projects from scratch involving many layers of software: Embedded, Web server by ExpressJS

### Physics

**Hanoi Amsterdam High School**

- Physics-specialized class

## Technical Skills

### Languages

Dart, Typescript, Java, C, C#, Kotlin, Bash script, Python

### Frameworks

Flutter, ExpressJS, NextJS, Spring Boot, ReactJS, React Native, Unity

### Databases

PostgreSQL, RealmDB, Firestore

### CI/CD automation

Fastlane, Github Actions

### Cloud platforms and tools

GCP, Docker, Git, Postman, Growthbook, New Relic, Fastlane, Nginx, VSCode

## Languages

- **Vietnamese** — Mother tongue
- **English** — Working Proficiency
- **Japanese** — Basic

## Interests

- Using automation tools to improve productivity
- Experimenting with emerging technologies and new tools, understanding how it works in-depth

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
