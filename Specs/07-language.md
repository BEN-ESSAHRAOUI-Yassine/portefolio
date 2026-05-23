# 07 — Language System

## Overview

Three languages, switchable from the navbar via flag icons:

| Flag | Code | Language | Default |
|------|------|----------|---------|
| 🇫🇷 | `fr` | Français | ✅ Yes |
| 🇬🇧 | `en` | English | — |
| 🇲🇦 | `ar` | العربية | — |

Language is stored in `localStorage` and applied as a `data-lang` attribute on `<html>`:

```html
<html data-profile="dev" data-mode="dark" data-lang="fr">
```

Arabic (`ar`) additionally sets `dir="rtl"` on `<html>` and loads an Arabic font.

---

## Navbar Selector

```html
<div class="lang-selector">
  <button class="lang-btn active" data-lang="fr">🇫🇷</button>
  <button class="lang-btn" data-lang="en">🇬🇧</button>
  <button class="lang-btn" data-lang="ar">🇲🇦</button>
</div>
```

- Active flag: accent border or subtle highlight background
- On click: calls `setLang(code)`
- Position in navbar: between profile tabs and mode toggle

---

## RTL Support (Arabic)

When `data-lang="ar"` is set:

```js
document.documentElement.setAttribute('dir', 'rtl');
document.documentElement.setAttribute('data-lang', 'ar');
```

When switching away from Arabic:
```js
document.documentElement.setAttribute('dir', 'ltr');
```

CSS adjustments for RTL (use logical properties where possible):

```css
[dir="rtl"] .timeline-item { flex-direction: row-reverse; }
[dir="rtl"] .navbar { flex-direction: row-reverse; }
[dir="rtl"] .about-grid { direction: rtl; }
[dir="rtl"] .section-divider { margin-right: 0; margin-left: auto; }
```

Arabic font: load `Noto Sans Arabic` from Google Fonts:
```html
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+Arabic:wght@400;500;600;700&display=swap" rel="stylesheet">
```

Apply it only when Arabic is active:
```css
[data-lang="ar"] body {
  font-family: 'Noto Sans Arabic', sans-serif;
}
[data-lang="ar"] h1, [data-lang="ar"] h2, [data-lang="ar"] h3 {
  font-family: 'Noto Sans Arabic', sans-serif;
}
```

---

## JS Logic

```js
function setLang(code) {
  document.documentElement.setAttribute('data-lang', code);
  document.documentElement.setAttribute('dir', code === 'ar' ? 'rtl' : 'ltr');
  localStorage.setItem('lang', code);

  // Update active flag button
  document.querySelectorAll('.lang-btn').forEach(btn => {
    btn.classList.toggle('active', btn.dataset.lang === code);
  });

  // Re-render all translatable elements
  renderTranslations(code);

  // Reset typewriter with new language strings
  resetTypewriter(code);
}

// On load
const savedLang = localStorage.getItem('lang') || 'fr';
setLang(savedLang);
```

---

## Translation Implementation

All translatable text elements get a `data-i18n` attribute with a key:

```html
<h1 data-i18n="hero.name">Yassine BEN ESSAHRAOUI</h1>
<p data-i18n="hero.tagline.dev">Building clean, efficient web solutions...</p>
<button data-i18n="nav.projects">Projets</button>
```

The JS `renderTranslations(lang)` function walks all `[data-i18n]` elements and replaces their `textContent` with the correct string from the translations object.

```js
function renderTranslations(lang) {
  document.querySelectorAll('[data-i18n]').forEach(el => {
    const key = el.getAttribute('data-i18n');
    const text = getTranslation(key, lang);
    if (text) el.textContent = text;
  });
}
```

---

## Translations Object

### Navigation

| Key | FR | EN | AR |
|-----|----|----|----|
| `nav.about` | À propos | About | من أنا |
| `nav.skills` | Compétences | Skills | المهارات |
| `nav.experience` | Expérience | Experience | الخبرة |
| `nav.projects` | Projets | Projects | المشاريع |
| `nav.contact` | Contact | Contact | تواصل |
| `nav.testimonials` | Témoignages | Testimonials | التوصيات |

---

### Hero — Dev profile

