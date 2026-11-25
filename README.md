# sorcerer-killer-workout-pwa
Self-hosted Progressive Web App (PWA) for a 4-day hybrid dumbbell, machine, and calisthenics workout routine—featuring per-set weight/rep logging, rest timers, workout history calendar, and offline storage.

Sorcerer Killer — Toji Fushiguro Workout PWA

A self-hosted, single-file Progressive Web App (PWA) designed around a 4-day hybrid hypertrophy, calisthenics, and mobility routine inspired by Toji Fushiguro (Jujutsu Kaisen). Built specifically for a home/multi-gym setup (dumbbells, lat pulldown/press station, 2-in-1 leg developer, and bodyweight calisthenics) with zero external build steps or backend database dependencies.

✨ Key Features

Hevy-Style Per-Set Logging: Track individual sets with SET, PREVIOUS (auto-populated from your last completed session), LBS, REPS, completion checkmarks, and a + Add Set button.

5-Day Structured Training & Recovery Split:

Day 1 — Upper Width & Thickness: V-taper back, overhead pressing, lateral raises, and gymnastic core compression + pre-session shoulder/thoracic mobility.

Day 2 — Lower Body & Explosiveness: Plyometric jumps, goblet squats, RDLs, Bulgarian split squats, and single-machine leg pairings (never pairs two machine setups back-to-back) + hip/ankle mobility.

Day 3 — Active Recovery & Mobility: Structured 20–25 minute protocol combining low-intensity cardio, World’s Greatest Stretch, 90/90 hip switches, thoracic open-books, and dead hangs/wall slides.

Day 4 — Push & Arms: Machine/dumbbell presses, slow-eccentric push-ups, dips, and arm supersets + chest/shoulder mobility prep.

Day 5 — Full-Body Power & Conditioning: Dumbbell swings, underhand pulldowns, commandos + burpees, farmer’s carries, and combat interval finishers.

Skip Exercise Toggles: Skip any movement on the fly without blocking your daily or weekly completion percentage.

Workout History & 28-Day Calendar: Tap Finish Workout to save a timestamped snapshot (duration, total volume in lbs, sets, weights, and reps) and browse past sessions on an interactive calendar.

Built-In Rest Timer & Session Clock: Live session elapsed clock, customizable countdown rest timer (60s–180s presets + one-click exercise rest triggers), and a Web Audio completion chime.

PWA & Offline Ready: Dynamic Web App Manifest, generated PNG home-screen icon, Service Worker caching, Screen Wake Lock toggle (keeps your screen awake between sets), and JSON Backup/Restore for transferring logs across devices.

🚀 Quick Start (Self-Hosting with Docker & Nginx)

Because the entire app lives in a single HTML file (sorcerer_killer_workout_pwa.html), you can host it on a Raspberry Pi, home server, or NAS using a lightweight nginx:alpine container.

1. Directory Structure

toji-workout/
├── docker-compose.yml
├── default.conf
└── site/
    └── sorcerer_killer_workout_pwa.html


2. default.conf

Serves sorcerer_killer_workout_pwa.html automatically at the root URL (/):

server {
    listen 80;
    server_name _;

    root /usr/share/nginx/html;
    index sorcerer_killer_workout_pwa.html index.html;

    location / {
        try_files $uri $uri/ /sorcerer_killer_workout_pwa.html;
    }
}


3. docker-compose.yml

services:
  toji-workout:
    image: nginx:alpine
    container_name: toji-workout
    restart: unless-stopped
    ports:
      - "8085:80"
    volumes:
      - ./site:/usr/share/nginx/html:ro
      - ./default.conf:/etc/nginx/conf.d/default.conf:ro


4. Launch the Container

docker compose up -d


Access the app at http://<server-ip>:8085/ (or over Tailscale / HTTPS via tailscale serve --bg 8085).

📱 Installing on Mobile (Android / iOS)

Open your hosted https:// (or local/Tailscale) URL in Chrome (Android) or Safari (iOS).

Tap Install App in the header—or open your browser menu and select Add to Home screen / Install app.

Launch from your home screen for a full-screen, app-like experience.

💾 Data Storage & Backups

All workout progress, weights, reps, notes, and calendar history are stored locally in your browser via localStorage (toji_workout_hevy_v4).

Click the Settings (Gear) icon in the top bar at any time to Export Backup (.json) or Import Backup (.json) when switching devices or browsers.
