---
# /docs/ai-eew.md (中文)
title: AI 輔助地震預警
layout: default
---

<p style="text-align: right;">
  <a href="en/ai-eew.html"><strong>Switch to English</strong></a>
</p>

# 🤖 AI 輔助地震預警 (AI-EEW)

傳統的地震預警系統（如前一頁所述的「有效震央法」）在「速度」與「準確度」之間存在一定的權衡。為了追求更快的警報，我們必須在地震P波剛抵達的最初幾秒內做出決策，但此時的資訊量往往有限。

為了突破這個限制，CWA 正積極與**國立臺灣大學 (NTU)** 的研究團隊合作，導入**人工智慧 (AI) 與深度學習 (Deep Learning)** 技術，以期在更短的時間內，做出更準確的預警判斷。

---

## AI-EEW 的核心目標

此合作計畫的核心目標，是利用 AI 模型強大的模式識別能力，來解決傳統演算法的兩大痛點：

1.  **更快的 P 波識別 (Faster P-wave Detection):**
    * 傳統方法需要多站觸發並進行關聯（如 `TCPD` 模組）。
    * AI 模型（如 CNN 或 Transformer）被訓練來**直接從單站的即時波形中**，辨識出微弱的 P 波訊號，並**即時判斷**是否為地震事件，這有潛力將「測站觸發」的時間點大幅提前。

2.  **更準確的早期預估 (More Accurate Early Estimation):**
    * AI 模型可以直接學習「P波前幾秒的波形特徵」與「最終地震規模 / 震度」之間的複雜關係。
    * 這使其有能力在極短的資料窗（例如 3-5 秒）內，就估算出比傳統公式（如 <i>M<sub>pd</sub></i> 公式）更穩健的規模與震度。

**最終目的：** 透過 AI 技術,進一步**縮短預警解算時間**（例如從 7.9 秒再縮短），並**擴大有效預警的範圍**（即縮小預警盲區）。

---

## AI 研發範例 1：震度等級預估模型

下圖展示了 CWA 與台大合作開發的「AI 震度預估模型」架構之一。此模型的核心是**僅使用 P 波抵達後的 3 秒鐘資料**，來快速預估該測站的最終震度。

![AI 地震震度預估模型架構 (CNN + Transformer)](./assets/img/ai-eew-model-architecture.png)
*圖1：AI 地震震度預估模型架構 (CNN + Transformer)。*

如圖所示，模型的運作流程如下：

1.  **多重特徵輸入 (Input Features):**
    模型不只使用原始的**加速度波形 (acceleration waveforms)**，還透過積分和傅立葉轉換，額外產生了**速度波形 (velocity waveforms)** 與**頻譜 (frequency spectrum)**。
2.  **特徵擷取 (CNN):**
    三種特徵分別被送入各自的卷積神經網絡 (CNN) 中，以擷取關鍵局部特徵。
3.  **整合與轉換 (Transformer):**
    擷取出的特徵被「正規化並串接」(Normalize & Concatenate) 起來，接著通過一個 **Transformer** 模型，以捕捉特徵之間的時間關聯性。
4.  **輸出 (Output):**
    最終，模型會輸出一系列機率，對應到該測站最終將觀測到的**震度等級** (Intensity 0 至 Intensity 5+)。

---

## AI 研發範例 2：PGA 閾值預估 (2024 花蓮地震)

下圖展示了另一個利用 AI 預估 PGA（地表峰值加速度，震度的重要指標）的範例，以及它在 2024 年花蓮地震的實際應用情形。

![AI (CNN) 預估 PGA > 80 gal 的流程與 2024 花蓮地震案例](./assets/img/ai-eew-cnn-example.jpg)
*圖2：AI (CNN) 預估 PGA > 80 gal (約震度 5+) 的流程與 2024 年 4 月 22 日花蓮地震 (規模 5.5) 案例。 (Chiang et al., 2022)*

此模型的工作流程更為直接：

1.  **輸入 (Input):** 系統從即時監測網路中接收到地震事件，取得測站的**三軸加速度波形** (P波前 3 秒資料)。
2.  **特徵擷取 (Feature extraction):** 系統將 P 波資料送入 **CNN（卷積神經網絡）**。
3.  **分類 (Classification):** CNN 擷取出特徵後，由一個**全連接網絡 (Fully connected network)** 進行分類，最終透過 Softmax 輸出場址 PGA 是否會大於 80 gal (約震度 5+) 的機率。

