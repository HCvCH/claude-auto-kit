---
name: motion-easing
description: Easing curves, spring physics and timing for animations that feel organic instead of robotic — which curve for which move, ready cubic-bezier and spring values (CSS, GSAP, Remotion, Framer Motion), durations by distance and size, overshoot, anticipation, follow-through, stagger and squash rules. Use whenever writing or fixing any animation (UI, website, motion graphics, Remotion video) or when motion looks stiff, linear, floaty or cheap.
---

# Motion Easing

Stiff AI animation almost always has the same causes: linear timing, one curve for everything, equal durations regardless of distance, and everything starting at once. Fix the physics first; style comes after. Look comes from `motion-styles`, Remotion craft from `remotion-motion-graphics`, UI micro-interactions from `animate`.

## 1. Pick the curve by what the object is doing

| Move | Curve | Why |
|---|---|---|
| Enters the frame / appears | ease-out (fast start, soft landing) | Arrives with energy, settles |
| Leaves / disappears | ease-in (slow start, fast end), shorter | Gets out of the way |
| Moves from A to B on screen | ease-in-out | Real objects accelerate and brake |
| Responds to a tap/click | spring or very short ease-out | Feels physical and immediate |
| Loops (breathing, floating) | sine | No visible start or end |
| Mechanical (clock hand, conveyor) | linear — the only legit use | Machines run at constant speed |

## 2. Ready values

| Name | cubic-bezier | GSAP | Use |
|---|---|---|---|
| Out expo | `0.16, 1, 0.3, 1` | `expo.out` | Hero entrances, big reveals |
| Out quart | `0.25, 1, 0.5, 1` | `power3.out` | Standard UI entrances |
| In-out quint | `0.83, 0, 0.17, 1` | `power4.inOut` | Camera moves, slides, Ken Burns |
| In quart | `0.5, 0, 0.75, 0` | `power3.in` | Exits |
| Back out | `0.34, 1.56, 0.64, 1` | `back.out(1.7)` | Playful pop with overshoot |

Springs (Remotion `spring({config})`, Framer Motion `type: "spring"`):

| Feel | damping | stiffness | mass |
|---|---|---|---|
| Snappy (buttons, words) | 14 | 160 | 0.6 |
| Smooth (cards, big blocks) | 20 | 90 | 1 |
| Bouncy (logos, mascots) | 11 | 170 | 0.7 |
| Heavy (large objects, 3D props) | 26 | 60 | 1.5 |

Lower damping = more bounce. Higher mass = slower, weightier. Use springs for anything the viewer should feel as "physical"; use bezier when the exact end time matters (sync to a beat or a word).

## 3. Duration follows distance and size

- Small UI change (color, icon): 100–200 ms. Medium (card, modal): 200–350 ms. Full-screen or camera move: 400–800 ms.
- In video at 30 fps: word pop 8–12 frames, element entrance 15–24, scene transition 8–14, camera move 30–60.
- Longer distance = longer duration, but not proportionally (double the distance ≈ 1.3× the time).
- Big objects move slower than small ones; heavy objects take longer to start and to stop.
- Exits ≈ 60–75 % of the entrance time.

## 4. The principles that make it feel alive

- **Anticipation:** a small move the opposite way (3–8 %) before a big move — a button dips before it launches.
- **Overshoot and settle:** land slightly past the target, then return. Back-out curve or a spring with damping 10–14.
- **Follow-through and overlap:** parts don't stop together — a character's hair, a card's shadow or a label trails 2–4 frames behind the body.
- **Squash and stretch:** fast-moving soft things stretch along the motion and squash on impact; keep volume constant (scaleX × scaleY ≈ 1). Never on text or UI chrome.
- **Arcs:** natural motion travels on curves, not straight diagonals — offset x and y with different curves.
- **Stagger:** groups never start together. Words 2–3 frames apart, list items 3–5, big blocks 6; or 30–60 ms in UI. Order by reading direction or by distance from the point of interaction.
- **Hold:** after a big move, stillness for 0.5–1 s. Contrast between motion and rest reads expensive; constant motion reads cheap.
- **Animate 2–3 properties together** on entrances (opacity + position + scale or blur), never a lone fade.

## 5. Common mistakes and fixes

| Looks like | Cause | Fix |
|---|---|---|
| Robotic, mechanical | Linear timing | ease-out for entrances, ease-in-out for moves |
| Floaty, sluggish | Ease-out tail too long, duration too long | Shorter duration or out-quart instead of out-expo |
| Jittery | Several curves fighting on one property, or sub-pixel text moves | One driver per property; round text positions |
| Everything feels the same | Same duration and curve everywhere | Vary by size, distance and importance |
| Bounces feel childish | Overshoot on serious content | Overshoot only on accents; smooth springs elsewhere |
| Busy, tiring | No holds, everything moving | Add stillness, animate fewer things at once |

## 6. Check

Scrub at 0.25× speed — curve problems invisible at full speed become obvious. Check the first and last frames of each move (no snapping), and that nothing appears before its entrance or lingers after its exit (clamp interpolations).

---
Written for this repo in its own words; values are common motion-design practice.
License: CC-BY-NC-SA-4.0 — © HCvCH, https://github.com/HCvCH/claude-auto-kit (see NOTICE.md)
