+++
date = '2025-08-03T14:01:02+07:00'
draft = false
title = 'Home'
aliases = [
  "/main",
  "/index",
  "/home"
]
+++

<div style="text-align: center; margin: 4rem 0;">
  <h2>Welcome to Nam's Portfolio</h2>
  <p style="font-size: 1.2rem; margin: 2rem 0;">Redirecting to About page...</p>
  <script>
    // Dynamic redirect that works for both local and remote
    const baseURL = window.location.origin;
    const currentPath = window.location.pathname;
    
    // For local: just use /about/
    // For GitHub Pages: use the full path with repo name
    if (window.location.hostname === 'localhost' || window.location.hostname === '127.0.0.1') {
      window.location.href = '/about/';
    } else {
      // Extract repo name from current path and construct about URL
      const pathParts = currentPath.split('/').filter(part => part);
      const repoName = pathParts[0] || '';
      window.location.href = repoName ? `/${repoName}/about/` : '/about/';
    }
  </script>
  <noscript>
    <a href="/about/" style="display: inline-block; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); color: white; padding: 12px 24px; border-radius: 25px; text-decoration: none; font-weight: 600;">
      Go to About Page →
    </a>
  </noscript>
</div>