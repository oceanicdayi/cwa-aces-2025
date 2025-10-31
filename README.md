# CWA Seismic Network and AI Early Warning System @ ACES Conference

Welcome! This repository contains all the resources, links, and information for the **Central Weather Administration (CWA) booth** at the ACES Conference.

## 🚀 Main Information Hub (GitHub Pages)

All detailed information, system architectures, case studies, and live demos are consolidated on our main project website.

➡️ **[Visit the CWA @ ACES Website Here](https://oceanicday.github.io/cwa-aces-2025/)** ⬅️

*(The website is available in both English and Traditional Chinese. Please use the language toggle in the top-right corner.)*

---

## ⚡ Interactive Demos

Get hands-on with our systems! We have deployed several interactive applications on Hugging Face Spaces and Dify for you to explore.

| Application / Demo | Description | Link |
| :--- | :--- | :--- |
| 🤖 **AI-EEW (TTSAM) Demo** | An AI model (Transformer) for advanced shaking alerts. | **[Try on Hugging Face](https://huggingface.co/spaces/SeisBlue/TTSAM)** |
| 💬 **AI Assistant (Dify)** | Ask our AI assistant questions about CWA's systems. | **[Ask the Bot](https://udify.app/workflow/ZGqKFFhE2yCmYrv1)** |
| 🔔 **Taiwan EEW Messages** | A dashboard displaying real-time EEW alerts in Taiwan. | **[Try on Hugging Face](https://huggingface.co/spaces/cwadayi/streamlit_alarm_Taiwan)** |
| 🌊 **Taiwan Seismic Waveforms** | An interactive tool to view and browse seismic waveforms. | **[Try on Hugging Face](https://huggingface.co/spaces/cwadayi/streamlit_obspy)** |
| 🗺️ **Global Epicenters** | A Streamlit app to visualize global earthquake epicenters. | **[Try on Hugging Face](https://huggingface.co/spaces/cwadayi/streamlit)** |
| 📊 **Live Monitoring Dashboard** | A real-time dashboard for earthquake monitoring and location. | **[Try on Hugging Face](https://huggingface.co/spaces/cwadayi/earthquake_monitoring)** |
| 📈 **Intensity Data Dashboard** | A Grafana-like dashboard for seismic intensity data. | **[Try on Hugging Face](https://huggingface.co/spaces/cwadayi/Grafana_like_2)** |

---

## 🏛️ Project Overview

This project showcases the end-to-end workflow of CWA's seismic monitoring and warning capabilities, divided into four core themes:

1.  **CWA Seismic Network:**
    An in-depth look at CWA's robust infrastructure, including the **TSMIP** (603+ stations) and **CWASN** (borehole, broadband, OBS) networks. It also features the extensive **Grafana dashboards** used for 24/7 system health, latency, and data monitoring.

2.  **CWA EEW System:**
    A detailed breakdown of CWA's operational **Earthquake Early Warning (EEW)** system. This includes the science (P/S waves), the "Effective Epicenter Method" algorithm, the Earthworm data flow, and a case study on the **2025 Dapu Earthquake**, which demonstrates the system's speed (7.9s warning) and accuracy (90%).

3.  **AI-Assisted EEW:**
    A showcase of our collaborative R&D with **National Taiwan University (NTU)**. This section details several advanced AI models (CNN, Transformers) like **TTSAM** and **Onsite-AI**, which are designed to further shorten warning times and conquer the epicentral "blind zone."

4.  **Live Booth Demo:**
    An introduction to the physical demo at our booth: a **Raspberry Shake 1D + Raspberry Pi** streaming live, local seismic data. Come by and do the "stomp test" to see the waveforms you create in real-time!

---

## 🛠️ Technical Resources

For researchers and developers, we provide the following open-source resources:

* **Docker Hub Image:**
    The CWA EEW system (based on Earthworm) is available as a Docker image, including source code, parameters, and test data.
    * `cwadayi/earthworm_ubuntu22.04_eew`
    * **[View on Docker Hub](https://hub.docker.com/r/cwadayi/earthworm_ubuntu22.04_eew)**

* **Seismic Data (GDMS):**
    All CWA seismic data (CWASN, TSMIP) is available for free.
    * **[Access Data via GDMS](https://gdms.cwa.gov.tw/)**
    * *(Note: Requires free registration. Real-time data has a 15-minute delay.)*

* **Sample Code:**
    This repository contains sample code and configuration files used for our demos.

## 🇹🇼 About the CWA

The **Seismological Center** of the Central Weather Administration (CWA), Taiwan, is the official agency responsible for monitoring seismic activity, issuing earthquake reports, and providing real-time earthquake early warnings to protect the public.

---
---

# CWA 地震觀測網與 AI 預警系統 @ ACES 研討會

歡迎！本 GitHub Repo 包含了**中央氣象署 (CWA)** 於 ACES 研討會攤位的所有資源、連結與相關資訊。

## 🚀 資訊總站 (GitHub Pages)

所有詳細的系統架構、案例研究、技術細節與互動 Demo，都已彙整於我們的主要計畫網站。

➡️ **[點此參觀 CWA @ ACES 網站](https://oceanicday.github.io/cwa-aces-2025/)** ⬅️

*(本網站提供中、英文雙語版本，您可在頁面右上角切換語言。)*

---

## ⚡ 互動體驗區 (Live Demos)

歡迎您親自動手操作！我們已將多個互動式應用程式部署於 Hugging Face Spaces 與 Dify 供您探索。

| 應用程式 / Demo | 說明 | 連結 |
| :--- | :--- | :--- |
| 🤖 **AI-EEW (TTSAM) Demo** | (與台大合作) 先進的 Transformer AI 地震預警模型。 | **[點此體驗 (Hugging Face)](https://huggingface.co/spaces/SeisBlue/TTSAM)** |
| 💬 **AI 智能助理 (Dify)** | 對 CWA 系統有疑問嗎？直接詢問我們的 AI 助理。 | **[點此提問 (Dify)](https://udify.app/workflow/ZGqKFFhE2yCmYrv1)** |
| 🔔 **台灣地震預警訊息** | 顯示台灣即時地震預警訊息的儀表板。 | **[點此體驗 (Hugging Face)](https://huggingface.co/spaces/cwadayi/streamlit_alarm_Taiwan)** |
| 🌊 **台灣地震波形紀錄** | 互動式工具，用以瀏覽台灣的歷史地震波形。 | **[點此體驗 (Hugging Face)](https://huggingface.co/spaces/cwadayi/streamlit_obspy)** |
| 🗺️ **全球地震震央** | 顯示全球地震震央的 Streamlit 應用程式。 | **[點此體驗 (Hugging Face)](https://huggingface.co/spaces/cwadayi/streamlit)** |
| 📊 **即時地震監測儀表板** | 一個即時的地震監測與定位儀表板。 | **[點此體驗 (Hugging Face)](https://huggingface.co/spaces/cwadayi/earthquake_monitoring)** |
| 📈 **地震震度資料儀表板** | 一個類 Grafana 風格的地震震度展示儀表板。 | **[點此體驗 (Hugging Face)](https://huggingface.co/spaces/cwadayi/Grafana_like_2)** |

---

## 🏛️ 計畫總覽

本計畫旨在展示 CWA 從地震監測到預警發布的完整端到端工作流程，分為四大核心主題：

1.  **CWA 地震觀測網:**
    深入介紹 CWA 強大的基礎設施，包含 **TSMIP** (603+ 個測站) 和 **CWASN** (井下、寬頻、海底地震儀) 觀測網。同時展示 CWA 用於 24/7 全天候監控系統健康、延遲與資料的 **Grafana 儀表板**。

2.  **CWA 地震預警系統 (EEW):**
    詳細分解 CWA 現行的**地震預警 (EEW)** 系統。內容包含科學原理 (P/S波)、核心的「**有效震央法**」演算法、Earthworm 系統內的資料流，以及「**2025 年大埔地震**」的案例研究，證明系統的速度 (7.9秒) 與準確度 (90%)。

3.  **AI 輔助地震預警 (AI-EEW):**
    展示 CWA 與**國立臺灣大學 (NTU)** 的合作研發成果。此部分詳細介紹了多種先進 AI 模型 (CNN, Transformer)，例如 **TTSAM** 和 **Onsite-AI (單站預警)**，其設計目標是進一步縮短預警時間並攻克「預警盲區」。

4.  **攤位現場即時展示:**
    介紹我們在攤位上實體展示的設備：一台 **Raspberry Shake 1D + Raspberry Pi (樹莓派)**，正即時串流本地的地震訊號。歡迎您到攤位「跺腳」，親眼看看您製造的地震波形！

---

## 🛠️ 技術資源

我們為研究人員和開發者提供了以下的開源資源：

* **Docker Hub 映像檔:**
    CWA 的 EEW 系統（基於 Earthworm）已被打包為 Docker 映像檔，包含原始碼、參數檔與測試資料。
    * `cwadayi/earthworm_ubuntu22.04_eew`
    * **[點此前往 Docker Hub](https://hub.docker.com/r/cwadayi/earthworm_ubuntu22.04_eew)**

* **地震資料 (GDMS):**
    所有 CWA 的地震資料 (CWASN, TSMIP) 均可免費下載。
    * **[點此前往 GDMS 網站](https://gdms.cwa.gov.tw/)**
    * *(註：需免費註冊。即時資料有 15 分鐘的延遲。)*

* **範例程式碼:**
    本 Repo 中包含了我們用於 Demo 的範例程式碼與設定檔。

## 🇹🇼 關於 CWA

**交通部中央氣象署 (CWA) 地震測報中心** 是臺灣官方的地震監測機構，負責監測地震活動、發布地震報告，並提供即時的地震預警，以保障民眾安全。