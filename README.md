
# PrivateLink: Privacy-Preserving Integration and Sharing of Datasets
:heavy_exclamation_mark:為避免格式跑掉請點擊右方HackMD連結開啟
## 主要內容  
提出一方法用以在一群組間共享數據時能做到隱私保護，且此方法能在效率、保密性、實用性三者中取得合理平衡。  
此方案可在保護隱私的方式下，使用個人特定數據庫集成(數個由多個身份屬性組成的數據集成)。

## 核心概念  
**此方案之主要核心為新的 Interactive protocol : PrivateLink。**    

## 簡要概念說明  

- 透過 PrivateLink，參與者可透過 **獨立且不受信任的** 第三方隨機分配其數據集(dataset)。
- 再由群組內其他參與者，將其結果與其他結果與其他數據集合併。
- 第三方回傳之資料可由群組間參與者檢驗其正確性。
-  **不需參與者之間密鑰共享**  (?)
This is particularly useful  for private, fine-grained integration of network traffic data.
- 通過此方法，代理商提供的數據集可以合併，在任何其他授權機構之間共享，但不會損害到合併數據集中的特定個人。

## 與先前已存在之方案差別

- 先前已存在之解決方案受下方限制 : 
  1. 安全可信任的第三方
  2. 要求參與者間共享密鑰。
- 現有的無密鑰解決方案 (使用 keyless cryptographic hash function生成、比較 ID 的 hash值)不安全 ! 且此方法不考慮數據整合(Data integration)。
- 獨立的代理商或不受信任的第三方反過來扮演整合來自不同機構數據集的促進者。

## 欲達到之目標  
==**A. Privacy**== 
不受信任的第三方（服務器）處理來自不同機構的單個數據集(客戶)，而無需學習關聯的原始身份屬性。此外，實體（例如客戶，數據分析師或攻擊者）掌握合併後的
數據集將無法重新標識與任何記錄關聯的原始屬性。

==**B. Verifiability** (可驗證性)==
我們通過 PrivateLink，在代理機構和不受信任的第三方之間共同地隨機化數據集。
<font color="#83D3E4">**-基於密鑰同態加密之遺忘的偽隨機函數** </font>
**(Oblivious pseudorandom function based on key homomorphic encryption)：**
 我們使用密鑰同構運算在客戶端和服務器之間構建兩方協議，用以計算遺忘的偽隨機函數。服務器使用該功能來屏蔽ID記錄，使得服務器無法得知關於原始ID的任何信息、客戶端也不會得到服務器用來致盲之密鑰的任何信息。
<font color="#83D3E4">**-基於零知識證明的可驗證性** </font>
 通過零知識證明領域的技術可實現可驗證的遺忘偽隨機函數。它允許客戶端驗證服務器是否已正確使ID致盲。
