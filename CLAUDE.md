# CLAUDE.md — Isares Samruayruen Portfolio

> สรุปงานที่ทำในโปรเจคนี้ เพื่อให้ session ใหม่เข้าใจ context ได้ทันที

## ⚠️ กฎสำคัญ
- **ต้องขออนุญาตจากผู้ใช้ก่อนเสมอ** ก่อน push code ขึ้น GitHub — ห้าม push เองโดยไม่ได้รับอนุญาต (commit ในเครื่องทำได้เมื่อจำเป็น แต่ push ต้องถามก่อน)
- สื่อสารกับผู้ใช้เป็นภาษาไทย

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
├── index.html                    # ทั้งเว็บ
├── images/
│   ├── img.jpg                   # รูปโปรไฟล์ (ใช้ใน hero avatar)
│   ├── portfolio-qr.png          # QR code ชี้ไป live URL (ใช้ฝัง CV ไม่ใช่ในหน้าเว็บ)
│   ├── favicon.svg                # favicon หลัก (vector, glassmorphism + ตัว "i" gradient ฟ้า→ม่วง ไม่มีพื้น navy)
│   ├── favicon-32.png / favicon.png / apple-touch-icon.png  # fallback raster ของ favicon (สร้างด้วย rsvg-convert)
└── cv/
    └── CV_ISARES_S.pdf           # CV ดาวน์โหลดได้จากปุ่มใน hero
```
- favicon source ทำเป็น SVG (`images/favicon.svg`) แก้ตรงนั้นแล้ว re-export PNG ด้วย `rsvg-convert -w <size> -h <size> favicon.svg -o <out>.png` (ติดตั้งผ่าน `brew install librsvg`)
- **ข้อควรระวัง SVG gradient:** ต้องใส่ `gradientUnits="userSpaceOnUse"` ถ้าใช้ค่า x1/y1/x2/y2 เป็นพิกัดจริง (ไม่ใส่จะตีความเป็น fraction ของ bounding box ทำให้ไล่สีเพี้ยน/จืด — เคยเจอปัญหานี้มาแล้ว)

## ลำดับ section ในหน้าเว็บ (บนลงล่าง)
1. Hero/About (`#about`) — มีรูป + ปุ่ม Get In Touch / View Experience / **Download CV** + ลิงก์ **LinkedIn** เล็กๆใต้ปุ่ม (ไม่เด่น, `linkedin.com/in/isares-s`)
2. Quick Stats (`.stats` section แยก: 13+, 4+, 100%, **50+ Technologies** — มี count-up animation ทุกอัน เปลี่ยนจาก "Agile" เดิมแล้ว)
3. Education (`#education`) — มี icon (graduation cap, SVG sprite) + ปีจบ/GPA: MSIT 2016 GPA 3.95, BSc CS 2012 GPA 2.57
4. Experience (`#experience`)
5. Skills (`#skills`) — ตอนนี้มี **5 กล่อง** (ดูด้านล่าง)
6. Projects (`#projects`)
7. Contact (`#contact`) — อยู่ล่างสุดก่อน footer, มี 4 การ์ด: Email, Phone, **LINE ID (noom.isarez)**, Location — เรียง grid 4 คอลัมน์เท่ากัน
- Navbar order: About → Education → Experience → Skills → Projects → Contact (มี scroll-spy highlight + underline animation)
- Footer: มี SVG robot icon ด้านบน + "Powered by Claude" (มี sparkle icon หน้าคำว่า Claude แทนโลโก้จริง เพราะไม่ใช้โลโก้ trademark ของ Anthropic)

