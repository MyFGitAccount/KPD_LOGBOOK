Here is the **complete checklist** of everything you must include to make your logbook **perfect and complete** (exactly what an examiner or future developer would expect for full marks / full reproducibility).

### 1. Project Identification & Metadata
- Project title (EFS + Timetable Planner)
- Your name / student ID / group members
- Course code & semester (e.g., HD101 / 2025–26 S1)
- Final submission date
- GitHub / repo link (if any)
- Current version of the logbook

### 2. Real-Life Problem Definition (must be crystal clear)
- Exact pain point during add/drop period at HKU SPACE
- Why the official PDF timetable is unusable for planning
- How students currently waste 3–10 hours manually planning
- Target users: HKU SPACE CC / Po Leung Kuk Stanley Ho students

### 3. Evolution of Project Scope
- Initial idea → final delivered features
- List every feature that exists now:
  - Timetable planner (drag-and-drop + PNG export)
  - Login / account creation with student card verification
  - Admin panel (course + account approval)
  - Course viewer with materials, mock exercise, timetable
  - EIS PDF Analyzer with OpenAI fallback
  - Forum redirect page
  - Calendar page (credits system placeholder)

### 4. Tech Stack Decision & Justification (vs alternatives)
| Stack          | Why chosen                                      | Why NOT Rust / Go / Python+Django / PHP / Next.js etc. |
|----------------|--------------------------------------------------|---------------------------------------------------------|
| MERN (Node + Express + MongoDB + Vanilla JS) | Full JS, rapid prototyping, Mongo flexibility | Rust/Go overkill, Python slower async, PHP outdated   |

### 5. Development Environment Setup Instructions (100% reproducible)
- Node version
- MongoDB (local vs Atlas)
- Python + PyMuPDF version
- .env example
- npm install / pip install commands
- How to run server.js
- How to regenerate courses.js from PDF
- Vercel deployment notes

### 6. Potential Risks & Real Issues Encountered (you MUST list these)
| Issue                                      | Impact                          | Mitigation / Fix Applied                                 |
|--------------------------------------------|---------------------------------|-----------------------------------------------------------|
| courses.js ~3702 lines → slow load         | High on mobile                  | Debounced search, lazy loading, minification               |
| Vercel serverless cannot write files        | courses.js regeneration fails    | Keep courses.js in repo or move to DB                      |
| MongoDB connection timeout / URI wrong      | App completely down              | Cached connection + error page                                     |
| SMTP / Brevo email delivery failure         | Account approval emails lost    | Fallback to console + manual approval                             |
| Large PDF crashes browser in EIS viewer     | UX failure                       | Client-side chunking + progress bar                                |
| Duplicate student IDs / pending accounts    | Security risk                   | /accounts/check endpoint + DB constraints                          |
| html2canvas fails on huge calendar         | Export broken                   | Force fixed width + scale=2 workaround                             |

### 7. Data Extraction Pipeline (PDF → courses.js)
- Why Python + how the 3 Python scripts work (ext.py → ext2_1.py → merge.py)
- Why weekday extraction had to be split into a separate script
- How you verified 100% accuracy against the original PDF

### 8. Major Architectural Decisions & Trade-offs
| Decision                                 | Chosen Option                  | Rejected Alternative               | Rationale & Trade-off                                        |
|------------------------------------------|--------------------------------|-----------------------------------|-------------------------------------------------------------|
| Static courses.js vs MongoDB collection    | Static file                    | DB collection                      | Speed vs real-time updates                                   |
| Vanilla HTML/JS vs React/Vue             | Vanilla                        | React                             | Faster dev, smaller bundle, no build step                    |
| Client-side PDF processing vs server       | Client-side (PDF.js)           | Server (PyMuPDF)                  | No server cost, works offline, privacy                       |
| FullCalendar v6 vs custom grid            | FullCalendar                    | Custom CSS grid                    | Drag-and-drop out-of-the-box, worth the 200 KB              |
| File-based auth vs JWT + sessions         | Simple in-memory / DB check     | JWT                               | Simpler for prototype, sufficient for low traffic              |

### 9. Feature-by-Feature Technical Breakdown
For every major file, write 2–3 lines:
- eis-viewer.html → purpose, PDF.js + OpenAI flow, heuristic fallback
- calendar.html / calendar.js → FullCalendar setup, draggable, conflict detection, export logic
- server.js → all important routes with purpose (/auth/login, /course/:code, /admin/…)
- admin.html → photo full-URL fix explanation
- account-create.html → duplicate SID check + preview
- Mainpage.html → course code validation flow

### 10. Testing & Validation Performed
- Tested with real 2025–26 timetable PDF
- Tested account creation → approval → login flow
- Tested timetable export on mobile & desktop
- Tested with 10+ overlapping classes (conflict detection works)
- Tested EIS with 50-page PDF (no crash)

### 11. Future Improvements / Known Limitations
- Move courses.js → MongoDB collection + API endpoint
- Add real-time conflict highlighting (red background)
- Add “save timetable” with localStorage or user account
- Mobile-responsive improvements
- Dark mode toggle
- Unit tests / CI pipeline

### 12. References & Credits
- FullCalendar docs
- PDF.js GitHub
- Brevo SDK
- PyMuPDF docs
- Original PDF source: HKU SPACE master timetable PDF

Just fill in the above 12 sections in order and your logbook will be **bulletproof** and extremely professional. You can copy-paste this checklist directly into your logbook as a table of contents. Good luck — you’re almost done!
