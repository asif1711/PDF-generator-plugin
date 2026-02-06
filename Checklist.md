## ✅ Pre-Activation Checklist (PDF Generator – CF7)

Use this checklist **before activating the plugin on any new system**
(local, staging, or production).

---

### 🔧 Configuration
- [ ] `CF7_PDF_ENABLED` set to `true`
- [ ] `CF7_PDF_ENV` set correctly (`dev`, `staging`, `production`)
- [ ] `CF7_PDF_ALLOWED_ENVS` includes the current environment
- [ ] `CF7_PDF_TEMPLATE` matches an existing template file
- [ ] `CF7_PDF_DEBUG` set appropriately (on for dev, off for prod)

---

### 📝 Contact Form 7
- [ ] Correct form ID added to `$CF7_PDF_ALLOWED_FORMS`
- [ ] Form fields match required names exactly:
  - `student_name`
  - `course_name`
  - `log_date`
  - `activity`
  - `hours`
- [ ] Form submission works normally

---

### 📄 WordPress Pages
- [ ] Page with slug `pdf-ready` exists
- [ ] Page content is empty (plugin injects UI)

---

### 📦 Plugin Files
- [ ] `dompdf/autoload.inc.php` exists
- [ ] Selected template exists in `templates/`
- [ ] Plugin activated once after upload (DB table created)

---

### 🗄️ Database
- [ ] Table `wp_cf7_pdf_logs` exists
- [ ] Test submission inserts a DB record

---

### 🔐 Environment Safety
- [ ] Filesystem permissions confirmed (or storage disabled)
- [ ] Panic button tested (`CF7_PDF_ENABLED = false`)
- [ ] No PHP fatal errors on activation

---

### 🧪 Final Sanity Test
- [ ] Submit form once
- [ ] PDF generated (or safely skipped per environment)
- [ ] Redirect to `/pdf-ready/` works
- [ ] Download link appears (if enabled)
- [ ] DB record visible

---

### 🛑 Emergency Rollback
- Set `CF7_PDF_ENABLED = false`
- Save file
- Site remains fully functional
