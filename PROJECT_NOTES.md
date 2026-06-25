# Project Notes — Isares Samruayruen Portfolio

> สรุปงานที่ทำในโปรเจคนี้ เพื่อให้ session ใหม่เข้าใจ context ได้ทันที

## ภาพรวม
- เว็บ portfolio/resume แบบ **single-file static site** (`index.html` ไฟล์เดียว, CSS+JS อยู่ในไฟล์, ไม่มี build step)
- เจ้าของ: **Isares Samruayruen** — ตำแหน่ง **Technical Lead Software Developer**
- ธีม: dark navy (`#0b0f19`) + accent gradient ฟ้า→ม่วง (`#38bdf8` → `#6366f1`), ฟอนต์ Plus Jakarta Sans + Prompt (รองรับไทย)

## Deploy
- **GitHub repo:** https://github.com/Isarez/portfolio (public)
- **Live URL:** https://isarez.github.io/portfolio/ (GitHub Pages, deploy จาก branch `main` / root อัตโนมัติ)
- Auth: ใช้ `gh` CLI (login แล้วในชื่อ account `Isarez`), credential helper เครื่องนี้เดิมเป็นของ AWS CodeCommit
- Commit แบบ push เมื่อผู้ใช้สั่งเท่านั้น

## โครงสร้างไฟล์
```
index/
├── index.html              # ทั้งเว็บ
├── images/
│   ├── img.jpg             # รูปโปรไฟล์ (ใช้ใน hero avatar)
│   └── portfolio-qr.png    # QR code ชี้ไป live URL
└── cv/
    └── CV_ISARES_S.pdf     # CV ดาวน์โหลดได้จากปุ่มใน hero
```

## ลำดับ section ในหน้าเว็บ (บนลงล่าง)
1. Hero/About (`#about`) — มีรูป + ปุ่ม Get In Touch / View Experience / **Download CV**
2. Quick Stats (`.stats` section แยก: 13+, 4+, 100%, Agile — มี count-up animation)
3. Education (`#education`)
4. Experience (`#experience`)
5. Skills (`#skills`)
6. Projects (`#projects`)
7. Contact (`#contact`) — อยู่ล่างสุดก่อน footer
- Navbar order: About → Education → Experience → Skills → Projects → Contact (มี scroll-spy highlight + underline animation)

## เนื้อหา Experience (สำคัญ — เคยเรียบเรียงใหม่เป็นภาษาอังกฤษ)
- **Thai Credit Bank** (Technical Leader, Mar 2020–Present): กล่องเดียว แยก 3 subtitle — **eKYC Platform**, **NDID Platform**, **OCR Service**
- **Saitech Solution (TRUE Corp.)** (Senior Software Developer): OMX Mobile Backend (TIBCO/Java) + Webtool Application (ReactJS/Spring Boot/Oracle/Elasticsearch/JMS)
- **PSP (Thailand) / Bank of Ayudhya** (Software Developer): DMS Data Correction + File Management + Dataset Dashboard (AngularJS/Spring Boot/MSSQL/iReport)
- **Pro Technical Info Service**: กล่องเดียว แยก 2 subtitle — Software Developer (Oct 2012–May 2015, TOT Wi-Fi + NACC) และ Freelance (Jun 2015–Feb 2016, TOT Wi-Fi maintenance)
- Featured Focus Projects: 6 การ์ด อ้างอิงตาม experience

## Animations / effects ที่ทำไว้ (อยู่ใน `<style>` และ `<script>` ท้ายไฟล์)
- **Particle background** — `<canvas id="particles">` วาด particle ลอย + เส้นเชื่อม (constellation), ปรับจำนวนตามขนาดจอ
- **Avatar glow** — conic-gradient ring หมุน (`avatarSpin` 9s) + pulsing halo (`avatarPulse`) + glow pulse หลังรูป
- Hero fade-up เข้าทีละ element, scroll-reveal (IntersectionObserver) สำหรับ cards/timeline, section-title underline grow, count-up stats
- ทุก animation respect `prefers-reduced-motion: reduce`

## ตำแหน่ง QR code ในไฟล์ PDF (สำคัญ — ผู้ใช้ปรับหลายรอบจนพอใจ)
ทำด้วย Python (reportlab วาด overlay → pypdf merge ทับหน้า). venv อยู่ที่ `/tmp/pdfenv`
- **Page size:** 595.92 × 842.88 pt (A4), origin มุมล่างซ้าย (reportlab/pdf coordinate)
- **ตำแหน่งสุดท้ายที่ผู้ใช้พอใจ** (บนขวา ใต้ชื่อ/contact เหนือเส้นแบ่ง section สีน้ำเงิน):
  - QR: `qr_x = 508`, `qr_y = 700`, `qr_size = 55` pt
  - Caption "Scan to full profile": Helvetica **6pt** สี navy `#09296A`, จัด center เหนือ QR (`text_y = qr_y + qr_size + 3`)
- เส้นแบ่ง section (divider สีน้ำเงิน) อยู่ที่ y ≈ 677.6 — **อย่าให้ rectangle สีขาวที่ใช้ลบ QR เก่าทับเส้นนี้** (เคยพลาดทำให้เส้นขาด ต้องวาดเส้นซ่อม `rect(226.5, 677.58, ...)`)
- caption ต้องเล็กและอยู่ชิด QR (ผู้ใช้ย้ำ)
- **note:** ไฟล์ `CV_2026.pdf` / `CV_2026_v2.pdf` ที่เคยทำใน Downloads ตอนนี้ไม่อยู่แล้ว; ไฟล์ CV ในโปรเจคคือ `cv/CV_ISARES_S.pdf`

## การแก้ชื่อ/ข้อความที่ผู้ใช้สั่ง
- "Isarez" → **"Isares"** Samruayruen (ทั้งไฟล์)
- "Technical Leader & Senior Software Developer" → **"Technical Lead Software Developer"**

## Preferences ของผู้ใช้
- ชอบดีไซน์ **minimal แต่ premium**, animation ไม่รบกวนสายตาในการอ่าน
- สื่อสารภาษาไทย
- ให้ push/deploy เมื่อสั่งเท่านั้น
