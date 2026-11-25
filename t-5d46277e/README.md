# Ren: kettlebell coach (private friends test)

A phone web app. Ren watches your kettlebell swings and goblet squats through the camera, counts reps, calls out form faults out loud, stops the set when form breaks down, talks to you between sets, and remembers each person between sessions.

## What's in this folder

| File | What it is |
|---|---|
| `index.html` | The whole app (screens, camera, pose analysis, voice). Set `API_URL` near "trainer API" |
| `worker/worker.js` | The server part, for Cloudflare Workers: checks the access code, adds Ren's personality, calls Claude. **Ren's personality is at the top of this file** |
| `.gitignore` | Keeps `worker/` and the old PHP files out of your public GitHub repo |
| `api.php`, `config.php`, `persona.php`, `.htaccess` | The old PHP version, only for hosts that run PHP. Not used with GitHub Pages |
| `pose*`, `*.wasm`, `*.tflite`, `*.data`, `*.binarypb` | The body-tracking model (Google MediaPipe Pose, Apache 2.0). Don't rename |
| `formcheck-demo/` | The earlier stand-alone form checker (squat, push-up, plank, curl) |

## Set it up: GitHub Pages + Cloudflare (about 20 minutes)

GitHub Pages only serves files, so the part that holds your API key runs as a free Cloudflare Worker. Your key and access code live only in Cloudflare, never in GitHub. This README is pushed to your public repo, so never write the key or the code in it.

**1. Claude API key.** At console.anthropic.com add some credit (5 USD is plenty for a friends test), then Settings > API keys > Create key. Also set a low monthly spend limit (Settings > Limits) as a safety net.

**2. Cloudflare Worker.**
1. Sign up free at dash.cloudflare.com. You don't need to move your domain there.
2. Workers & Pages > Create > Worker > start from "Hello World". Name it `ren-coach` and deploy.
3. Edit code: delete everything, paste the whole of `worker/worker.js`, Deploy.
4. Worker > Settings > Variables and Secrets > Add, type **Secret**:
   - `ANTHROPIC_API_KEY` = your Claude key
   - `ACCESS_CODE` = the code for your friends
5. Optional hourly cap: Storage & Databases > KV > Create a namespace called `ren-rate`. Then Worker > Settings > Bindings > Add > KV namespace, variable name `RATE`, pick `ren-rate`. Default cap is 200 replies per hour (change with a text variable `HOURLY_CAP`).
6. Copy the Worker's address, like `https://ren-coach.yourname.workers.dev`.

If your site is not served from `https://andrejsavcic.com` or `https://www.andrejsavcic.com`, add a text variable `ALLOWED_ORIGINS` with the right address (comma-separated). The Worker refuses calls from any other site.

**3. Point the app at the Worker.** In `index.html`, search for `API_URL` and replace `PASTE-YOUR-WORKER-URL-HERE` with the Worker address.

**4. Put the app on GitHub Pages.** Copy this whole folder into your site's repository as a folder with a hard-to-guess name, for example `t-7k2f9q/`, then commit and push. The `.gitignore` keeps `worker/` and the PHP files out. The app is then at `andrejsavcic.com/t-7k2f9q/`. Your repo is public, so the folder name can be found there; the access code is what really keeps strangers out.

**5. Test on your own phone first:** open the link, enter the code, meet Ren, then do one set of swings. If Ren says "Trainer unavailable", open the Worker in Cloudflare > Logs to see why (a wrong model name shows up there; change it with a text variable `MODEL`).

**6. Send friends the link and the code.** On iPhone, Share > Add to Home Screen makes it feel like an app. To change the code later, edit the `ACCESS_CODE` secret in Cloudflare.

## How a session goes

The full design is in `FLOW.md`. In short:

Check in → Start session → prop the phone side-on, 2 to 3 metres away, and Ren tells you when he can see you → 2-minute warm-up (5 hip hinges, 5 light swings; skippable) → Ren briefs the exercise → stand still in position and he counts you in → during the set he coaches one fault at a time: a cue, a second cue worded differently, then a pause to park the bell and fix it (reps are kept; get back in position to carry on) → he reacts to the set → rest starts once he's finished talking → next set → debrief, and Ren updates his notes about you.

Hands-free where the phone supports speech input: say "go", "wait", "pause", "stop", "skip", "repeat" or "end session". Saying "ouch", "pain" or "hurts" stops the exercise straight away. Taps always work too. The screen stays awake during a session.

## What Ren checks

**Swing (two-hand Russian, side view)**
- Squatting the swing: knee angle under 125° at the bottom
- No hip lockout: hip angle under 163° at the top
- Leaning back at the top: torso more than 12° behind vertical
- Lifting with the arms: elbow under 140° at the top
- Bell too low: hands below halfway between hips and shoulders at the top

**Goblet squat (side view)**
- Depth: knee angle should reach 100° or less
- Chest dropping: torso more than 45° from vertical
- Bell drifting away from the chest

These thresholds are my estimates, not validated standards. Tune them in `index.html` (search for `makeSwing` and `makeGoblet`) after watching your friends move.

## Privacy and cost

- Video never leaves the phone. Only rep numbers, angles, and what people type or say go to the Worker and on to Claude.
- Each friend's profile, history and Ren's notes live in their own phone's browser storage. Clearing browser data or Settings > Forget me deletes them. No database needed.
- The optional KV hourly cap and your Anthropic spend limit are the safety nets. A session is roughly 10 to 15 short replies; on a Haiku-class model that's a fraction of a cent.

## Known limits

- Single phone camera, flat 2D view: it can't see back rounding or knees caving in.
- Phone voices are robotic; pick the best one in Settings.
- Speech input availability varies by phone and browser.
- Tested: the swing and squat logic on synthetic poses, the screens, and the server script wiring. Not yet tested on a real person swinging a real bell. Do that first.
