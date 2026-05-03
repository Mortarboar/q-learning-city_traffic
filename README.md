#  UrbanQ：基於 Q-Learning 強化學習之都市空間決策模擬器 
**(UrbanQ: Q-Learning Urban Spatial Decision Simulator)**
基於 Q-Learning 強化學習之都市空間決策與交通分流模擬器。探討 AI 如何在充滿路況阻力的都市路網中，演化出具備全域視野的最佳通勤動線。

![Open Source](https://img.shields.io/badge/Open%20Source-%E9%96%8B%E6%BA%90-success?style=for-the-badge&logo=open-source-initiative&logoColor=white)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-323330?style=for-the-badge&logo=javascript&logoColor=F7DF1E)
![Chart.js](https://img.shields.io/badge/Chart.js-FF6384?style=for-the-badge&logo=chartdotjs&logoColor=white)

>  **這是一個探討「人工智慧空間決策」與「都市交通動力學」的跨領域自主學習專題。**
> 透過從零建構的網頁版強化學習模擬器，驗證 AI 如何在充滿阻力（如塞車、死胡同）的都市路網中，演化出具備全域視野的最佳通勤動線。

###  線上體驗 (Live Demo)
本專案包含兩個漸進式的演化版本，請點擊下方連結直接在瀏覽器中體驗：

*  **[版本一] 基礎網格迷宮版 (Basic Maze Edition)**：[點此進入下載](https://github.com/Mortarboar/UrbanQ-Simulator/blob/main/basic.html)
  > *展示傳統 Q-Learning 演算法如何在絕對的牆壁與通道中尋找最短幾何路徑。*
*  **[版本二] 都市地形阻力版 (Urban Traffic Edition)**：[點此進入下載](https://github.com/Mortarboar/UrbanQ-Simulator/blob/main/index.html)
  > *專題核心成果 導入時間成本與地形權重（塞車、快速道路），模擬真實世界的動線分流。*

---

##  專案簡介 (Project Overview)

在傳統的資訊科學中，尋徑演算法往往只追求「最短幾何路徑」；但在真實的都市規劃中，通勤的成本是由「時空距離（路況阻力）」所決定的。

本專案不使用任何現成的機器學習套件，完全採用原生 JavaScript 從零實作 Q-Learning 底層演算法（貝爾曼方程式），並搭配 HTML5 Canvas 與 CSS3 建構高互動性的視覺化介面。專案從單純的「網格迷宮」出發，最終升級為具備「地形阻力（Terrain Weights）」的都市交通模擬器。

透過本系統，我們可以觀察到 AI 代理人（Agent）如何像真實世界的通勤者一樣，為了避開嚴重的交通壅塞，主動放棄直線捷徑，選擇繞道快速道路，進而達成交通動線的**全域最佳化（Global Optimization）**。

---

##  核心功能 (Key Features)

### 1. 互動式都市地圖編輯器 (僅限都市版)
提供「地形畫筆」功能，使用者可自由在網格上繪製：
* 🟩 **住宅區 (起點)** & 🟥 **商業區 (終點)** ｜ Reward: +100
* ⬜ **一般道路** ｜ Reward: -1 (基準時間成本)
* 🟧 **塞車路段** ｜ Reward: -5 (嚴格時間懲罰)
* 🟪 **快速道路** ｜ Reward: -0.2 (鼓勵長途分流)
* ⬛ **建築物** ｜ Reward: -10 (實體障礙)

### 2. 動態參數控制面板 (Real-time Hyperparameter Tuning)
視覺化拖曳滑桿，無須修改程式碼即可即時觀察三大數學變數對 AI 行為的影響：
* **學習率 α (Learning Rate)**：AI 對新經驗的敏感程度。
* **折現因子 γ (Discount Factor)**：模擬通勤者的「遠見」。(低 γ = 短視近利；高 γ = 深謀遠慮)。
* **探索率 ε (Exploration)**：模擬尋找替代道路的意願。

### 3. 多模式訓練與即時視覺化
* 支援「單步執行」、「觀察動畫」與「高速批次運算」。
* 即時渲染 **Q-Table 熱力圖** 與 **最佳決策方向箭頭 (Policy Arrow)**，將 AI 的思考過程完全具象化。
* 整合 Chart.js，動態繪製 AI 學習收斂曲線，並內建數據降採樣（Downsampling）機制以維持前端效能。

---

##  實驗發現與跨域反思 (Academic Insights)

### 1. 樂觀初始值與被動探索 (Optimistic Initial Values)
在實測中發現，即便設定探索率 $\epsilon=0$（絕對貪婪、不主動探索），AI 最終仍能找出繞過塞車區的完美路線。經查閱文獻，此現象印證了 R.S. Sutton 所提出的「樂觀初始值」理論。因為系統初始 Q 值為 `0`，而都市路況皆為「負向懲罰（如塞車 -5）」，這種理想與現實的落差，迫使沒有探索意願的 AI 對眼前的塞車感到「失望」，進而被動地尋找出其他未知的替代道路。

### 2. 科技與都市空間的仿生對話
本專案中的 Q-Learning 代理人，其尋找最佳路徑的試錯過程，宛如著名生物實驗中的「黏菌（Slime mold）在東京地鐵網培養皿上的蔓延」。這證明了不論是單細胞生物的覓食本能、通勤者趨利避害的心理，還是強化學習的數學矩陣，其底層都遵循著同一套尋求「全域最佳化」的自然法則。

---

##  本機執行方式 (Installation & Usage)

本專案為純前端單頁式應用（SPA），無須安裝任何後端伺服器或 Node.js 環境。

1. 複製此專案到本機：
   ```bash
   git clone https://github.com/mortarboar/UrbanQ-Simulator.git
