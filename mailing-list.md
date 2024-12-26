---
layout: default
title: mailing list
permalink: /mailing-list/
---

# Mailing list

Don't use this yet it's not gonna work

<form id="signup-form" class="max-w-md mx-auto p-4">
  <input 
    type="email" 
    id="email" 
    required 
    placeholder="Enter your email"
    class="w-full p-2 border rounded mb-2"
  >
  <button 
    type="submit"
    class="w-full bg-blue-500 text-white p-2 rounded hover:bg-blue-600"
  >
    Subscribe
  </button>
  <p id="status" class="mt-2 text-center"></p>
</form>

<script>
document.getElementById('signup-form').addEventListener('submit', async (e) => {
  e.preventDefault();
  const email = document.getElementById('email').value;
  const statusElement = document.getElementById('status');
  
  try {
    const response = await fetch('https://mailing-list.nialls-account.workers.dev/api/subscribe', {
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