## เนื้อหา Experience (สำคัญ — เคยเรียบเรียงใหม่เป็นภาษาอังกฤษ)
- **Thai Credit Bank** (Technical Leader, Mar 2020–Present): กล่องเดียว แยก 3 subtitle — **eKYC Platform**, **NDID Platform**, **OCR Service**
- **Saitech Solution (TRUE Corp.)** (Senior Software Developer): OMX Mobile Backend (TIBCO/Java) + Webtool Application (ReactJS/Spring Boot/Oracle/Elasticsearch/JMS)
- **PSP (Thailand) / Bank of Ayudhya** (Software Developer): DMS Data Correction + File Management + Dataset Dashboard (AngularJS/Spring Boot/MSSQL/iReport)
- **Pro Technical Info Service**: กล่องเดียว แยก 2 subtitle — Software Developer (Oct 2012–May 2015, TOT Wi-Fi + NACC) และ Freelance (Jun 2015–Feb 2016, TOT Wi-Fi maintenance)
- Featured Focus Projects: 6 การ์ด อ้างอิงตาม experience

## Skills section (อัปเดต — แยก AWS ออกมาแล้ว)
5 กล่อง: **Leadership & Architecture**, **Backend Engineering** (เอา "AES/GCM Encryption" ออกแล้ว), **Frontend & Integration**, **DevOps & Databases** (Docker/Kubernetes/databases), **Cloud Services** (AWS badge ทั้งหมด 13 ตัว แยกมาจากกล่องเดิม — กล่องนี้ตั้ง `grid-column: 1 / -1` ให้กว้างเต็มแถวเพราะมี badge เยอะ)

## Icon system (สำคัญ — เปลี่ยนจาก emoji เป็น SVG sprite ทั้งหมด)
- มี `<svg style="display:none">` sprite อยู่ต้น `<body>` เก็บ `<symbol>` ของไอคอนทั้งหมด (icon-flag, icon-server, icon-code, icon-database, icon-cloud, icon-mail, icon-phone, icon-chat, icon-pin, icon-cap, icon-id, icon-link, icon-scan, icon-activity, icon-shield, icon-wifi)
- เรียกใช้ด้วย `<svg class="icon-svg"><use href="#icon-xxx"/></svg>` — ใช้กับ: skills category title, contact card, education card, project card
- สไตล์ icon: line-icon สีเดียว (`var(--color-primary)`) ใส่ในกล่องพื้นหลังวงกลม/สี่เหลี่ยมมุมโค้งจาง (`rgba(56,189,248,0.12)`) ตอน hover การ์ดจะเปลี่ยนพื้น icon เป็น gradient เต็ม + ตัว icon เป็นสีขาว
- ห้ามใช้ emoji อีก — ผู้ใช้สั่งให้เอา emoji ออกให้หมดและทำเป็น SVG ธีมเดียวกันแทน

## Experience Timeline (สำคัญ — เคยปรับหลายรอบ)
- เส้นซ้ายของ `.timeline` ไม่ใช้ bullet/circle marker ธรรมดาแล้ว — แต่ละ `.timeline-item` มี `data-year` attribute (เช่น `data-year="2020-Present"`, `"2018"`, `"2016"`, `"2012"`) แสดงผลผ่าน CSS `content: attr(data-year)` บน `::before`
- ป้ายปีเป็น **auto-width pill** (ไม่ fix width) ใช้ `left: 43px; transform: translateX(-50%)` (เลขต้องตรงกับ `left` ของเส้น `.timeline::before`/`::after`) ให้อยู่กึ่งกลางเส้นเสมอไม่ว่าข้อความจะยาวแค่ไหน — ตอน hover ต้องคง `translateX(-50%)` ไว้คู่กับ `scale()` ไม่งั้นป้ายจะเด้งหลุดจากกึ่งกลาง
- สีป้าย: gradient เข้ม `linear-gradient(135deg, var(--bg-card) 0%, #1e2942 45%, #2d2470 100%)` (จับคู่จากพื้นหลังกล่อง experience ไม่ใช่ accent สีสว่าง) + ขอบฟ้าจาง `rgba(56,189,248,0.4)` กัน sink หายไปกับพื้นหลังหน้าเว็บที่เข้มใกล้เคียงกัน
- **ไม่มี** pulsing glow ring ที่ป้ายแล้ว (ผู้ใช้สั่งเอาออก) — มีแค่ hover scale + shadow เข้มขึ้น
- เส้น timeline มี 2 ชั้น: เส้น track จางไล่หายปลายเส้น (`::before`) + เส้นแสงไหลลงเรื่อยๆ (`::after`, `timelineFlow` animation) ที่ตอนนี้ทำให้จางลงแล้ว (`opacity: 0.35`)
- **บั๊กที่เคยเจอ:** `::after` ของ parent element ถูก paint เป็นลูกตัวสุดท้ายตามสเปก CSS เลยทับอยู่หน้า `.timeline-item` (ลูกจริง) ที่มาก่อนหน้ามันใน DOM — แก้ด้วยการเพิ่ม `z-index: 1` ให้ `.timeline-item` (ต้องมี `position: relative` ด้วย) จะจำสิ่งนี้ไว้เผื่อเจอปัญหา stacking ลักษณะนี้อีกที่อื่นในเว็บ

