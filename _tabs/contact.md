---
layout: page
title: Contact Me
icon: fas fa-envelope
order: 6
---

If you'd like to work together, please fill out the form below. Alternatively, you can [hire me as freelance/part-time on Upwork](https://www.upwork.com/freelancers/~014b92184d51e08658).

<div class="contact-form" style="margin-top: 2em;">
  <form action="https://formsubmit.co/arief@tuxnoob.com" method="POST">
    <!-- Honeypot for spam protection -->
    <input type="text" name="_honey" style="display:none">
    
    <!-- Next URL after form submission (optional, it goes to a default thank you page otherwise) -->
    <!-- <input type="hidden" name="_next" value="https://tuxnoob.com/thank-you.html"> -->
    
    <div style="margin-bottom: 1.2em;">
      <label for="name" style="display: block; margin-bottom: 0.3em; font-weight: bold;">Name</label>
      <input type="text" id="name" name="name" required style="width: 100%; padding: 0.6em; border-radius: 4px; border: 1px solid #ccc; background: var(--main-bg);">
    </div>
    
    <div style="margin-bottom: 1.2em;">
      <label for="country" style="display: block; margin-bottom: 0.3em; font-weight: bold;">Country</label>
      <input type="text" id="country" name="country" required style="width: 100%; padding: 0.6em; border-radius: 4px; border: 1px solid #ccc; background: var(--main-bg);">
    </div>

    <div style="margin-bottom: 1.2em;">
      <label for="email" style="display: block; margin-bottom: 0.3em; font-weight: bold;">Email</label>
      <input type="email" id="email" name="email" required style="width: 100%; padding: 0.6em; border-radius: 4px; border: 1px solid #ccc; background: var(--main-bg);">
    </div>
    
    <div style="margin-bottom: 1.2em;">
      <label for="hire_type" style="display: block; margin-bottom: 0.3em; font-weight: bold;">Hire Type</label>
      <select id="hire_type" name="hire_type" required style="width: 100%; padding: 0.6em; border-radius: 4px; border: 1px solid #ccc; background: var(--main-bg);">
        <option value="" disabled selected>Select an option...</option>
        <option value="Full-time">Full-time</option>
        <option value="Part-time">Part-time</option>
        <option value="Freelance">Freelance</option>
        <option value="Contract">Contract</option>
      </select>
    </div>
    
    <div style="margin-bottom: 1.2em;">
      <label for="job_description" style="display: block; margin-bottom: 0.3em; font-weight: bold;">Job Description</label>
      <textarea id="job_description" name="job_description" rows="6" required style="width: 100%; padding: 0.6em; border-radius: 4px; border: 1px solid #ccc; background: var(--main-bg);"></textarea>
    </div>
    
    <button type="submit" style="padding: 0.8em 2em; cursor: pointer; background-color: var(--link-color, #007bff); color: white; border: none; border-radius: 4px; font-weight: bold;">Send Message</button>
  </form>
</div>
