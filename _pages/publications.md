---
layout: simple
permalink: /publications/
title: Publications
years: [2025, 2024, 2023, 2022, 2021, 2019]
---

<!-- _pages/publications.md -->
<div class="publications">

{%- for y in page.years %}
  <h2 class="year">{{y}}</h2>
  {% bibliography -f papers -q @*[year={{y}}]* %}
{% endfor %}

</div>

<script>
document.addEventListener('DOMContentLoaded', function() {
  console.log('Publications script loaded');
  
  // Wait for Jekyll Scholar to render
  setTimeout(function() {
    // Find all bibliography entries
    const bibliographyEntries = document.querySelectorAll('.bibliography li, ol.bibliography li, li');
    console.log('Found bibliography entries:', bibliographyEntries.length);
    
    bibliographyEntries.forEach((entry, index) => {
      console.log('Processing entry', index);
      
      // Look for existing content blocks
      const abstractContent = entry.querySelector('div.abstract');
      const bibtexContent = entry.querySelector('div.bibtex');
      
      // Create our own toggle buttons
      if (abstractContent || bibtexContent) {
        // Create button container
        const buttonContainer = document.createElement('div');
        buttonContainer.className = 'custom-toggle-buttons';
        buttonContainer.style.marginTop = '10px';
        buttonContainer.style.marginBottom = '15px';
        
        // Add abstract button if content exists
        if (abstractContent) {
          const abstractBtn = document.createElement('button');
          abstractBtn.className = 'custom-toggle-btn';
          abstractBtn.textContent = 'Abstract';
          abstractBtn.setAttribute('data-target', `custom-abstract-${index}`);
          buttonContainer.appendChild(abstractBtn);
          
          // Set up abstract content
          abstractContent.id = `custom-abstract-${index}`;
          abstractContent.style.display = 'none';
          abstractContent.classList.add('custom-content');
        }
        
        // Add bibtex button if content exists
        if (bibtexContent) {
          const bibtexBtn = document.createElement('button');
          bibtexBtn.className = 'custom-toggle-btn';
          bibtexBtn.textContent = 'BibTeX';
          bibtexBtn.setAttribute('data-target', `custom-bibtex-${index}`);
          buttonContainer.appendChild(bibtexBtn);
          
          // Set up bibtex content
          bibtexContent.id = `custom-bibtex-${index}`;
          bibtexContent.style.display = 'none';
          bibtexContent.classList.add('custom-content');
        }
        
        // Insert button container after the entry content
        entry.appendChild(buttonContainer);
        
        // Add click handlers
        const buttons = buttonContainer.querySelectorAll('.custom-toggle-btn');
        buttons.forEach(button => {
          button.addEventListener('click', function() {
            const targetId = this.getAttribute('data-target');
            const target = document.getElementById(targetId);
            
            if (target) {
              if (target.style.display === 'none') {
                target.style.display = 'block';
                this.textContent = 'Hide ' + this.textContent;
                this.classList.add('active');
              } else {
                target.style.display = 'none';
                this.textContent = this.textContent.replace('Hide ', '');
                this.classList.remove('active');
              }
            }
          });
        });
      }
    });
  }, 1000);
});
</script>