## 四大特色
- 透過不信任的第三方，支持組織中共享和多個數據集集成，且不會損害任何人的身份信息。
- 它使隱私保留數據集(privacy-preserved datasets)的正確性可被驗證且不會向第三方透露任何敏感信息。
- 參與者間不需要為了共享和集成數據集而共享密鑰，客戶端和服務器的密鑰管理變得更加簡單。
- 因為架構是通用的，所以可以獨立，這使得此解決方案有可擴展性。
## <font color="#D34343">零知識證明: </font>
引用麻省理工學院多媒體實驗室（MIT Media Lab）對零知識證明的解釋：
> 你手上有兩顆撞球，分別是綠色和紅色，除了顏色之外這兩顆撞球一模一樣。假設我是紅綠色盲，因此，就我看來你手上拿的是兩顆一模一樣的撞球。
問題來了，請問你是否能在不提到任何顏色資訊的前提下，說服我這個色盲相信這兩顆球的顏色，確實不同？
當然可以！
你只要把兩顆球交給我這個色盲，然後要我拿到背後去隨意變換左右順序之後，再拿出來讓你「猜」原本在左手的球，現在換到了哪一手。
對你來說，你一眼就可以判斷本來左手拿的是綠色，現在綠色跑到右手去，根本不用猜，很輕易就能指出球換位置了。但是，這對色盲來說簡直驚訝！因為就我看來，這是完全相同的兩顆球，你肯定只是運氣好猜中的。
不過，只要重複做個幾次測試，我很快就會相信你說的，這兩顆球肯定有哪裡不同，只是我看不出來。而且，你也完全沒有透露任何關於顏色的資訊。
這就叫做零知識證明。
* 證明者向驗證者證明自己擁有某一特定數據，但不透露任何該數據內容
* 分為<font color="#549CE1 "> 交互式</font> /<font color="#549CE1 "> 非交互式</font>  (驗證者和示證者之間是否直接通訊)
* 特性:
  1. <font color="#D82F24 "> **完備性**</font>: 
  若雙方皆若雙方皆誠實且進行正確的證明過程與計算，則驗證必通過。
  2. <font color="#D82F24 "> **正確性**</font> (合理性/穩定性):
     若證明者沒有該數據，則近乎不可能通過驗證。
  3. <font color="#D82F24 "> **零知識性**</font>:
     驗證方不會得到任何關於該數據之內容。
- 零知識運用到的核心關鍵: <font color="#7DCD5E  ">**同態隱藏**</font>
  - 滿足同態隱藏的一對一~~函式~~排列f(x)定義
    1.難透過f(x)回推x
    2.不同x導致不同f(x)
        3.若已知f(x)和f(y)，可得到f(x+y)
        //此處"+"表特殊運算元   
### <font color="#D34343">同態加密: </font>
設x , y為原始數據之代稱；f為加密函數f(x)；f^-1^表其反函數。
//此處"+"亦表特殊運算元 
$$f(x+y) = f(x) + f(y)$$
設 $R = f(x+y)$ 則 $f^{-1}(R) =f^{-1}(f(x)+f(y))=x+y$
  
- 此文中採用
  令q為subgroup的size，p為<font color="#BE88D7 ">二次剩餘循環組</font>的order(循環回第一個需要多少個)，p = 2q + 1,其中q 為 prime。文中之同態加密算法被定義為 F~k~(ID) := H(ID)^k^ % P，其中 H:{0,1}^*^ → {1, 2, … ,q-1}產生隨機組元素。
  此時，$(H(ID)^{k1} mod  P)^{k2} mod P = H(ID)^{k1k2} mod P = (H(ID)^{k2} mod P)^{k1} mod P$ <font color="#7DCD5E  ">(**指數律**)</font>
  
  :heavy_exclamation_mark:F is deterministic，不能保證安全(但這是此PPDI解決方案所需的屬性)  :arrow_right: 使用橢圓曲點乘法(elliptic curve point multiplication)提高效能 (?)
  
## 方案概述
:::info
:pushpin: 圖例:
C : client
S : Server
F~k~( ) : 用密鑰(k)的同態加密函數
H( ) : 偽隨機函數
ZKP : Zero-Knowledge Proof

:::
 - 除了ID列外只有一非身份屬性列(Att) => (ID,Att)
 ==**But**== <font color="green"> **這協議可支援多個非身份屬性列**</font>
 - 此方案假設 Server 和 Client 的key在不同的目標Dataset時會刷新
 ###  <font color="orange">PrivateLink</font>
 