## Animations / effects ที่ทำไว้ (อยู่ใน `<style>` และ `<script>` ท้ายไฟล์)
- **Particle background** — `<canvas id="particles">` วาด particle ลอย + เส้นเชื่อม (constellation), ปรับจำนวนตามขนาดจอ (แทนที่ bgSheen เดิมที่เคยลองแล้วเปลี่ยนมาเป็น particle ตามที่ผู้ใช้ขอ)
- **Avatar glow** — conic-gradient ring หมุน (`avatarSpin` 9s) + pulsing halo (`avatarPulse`) + glow pulse หลังรูป (ปรับให้เข้มขึ้นรอบล่าสุดตามที่ผู้ใช้ขอ "ทำให้เด่นขึ้น")
- Hero fade-up เข้าทีละ element (รวมถึง social-row ลิงก์ LinkedIn), scroll-reveal (IntersectionObserver) สำหรับ cards/timeline, section-title underline grow, count-up stats
- ทุก animation respect `prefers-reduced-motion: reduce`

## SEO / Meta tags
- `<title>` แก้ให้ตรงกับ hero แล้ว: "Isares Samruayruen | Technical Lead Software Developer"
- มี `<meta name="description">`, Open Graph (`og:title/description/image/url`), Twitter card tags ครบแล้ว (ใช้ `images/img.jpg` เป็น share image, URL อ้างอิง `https://isarez.github.io/portfolio/`)

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

## รีวิวหน้าเว็บ — สิ่งที่ผู้ใช้ "ปฏิเสธ/ยังไม่ต้องทำ" แล้ว (อย่าเสนอซ้ำโดยไม่ถูกถาม)
หลังรีวิวหน้าเว็บรอบหนึ่ง มีข้อเสนอที่ผู้ใช้บอกว่ายังไม่ต้องทำ:
- ไม่ต้องเพิ่ม Certifications section
- ไม่ต้องเพิ่มลิงก์/ปุ่มในการ์ด Featured Projects (งานเป็นข้อมูลองค์กรการเงิน confidential)
- favicon เป็นเรื่องที่ตกลงทำแยกทีหลัง (ทำเสร็จแล้วในรอบถัดมา — ดูหัวข้อโครงสร้างไฟล์)

## Preferences ของผู้ใช้
- ชอบดีไซน์ **minimal แต่ premium**, animation ไม่รบกวนสายตาในการอ่าน
- ไม่ชอบใช้ emoji ในหน้าเว็บ — ให้ทำเป็น SVG icon ที่เข้าธีมสีเสมอ
- สื่อสารภาษาไทย
- ให้ push/deploy เมื่อสั่งเท่านั้น
- เวลาทำ favicon/logo: ลอง design ใหม่ได้เรื่อยๆถ้าผู้ใช้บอกว่า "ยังไม่สวย" — ไม่ต้องยึดติด concept เดิม (เคยเปลี่ยนจากตัวอักษร IS → glassmorphism → spark/compass mark → ตัวอักษร "i" ก่อนจะลงตัว)