| Key | FR | EN | AR |
|-----|----|----|----|
| `hero.title.dev` | Développeur Full Stack | Full Stack Developer | مطور ويب متكامل |
| `hero.tagline.dev` | Des solutions web propres et efficaces — de l'idée au déploiement. | Building clean, efficient web solutions — from idea to deployment. | حلول ويب نظيفة وفعّالة — من الفكرة إلى النشر. |
| `hero.cta.projects` | Voir les projets | View Projects | عرض المشاريع |
| `hero.cta.cv` | Télécharger CV | Download CV | تحميل السيرة الذاتية |

### Hero — Telecom profile

| Key | FR | EN | AR |
|-----|----|----|----|
| `hero.title.telecom` | Référent BE FTTH & Géomaticien | FTTH Network Engineer & GIS Specialist | مهندس شبكات الألياف الضوئية |
| `hero.tagline.telecom` | Conception de réseaux fibre et automatisation de workflows techniques depuis 2016. | Designing fiber networks and automating technical workflows since 2016. | تصميم شبكات الألياف وأتمتة سير العمل التقني منذ 2016. |

### Hero — IT profile

| Key | FR | EN | AR |
|-----|----|----|----|
| `hero.title.it` | Technicien Support & Réseaux | IT Support & Network Technician | تقني دعم تقني وشبكات |
| `hero.tagline.it` | Maintenir les systèmes opérationnels — du helpdesk aux infrastructures réseau. | Keeping systems running — from helpdesk to network infrastructure. | الحفاظ على تشغيل الأنظمة — من الدعم التقني إلى البنية التحتية. |

---

### About

| Key | FR | EN | AR |
|-----|----|----|----|
| `about.title` | À propos de moi | About Me | من أنا |
| `about.bio.dev` | Développeur Full Stack spécialisé en PHP et Laravel, avec une solide expérience en automatisation industrielle et télécoms. Autonome, rigoureux et orienté qualité du code. | Full Stack Developer specializing in PHP and Laravel, with a strong background in industrial automation and telecom. Self-driven and quality-focused. | مطور ويب متكامل متخصص في PHP وLaravel، مع خلفية قوية في الأتمتة الصناعية والاتصالات. مستقل ودقيق وملتزم بجودة الكود. |
| `about.bio.telecom` | Référent BE FTTH avec 4+ ans d'expérience en études de réseaux fibre optique, conception AutoCAD/QGIS, et automatisation de workflows techniques. | FTTH reference engineer with 4+ years of experience in fiber optic network studies, AutoCAD/QGIS design, and technical workflow automation. | مهندس مرجعي FTTH بخبرة 4+ سنوات في دراسات شبكات الألياف الضوئية وتصميم AutoCAD/QGIS وأتمتة سير العمل. |
| `about.bio.it` | Technicien polyvalent en maintenance informatique, réseaux et support utilisateurs. Expérience sur LAN/WAN, postes Windows/Linux, et gestion de parc. | Versatile IT technician in computer maintenance, networks, and user support. Experience with LAN/WAN, Windows/Linux workstations, and asset management. | تقني متعدد المهارات في صيانة الحواسيب والشبكات ودعم المستخدمين. خبرة في LAN/WAN وأنظمة Windows/Linux وإدارة الأصول. |
| `about.stats.exp` | Années d'expérience | Years of experience | سنوات الخبرة |
| `about.stats.projects` | Projets réalisés | Projects completed | مشاريع منجزة |
| `about.stats.certs` | Certifications | Certifications | الشهادات |
| `about.stats.techs` | Technologies | Technologies | التقنيات |

---

### Skills

| Key | FR | EN | AR |
|-----|----|----|----|
| `skills.title` | Compétences | Skills | المهارات |
| `skills.frontend` | Frontend | Frontend | الواجهة الأمامية |
| `skills.backend` | Backend | Backend | الواجهة الخلفية |
| `skills.database` | Base de données | Database | قواعد البيانات |
| `skills.devops` | Outils & DevOps | Tools & DevOps | الأدوات |
| `skills.ai` | Outils AI | AI Tools | أدوات الذكاء الاصطناعي |
| `skills.languages` | Langages & Data | Languages & Data | لغات البرمجة |
| `skills.pm` | Gestion de projet | Project Management | إدارة المشاريع |
| `skills.telecom` | Études réseau | Network Studies | دراسات الشبكة |
| `skills.cad` | CAO/DAO | CAD/GIS | التصميم الهندسي |
| `skills.civil` | Génie civil | Civil Engineering | الهندسة المدنية |
| `skills.systems` | Systèmes | Systems | الأنظمة |
| `skills.networks` | Réseaux | Networks | الشبكات |
| `skills.maintenance` | Maintenance | Maintenance | الصيانة |
| `skills.support` | Support | Support | الدعم التقني |

