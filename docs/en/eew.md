---
# /docs/en/eew.md (English)
title: CWA Earthquake Early Warning (EEW)
layout: default
---

<p style="text-align: right;">
  <a href="../eew.html"><strong>切換至中文</strong></a>
</p>

# ⚡ CWA Earthquake Early Warning (EEW) System

The core principle of an Earthquake Early Warning (EEW) system is "a race against the seismic waves."

It utilizes seismic stations deployed near the epicenter to detect the initial signal within the **first few seconds** of an earthquake. The system rapidly calculates the event information (location, magnitude, estimated intensities) and issues an alert to areas likely to experience strong shaking *before* the most destructive seismic waves (S-waves) arrive.

The goal of this system is to provide a "golden time" of **several to tens of seconds**, allowing the public, transportation systems, and critical facilities to take protective measures and reduce potential damage.

---

## The Science Behind the Warning: P-waves vs. S-waves

Earthquakes generate two main types of body waves that travel at different speeds. This physical difference is the foundation of EEW:

1.  **P-wave (Primary / Compressional Wave):**
    * **Travels fast** (approx. 5-7 km/s).
    * **Smaller amplitude**, causing minor, often non-damaging, shaking.
    * It is the **first** seismic wave to arrive.

2.  **S-wave (Secondary / Shear Wave):**
    * **Travels slower** (approx. 3-4 km/s).
    * **Larger amplitude** and is the **main cause** of structural damage.
    * It arrives *after* the P-wave.

**The Golden Warning Time:**
The EEW system works by detecting the **first-arriving P-wave**, instantly issuing an alert, and delivering it to target areas before the **later-arriving, destructive S-wave** hits. The farther an area is from the epicenter, the greater the time lag between P and S-wave arrivals, resulting in a longer potential warning time.

---

## CWA EEW System Overall Architecture

CWA's EEW system is a complex, high-availability system. Its overall architecture can be divided into four main stages:

![CWA EEW System Architecture and Real-time Network](../assets/img/EEWsystem_seismicnetwork.jpg)
*Figure 1: CWA EEW System Overall Architecture (left) and 2024 Real-time Land-Sea Network (right).*

As shown in the diagram (left), the system flow is as follows:

1.  **Collect Real-Time Data (RSD System):**
    This stage is responsible for **collecting real-time data from field stations**. The data source is the "Integrated Real-Time Land-Sea Seismographic Network" (Fig. 1, right), which comprises 632 stations as of 2024.

2.  **Parallel Calculation (EEW System):**
    To ensure stability and accuracy, CWA employs a mechanism of **multiple, parallel EEW systems**. These systems run different algorithms (or the same algorithm with different parameters) to process the incoming data simultaneously. They include:
    * **EEW-AI** (AI-based)
    * **IPFX System**
    * **eBear System** (housing EEW1, EEW2, EEW3)
    * **ESE System** (FinDer, VS)

3.  **Decision (Estimate Impact & Decide):**
    All results (earthquake parameters) from the parallel systems are fed into a common decision system (e.g., the `EEWRing`). This system integrates all information to make a final decision on whether to issue an alert.

4.  **Send Alerts (EEW Message Issue):**
    Once the decision is made, the issuing system **sends alerts via different channels**, such as `DCSN1` (EIP, TV), `pwssend` (PWS), etc.

---

## Network Evolution and Warning Effectiveness

The success of an EEW system is directly linked to the "**density**" of its seismic stations. **A higher density network leads to a faster warning time, which in turn reduces the size of the "blind zone."**

