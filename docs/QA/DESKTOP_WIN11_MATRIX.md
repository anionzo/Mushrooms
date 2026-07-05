# QA matrix — Windows 11 desktop integration (M1 / VS2)

**When:** Before VS2 sign-off and M8 regression.

## Environment matrix

| ID | OS | GPU | Monitors | DPI | Mode |
| --- | --- | --- | --- | --- | --- |
| W1 | Win11 23H2+ | iGPU laptop | 1 | 125% | Wallpaper + click-through |
| W2 | Win11 | dGPU desktop | 2 | 100% | Primary garden |
| W3 | Win11 | iGPU | 1 | 150% | Interaction mode |
| W4 | Win11 | any | 1 | 100% | Fallback windowed overlay |

## Cases

| Case | Steps | Expected |
| --- | --- | --- |
| D-01 Launch | Start exe | Single instance; no duplicate tray |
| D-02 Transparent | Desktop mode | Desktop icons visible; alpha correct |
| D-03 Click-through ON | Click empty | Click hits desktop app below |
| D-04 Click-through OFF | Click mushroom | Harvest/water works |
| D-05 Tray | Minimize | Sim continues; restore OK |
| D-06 Reboot monitor | Unplug 2nd monitor | Window on valid display |
| D-07 Sleep resume | S3 sleep | No hang; sim catches up capped |
| D-08 Alt-tab | | No focus steal in passive mode |

## Performance (spot)

| Metric | Pass |
| --- | --- |
| CPU 5 min idle | <5% one core (target) |
| Working set | <600 MB typical |

## Evidence

Screenshot + `Player.log` snippet per failed case; link in story US-M1-11.