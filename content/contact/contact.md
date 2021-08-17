---
# An instance of the Contact widget.
# Documentation: https://sourcethemes.com/academic/docs/page-builder/
widget: contact

# This file represents a page section.
active: true
headless: true

# Order that this section appears on the page.
weight: 10

title: Contact
subtitle: If you would like to get in contact with me, please view my contact information or fill out the form.

content:
  # Automatically link email and phone or display as text?
  autolink: true
  
  # Email form provider
  form:
    provider: formspree
    formspree:
      id: test
    netlify:
      # Enable CAPTCHA challenge to reduce spam?
      captcha: false
  
design:
  columns: '2'
---