### <font color="#549CE1 ">**集成**</font>- Between C1 & C2

 兩Dataset  D~1~ = (<δ~i~ ,Att~i~>)^n^~i=1~和 D~2~ = (<δ'~i~ , Att'~i~>)^n'^~i=1~
 
 (a) 若 ==**$δ_i\in D_1 = δ'_j\in D_2$**==
     =>合併兩者<δ~i~ , Att~i~>和<δ'~j~ , Att'~j~>成<δ~i~ , Att~i~ , Att'~j~>
     
 (b) 若 ==**$δ_i\in D_1$，但 D~2~無**==
 =>存成<δ~i~ , Att~i~ , NULL>
 
 (c') 若 ==**$δ'_j\in D_2$，但 D~1~無**==
 =>存成<δ~i~ , NULL , Att'~j~>
 
 ## <font color="#549CE1 ">**所有流程**</font>- Between C & S
 ### <font color="#549CE1 ">**Key 建立**</font>
 C產生Key x；S產生Key y <font color="orange">//For 隨機化和致盲</font>
 Public key $(\alpha_0:=g , \beta_0:=g^y)$ <font color="orange">//For 零知識證明</font>
 ### <font color="#549CE1 ">**Generalization(泛化/一般化?)和隨機化**</font>
 1. C 先對 dataset 中的各個 Att~i~ 執行標準化匿名技術(generalization) 
 :arrow_right:  <font color="orange"> remove unique values</font>
 2. C 對 dataset 中的各個 ID~i~ 執行隨機化(using <font color="orange">cryptographic techniques</font>)
:arrow_right: 計算出 $\alpha_i=F_x(ID_i)$ ,for i =1 to n
 3. C 將隨機化後的ID列表$((\alpha_i)_{i=1}^n)$交給S
### <font color="#549CE1 ">**致盲和證明**</font>
  1. S對隨機ID序列致盲(由於ID已被隨機化，因此S不知原始ID)
:arrow_right:計算出$\beta_i=F_y(\alpha_i)$ ,for i =1 to n 
  2. S returns the blinded IDs ($(\beta_i)_{i=1}^n$) to C.
  3. S和C共同生成零知識正確性證明，以便C可以驗證是否成功致盲。
 ### <font color="#549CE1 ">**驗證和集成(Verification & Integration)**</font>
  1. 給定盲目ID，C 驗證收到的零知識正確性證明。
  2. C 將其blinded dataset與從其他客戶端獲得的其他數據集（由同一 S處理的）合併和集成。
  
  <font color="orange">集成由客戶端本身完成</font>，而無需與服務器進行任何交流。 因此C擁有最終合併的數據集。 
  
  ---
  ## <font color="#D34343">零知識證明於此方案 </font>
  - 簡單的方法:
  compute ZKP for every pair (αi, βi ) separately
  <font color="red">**缺點**</font> : 須較多的計算與通訊
  - 1. 由S致盲的方法可知，可知道
  $α_i = F_x (ID_i)$ and $β_i = F_y(α_i) = F_{xy}(ID_i)$
    2. 而 C 知道所有的$α_i 和 β_i$  
    
    :arrow_right: 
   S can prove to the C its knowledge of the key y(用於致盲) such that $\beta_0=\alpha_0^y$ <font color="#549CE1 ">且不透露y給C</font>
(其中$\alpha_0$由C提供，$\beta_0$由S提供)
- 同樣的，服務器可以向客戶端證明其知道密鑰y'使得$V'  =  U'^ {y'}$，同樣不洩露y'給C，其中由C計算出$U'=Π_i\alpha_i^{r_i}$ 和 $V'=Π_i\beta_i^{r_i}$ ($\alpha_i$亦由C提供，$\beta_i$由S提供)
$$Π_i\beta_i^{r_i}=V'=U'^{y}=(Π_i\alpha_i^{r_i})^{y}=(Π_i\alpha_i^{y})^{r_i}⇒Π_i(\frac{\beta_i}{\alpha_i^{y}})^{r_i}=1$$
:heavy_exclamation_mark:在固定$\alpha_i$，$\beta_i$ 和 $y=log_{\alpha_0}(\beta_0)$後， r~i~ 是由C從一指數空間(in security parameter)隨機選擇的。
 令 $w_i=\frac{\beta_i}{\alpha_i^y}$，g be a generator in the group，對各個$w_i$存在一特殊指數$e_i$，使得$w_i=g^{e_i}$，因此$$1=Π_iwi^{r_i}=g^{Σ_ie_i‧r_i}⇒Σ_ie_i‧r_i=0$$
 對於未知但固定之向量($e_0,…,e_n$)，C選擇一向量($r_0,…,r_n$)，每個$r_i$是從[1,2^λ^]中隨機選擇的，則此兩向量內積為零(互相垂直)的情況，有著不可輕忽的可能會發生。
 而此方案要的是當<font color="orange">($e_0,…,e_n$)為零向量</font>，因此$w_i=1$，也就是說 ==${\beta_i}={\alpha_i^y}$==
 //The zero knowledge nature of our protocol for n elements can be proved in the same way as in [43, Section 5] and [44].
 >[43] I. Damgård. On -Protocols. Accessed: Jan. 2019. [Online]. Available:http://www.cs.au.dk/~ivan/Sigma.pdf
 [44] Proof of Knowledge for Double Exponent. Accessed: Jan. 2019.[Online]. Available:https://courses.cs.ut.ee/MTAT.07.003/2016fall/
