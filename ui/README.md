# UI

React + Vite + Tailwind front end for the onboarding agent. It talks to the FastAPI server in [`../workflow_server.py`](../workflow_server.py) on port 8000.

```bash
npm install
npm run dev      # http://localhost:5173
npm run build
```

The navbar has a role toggle. **Manager** sees Pre-boarding, Coaching Notes, Certification, Debrief Reviews, and Dashboard. **Trainee** sees AI Tutor, Cold Call Simulation, and Onboarding Debrief. Every AI output renders with its cited sources and an approve / edit / reject / escalate panel.
