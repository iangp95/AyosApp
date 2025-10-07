# AYOS App — Home Maintenance Marketplace (School Project)

**Lead / Contact:** Rahardian Gusta Patria (rahardiangusta@gmail.com)  
**Tools:** Figma (UI/UX) · Python (prototype/algorithms) · Excel (data) · Google Maps API (proximity)  

---

## 📘 Project Overview
**AYOS** connects homeowners with reliable, vetted service providers in a few taps.  
The app solves three core problems: unreliable contractors, time-consuming search processes, and opaque pricing. AYOS offers pre-screened providers, transparent pricing, secure payments, and a scoring-based matching system so users can confidently “say AYOS” — it’s fixed and it’s good. :contentReference[oaicite:1]{index=1}

---

## 🎯 Objectives
- Build a minimal viable workflow that allows a homeowner to request a job, receive ranked provider matches, book a provider, and rate the outcome.  
- Demonstrate a relevance-scoring algorithm that ranks providers by **budget fit, distance, and rating**.  
- Produce UI/UX mockups, a short prototype, and a technical appendix describing data requirements and revenue mechanics. :contentReference[oaicite:2]{index=2}

---

## 🧩 Key Features (Product Requirements)
- **User flows:** Search services, select date/time, view providers, chat/coordinate, book & pay.  
- **Provider verification:** ID, certifications (TESDA), past work, insurance flag.  
- **Relevance scoring & ranking** (see Algorithm section).  
- **Budget slider & pricing transparency** (show price vs budget).  
- **Map integration** — show providers near user; proximity-based filtering.  
- **Bookings dashboard** — user and provider views.  
- **Ratings & reviews** — feed into provider score and visibility. :contentReference[oaicite:3]{index=3}

---

## 🧠 Algorithm (Total Score) — core matching logic
Total_Score = Wb * Budget_score + Wd * Distance_score + Ws * Rating_score

### Budget_score
    if Price > Budget:
        Budget_score = -1.0    # strong penalty for out-of-budget providers
    else:
        Budget_score = (Budget - Price) / Budget   # normalized 0..1 scale

### Distance_score
    Distance_score = 0                      if Distance_km > MAX_DISTANCE_KM
                   = 1 - (Distance_km / MAX_DISTANCE_KM) otherwise
    (Default: MAX_DISTANCE_KM = 10 km)

### Rating_score
    Rating_score = Rating / 5.0   # normalized 0..1 scale (rating is 0–5)

### Weights (example)
    Wb (Budget)    = 0.40
    Wd (Distance)  = 0.30
    Ws (Rating)    = 0.30

### Example Calculation
User budget = 100  
Provider price = 80 → Budget_score = 0.20  
Distance = 2 km → Distance_score = 0.8  
Rating = 4.2 → Rating_score = 0.84  

Total_Score = 0.4*0.20 + 0.3*0.8 + 0.3*0.84 = **0.572**

Higher score = better match.

---

## 📊 KPIs & Target Outcomes (for the dashboard / prototype)

**Page 1 — Financial / Market View**
- Total bookings per month  
- Average price per job vs median budget  
- Provider revenue share & platform take rate  
- Planned vs realized revenue trends (monthly/quarterly)

**Page 2 — Operations / Execution View**
- Match success rate (accepted bookings / offers)  
- Average time-to-fulfill (hours)  
- Provider verification rate (verified / total)  
- NPS / average rating per provider category  

These KPIs align with AYOS’s business model — tracking both user adoption and provider performance.

---

## 🏗️ Tech Stack & Implementation Notes
- **Prototype:** Figma static screens + Python prototype for matching simulation.  
- **Algorithm & prototype code:** Python scripts / Jupyter notebooks to compute relevance scores and visualize matches.  
- **Data:** CSVs for demo (providers + requests). Production version uses PostgreSQL or SQLite.  
- **APIs:** Google Maps API for distance; optional payment gateway mock for checkout.  

---

## 📁 Contact

📝 Notes for Reviewers
- The repository includes sanitized demo data and a single-command runnable prototype.
- Add screenshots in /ui/ and a short GIF demo for better presentation.
- Include the final documentation PDF in /docs/ for academic submission.