uploads/Main/0902-proof-of-knowledge-for-double-exponent.pdf
---
 ## <font color="#549CE1 ">**安全性**</font>
 在滿足隱私和可驗證性的理想功能下，來說明PrivateLink的安全性
 1. 假設F和H是安全的，PrivateLink安全地實現理想功能Fppdi。
    - 證明草圖：我們考慮了針對服務器的安全性和針對客戶端的安全性。 我們首先聲明基礎函數F的安全性，並假設H實例化的安全性，然後展示如何基於這些安全實例化來模擬C和S的視圖（假設對手既不能同時破壞服務器和客戶端 ）。
 2. 
 
---
### <font color="#BE88D7 ">**安全定義**</font>
:::info
 <font color="orange">Fppdi</font> : 為一理想功能,incorruptible(廉潔的) 第三方 ，作用於C和S之間(which captures the privacy and verifiability goals)
:::
<font color="#83D3E4">**對手模型與假設**:</font>
- 首先，假設有貢獻的客戶不會與其他客戶串通。
- 為遵循執行協議，客戶為半誠實的(semi-honest)。
:heavy_exclamation_mark: 我們無法阻止C故意與其他客戶共享其原始數據集
- 假設存在一個不受信任的獨立第三者(為服務器形式)，它可促成以隱私保護的方式集成多個數據集。
服務器可能是惡意的，即使數據集已被隨機化仍會被試圖刪除或修改。
:arrow_right: 最終，假設ID列只包含唯一條目

<font color="#83D3E4">**此方案方法**:</font>
保存每筆數據紀錄的身分信息 , 同時實現數據集的記錄級集成。
==**But**==
若對手有外在之背景知識，則個人身分信息可能洩露。
:arrow_right:此方案包含基本的泛化(generalization)技術 
用以最大限度地減少信息洩露，我們的解決方案可以通過針對非身份屬性值的<font color="orange">最新正交隱私保護技術(state-of-the-art orthogonal privacy preservation techniques)</font>得到進一步增強

---
### <font color="#BE88D7 ">**去識別化(De-identification)技術**</font>

-  <font color="#40B9D2 ">抑制(Suppression)</font> :移除部分資料以降低資料集的準確性
   - 紀錄抑制(Record suppression)：刪除單一資料(如偏離值)。
   - 區域抑制(Field suppression)：刪除敏感資料類別。
   - 遮罩(Masking)：將所有唯一識別符移除。
- <font color="#40B9D2 ">擬匿名化(Pseudonymization)</font> : 以擬匿名資料取代唯一識別符(unique identifiers)，保留不同資料庫之間的連結，但去除個人資料被識別的可能性。
   - 常用 : Hashing、匿名演算法等密碼學技術
-  <font color="#40B9D2 ">泛化(Generalization)</font> : 將原始資料修改至較概略的資料，但保留資料的準確性
   - 四捨五入(Rounding)
   - 上/下端編碼(Top/bottom coding)：針對資料的極值調整為大於或小於某個數值
