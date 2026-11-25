# Ren session flow: spec v1 (draft for review)

This is the plan for how a training session with Ren should feel and behave, step by step. Once you've reviewed it, the app gets rebuilt to follow it. Anything marked **Decision** needs your call (they're collected at the end).

---

## 1. Design rules

These come from what the athlete is physically doing, and every state below follows them.

1. **Hands are busy, eyes are elsewhere.** The bell is in your hands and the phone is 2 to 3 metres away. During a set, voice is the main channel. The screen is a backup, readable from 3 m: big rep count, one short line of text.
2. **No taps during a set.** Starting, pausing, resuming and finishing work by body position or voice. Taps stay as a fallback, never as the only way.
3. **One voice, one thing at a time.** Ren never talks over himself and says at most one thing per rep. Long talk only happens when the bell is down.
4. **Brief, do, one cue, watch, react.** A real coach's rhythm. One fault at a time, wait to see if the cue worked, praise it when it does.
5. **Pause, don't punish.** Form breaking down means stop and fix, then carry on. The set isn't failed.
6. **Never rushed.** Rest starts after Ren stops talking. The next thing waits until you're in position. Silence is fine.
7. **Works offline mid-set.** Rep counting, cues, pauses and timers all run on the phone. The AI only speaks when the bell is down, and falls back to fixed lines if the network is slow.

---

## 2. Session arc

```
Check-in → Set-up → Warm-up → ┌─ Brief → Ready → Countdown → Working ─┐ → Cool-down → Debrief
                               │            ↑          (cue/watch loop)   │
                               │            └── Paused ←──────────────────┤
                               └─ Rest ← Set review ←─────────────────────┘
                                   (next set, or next exercise's Brief)
```

---

## 3. States

For each state: what Ren says, what the screen shows, what the camera watches for, and how you leave it.

### 3.1 Check-in (home screen)
- **Ren:** greets you and refers to your notes or last session. If you've told him your training days, he says so; otherwise he doesn't invent one. He proposes today's plan.
- **Screen:** chat plus today's plan. You can type, or hold the mic, to change the plan ("my back's tight, go light").
- **Leave:** tap **Start session** → Set-up.

### 3.2 Set-up (framing)
- **Ren:** "Prop the phone side-on, two to three metres away, whole body in view. I'll tell you when I can see you."
- **Screen:** live camera with a framing guide: a body outline the person should fill, and a status chip ("Step back", "Turn side-on", "Got you").
- **Camera:** whole body in the picture, side-on, steady for 2 s.
- **Leave:** framing good → Ren: "Got you." → Warm-up (or Brief if warm-up is skipped).
- **If it takes long:** after 20 s Ren gives one specific hint ("I can't see your feet, tilt the phone down"). He doesn't nag.

### 3.3 Warm-up (about 2 minutes, skippable)
- **Content:** 5 slow hip hinges without the bell, then 5 light swings.
- **Coaching:** reps are watched and cues are given, but nothing pauses and nothing is scored. Ren uses this to spot today's likely fault.
- **Leave:** done → Brief for the first exercise. "Skip warm-up" by voice or tap.
- **Decision 1:** warm-up every session, or only for the first few?

### 3.4 Brief (before each exercise, and before each set in short form)
- **Ren (first set of an exercise, AI line, bell down):** what the exercise is and the one thing to focus on, based on notes and the warm-up. Under 30 words.
- **Ren (later sets, fixed line):** "Set 2. Focus: arms loose, hips drive."
- **Screen:** exercise name, "Set 2 of 3 · 10 reps · 12 kg", the focus cue.
- **Leave:** Ren finishes → Ready.

### 3.5 Ready (hands-free start)
- **Camera:** you're in frame, side-on, and standing still for 2 s (that's the signal "I'm set").
- **Ren:** "Counting you in."
- **Voice:** "wait" holds it, "go" starts immediately. Tap **Start** as a fallback.
- **Leave:** → Countdown.
- **Decision 2:** auto-start when you stand still, or always wait for "go" or a tap?

### 3.6 Countdown
- **Ren:** "Three. Two. One. Hike and swing." One second each.
- **Screen:** big numbers.
- **Leave:** → Working.

### 3.7 Working (the set)
- **Camera:** counts reps and checks each rep for faults (section 5).
- **Ren:** follows the coaching loop (section 5) and the speech rules (section 4). Clean reps get the count, quietly.
- **Screen:** big rep count, one status chip ("Clean", "Better", "Fix: arms loose").
- **Leave:**
  - Target reached → "Ten. Park it." → Set review.
  - Fault survives two cues → Paused.
  - No rep for 8 s and you're standing still (bell parked) → "Set's done." → Set review.
  - Voice "pause" → Paused (no fault given). Voice "stop" → Set review.
  - Lost tracking → see section 6.

