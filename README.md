# VeloGuard

**A camera-assisted one-way-lane event-review concept, explored through a browser-based tabletop simulation.**

VeloGuard explores a practical question for a campus or managed estate: can potentially wrong-direction vehicle movements at a defined entrance be surfaced as reviewable events, so a site manager can decide whether signage, staffing, or another low-cost intervention is justified?

> [!IMPORTANT]
> **Prototype status and limits:** The checked-in application is a generated, browser-side tabletop simulation. It does not connect to a real camera, ESP32, OpenCV pipeline, or road feed. Road performance is unknown. The simulated events and any labelled synthetic examples must not be presented as field results or proof of safety impact.

## What is in this repository

| File | Purpose |
|---|---|
| `veloguard_demo.html` | Self-contained interactive demo console, including styling and browser-side simulation logic |
| `README.md` | Project overview, operation instructions, evaluation boundaries, and limitations |

The demo references a Python reference script named `veloguard_tabletop.py` in its interface, but that script is **not currently included** in this repository.

## Demonstration workflow

The console illustrates the proposed event-review pipeline:

1. Start with a generated desk-lane scene.
2. Calibrate the expected travel direction with an arrow and define a region of interest.
3. Generate moving objects and synthetic disturbances.
4. Build a foreground mask, identify blobs, and link their centres into tracks in the simulation.
5. Compare track displacement with the configured direction using a cosine check.
6. Create candidate events with an ID, snapshot, and simulated clip.
7. Let a human reviewer accept or reject each candidate.
8. Review event counts alongside the minutes actually observed.

This is a demonstration of a workflow and its failure modes, not a deployed vehicle-detection system.

## Demo capabilities

- **Calibration controls:** set the direction arrow, draw the lane region, reverse the arrow, or restore defaults.
- **Scenario generation:** legal pass, reverse pass, sideways crossing, moving shadow, glare/reflection, pedestrian, split-object failure case, and camera bump.
- **Detection visualisation:** simulated foreground mask, track history, and direction score.
- **Review queue:** inspect candidate events and record accept/reject decisions.
- **Observation accounting:** view events by time bucket with observed minutes and downtime.
- **Evidence and evaluation guidance:** inspect the TP/FP/FN scoring approach, blind-label protocol, and examples of failure modes.
- **Presentation support:** presenter sequence, judge Q&A rehearsal, and a final checklist.

## Run locally

No package installation or build step is required for the checked-in HTML demo.

1. Clone the repository:
   ```bash
   git clone https://github.com/i803/VeloGuard.git
   cd VeloGuard
   ```
2. Open `veloguard_demo.html` in a modern desktop browser.

   On Windows PowerShell:
   ```powershell
   Start-Process .\veloguard_demo.html
   ```

   On macOS:
   ```bash
   open veloguard_demo.html
   ```

   On Linux:
   ```bash
   xdg-open veloguard_demo.html
   ```

The page uses browser-native HTML, CSS, Canvas, and JavaScript. The simulated scene is generated in the browser; the page does not require a camera or network connection.

## Evaluation: what would be needed before field claims

Before reporting real-world detection performance, the team would need to:

- Obtain site-owner permission and document the lane rules, operating hours, exceptions, camera position, and retention policy.
- Collect a representative, authorised dataset with a documented ground-truth labelling protocol.
- Have reviewers label the original footage independently before reviewing detector flags.
- Match detections to ground-truth crossings and report precision, recall, false positives, false negatives, and observation coverage.
- Include difficult cases such as shadows, glare, camera movement, partial occlusion, pedestrians, and multiple objects.
- Compare the proposed intervention with a simpler baseline, such as signage changes or scheduled staff observation.

A simulated run, replay, or synthetic example is not a substitute for independent field evaluation.

## Safety, privacy, and responsible use

The demo describes a human-reviewed decision-support workflow. A candidate event is not proof of intent or wrongdoing. The prototype does not identify drivers, recognise number plates, issue fines, contact police, or control roadside equipment.

The proposed data-handling protocol in the demo is to keep original footage local, restrict it to named reviewers, disable cloud sync, log access and deletion, and avoid sharing raw footage in group chats or on presentation screens. These are project requirements to implement and verify; the HTML demo does not itself enforce an operational footage-management system.

The candidate site and any buyer, price, grant, or impact assumptions shown in the demo remain unverified until supported by permission, interviews, quotes, and measured evidence.

## Current limitations

- Browser-generated synthetic scenes only.
- No real camera ingestion or hardware connection.
- No trained vehicle classifier or validated real-world tracking pipeline.
- No number-plate recognition or driver identification.
- No verified field accuracy, buyer, price, or mobility impact.
- No automated test suite is currently included in this repository.

## Next engineering milestones

1. Package the reference detection pipeline and document its interface.
2. Add a reproducible dataset and ground-truth annotation workflow.
3. Test against authorised recordings and publish metrics with observation coverage.
4. Add a privacy-preserving local capture and review workflow.
5. Compare operational effectiveness with simpler interventions before proposing deployment.

---

**Project context:** RVCE student prototype. The current repository is the demonstration console; claims about real-road operation remain unverified.
