# 03 — Sections

## Section Visibility per Profile

| Section | Dev | Telecom | IT Support |
|---------|-----|---------|------------|
| Hero | ✅ (dev variant) | ✅ (telecom variant) | ✅ (IT variant) |
| About | ✅ shared (bio adapts) | ✅ shared | ✅ shared |
| Skills | ✅ dev skills | ✅ telecom skills | ✅ IT skills |
| Experience | ✅ dev-focused entries | ✅ telecom entries | ✅ IT entries |
| Projects | ✅ web projects | ✅ AutoLISP/QGIS tools | ✅ infra/scripts |
| Testimonials | ✅ shared | ✅ shared | ✅ shared |
| Contact | ✅ shared | ✅ shared | ✅ shared |

Each section has **profile variants** — same component, different content shown via `data-show-in` attributes.

---

## Section Order (all profiles)

1. Hero
2. About
3. Skills
4. Experience
5. Projects
6. Testimonials
7. Contact

---

## 1. Hero

Full viewport height. Name as H1, animated typewriter subtitle, 2 CTAs, scroll arrow.

### Dev variant (`data-show-in="dev"`)
- Title: **Développeur Full Stack**
- Roles (typewriter): "Full Stack Developer", "PHP & Laravel Engineer", "Web Automation Builder"
- Tagline: "Building clean, efficient web solutions — from idea to deployment."
- CTA 1: "View Projects" → #projects
- CTA 2: "Download CV" → [PLACEHOLDER PDF]

### Telecom variant (`data-show-in="telecom"`)
- Title: **Référent BE FTTH & Géomaticien**
- Roles (typewriter): "FTTH Network Engineer", "GIS & AutoCAD Specialist", "Workflow Automation Expert"
- Tagline: "Designing fiber networks and automating technical workflows since 2016."
- CTA 1: "View Projects" → #projects
- CTA 2: "Download CV" → [PLACEHOLDER PDF]

### IT variant (`data-show-in="it"`)
- Title: **Technicien Support & Réseaux**
- Roles (typewriter): "IT Support Technician", "Network & Hardware Specialist", "Systems Administrator"
- Tagline: "Keeping systems running — from helpdesk to network infrastructure."
- CTA 1: "View Experience" → #experience
- CTA 2: "Download CV" → [PLACEHOLDER PDF]

---

## 2. About

Shared section. Two-column layout (photo left, text right). Photo placeholder with initials "YB".

**Bio adapts per profile** (short paragraph swap):

- **Dev:** "Développeur Full Stack spécialisé en PHP et Laravel, avec une solide expérience en automatisation industrielle et télécoms. Autonome, rigoureux et orienté qualité du code."
- **Telecom:** "Référent BE FTTH avec 4+ ans d'expérience en études de réseaux fibre optique, conception AutoCAD/QGIS, et automatisation de workflows techniques."
- **IT:** "Technicien polyvalent en maintenance informatique, réseaux et support utilisateurs. Expérience sur des environnements LAN/WAN, postes Windows/Linux, et gestion de parc."

**Stat badges (adapt per profile):**

| Profile | Stat 1 | Stat 2 | Stat 3 | Stat 4 |
|---------|--------|--------|--------|--------|
| Dev | 7+ ans exp. | [N] projets web | 3 certifications | 20+ technos |
| Telecom | 4+ ans FTTH | 100+ études réalisées | AutoCAD + QGIS | Orange, SFR, Bouygues… |
| IT | 6+ ans terrain | LAN / WAN | Windows + Linux | Helpdesk + Réseaux |

---

## 3. Skills

Grouped badges. Groups shown/hidden per profile.

### Dev profile skills
- **Frontend:** HTML5, CSS3, JavaScript
- **Backend:** PHP, Laravel, Blade
- **Database:** MySQL, SQL, Modélisation relationnelle
- **DevOps / Outils:** Git, GitHub, XAMPP, Vite, Composer, VS Code
- **AI Tools:** Claude Code, AntiGravity, OpenCode
- **Langages:** Python, VBA, AutoLISP
- **Gestion de projet:** Jira, Agile (Kanban, Scrum)

### Telecom profile skills
- **Études réseau:** FTTH, FTTA, APS, APD, DFT, DOE, VDR
- **Calculs & livrables:** CAPFT, COMAC, TOPOCALC
- **CAO/DAO:** AutoCAD, QGIS, ArcGIS, FiberGIS, Fiberscript
- **Automatisation:** AutoLISP, VBA, Python (QGIS API)
- **Génie civil:** Piquetage, coordination chantiers, plans GC
- **Clients:** Orange, SFR, Bouygues, Axione, TDF, Kyntus…

### IT Support profile skills
- **Systèmes:** Windows, Linux, déploiement postes
- **Réseaux:** LAN, WAN, switchs, routeurs, Wi-Fi, câblage
- **Maintenance:** PC, imprimantes, serveurs, périphériques
- **Outils:** XAMPP, VS Code, Active Directory, antivirus
- **Automatisme:** PLC, supervision process, Vijeo Citect, Unity Pro UL
- **Support:** Helpdesk, ticketing, reporting, formation utilisateurs

---

## 4. Experience

Vertical timeline, most recent first. Entries filtered per profile.

### Dev profile entries
1. Référent BE FTTH — OPTICAL TELECOM (2022–2024) → highlight: AutoLISP/VBA dev, QGIS Python extension
2. Chargé d'études FTTH — ID2S Telecom (2020–2022) → highlight: VBA automation, data processing

### Telecom profile entries
1. Référent BE FTTH — OPTICAL TELECOM (2022–2024) → highlight: études APS/APD/DFT/DOE, AutoCAD/QGIS, chantiers
2. Chargé d'études FTTH — ID2S Telecom (2020–2022) → highlight: modélisation SIG, calcul de charge, livrables clients

### IT Support profile entries
1. Technicien réseaux — UNIVERS HIGH TECH (2019)
2. Technicien maintenance informatique — INFOSAT (2018–2019)
3. Technicien automatisme — SCADELEC (2018)
4. Automaticien — LES HUILERIES DU SOUSS BEL HASSAN (2016–2017, 2016)
5. Maintenance électrique — STE MAROCAINE DES EMBALLAGES FANTASIA (2015)

**Education + Certifications** — shown in all profiles at bottom of section.

---

## 5. Projects

Card grid (2 cols desktop, 1 col mobile).

### Dev profile projects
1. **GameCafé Manager** — PHP, MySQL (PDO), auth, roles, real-time sessions
2. **Personal Blog** — Laravel, Blade, Tailwind CSS, CRUD, auth, pagination

### Telecom profile projects
1. **AutoCAD AutoLISP Tools** — AutoLISP + VBA, Excel→DXF, layer/block automation
2. **QGIS Python Extension** — Python, QGIS API, SHP generation, telecom data processing

### IT Support profile projects
- [PLACEHOLDER — Yassine to confirm if there are relevant IT scripts or tools to showcase]
- Fallback: show AutoLISP + QGIS projects here too as "automation tools"

---

## 6. Testimonials

Shared across all profiles. Horizontal scroll (mobile), grid (desktop).
Content: [PLACEHOLDER — 2–3 real testimonials needed]

---

## 7. Contact

Shared across all profiles.
- Left: email, phone, location, LinkedIn, GitHub
- Right: contact form (Name, Email, Subject, Message, Send)
- Form: client-side validation + mailto fallback