### 3.8 Paused
- **Ren:** "Pause there. Park the bell." Then, from the AI, what he saw and one thing to try without the bell (for example five slow hip hinges). Under 50 words.
- **Screen:** "Paused" with the fault and a short written fix. It appears straight away, before the AI line arrives.
- **Leave:**
  - You're back in position and still for 2 s, after Ren finishes → "Ready when you are" → Countdown, with reps kept.
  - Voice "go", or tap **Resume set**.
  - Voice "end set", or tap **End this set** → Set review.
- **Second pause in the same set for the same fault:** Ren offers to end the set and suggests a drill or a lighter bell next time. He doesn't push on.
- **Decision 3:** two pauses per set, then offer to end it. Is that right?

### 3.9 Set review (bell down)
- **Ren (AI):** one specific observation using the numbers, whether a fix held, and the focus for the next set. Under 45 words.
- **Screen:** "8 clean of 10" and the focus for next set.
- **Leave:** Ren finishes → Rest. After the last set of the last exercise → Cool-down.

### 3.10 Rest
- **Timer:** starts once Ren finishes talking. He says "Ten seconds" at 10 s.
- **At zero:** "Rest's up." → Brief (short form) → Ready. Nothing starts until you're in position.
- **If you're not back after 30 s extra:** one gentle "Whenever you're ready." Then quiet.
- **Voice or tap:** "skip" ends rest early. "Repeat" repeats Ren's last line.

