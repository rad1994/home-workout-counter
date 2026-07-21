# Home Workout Counter

A web app that uses your phone's camera to count exercise reps automatically and plays a sound when you reach your goal.

**Exercises:** Push-Ups · Squats · Jumping Jacks · Crunches

## How it works
- Uses **MediaPipe Pose** (runs fully in the browser, no server needed) to track your body landmarks.
- Each exercise has its own up/down state machine with hysteresis:
  - **Push-Ups** — elbow angle (< 95° down, > 155° up), side view
  - **Squats** — knee angle (< 110° down, > 160° up), front or side view
  - **Jumping Jacks** — wrists above head + ankle spread vs shoulder width, front view
  - **Crunches** — hip angle (< 80° crunched, > 115° lying), side view
- Each rep: beep + spoken count. Goal reached: fanfare + voice announcement.

## Running it on your phone
The camera API requires **HTTPS or localhost**, so you can't just open the file over `http://` on your local network. Easiest options:

1. **Host it for free** (recommended): push `index.html` to GitHub Pages, Netlify Drop (drag & drop at https://app.netlify.com/drop), or Vercel. Then open the URL on your phone.
2. **Local tunnel**: run a local server and tunnel it:
   ```
   npx serve .
   npx localtunnel --port 3000
   ```
   Open the generated https URL on your phone.
3. **Desktop testing**: just run `npx serve .` and open `http://localhost:3000` — localhost counts as a secure context.

## Usage tips
- Pick an exercise — the app shows where to place the phone for that exercise.
- Your tracked joints must stay visible; the app tells you when they're not.
- Set your goal with +/− and press **Start Workout**.

## Notes
- Needs internet on first load (model downloads from CDN, ~5 MB), then it's cached.
- Everything runs on-device; no video is uploaded anywhere.