**實例應用 (圖右下):**
在 2024 年 4 月 22 日的花蓮地震（規模 5.5）中，此 AI 系統成功運作：

* **LINE Notify 警報 (圖右上):** 系統在 17:08:46.174654 發出警報，指出「**目前有3個測站預測PGA > 80**」（水璉國小、溪口國小、大樂國小）。
* **成效：** 如右下角文字所述，此 AI 系統**大約在 7 秒內**即可針對花蓮地區發出警報，展現了 AI 在爭取預警時效上的巨大潛力。

---

## AI 研發範例 3：臺灣 Transformer 搖晃警報模型 (TTSAM)

CWA-NTU 合作的另一項前瞻研究是「臺灣 Transformer 搖晃警報模型 (Taiwan Transformer Shaking Alert Model, TTSAM)」。此模型的目標是利用 Transformer 的強大能力，來整合**多個測站**的資訊，以輸出更精確的 PGA (地表峰值加速度) 機率分佈。

![臺灣 Transformer 搖晃警報模型 (TTSAM) 架構圖](./assets/img/ai-eew-ttsam-model.png)
*圖3：臺灣 Transformer 搖晃警報模型 (TTSAM) 架構圖。*

1.  **特徵擷取 (Feature extraction):**
    * 系統內的 25 個測站（Station 1... Station 25）各自的 15 秒波形資料被送入專屬的 CNN 模型，以擷取特徵圖 (Feature map)。
    * 這些特徵與測站的「位置編碼」(Positional embedding) 和「目標測站資訊」(Target information) 相結合。

2.  **特徵組合 (Feature combination):**
    * 所有測站的特徵矩陣被送入一個 **Transformer 編碼器 (Transformer Encoder)**。
    * Transformer 的「自注意力機制」能夠動態地權衡**不同測站**在此時此刻的重要性，有效地整合全域的地震波場資訊。

3.  **PGA 預估 (PGA estimation):**
    * 最終，模型輸出的不是單一的 PGA 數值，而是**PGA 的機率密度函數 (Probability density functions)**。
    * 這種機率式的輸出，能更完整地表達預估的不確定性，為未來的預警決策提供更豐富的依據。

---

## AI 研發範例 4：單站 AI 地震預警 (Onsite AI Method)

除了使用 AI 進行全區的震度預估，CWA-NTU 也在研發「**單站 AI 預警**」(Onsite AI Method)，這是一種速度更快的預警模式，專門用於**解決震央盲區**的問題。

![單站 AI 預警 (Onsite AI Method) 示意圖](./assets/img/ai-eew-onsite-model.jpg)
*圖4：單站 AI 地震預警 (Onsite AI Method) 流程與成效示意圖。*

如上圖所示，此方法不需等待多站關聯：

1.  **單站觸發：** 位於震央附近的單一測站（藍色圓圈）偵測到 P 波。
2.  **AI 即時分析：** 系統僅擷取**P波前 3 秒**的資料（`Use 3 sec P wave`），並立即送入 AI 模型（圖中的 CNN 模型）。
3.  **鄉鎮警報：** AI 模型**直接預估**鄰近鄉鎮的震度（如圖左地圖所示），並發布警報（`Provide Warnings !!!`）。
4.  **爭取時效：** 在此案例中（2024-04-02 花蓮地震），此方法成功在 S 波（強震動）抵達前，爭取到了 **15 秒的預警時間**（`Have 15 sec leading time`）。

這種 Onsite 方法對於**震央極近區域**（即傳統的預警盲區）的警報發布，具有極高的應用價值。

---

## 🚀 互動式 AI 預警 Demo (Hugging Face)

為了展示 AI-EEW 系統的實際成效，我們已將此模型部署於 Hugging Face Spaces，提供互動式的操作介面。

此 Demo 允許您選取歷史地震事件，並觀察 AI 模型如何即時分析波形、偵測 P 波，並快速給出地震規模與震度的預估值。

> **[請將下方 `[請貼上您 AI-EEW 的 HF Space 連結]` 替換成您 Hugging Face Space 的網址]**

<iframe
	src="[請貼上您 AI-EEW 的 HF Space 連結]"
	frameborder="0"
	width="100%"
	height="1000"
></iframe>

---

### 相關連結

* **[返回首頁](index.html)**
* **[返回：CWA 地震預警 (EEW)](eew.html)**
* **[下一步：攤位現場即時展示](live-demo.html)**