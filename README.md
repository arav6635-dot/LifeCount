# LifeClock

LifeClock is a single-page web app that compares:

- Your **Current Routine**
- A **Healthy Target** routine

It estimates how daily habits may affect projected life expectancy and free/social time.

## Features

- Compare **current vs target** life expectancy
- Show **potential years gained**
- Visualize both scenarios with **100-year timeline blocks**
- Show **factor-by-factor impact** (sleep, screen time, diet, exercise, stress, smoking, AQI)
- Track daily **free time** and **phone vs people time**
- Warn when your routine exceeds 24 hours/day

## Inputs

### Current Routine
- Age
- Sleep hours/day
- Work hours/day
- Phone screen time/day
- Commute hours/day

### Health Factors (Current)
- Average AQI
- Eating quality (1-10)
- Exercise mins/day
- Stress (1-10)
- Cigarettes/day

### Healthy Target (Editable)
- Target sleep/day
- Target phone/day
- Target eating quality
- Target exercise
- Target stress
- Target cigarettes/day
- Target AQI (optional, blank = same as current AQI)

## How It Calculates

Base model:

- `base_expectancy = 85`
- Final expectancy is clamped to `45..100`

Daily time model:

- `fixed = sleep + work + commute`
- `free = max(0, 24 - fixed)`
- `people = max(0, free - screen)`
- Overflow warning if `fixed + screen > 24`

Habit impact model (years):

- Sleep: reward near 8h, penalty as it moves away
- Screen time: penalty above 2h/day
- Work + commute load: penalty above 10h/day combined
- Diet: scaled from 1..10
- Exercise: tiered positive/negative adjustment
- Stress: penalty as stress rises above healthy range
- Smoking: per-cigarette penalty
- AQI: tiered air-quality adjustment

## Run Locally

No build tools are required.

1. Open `index.html` directly in a browser.
2. Edit inputs and see metrics update live.

## Project Structure

- `index.html` - UI, styles, and app logic (all-in-one file)

## Notes

- This is a **heuristic behavior model**, not medical advice.
- Numbers are intended for relative comparison and awareness, not diagnosis.
# LifeCount
