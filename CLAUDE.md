# Lower Back Recovery Workout App

## What This Is
A personal workout web app built for John to help recover from lumbar arthritis and bone spurs. Full gym access. Built in Cowork with Claude.

## Live URL
**https://lower-back-workout-production.up.railway.app**
(Works on iPhone, iPad, Mac, any device — bookmarked on iPhone home screen)

## Where the Files Live
- **This folder** (`/Users/john/Back Workout/`) — the source of truth going forward
- **GitHub**: https://github.com/jgarner31/lower-back-workout
- **Railway project**: https://railway.com/project/14a005eb-f3d1-49d7-aa42-a58efa98c8ac

## Files
- `index.html` — the entire workout app (self-contained, no dependencies)
- `CLAUDE.md` — this file (project context for future Claude sessions)

## How Deployment Works
Railway watches the GitHub repo. To update the live app:
1. Edit `index.html` in this folder (Claude can do this)
2. Upload the new `index.html` to GitHub at https://github.com/jgarner31/lower-back-workout
3. Railway auto-deploys in ~30 seconds

## The App Structure
Two tabs:
- **Workout tab**: 24 exercises total (exercise IDs 0–23) with checkboxes, instructions, tips, per-exercise weight tracking, and YouTube video links. Progress bar tracks the session and only counts exercises visible for that day's Workout A/B variant. Reset button clears checkboxes, advances the workout counter, and bumps weight streaks.
- **Schedule tab**: Mon/Wed/Fri weekly calendar, an A/B explainer card, and a single "Your Routine" info box (full 3-set routine every session, no phases).

### 6 Exercise Sections (as of 2026-07-06 redesign)
1. Warm-Up (4 staple + 1 rotating) — Stationary Bike, Cat-Cow, QL Ball Release, Deep Core Activation, + Rowing Machine (Workout A) / Ski Erg (Workout B)
2. Mobility & Stretching (3, unchanged) — Knee-to-Chest, Figure-4, Hip Flexor
3. Core & Stability — Machine-Based (3, unchanged from redesign) — Seated Ab Crunch Machine, Machine Back Extension, Pallof Press
4. Lower Body (2 staple + 2 rotating) — Leg Press, Seated Hamstring Curl, + Hip Abductor/Leg Extension (A) or Hip Adductor/Suitcase Carry (B)
5. Upper Body (2 staple + 1 rotating) — Lat Pulldown, Seated Cable Row, + Chest Press Machine (A) or Standing Single-Arm Cable Row (B)
6. Cool-Down (2, unchanged) — Seated Hamstring Stretch, Child's Pose

**Redesigned 2026-07-06**: Removed Bird Dog, Dead Bug, Glute Bridge, and Side Plank (floor/kneeling work aggravated John's knees; Side Plank also loaded his arthritic shoulder). Replaced with machine-based core work. Added Workout A/B rotation (derived from `workoutCount` parity — odd = A, even = B) so session length stays ~20 exercises while still cycling through more machine variety across the week. Added a "last weight used" input per strength exercise (`localStorage.weightData`, keyed by exercise id) with a streak counter that surfaces an "⬆️ Try adding weight" badge once the same weight has been logged 6 workouts in a row.

**Phases removed 2026-07-06**: John was 12+ days in and wanted to skip straight to the full routine. Removed the 4-phase progression system entirely (phase chip, phase blocks on the Schedule tab, phase-up modal, and all phase JS logic). The app now always runs the full 3-set A/B routine — no more Phase 1-4 unlocking. A one-time migration flag (`localStorage.phasesRemovedV1`) resets `workoutCount` to 1 the first time the updated app loads, so the A/B rotation restarts fresh at Workout 1/A instead of picking up mid-phase.

Workout days: Monday / Wednesday / Friday

## Future Ideas / Things to Add
(Add notes here as you think of them)
-

## Medical Context
- Lumbar arthritis and bone spurs (lower back)
- Shoulder arthritis — avoid overhead pressing/loading and floor planks that load the shoulder
- Knees bothered by floor/kneeling exercises — app avoids kneeling positions and all-fours work; offers standing/seated alternatives where a stretch traditionally requires kneeling
- Returning from ~6 months of inactivity
- Full gym equipment, free weights, rowing machine, and ski erg available
- Key rule: stop for sharp/shooting pain; mild stiffness is OK
