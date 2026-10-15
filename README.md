# 🎓 AlphabetAI Attendance

> **Intelligent, Deterministic, & Secure Full-Stack Attendance Management System**  
> Built with **React 19**, **TypeScript**, **Tailwind CSS v4**, and **Supabase (PostgreSQL & RLS)**.

---

## 🌟 Key Features

### 1. 🔤 Alphabetical-First Deterministic Roster
- **Default Ordering**: Students are displayed strictly alphabetically by **First Name (A → Z)** by default.
- **Dynamic Sorting Options**: Switch seamlessly between First Name, Last Name, and Roll Number with ascending/descending order.
- **Architectural Safety Guarantee**: Attendance records are linked directly to unique **Student UUIDs** (`student_id`), **never** row array indices. Re-sorting, searching, or filtering will *never* misalign or shuffle attendance marks.

### 2. 👥 Role-Based Access Control (RBAC)
- **Teacher Mode**:
  - Live attendance marking: **Present**, **Absent**, **Late**, **Excused**.
  - Quick action helpers: *Mark All Present*, *Mark All Absent*, *Fill Unmarked*, *Reset*.
  - Real-time counters showing Total Roster, Present, Absent, Late, Excused, and percentage compliance.
  - Save as **Draft** or **Finalize Session** (with celebratory confetti).
  - Export attendance reports in downloadable **CSV** and **PDF** formats.
  - Interactive **AI Insights** & Guardian Alert generator.
  - Optional **Face AI Attendance** with physical teacher verification.
- **Admin Mode**:
  - Full institutional authority over Classes, Sections, and Curricular Subjects.
  - Add, edit, and delete student records.
  - Bulk import student rosters via **CSV** or **Microsoft Excel (.xlsx)** with sample templates.
  - View full tamper-evident **Audit Logs** with modification reasons and timestamps.

### 3. 🧠 Explainable AI Insights & Absenteeism Watchlist
- **Chronic Absenteeism Detector**: Automatically flags students whose unexcused absence rate exceeds standard institutional risk benchmarks (≥ 15%).
- **Weekly Trend Detector**: Identifies day-of-week attendance drops (e.g. Friday/Monday patterns).
- **Streak & Deterioration Warnings**: Highlights consecutive absence clusters.
- **AI Guardian Notice Drafter**: Generates personalized, professional formal letters for guardians with 1-click clipboard copy.
- **100% Explainable & Factual**: Insights are calculated deterministically from recorded sessions with transparent mathematical thresholds.

### 4. 📷 Optional Face Recognition (Privacy-First)
- **Disabled by default**.
- **Consent-Gated**: Requires explicit student/parent biometric consent flag (`biometric_consent: true`). Students without consent are marked *"Manual Only"* and protected.
- **Teacher Verification Required**: Matches trigger a verification prompt requiring the teacher to confirm the physical match before recording attendance.
- **Manual Fallback**: Manual attendance marking is always instantly accessible.

### 5. 🗄️ Supabase PostgreSQL Backend & RLS
- Complete database schema provided in `supabase/schema.sql`.
- Configured with Row Level Security (RLS) policies protecting classes, students, sessions, records, and audit logs.
- Prevents duplicate attendance marks with `UNIQUE(session_id, student_id)`.
- **Dual-Mode Offline/Online Support**: Runs immediately out of the box with realistic mock data in LocalStorage, and connects seamlessly to your live Supabase database when credentials are added.

---

## 🚀 Quickstart Guide

### 1. Install Dependencies
```bash
npm install
```

### 2. Start Development Server
```bash
npm run dev
```
Open your browser to `http://localhost:5173`.

### 3. Build for Production
```bash
npm run build
```

---

## ⚙️ Connecting to Supabase (Optional)

1. Go to [database.new](https://database.new) and create a free Supabase project.
2. In the Supabase dashboard, open the **SQL Editor**.
3. Copy the entire contents of [`supabase/schema.sql`](./supabase/schema.sql) and click **Run**.
4. In your project root, create a `.env` file (copy from `.env.example`):
   ```env
   VITE_SUPABASE_URL=https://your-project-id.supabase.co
   VITE_SUPABASE_ANON_KEY=your-supabase-anon-key
   ```
5. Restart Vite (`npm run dev`). The status badge in the top navigation will automatically switch to **"Supabase Live"**!

---

## 📊 Sample Roster Import Format

Download the sample templates directly inside the app, or format your CSV / Excel as:

```csv
roll_number,first_name,last_name,email,gender,guardian_name,guardian_email,guardian_phone,biometric_consent
R-201,Alexander,Hamilton,a.hamilton@student.alphabetai.edu,Male,James Hamilton,james.h@gmail.com,+1 (555) 987-6543,yes
R-202,Chloe,Bennet,chloe.b@student.alphabetai.edu,Female,Mary Bennet,mary.b@gmail.com,+1 (555) 876-5432,yes
R-203,Daniel,Craig,d.craig@student.alphabetai.edu,Male,Olivia Craig,olivia.c@gmail.com,+1 (555) 765-4321,no
```

---

## 🔒 Security & Audit Compliance
- Any modification to an already finalized session prompts the teacher or admin for a mandatory justification note.
- All modifications are permanently recorded in the institutional **Audit Trail** with timestamp, authorized user ID, previous status, and justification reason.
