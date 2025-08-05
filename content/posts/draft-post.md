+++
date = '2025-08-04T00:28:20+07:00'
draft = false
title = 'Create your first blog using GitHub Pages and Hugo'
+++

# Building a Personal Page Blog using GitHub Pages and Hugo

In this guide, we will walk through the process of setting up a personal page blog using GitHub Pages and Hugo. This will allow you to create a professional-looking blog with minimal effort.

## Prerequisites

Before we begin, make sure you have the following:

- A GitHub account
- Basic knowledge of Git
- A text editor
- A terminal

## Step 1: Setting up GitHub Pages

1. Go to your GitHub account and create a new repository. Name it `yourusername.github.io`, where `yourusername` is your GitHub username.
2. Clone the repository to your local machine.
3. Create a new file in the repository root called `index.html`. This will be your blog's homepage.
4. Commit and push the changes to the repository.

## Step 2: Installing Hugo

1. Download and install Hugo from the [official website](https://gohugo.io/getting-started/installing/).
2. Verify the installation by running `hugo version` in your terminal.

## Step 3: Creating a New Hugo Site

1. In your terminal, navigate to the directory where you want to create your Hugo site.
2. Run `hugo new site yourusername.github.io`. This will create a new Hugo site in the directory.
3. Navigate to the new site directory by running `cd yourusername.github.io`.

## Step 4: Adding a Theme

1. Choose a theme for your blog from the [Hugo Themes](https://themes.gohugo.io/) website.
2. Download the theme to your local machine.
3. Extract the theme to the `themes` directory in your Hugo site.

## Step 5: Configuring the Theme

1. Open the `config.toml` file in the root of your Hugo site.
2. Set the `theme` parameter to the name of the theme you downloaded.

## Step 6: Creating a New Post

1. Run `hugo new posts/my-first-post.md` in your terminal. This will create a new post in the `content/posts` directory.
2. Open the new post file and add your content.

## Step 7: Previewing the Site

1. Run `hugo server -D` in your terminal. This will start a local server and open your site in a web browser.
2. Make any necessary changes to your site and preview them in the browser.

## Step 8: Deploying the Site

1. Once you are happy with your site, stop the local server by pressing `Ctrl + C` in your terminal.
2. Run `hugo` in your terminal. This will generate the static files for your site.
3. Commit and push the changes to your GitHub repository.

Congratulations! You have now set up a personal page blog using GitHub Pages and Hugo. You can continue to customize your site and add new content as you see fit.

<!--more-->

## Additional Tips

Here are some additional tips to enhance your blog:

- **Custom CSS**: Add your own styles to make your blog unique
- **SEO Optimization**: Use proper meta tags and descriptions
- **Analytics**: Track your visitors with Google Analytics
- **Comments**: Enable comments using services like Disqus

<div style="text-align: center; margin: 2rem 0; padding: 1.5rem; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); color: white; border-radius: 12px;">
  <h3 style="margin-top: 0; color: white;">🚀 Ready to Start Blogging?</h3>
  <p style="margin-bottom: 1rem;">Now that you've set up your blog, start creating amazing content!</p>
  <a href="/about/" style="display: inline-block; background: white; color: #667eea; padding: 12px 24px; border-radius: 25px; text-decoration: none; font-weight: 600; transition: transform 0.2s;">
    📝 Learn More About Me →
  </a>
</div>
