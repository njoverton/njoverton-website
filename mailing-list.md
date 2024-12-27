---
layout: default
title: Mailing list
permalink: /mailing-list/
date: 2024-12-27
---

<article class="post">
  <h1>{{ page.title }}</h1>
  <time datetime="{{ page.date | date_to_xmlschema }}">
    last updated on {{ page.date | date: "%d %B %Y" }}
  </time>
  <hr>
</article>

<figure>
  <img src="{{ site.baseurl }}/assets/images/edvard_munch_the_sun.jpg" alt="The Sun Edvard Munch" style="max-width: 100%; height: auto;">
  <figcaption>The Sun by Edvard Munch, 1909</figcaption>
</figure>

<p>Subscribe for new posts to be sent to your inbox.</p>

<div id="form-container" style="display: flex; flex-direction: column; align-items: center; margin: 0 auto; text-align: center;">
  <form id="signup-form" style="display: flex; align-items: center; justify-content: center; gap: 0.5em; margin: 0.5em 0;">
    <input 
      type="email" 
      id="email" 
      required 
      placeholder="enter your email"
      style="padding: 0.5em; border: 1px solid #333;"
    >
    <button 
      type="submit"
      style="padding: 0.5em 1em; background: #e4d5b7; border: 1px solid #333; cursor: pointer; color: #333;"
	  onmouseover="this.style.background='#d4c0a5';" 
      onmouseout="this.style.background='#e4d5b7';"
    >
      subscribe
    </button>
  </form>
  <!-- Add this status paragraph -->
  <p id="status" style="margin: 0.5em 0"></p>
</div>

<script>
document.getElementById('signup-form').addEventListener('submit', async (e) => {
  e.preventDefault();
  const email = document.getElementById('email').value;
  const statusElement = document.getElementById('status');
  
  try {
    const response = await fetch('https://mailing-list.nialls-account.workers.dev', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({ email })
    });
    
    const data = await response.json();
    
    if (response.ok) {
      statusElement.textContent = 'Thanks for subscribing!';
      statusElement.className = 'mt-2 text-center text-green-600';
    } else {
      throw new Error(data.message || 'Something went wrong');
    }
  } catch (error) {
    statusElement.textContent = error.message;
    statusElement.className = 'mt-2 text-center text-red-600';
  }
});
</script>