-   <font color="#40B9D2 ">隨機(Randomization) </font> : 將原始資料內容修改為接近的資訊，以降低準確性
    - 加入雜訊(Noise addition)：對資料集中資料加入隨機數值，以降低識別可能性，但保持資料集的統計資訊正確。
    - 置換(Permutation)：保持原始資料，但將資料內容彼此交換。
-  <font color="#40B9D2 ">彚集(Aggregation)</font> : 用統計數據(如：平均、分布圖)替代原始資料 
---
## <font color="#D34343">最新正交隱私保護技術(state-of-the-art orthogonal privacy preservation techniques):</font>
for example, by adopting the<font color="#BE88D7 "> HIPAA</font> <font color="#549CE1 "> Expert Determination</font> or <font color="#549CE1 ">Safe Harbor</font> methods,the technical steps recommended in NIST publication on de-dentifying government datasets [33],<font color="#BE88D7 "> differential privacy</font> [22].

![hipaa](https://images.slideplayer.com/5/1487408/slides/slide_20.jpg) 

### <font color="#BE88D7 "> HIPAA</font>
美國「健康保險可攜式與責任法(Health Insurance Portability and Accountability Act，HIPAA)」主要是針對PHI(受保護之醫療資訊, Protected Health Information)所設計的去識別化方法
![hipaa](https://djhurij4nde4r.cloudfront.net/images/images/002/128/700/fullsize/HIPAA_De-identification.png?1512508444)

![](https://upload.cc/i1/2020/08/17/ntlZGp.jpg)



<font color="#549CE1 ">**「專家評估 (Expert Determination)」**</font>
- 透過評估下列4個原則來決定資料的安全與否。
  - <font color="#40B9D2 ">資料的可複製性(Replicability)</font>: 
  依照資料重複發生於個體的機率排序
  - <font color="#40B9D2 ">資料來源可用性(Data source Availability)</font>:
  是否容易從外部取得資料
  - <font color="#40B9D2 ">可辨識性(Distinguishability) </font>:
  決定醫療資料中個體資訊可以被區分的程度
  - <font color="#40B9D2 ">風險評鑑(Assess Risk)</font>:
  上述的可重複性、資源可用性、可識別性越高，其風險也越大
  
  將獨特可識別之號碼 Unique Identifying Numbers(病歷號碼、就醫地點)用亂數替代
  
 ==優點:== 可保留下來的訊息較多
 
 <font color="red">**缺點**</font> : 需要較多時間與人力成本
 
<font color="#549CE1 ">**「安全港法 (Safe Harbor)」**</font>
- 依照規定將指定之資料刪除
- 除規定之資料外，有些資料因為情況特殊(有該項特徵的人很少)需要手動調整。例如：如果資料裡面有人的職業是總統，則可能需要另外遮蔽該訊息。

==優點:== 執行簡單
 
 <font color="red">**缺點**</font> : 少數特殊情況很有可能會被忽略，從而導致個人資料洩漏。

Safe Harbor規定需要處理的資料:

![hipaa](https://www.iri.com/assets/uploads/editor/Infographics/PHI.png)  
> - 名字
  所有比「州」小的地理單位
與個人相關的所有日期要素（不包括年份），包括入院和出院日期，生日，死亡日期；而所有年齡超過89歲及其相關日期資料（含年份）合併為「90歲或以上」之單一類別
電話，手機和傳真號碼
電子郵件地址
IP地址
社會安全號碼
病歷號
健康計劃受益人編號
設備標識符和序列號
證書/許可證號
帳號
車輛標識符和序列號，包括車牌
網站網址
全臉照片和類似圖像
生物識別符（包括指紋和聲紋）
任何唯一的識別號碼，特徵或代碼

HIPAA會基於比例原則，考量資料效用是否會低於去識別化的成本

### <font color="#BE88D7 "> Differential privacy 差分隱私</font>
在查詢結果裡加入<font color="orange">隨機性</font>

- **差分隱私的核心思想** : 對於差別只有一條記錄的兩個數據集，查詢它們獲得相同值的概率非常非常的接近

任何一種方法，只要用在數據集上能滿足差分隱私的核心思想，那這個方法就是滿足差分隱私的。
最常用的方法是在結果上<font color="orange">加滿足某種分佈的噪音</font>(Noise addition)，使查詢結果隨機化。

目前常用的有兩種方法，一個是<font color="#549CE1 ">Laplace機制</font>，在查詢結果裡加入拉普拉斯分布的噪音（Laplace noise），適用於<font color="#40B9D2 ">數值型</font>輸出。
另外一個是<font color="#549CE1 ">指數機制</font>，在查詢結果裡用指數分佈來調整概率，適用於<font color="#40B9D2 ">非數值型</font>輸出。

數據量很大時，噪音的影響小，但若數據量小，噪音的影響就顯得比較大，會使得最終結果偏離準確值較遠而變得不可用。

>Data De-Identification Standardized implementation of Big Data:
Based on ISO/IEC 2nd WD 20889 [Online]. Available: https://cccisa.ccisa.org.tw/article/download/1915/1922
---

## 保留結構的數據集成

在前面的部分中，我們假設數據集的標識屬性可能會包含一些細分。一個示例是IPv4地址，其中一個地址（例如192.168.1.1）可以分為四個段，每段與其點分格式表示的一個八位位組相匹配（可以類似的方式應用於IPv6地址）。 IP地址段對於網絡分析至關重要，例如，以確定一組IP地址是否源自同一子網。
:heavy_exclamation_mark: 若失去這結構則數據集失去效用且價值有限，任何隨機化（或屏蔽）這類身份屬性的方法都必須保留其結構。

我們展示了如何部署PrivateLink以達成此目的，進一步證明了該協議的靈活性。
- 一種簡單的方法是將PrivateLink直接部署在每個段上，並將每個段視為單個標識屬性。
<font color="red">**缺點**</font> : 效率不佳
- 讓客戶選擇要隨機化的段落，並創建一個列表L，其中L包含這些所選段的標識符。只有列表中的片段要隨機化和盲化(分階段進行)。

我們的直覺是在大多數情況下與原始數據集做相比，第一個匹配項（交集）的結果數據集包含的記錄要少。接著處理第二個選定的分段，與第一個匹配後得出的較小數據集做匹配。
可以根據期望的匹配程度，對其餘段執行後續映射。
### <font color="#549CE1 ">**範例 A. IP Addresses**</font>
1. 將IP address分為4段( H(A) , H(A.B) , H(A.B.C) , H(A.B.C.D) )，此處的H(.)為<font color="#BE88D7 "> cryptographic hash function</font>，這種表示法保存了 IP address的前綴
:arrow_right: 是<font color="#EF8273">唯一</font>能維持IP address結構且不洩露資訊的方法
<font color="#EF8273">Client可能希望找到在H(A.B)和較後段H(A.B.C)的映射(mapping)</font>
2. 首先 Client 隨機化(randomizes)上述4段，然後如同 PrivateLink 對非身分屬性Att~i~ 做泛化(generalizes)
3. Client 創建一列表L，列表中包含2個識別符，一個用於H(A.B)，另一個用於H(A.B.C)。
4. Client 和 Server 選取列表中H(A.B)的識別符，找回H(A.B)並一同對其執行隨機化與致盲以在其他客戶提供的Dataset找到匹配資料。
> TCPdpriv [52],Crypto-PAn [31] and proposals in [60].
<font color="#EF8273">The lookup table (randomized IP addresses) or key (produces pseudonymized IP addresses) must be shared between the parties that perform pseudonymization.</font>
:arrow_right: 在每個參與者都給定 lookup table 或 key的情況下，Dataset可能被知曉，不符合我們想達到的目的。
 
