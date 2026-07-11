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
- **Workout tab**: 22 exercises total (exercise IDs 0–23, with 2 and 10 retired/unused — see MRI update below), checkboxes, instructions, tips, per-exercise weight tracking, and YouTube video links. Progress bar tracks the session and only counts exercises visible for that day's Workout A/B variant (18 per session as of the 2026-07-07 MRI update). Reset button clears checkboxes, advances the workout counter, and bumps weight streaks.
- **Schedule tab**: Mon/Wed/Fri weekly calendar, an A/B explainer card, and a single "Your Routine" info box (full 3-set routine every session, no phases).

### 6 Exercise Sections (as of 2026-07-10 PT update)
1. Warm-Up (4, all staple) — Stationary Bike, Cat Stretch, Deep Core Activation, Ski Erg
2. Mobility & Stretching (3) — Figure-4, Hip Flexor Stretch (Kneeling), Couch Stretch
3. Core & Stability (3) — Opposition Crunch, Pallof to Warrior Press, Dead Bug
4. Lower Body (3 staple + 2 rotating) — Leg Press, Seated Hamstring Curl, Glute Bridge, + Hip Abductor/Leg Extension (A) or Hip Adductor/Suitcase Carry (B)
5. Upper Body (1, rotating only — no staples) — Chest Press Machine (A) or Standing Single-Arm Cable Row (B)
6. Cool-Down (3) — Seated Hamstring Stretch, Somatic Forward Fold, 90/90 Decompression

**Redesigned 2026-07-06**: Removed Bird Dog, Dead Bug, Glute Bridge, and Side Plank (floor/kneeling work aggravated John's knees; Side Plank also loaded his arthritic shoulder). Replaced with machine-based core work. Added Workout A/B rotation (derived from `workoutCount` parity — odd = A, even = B) so session length stays ~20 exercises while still cycling through more machine variety across the week. Added a "last weight used" input per strength exercise (`localStorage.weightData`, keyed by exercise id) with a streak counter that surfaces an "⬆️ Try adding weight" badge once the same weight has been logged 6 workouts in a row.

**Phases removed 2026-07-06**: John was 12+ days in and wanted to skip straight to the full routine. Removed the 4-phase progression system entirely (phase chip, phase blocks on the Schedule tab, phase-up modal, and all phase JS logic). The app now always runs the full 3-set A/B routine — no more Phase 1-4 unlocking. A one-time migration flag (`localStorage.phasesRemovedV1`) resets `workoutCount` to 1 the first time the updated app loads, so the A/B rotation restarts fresh at Workout 1/A instead of picking up mid-phase.

**MRI-driven update 2026-07-07**: John shared his lumbar MRI findings — multilevel DDD worst at L3-L4/L4-L5, mild bilateral foraminal/canal narrowing at L4-L5 (right side crowding the right L5 nerve root, no confirmed contact), facet arthritis at L3-L4 and L5-S1, and a history of deep tissue massage triggering radiating leg pain and foot numbness (a nerve-irritation flag). Based on this, removed **QL Ball Release** (sustained direct pressure right next to the spine at the affected levels — too close to the same kind of stimulus that triggered nerve symptoms during massage) and **Machine Back Extension** (spinal extension narrows foramina and loads facet joints, both already compromised) from the routine — exercise IDs 2 and 10 are retired/unused in the code rather than renumbered, to preserve existing weight-tracking data for the remaining exercises. Kept **Seated Ab Crunch Machine** since John already uses light weight and partial range of motion. Also updated the workout tab's warning note to say to stop for radiating leg pain, tingling, or numbness (not just sharp/shooting pain), since that's the specific red flag from his MRI/symptom history. John has not yet run these changes by his doctor/PT — worth flagging if this comes up again.

**Decompression addition 2026-07-07**: John asked about spinal decompression since compression (walking, stairs) is his main pain trigger. Added **90/90 Decompression** (exercise ID 24) to Cool-Down: lying on back with calves on a chair/bench, hips/knees at 90°, 5-10 min. Chosen over an inversion table because inversion increases lumbar lordosis (extension), which narrows the same foramina/facet joints already compromised in his MRI — the 90/90 position unloads the discs via flexion instead, with no shoulder or knee involvement. Also discussed his Chirp Halo TENS/EMS device for muscle guarding: recommended the device's "Pain Relief" preset (mixed TENS+EMS, 20 min) placed via the lower back pad, since pure TENS (via endorphin release) is what interrupts the guarding/spasm cycle, while EMS adds blood flow. Advised against placing it directly over the most symptomatic right-sided L4-L5 area at high intensity given his nerve sensitivity.

**Cat-Cow modified, Glute Bridge restored 2026-07-10**: John reported the Cow (extension) half of Cat-Cow reproduces his pain — consistent with the facet arthritis/foraminal narrowing already driving the QL Ball Release and Back Extension removals. Renamed the exercise to **Cat Stretch** (exercise ID 1, unchanged) and rewrote the instructions to stop at neutral spine instead of arching into extension. Also restored **Glute Bridge** (new exercise ID 25) into Lower Body as a staple every session, per John's request — cued to lift only to a straight shoulders-to-knees line and avoid arching the lower back at the top, for the same extension-avoidance reason as the Cat Stretch change.

**PT-directed update 2026-07-10**: John saw his PT, who evaluated his range of motion in person and directed removing 6 exercises: Rowing Machine, Knee-to-Chest Stretch, Seated Ab Crunch Machine, Lat Pulldown, Seated Cable Row, and Child's Pose (exercise IDs 4, 6, 9, 18, 19, 23 — all retired/unused, not renumbered). John supplied 5 replacement exercises from two Fitness 4 Back Pain YouTube videos: Pallof to Warrior Press, Opposition Crunch, Somatic Forward Fold, Couch Stretch, and Dead Bug. Placement logic:
- **Pallof to Warrior Press** (id 11, same slot as the old Pallof Press) — upgraded in place rather than added as a duplicate, since it's a direct progression of the existing exercise (adds an overhead reach after the standard press-out).
- **Opposition Crunch** (id 26) and **Dead Bug** (id 27) — added to Core & Stability, covering the ab/coordination stimulus lost when Ab Crunch Machine was removed.
- **Couch Stretch** (id 28) — added to Mobility & Stretching in the Knee-to-Chest slot (deeper hip flexor stretch, PT's pick over the existing standard Hip Flexor Stretch which stays too).
- **Somatic Forward Fold** (id 29) — added to Cool-Down in the Child's Pose slot (posterior chain release, better suited post-workout when muscles are warm).
- **Ski Erg** (id 5) — promoted from a Workout-B-only rotator to an every-session staple, since Rowing Machine (its Workout-A counterpart) was removed and warm-up needed to stay a consistent length. Its `data-variant` was removed.

**Known gap to flag**: Removing both Lat Pulldown and Seated Cable Row leaves Upper Body with zero staple exercises — it's now just one alternating machine per session (Chest Press on A, Standing Single-Arm Cable Row on B). None of the 5 PT-supplied exercises replace upper-body pulling volume. Worth asking John's PT whether that's intentional or whether more upper-body work should be added back once his ROM improves.

I could not independently verify the exact 2 YouTube videos John watched (Claude in Chrome wasn't connected in this session), so the exercise instructions above are built from Fitness 4 Back Pain's published site content for Opposition Crunch and their general Pallof Press / Dead Bug material, plus standard technique sources for Couch Stretch and Somatic Forward Fold. Video links in the app use search queries rather than direct video IDs (consistent with every other exercise in the app) so John can confirm against the actual PT-referenced video.

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