![Evolution of CWA's Real-time Seismic Network (2010-2025)](../assets/img/eew_evolution_station.jpg)
*Figure 2: Evolution of CWA's Real-time Seismic Network (Left: 2016, Middle: 2010, Right: 2025)*

As shown above (Fig. 2), the CWA's real-time network has expanded significantly, reaching **362 ACC stations**, **19 VEL stations**, and **9 OBS stations** by 2025.

---

## Case Study: The 2025 Dapu Earthquake

This network densification is directly reflected in the reduction of the blind zone and the effectiveness of the warning.

### 1. The Shrinking Blind Zone (Theory)

![Using the 2025 Dapu EQ P/S travel times to illustrate the reduction of the EEW blind zone](../assets/img/blindzone_evolution_dapuEQ.jpg)
*Figure 3: Using the P/S travel times from the 2025 Dapu EQ to illustrate the reduction of the EEW blind zone.*

This plot shows the continuous improvement in CWA's "processing time" required to issue an alert:

* **2010 (Jiasian M6.4):** The system required **27.0 seconds**, resulting in a blind zone radius of **86 km**.
* **2016 (Meinong M6.6):** The time was reduced to **12.0 seconds**, shrinking the blind zone to **28 km**.
* **2025 (Dapu M6.8):** The current system requires only **7.9 seconds**, dramatically reducing the blind zone to **12 km**.

### 2. Warning Performance: Timing (In Practice)

The following image shows the **actual performance** of the EEW system during the 2025 Dapu Earthquake.

![EEW Performance Heatmap for the 2025 Dapu Earthquake](../assets/img/eew_performance_dapu_eq.jpg)
*Figure 4: EEW performance heatmap for the 2025 Dapu EQ (left) and the TSMIP network used for observation (right).*

* **Left (Heatmap):** This shows the "Maximum Intensity" observed at different latitudes (Y-axis) over the first 60 "Time Steps" (X-axis).
    * **Yellow Lines:** Mark the moments the CWA alerts were issued (`1st Warning 7.9 s` and `2nd Warning 9.0 s`).
    * **Analysis:** Although the system took 7.9 seconds to issue the first alert, for the regions outside the epicenter that observed high intensities (e.g., 5+ and 6-, the green/yellow/red areas between 23.3-24.3 latitude), the warning **still arrived before** the strong ground motion. This successfully provided **several to tens of seconds** of advance warning.
* **Right (Map):** This shows the "Taiwan Strong Motion Instrument Program (TSMIP)" network (603 real-time stations) that was used to record the "ground truth" intensities shown in the heatmap.

### 3. Warning Performance: Intensity (In Practice)

In addition to speed, accuracy is paramount. The figure below compares the "Predicted Intensity" from the EEW system with the "Observed Intensity."

![Predicted vs. Observed Intensity for the 2025 Dapu Earthquake](./assets/img/eew_performance_dapu_eq_intensity.jpg)
*Figure 5: Predicted vs. Observed Intensity Comparison for the 2025 Dapu Earthquake.*

* **(a) First Alarm (7.9 s):** The **predicted intensity map** issued by the system (covering 19 cities).
* **(b) Second Alarm (9.0 s):** The system's updated **predicted intensity map** (coverage reduced to 1 city).
* **(c) Catalog and Observations:** The **final observed intensity map** recorded by all TSMIP stations after the event.
* **(d) First Alarm Accuracy:** A confusion matrix comparing "Prediction Intensity" vs. "Observation Intensity," showing **90% of predictions were correct**.
* **(e) Second Alarm Accuracy:** The matrix for the second alarm, showing **83% accuracy**.

**Conclusion:** This case study demonstrates that CWA's EEW system not only issues alerts faster than the arrival of strong shaking but also achieves **a very high accuracy (90%) in its intensity predictions**.

---

## Algorithm in Focus #1: Effective Epicenter Method

Among the parallel systems, one of CWA's current primary systems uses the "Effective Epicenter Method." Its core principle is **speed**:

![Effective Epicenter Method Flowchart](../assets/img/effective_epicenter_eew.png)
*Figure 6: The four steps of the Effective Epicenter Method.*

As shown above, this method demonstrates the complete automated flow of the EEW system:

* **(a) Triggers:**
    When the P-wave arrives, the PGA at several stations (gray triangles) exceeds a threshold.

* **(b) Association:**
    Through spatial and temporal filtering, the system "associates" these independent triggers into a single event (red triangles).

* **(c) Location:**
    The system calculates the **geometric center (yellow star)** of this cluster, treating it as the "Effective Epicenter." This method is **extremely time-saving** and effectively reflects the source of the vibrational energy.

* **(d) Intensity:**
    Once the effective epicenter is determined, the system immediately calculates the magnitude and applies an intensity prediction formula to assess estimated intensities across Taiwan (Fig d).

### Core Calculation Formulas

**1. Magnitude (<i>M<sub>pd</sub></i>) Calculation**
The system uses the vertical displacement (<i>P<sub>d</sub></i>) from the first few seconds of the P-wave and the epicentral distance (<i>R</i>) to estimate the magnitude <i>M<sub>pd</sub></i>:

<img src="https://latex.codecogs.com/png.latex?%5Cdpi%7B150%7D%20M_%7Bpd%7D%20%3D%205.067%20&plus;%201.281%20%5Ctimes%20%5Clog10%28P_d%29%20&plus;%201.760%20%5Ctimes%20%5Clog10%28R%29" alt="M_pd = 5.067 + 1.281 * log10(P_d) + 1.760 * log10(R)">

**2. PGA Prediction (Intensity)**
Next, the system uses the estimated magnitude (<i>M</i>), epicentral distance (<i>r</i>), and station site effect (<i>S<sub>i</sub></i>) to predict the Peak Ground Acceleration (PGA):

<img src="https://latex.codecogs.com/png.latex?%5Cdpi%7B150%7D%20PGA%20%3D%201.657%20%5Ctimes%20e%5E%7B1.533%20%5Ctimes%20M%7D%20%5Ctimes%20r%5E%7B-1.607%7D%20%5Ctimes%20S_i" alt="PGA = 1.657 * e^(1.533 * M) * r^(-1.607) * S_i">

---

### Earthworm Data Flow for the Effective Epicenter Method

The algorithm described above is implemented within CWA's Earthworm system as a series of modular data flows:

![CWA EEW System Data Flow Architecture within Earthworm](../assets/img/eew_system_architecture_in_earthworm.png)
*Figure 7: CWA EEW System Data Flow Architecture within Earthworm.*

1.  **Data Import:** `IMPORT` module **imports real-time data**.
2.  **Waveform Ring (WAVE_RING):** Stores all real-time **wave packets**.
3.  **P-wave Picking (Auto-pick):** `PICK_EEW` module **auto-picks P-wave arrivals** and **calculates P-wave amplitudes (<i>P<sub>d</sub></i>)**.
4.  **Pick Ring (PICK_RING):** Stores the P-arrival times and <i>P<sub>d</sub></i> values.
5.  **Location & Estimation (Locate & Estimate):** `TCPD` module reads P-info, **locates the event**, and **estimates the magnitude**.
6.  **Hypocenter Ring (HYPO_RING):** Stores the resulting **earthquake message**.
7.  **Decision & Release (Decision Making):** `DCSN` module reads the message, **estimates intensities**, and makes the **decision to release the EEW**.
8.  **Data Output (Output):** The final alert is **sent** to partners and written to `XML FILES` and a `DATABASE`.

---

### 🐳 Open-Source Release: Docker Hub Image

To promote academic exchange and technical transparency, CWA has packaged the EEW system (including the Earthworm environment, EEW source code, and parameter files) into a Docker image, which is available on Docker Hub for public download and research.

![CWA EEW System Docker Hub Image](../assets/img/eew-dockerhub.png)
*Figure 8: The Docker Hub page for CWA's EEW system (cwadayi/earthworm_ubuntu22.04_eew).*

* **Docker Hub Repository:**
    `cwadayi/earthworm_ubuntu22.04_eew`

As shown, this image contains the CWA EEW system's **source code** (`EEW_src`), related **parameter files**, and the operating environment. Researchers can download this image and use it along with **test data** from the CWA GDMS website to replicate and study the system.

---

## Ongoing Project: The IPFx System

As shown in the Overall Architecture (Fig 1), CWA runs multiple algorithms in parallel. The IPFx System is one of the advanced systems currently under development (ongoing project).

![IPFx System real-time execution and data flow architecture](../assets/img/eew_project_ipfx.png)
*Figure 9: IPFx System real-time execution (left) and data flow architecture (right).*

This image shows the IPFx system's real-time execution and architecture:

* **Real-time Execution (Left):**
    * **Map (top-left):** Shows the real-time triggered stations (red triangles) and the solved epicenter (black star).
    * **Convergence Plots (middle):** These plots show how the Epicentral Distance (Δ R) and Depth rapidly converge and stabilize within seconds of the event.
    * **Magnitude Plot (top-right):** Shows the Magnitude (Mag/SI) also stabilizing quickly.

* **Data Flow Architecture (Right):**
    * **MQTT/EMQX:** This system uses modern **MQTT/EMQX** message queueing technology to receive 609 channels of real-time station data, demonstrating high efficiency and low latency.
    * **Low Latency:** The total delay is only ~3 seconds, and processing can begin with a 1-second data window.
    * **Output:** The final results are sent to `win2disp` (for live display) and `eew_rbis` (the alert decision system) for further action.

---

## Alert Dissemination Channels, Criteria, and Latency

CWA's alert dissemination uses a **tiered** strategy, with different criteria and latencies for different channels:

| Channel | Dissemination Criteria | Transmitting Delay |
| :--- | :--- | :--- |
| **PWS** | <i>M</i> &ge; 5.0 <b>and</b> <i>I</i> &ge; 3 <br> <b>or</b> <br> <i>M</i> &ge; 6.5 <b>and</b> <i>I</i> &ge; 2 | 5.5 Seconds |
| **TV** | <i>M</i> &ge; 5.0 <b>and</b> <i>I</i> &ge; 2 | 10–20 Seconds |
| **DC** | <i>M</i> &ge; 4.5 <b>and</b> <i>I</i> &ge; 2 | 0.8 Seconds |

<br>

**Channel Definitions:**

* **PWS (Public Warning Service):**
    This is the national cell broadcast sent to the public's mobile phones. It has the highest threshold (typically Intensity 4, though <i>I</i> &ge; 3 is the system setting) to avoid frequent, disruptive alerts.

* **TV (Television):**
    Alerts are sent to television broadcasters for on-air interruption or tickers.

* **DC (Direct Connections):**
    This is the **fastest** alert, sent directly from CWA to **specific end users**, and has the lowest threshold (M 4.5).
    * These (about 3800) end users are mostly **schools**, **disaster prevention agencies**, and **public transportation systems** (e.g., High-Speed Rail, Metro), as well as 15 private companies providing warnings to their customers.
    * This explains why sometimes a school's or building's alarm (DC) will sound, but a personal mobile phone (PWS) will not.

---

### Related Links

* **[Back to Home](index.html)**
* **[Next: AI-Assisted EEW](ai-eew.html)**