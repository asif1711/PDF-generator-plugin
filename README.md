# PDF Generator

**Version:** 0.1  
**Author:** Nurul Islam  
**Dependencies:** WordPress 6.9 · Nginx · PHP 7.4.30 · Contact Form 7 · Dompdf · MySQL DB

---

## 📌 Overview

This plugin generates a **PDF logbook** when a specific Contact Form 7 form is submitted and provides a **controlled download link** on a dedicated page.

---

## ✅ What This Plugin Does

- Listens to a **specific Contact Form 7 form**
- Extracts predefined form fields
- Generates a PDF using Dompdf
- Stores the PDF in WordPress uploads (local / production)
- Logs submission metadata in the database
- Redirects the user to a download page
- Allows **safe disabling at any time**

---

## 🧠 Architecture Summary

Contact Form 7 (submission)  
↓  
Plugin guardrails (panic switch, env, form ID)  
↓  
PDF generation (Dompdf)  
↓  
PDF stored in uploads/logbooks  
↓  
Metadata stored in database  
↓  
CF7 redirects to `/pdf-ready/`  
↓  
Plugin injects download link  

---

## 📦 Installation

### Required files
# PDF Generator

**Version:** 0.1  
**Author:** Nurul Islam  
**Dependencies:** WordPress 6.9 · Nginx · PHP 7.4.30 · Contact Form 7 · Dompdf  

---

## 📌 Overview

This plugin generates a **PDF logbook** when a specific Contact Form 7 form is submitted and provides a **controlled download link** on a dedicated page.

---

## ✅ What This Plugin Does

- Listens to a **specific Contact Form 7 form**
- Extracts predefined form fields
- Generates a PDF using Dompdf
- Stores the PDF in WordPress uploads (local / production)
- Logs submission metadata in the database
- Redirects the user to a download page
- Allows **safe disabling at any time**

---

## 🧠 Architecture Summary

Contact Form 7 (submission)  
↓  
Plugin guardrails (panic switch, env, form ID)  
↓  
PDF generation (Dompdf)  
↓  
PDF stored in uploads/logbooks  
↓  
Metadata stored in database  
↓  
CF7 redirects to `/pdf-ready/`  
↓  
Plugin injects download link  

---

## 📦 Installation

### Required files
pdf-generator/
├── main.php
├── dompdf/
│       └── autoload.inc.php
└── templates/
        └── template-1.php

---

## 📄 Required WordPress Page

Create a page with:

- **Slug:** `pdf-ready`
- **Title:** Any
- **Content:** Leave empty

The plugin dynamically injects the download UI.

---

## 📝 Contact Form 7 Setup

### Required Form Fields

The Contact Form 7 form **must** contain fields with these exact names:

[text* student_name]
[text* course_name]
[date* log_date]
[textarea* activity]
[number* hours]

[submit "Generate PDF"]


⚠️ Field names are case-sensitive.

---

## 🔐 Plugin Guardrails

This plugin is intentionally defensive.

### 1. Execution Toggle (Panic Button)
define('CF7_PDF_ENABLED', true);

When disabled:
    Contact Form 7 continues to work
    No PDFs are generated
    No errors occur

### 2. Environment Guard
define('CF7_PDF_ENV', 'dev');
define('CF7_PDF_ALLOWED_ENVS', ['dev', 'staging']);

PDF generation only runs if the current environment is allowed.

Example:

CF7_PDF_ENV = 'production'


→ PDF generation blocked

This prevents accidental execution in restricted environments.

### 3. Hard Form Whitelist
$CF7_PDF_ALLOWED_FORMS = [
    80, // input form ID
];

Only whitelisted form IDs can generate PDFs.
All other forms are ignored safely.

## 📁 PDF Storage

PDFs are stored in:
    wp-content/uploads/logbooks/

Filename format:
    logbook-<timestamp>.pdf

## 🗄️ Database Logging (Phase 2)

On plugin activation, a database table is created:
    wp_cf7_pdf_logs

Stored fields:
    form_id
    student_name
    course_name
    pdf_file
    created_at

Purpose:
    Submission traceability
    Audit support
    Future admin reporting

## 🧾 PDF Template

Location
    templates/<template-name>.php


Purpose
    Layout
    Styling
    Variable rendering

Available variables
    $student_name
    $course_name
    $logbook_rows

## 🧪 Logging & Debugging

Enable debug logging:
    define('CF7_PDF_DEBUG', true);


Logs appear as:
    [CF7 PDF] PDF saved: logbook-1770008549.pdf

Recommended:
    Enable on local / staging
    Disable on production if not required

## 🔁 Safe Rollback Procedure

If unexpected behavior occurs:
    define('CF7_PDF_ENABLED', false);


Result:
    PDF generation stops immediately
    Site remains functional
    Plugin does not need to be deactivated

## 🔒 Security Model

No admin UI
No direct file access
Controlled execution via guardrails
Uses WordPress uploads system
Uses transients for short-lived state
Uses WordPress database APIs only

## 🔮 Future Extensions

This plugin currently supports Contact Form 7.
The architecture allows future integration with:
        Gravity Forms
        Multi-form handling
        Approval workflows
        Admin reporting UI



