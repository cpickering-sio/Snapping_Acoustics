# Snapping_Acoustics
This is my acoustic analysis pipeline  
# Snapping Shrimp Acoustic Density Estimation Tutorial

This tutorial walks through a minimal, **Butler‑style** workflow for estimating snapping shrimp densities from passive acoustic recordings using Python, with pointers to temperature and habitat effects you should consider for your own site. [web:1][web:3][web:5]

The pipeline is:

1. Convert raw WAV data to absolute sound pressure (calibration).
2. Detect individual snaps and compute received levels (RL).
3. Estimate distances to snap sources with a simple transmission loss model.
4. Export distances to a CSV for distance sampling (e.g., Distance in R).
5. Convert snap densities to shrimp densities using a cue rate (snaps per shrimp per unit time).

> This README is an implementation‑focused summary of:  
> Butler, J., Butler, M. J., & Gaff, H. (2017). Snap, crackle, and pop: Acoustic-based model estimation of snapping shrimp populations in healthy and degraded hard-bottom habitats. *Ecological Indicators, 77*, 377–385. [web:1][web:3]

Additional references on temperature, sound speed, and snapping shrimp behavior are acknowledged in the **References** section at the end. [web:5][web:17][web:21]

---

## 0. Setup and data assumptions

We assume:

- You have calibrated hydrophone + recorder metadata:
  - Hydrophone sensitivity (dB re 1 V/µPa).
  - Recorder scaling (e.g., volts per full‑scale digital count).
- WAV files contain continuous recordings with snapping shrimp.
- Water temperature during recordings was ~26–27 °C (78.8–80.6 °F) at typical ocean salinity (~35), on a sandy bottom with nearby reef structure (within a few meters).  
  - This matters mainly for snap **cue rates** (snaps per shrimp per unit time) and for tuning the propagation (spreading) coefficient. [web:5][web:18][web:19]

### Python dependencies

Install:

```bash
pip install numpy scipy soundfile pandas