---

### Experience

| Key | FR | EN | AR |
|-----|----|----|----|
| `exp.title` | Expérience | Experience | الخبرة المهنية |
| `exp.education` | Formation | Education | التعليم |
| `exp.certifications` | Certifications | Certifications | الشهادات |
| `exp.present` | Présent | Present | الحاضر |

---

### Projects

| Key | FR | EN | AR |
|-----|----|----|----|
| `projects.title` | Projets | Projects | المشاريع |
| `projects.github` | Voir le code | View Code | عرض الكود |
| `projects.demo` | Démo live | Live Demo | عرض مباشر |
| `projects.gamecafe.desc` | Application web de gestion des réservations et sessions gaming en temps réel. | Web app for managing reservations and real-time gaming sessions. | تطبيق ويب لإدارة الحجوزات وجلسات الألعاب في الوقت الفعلي. |
| `projects.blog.desc` | Plateforme de blog développée avec Laravel suivant l'architecture MVC. | Blog platform built with Laravel following MVC architecture. | منصة مدونة مبنية بـ Laravel باتباع معمارية MVC. |
| `projects.autolisp.desc` | Suite de scripts AutoLISP + VBA pour automatiser la génération de plans FTTH dans AutoCAD. | AutoLISP + VBA script suite to automate FTTH plan generation in AutoCAD. | مجموعة سكريبتات AutoLISP وVBA لأتمتة إنشاء خطط FTTH في AutoCAD. |
| `projects.qgis.desc` | Extension QGIS pour le traitement de données télécom et la génération de fichiers SHP. | Custom QGIS extension for telecom data processing and SHP file generation. | امتداد QGIS مخصص لمعالجة بيانات الاتصالات وإنشاء ملفات SHP. |

---

### Testimonials

| Key | FR | EN | AR |
|-----|----|----|----|
| `testimonials.title` | Témoignages | Testimonials | التوصيات |
| `testimonials.placeholder` | Les témoignages arrivent bientôt. | Testimonials coming soon. | التوصيات قادمة قريباً. |

---

### Contact

| Key | FR | EN | AR |
|-----|----|----|----|
| `contact.title` | Contact | Contact | تواصل معي |
| `contact.subtitle` | Discutons de votre projet | Let's talk about your project | لنتحدث عن مشروعك |
| `contact.name` | Nom | Name | الاسم |
| `contact.email` | Email | Email | البريد الإلكتروني |
| `contact.subject` | Sujet | Subject | الموضوع |
| `contact.message` | Message | Message | الرسالة |
| `contact.send` | Envoyer | Send | إرسال |
| `contact.success` | Message envoyé avec succès ! | Message sent successfully! | تم إرسال الرسالة بنجاح! |
| `contact.location` | Agadir, Maroc | Agadir, Morocco | أكادير، المغرب |

---

## Typewriter Roles per Language

```js
const typewriterRoles = {
  dev: {
    fr: ["Développeur Full Stack", "Ingénieur PHP & Laravel", "Automatiseur Web"],
    en: ["Full Stack Developer", "PHP & Laravel Engineer", "Web Automation Builder"],
    ar: ["مطور ويب متكامل", "مهندس PHP وLaravel", "بناء حلول أتمتة الويب"]
  },
  telecom: {
    fr: ["Ingénieur Réseau FTTH", "Spécialiste AutoCAD & QGIS", "Expert Automatisation"],
    en: ["FTTH Network Engineer", "AutoCAD & QGIS Specialist", "Workflow Automation Expert"],
    ar: ["مهندس شبكات FTTH", "متخصص AutoCAD وQGIS", "خبير أتمتة سير العمل"]
  },
  it: {
    fr: ["Technicien Support IT", "Spécialiste Réseaux & Systèmes", "Administrateur Systèmes"],
    en: ["IT Support Technician", "Network & Systems Specialist", "Systems Administrator"],
    ar: ["تقني دعم تقني", "متخصص شبكات وأنظمة", "مدير أنظمة"]
  }
};
```

---

## Navbar Layout with Language Selector

```
[ Name/Logo ]   [ 💻 Dev | 📡 Telecom | 🔧 IT ]   [ About Skills Projects Contact ]   [ 🇫🇷 🇬🇧 🇲🇦 ]   [ ☀ ]
```

On mobile (hamburger open):
- Nav links stacked
- Profile tabs row
- Language flags row
- Mode toggle