### 3.11 Cool-down and debrief
- **Ren:** "That's the session. Park the bell." Then the AI debrief: the best thing, the one thing to fix, and when to train next (he asks you if he doesn't know your schedule).
- **Screen:** back to home chat, so you can answer ("Saturday works").
- **Ren's notes** are updated with facts only. Your answer about the next day becomes a commitment only once you've said it.

---

## 4. Speech rules

**One queue, with priorities.** A higher priority may cut off a lower one. Equal or lower priorities wait or are dropped:

| Priority | What | Can cut off | If Ren is busy |
|---|---|---|---|
| 0 Safety | "Stop. Put the bell down." (pain, lost control) | everything | speaks now |
| 1 Control | countdown, "Pause there", "Park it" | 2 to 4 | speaks now |
| 2 Cue | "Arms loose, hips drive" | 3 to 4 | waits up to 1 rep, then dropped and retried next rep |
| 3 Praise | "Better. That's it." | 4 | dropped |
| 4 Count | "Six" | nothing | dropped |

- **One line per rep at most.** Cues are 6 words or fewer during a set.
- **Timing:** the rep is detected at the top of the swing, which is the right moment to speak. Nothing is said in the middle of a hinge.
- **AI lines only when the bell is down:** Brief, Paused, Set review, Debrief.
- **Fallback lines:** if the AI takes over 3 s, Ren uses a fixed line, and the AI line is shown when it arrives but not spoken.
- **Mic and voice:** speech recognition is muted while Ren is talking, so he doesn't hear himself.

---

## 5. Coaching loop (during Working)

1. **Rep 1 is the settle rep** (the swing out of the hike): counted, never coached.
2. **One focus fault at a time.** The first fault seen becomes the focus.
3. **Cue 1** (for example "Arms loose, hips drive"). Wait for the next rep that started after the cue finished. Reps already underway don't count against you.
4. **Fixed:** "Better. That's it." The focus clears.
5. **Not fixed:** Cue 2, worded differently ("Arms are ropes, let the hips throw it"). Watch again.
6. **Still not fixed:** Paused (3.8).
7. **After resuming,** the next bad rep goes straight to cue 2, then pause.
8. **Next set** starts focused on the most frequent fault of the last set.
9. **Other faults** wait their turn. They're logged and mentioned in Set review if they were frequent.

Faults checked today: swing (squatting it, no lockout, leaning back, arms lifting, bell too low) and goblet squat (depth, chest dropping, bell drifting). The thresholds are estimates until they're tuned on recorded swings.

---

## 6. When things go wrong

| Situation | What happens |
|---|---|
| You step partly out of frame mid-set | Reps stop counting straight away. After 2 s: "I've lost you, step back into view." After 10 s: Paused. |
| The phone falls over, or the camera goes dark | No body for 5 s → Paused: "I can't see you. Check the phone." |
| You say "ouch", "pain" or "hurts" (mic on) | Priority 0: "Stop. Put the bell down." The exercise ends. Ren asks what happened and follows the pain rule (stop that movement today, get it checked). |
| No network | Counting, cues and pauses all work. AI lines use fixed fallbacks. A small "offline" chip shows. |
| Voice muted, or no speech on the phone | Captions get bigger. A cue counts as delivered once it's on screen. |
| The screen tries to sleep | The screen is kept awake for the whole session (wake lock). Today it can sleep mid-rest and kill the camera. |
| End session tapped mid-set | The partial set is saved and goes into the debrief. |
| Someone walks through the frame | Out of scope for v1. Tracking follows one person. |

---

## 7. Control summary (hands-free first)

| Want to | Body | Voice | Tap (fallback) |
|---|---|---|---|
| Start a set | stand still in position 2 s | "go" | Start |
| Hold the start | move or step away | "wait" | — |
| Pause | — | "pause" | Set done |
| Resume | back in position, still 2 s | "go" | Resume set |
| End the set | park the bell, 8 s still | "stop" / "end set" | Set done / End this set |
| Skip rest | — | "skip" | Rest · skip |
| Hear it again | — | "repeat" | — |
| End session | — | "end session" | End session |

Voice commands work where the phone's browser supports speech recognition, and the mic is only on during a session. **Decision 4:** is an always-on mic during sessions OK?

---

## 8. What gets logged (on the phone only)

A timeline per session: state changes, each rep with its angles and faults, every cue, praise and pause and what happened next. This is for tuning the thresholds and for Ren's set reviews. It never includes video.

---

## 9. Scripts

How three sessions should sound. Read them out loud. If anything sounds rushed or naggy here, it will in the gym.

### A. First session, beginner, 12 kg

> **Ren:** Andrej, I'm Ren. Today's simple: three sets of ten swings, two of eight goblet squats. Start when you're ready.
> *(taps Start session)*
> **Ren:** Phone side-on, two to three metres away, whole body in view. I'll tell you when I can see you.
> **Ren:** Got you. Quick warm-up. Five hip hinges, no bell. Push your hips back like closing a car door.
> *(hinges)* **Ren:** Good. Now five light swings.
> *(swings)* **Ren:** Hips are doing the work. Set one: ten swings. Focus: snap the hips.
> *(stands still)* **Ren:** Counting you in. Three. Two. One. Hike and swing.
> *(rep 1, settle)* **Ren:** *(silent)*
> *(reps 2–4 clean)* **Ren:** Two. Three. Four.
> *(rep 5, arms lifting)* **Ren:** Arms loose, hips drive.
> *(rep 6 clean)* **Ren:** Better. That's it.
> *(reps 7–10)* **Ren:** Seven. Eight. Nine. Ten. Park it.
> **Ren:** Nine clean of ten. The arms crept in once and you fixed it straight away. Same again, and keep those arms as ropes.
> *(rest timer, 60 s)* **Ren:** Ten seconds. … Rest's up. Set two. Focus: arms loose, hips drive.

### B. A fault that won't shift, with a pause

> *(set 2, rep 4: arms)* **Ren:** Arms loose, hips drive.
> *(rep 5: arms again)* **Ren:** Arms are ropes, let the hips throw it.
> *(rep 6: arms again)* **Ren:** Pause there. Park the bell.
> **Screen:** Paused: arms loose. *Your arms are lifting the bell…*
> **Ren:** Your arms are doing the lifting. The last three tops came with bent elbows. Bell down, five slow hinges, and feel the hamstrings load before you snap. Get back in position when you're ready.
> *(hinges, stands in position, still)* **Ren:** Ready when you are. Three. Two. One. Hike and swing.
> *(rep 7 clean)* **Ren:** Better. That's it.
> *(reps 8–10)* **Ren:** Eight. Nine. Ten. Park it.
> **Ren:** Six clean of ten, and every rep after the pause was clean. That's the fix sticking. Set three, same focus.

### C. Things go wrong

> *(mid-set, steps out of frame)* *(2 s)* **Ren:** I've lost you, step back into view.
> *(back in frame)* *(counting continues; reps out of view weren't counted)*
> *(network drops; set ends)* **Ren:** Seven clean of nine. Rest a minute. *(fixed line; "offline" chip shows)*
> *(during set 3)* **Athlete:** Ouch.
> **Ren:** Stop. Put the bell down.
> **Ren:** What did you feel? If it's sharp pain rather than effort, we stop swings today and you get it checked by a physio.
> *(athlete types: lower back twinge)* **Ren:** Then we're done with swings today. Notes updated. Get it looked at before next time.

---

## 10. What changes from today

| Today | In this spec |
|---|---|
| Tap Start for every set | Stand still in position to start; voice "go"; tap as fallback |
| Resume needs a tap | Resume by getting back in position |
| No warm-up | 2-minute warm-up that also spots today's fault |
| No framing help | Framing guide with specific hints |
| Speech uses "skip if busy" | Priority queue: safety and control cut in; counts are dropped |
| AI lines can arrive late and be spoken late | 3 s limit, then a fixed line |
| Screen can sleep | Kept awake during sessions |
| Pain only handled in chat | "Ouch" or "pain" mid-set stops the exercise |
| No session log | Local timeline for tuning and reviews |

---

## 11. Decisions (agreed 2026-11-25)

1. **Warm-up:** every session, skippable.
2. **Auto-start:** count in when you stand still in position; "wait" holds it.
3. **Pauses:** after two in one set, Ren offers to end it.
4. **Mic:** on during sessions where supported, with a visible mic indicator.
5. **Bell weight:** Ren suggests lighter or heavier only between sessions, never mid-session.
