---
layout: page
title: HEP Tokens Project
description: Can LLMs be trained to understand tokens from particle physics foundation models?
permalink: /projects/experiment-visualization/
importance: 1
category: experiments
access_password: heptokens
_styles: |
  .project-lock {
    padding: 1rem;
    border: 1px solid #e0e0e0;
    border-radius: 0.5rem;
    background: #f8f9fa;
    max-width: 540px;
  }

  .project-lock form {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
    margin-top: 0.5rem;
    align-items: center;
  }

  .project-lock input {
    flex: 1 1 200px;
    min-width: 0;
  }

  .project-lock button {
    flex: 0 0 auto;
  }

  .project-lock .note {
    margin: 0.5rem 0 0;
    color: #6c757d;
    font-size: 0.95rem;
  }

  .project-content {
    margin-top: 1.5rem;
  }

  .project-content.is-locked {
    display: none;
  }

  .project-content iframe {
    width: 100%;
    min-height: 75vh;
    border: 1px solid #e0e0e0;
    border-radius: 0.5rem;
  }
---

Below are some results from asking various LLMs to "caption" simulated particle physics events.

<div class="project-lock" id="project-lock">
  <p>Enter the password to view the visualization.</p>
  <form id="project-password-form">
    <input type="password" id="project-password-input" class="form-control" placeholder="Password" required />
    <button type="submit" class="btn btn-primary">Unlock</button>
  </form>
  <p class="text-danger" id="project-lock-message"></p>
</div>

<div id="project-content" class="project-content is-locked">
  <iframe
    id="project-iframe"
    data-src="{{ '/assets/projects/experiment/model_test_results.html' | relative_url }}"
    title="Project visualization"
    loading="lazy"
  ></iframe>
</div>

<script>
  (() => {
    const PASSWORD = "{{ page.access_password | default: 'changeme' }}";
    const form = document.getElementById("project-password-form");
    const input = document.getElementById("project-password-input");
    const lock = document.getElementById("project-lock");
    const content = document.getElementById("project-content");
    const message = document.getElementById("project-lock-message");
    const iframe = document.getElementById("project-iframe");

    function unlock() {
      lock.style.display = "none";
      content.classList.remove("is-locked");
      if (!iframe.src) {
        iframe.src = iframe.dataset.src;
      }
    }

    form.addEventListener("submit", (event) => {
      event.preventDefault();
      const guess = input.value.trim();
      if (!guess) {
        message.textContent = "Enter the password to continue.";
        return;
      }
      if (guess === PASSWORD) {
        unlock();
      } else {
        message.textContent = "That password does not match.";
      }
    });
  })();
</script>
