---
layout: page
title: Resume
permalink: /resume/
---

<style>
.resume-pdf {
  width: 100%;
  height: 1100px;
  border: 1px solid #e8e8e8;
  border-radius: 4px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
}

.desktop-view { display: block; }
.mobile-view { display: none; }

@media (max-width: 768px) {
  .desktop-view { display: none; }
  .mobile-view { display: block; }
}

.download-btn {
  display: inline-block;
  padding: 12px 24px;
  background-color: #2a7ae4;
  color: white;
  text-decoration: none;
  border-radius: 6px;
  font-weight: 500;
  transition: background-color 0.2s;
}

.download-btn:hover {
  background-color: #1967d2;
}
</style>

<div class="desktop-view">
  <iframe class="resume-pdf"
          src="{{ '/assets/documents/resume.pdf' | relative_url }}" 
          title="Arunabh Ghosh Resume">
  </iframe>
</div>

<div class="mobile-view" style="text-align: center; padding: 3rem 1rem;">
  <h2>Resume</h2>
  <p>View my professional experience, skills, and achievements.</p>
  <a href="{{ '/assets/documents/resume.pdf' | relative_url }}" 
     class="download-btn"
     download="Arunabh_Ghosh_Resume.pdf">
    Download Resume (PDF)
  </a>
</div>
