# FaceRecognition
### [HackMD網址](https://hackmd.io/@fsxCZX7iQ3aJ2sYH5olAYw/HJM9mkfpK)
> 因為公式跑版，以防萬一我還是附上我Hackmd的連結。
### [GitHub網址](https://github.com/mrachelmon/FaceRecognition)
## 專案描述:
利用教授提供的資料庫，搭配使用LDA、PCA等做出一個人臉辨識模型
#### 教授給的步驟建議:
##### 步驟 1：
依據資料庫的影像格式，設計一個讀取pgm影像檔的函式。

##### 步驟 2：
每張人臉影像均為92x112=10304的灰階影像，讀取後請將其轉為10304x1的向量，即成為一個樣本。
資料庫共含有400張影像（40人，每人10張），訓練時請只用200張（每人取5張）。

##### 步驟 3：
利用PCA計算此200張影像的轉換矩陣，設法將維度從10304降至10, 20, 30, 40, 50維
以這些較低維度的樣本訓練出你所學過的任何分類器來進行辨識。
請比較不同維度的辨識率，並統計出混淆矩陣(Google一下這是什麼？)

##### 步驟 4：
請以降維後的樣本，繼續利用FLD(LDA)找出另一轉換矩陣，利用此矩陣轉換降維後的樣本（毋需降維只須轉換）為有較佳的類別分離度之新樣本。
以前述之辨識器再度評量辨識率以及統計混淆矩陣。
## 專案環境:
* Window10
* Python
* Jupyter
## 相關名詞:
### PCA
主成分分析(Principal Component Analysis, PCA)在機器學習內被歸類成為降維(Dimension reduction)內特徵擷取(Feature extraction)的一種方法，降維就是希望資料的維度數減少，但整體的效能不會差異太多甚至會更好。降維(Dimension reduction)是當資料維度數(變數)很多的時候，有沒有辦法讓維度數(變數)少一點，但資料特性不會差太多。
### LDA
線性區別分析(Linear Discriminant Analysis，LDA）是一種supervised learning，這個方法名稱會讓很人confuse，因為有些人拿來做降維(dimension reduction)，有些人拿來做分類(Classification)。

在降維度的方法上，LDA是PCA延伸的一種方法，PCA目標是希望找到投影軸讓資料投影下去後分散量最大化，但PCA不需要知道資料的類別。而LDA也是希望資料投影下去後分散量最大，但不同的是這個分散量是希望「不同類別之間的分散量」越大越好。所以LDA和PCA差異的部份，PCA是無監督式(unsupervised learning)方法，LDA多了這四個字(「不同類別」)是一種監督式(supervised learning)方法。
### SVM
SVM是一種監督式的學習方法，用統計風險最小化的原則來估計一個分類的超平面(hyperplane)，其基礎的概念非常簡單，就是找到一個決策邊界(decision boundary)讓兩類之間的邊界(margins)最大化，使其可以完美區隔開來。
### KNN
在圖型識別中，KNN演算法是一種用於分類和迴歸的無母數統計方法。在這兩種情況下，輸入包含特徵空間（Feature Space）中的k個最接近的訓練樣本。
* 在k-NN分類中，輸出是一個分類族群。一個物件的分類是由其鄰居的「多數表決」確定的，k個最近鄰居（k為正整數，通常較小）中最常見的分類決定了賦予該物件的類別。若k = 1，則該物件的類別直接由最近的一個節點賦予。
* 在k-NN迴歸中，輸出是該物件的屬性值。該值是其k個最近鄰居的值的平均值。
### 混淆矩陣
在機器學習領域和統計分類問題中，混淆矩陣是可視化工具，特別用於監督學習，在無監督學習一般叫做匹配矩陣。矩陣的每一列代表一個類的實例預測，而每一行表示一個實際的類的實例。之所以如此命名，是因為通過這個矩陣可以方便地看出機器是否將兩個不同的類混淆了（比如說把一個類錯當成了另一個）。
    ![](https://i.imgur.com/we1sp2B.png)


## 執行步驟:
### Step1:
導入dataset，其中包含了40個人的圖象，每個人又有10張圖，總共400張圖像。從每個人的圖像中隨機抽取五張圖當training_data，剩下的當testing_data，也就是說training_data and testing_data各有兩百張圖像。
### Step2:
使用sklearn的PCA指令降維到10維、20維、30維、30維、50維，在降到每個維度的時候皆利用sklearn.svm的SVC指令來分類，並使用sklearn.metrics的confusion_matrix統計出混淆矩陣，並畫出來。


### Step3 :
使用sklearn的LDA指令在各個維度的時候皆利用sklearn.svm的SVC指令來分類，並使用sklearn.metrics的confusion_matrix統計出混淆矩陣，並畫出來。

### Step4 :
同step2，只是分類器改為KNN

### Step5 :
同step3，只是分類器改為KNN
## 結果展示:
### 分類器:SVM
* #### Dimension = 10
    ![](https://i.imgur.com/orf0fVu.png)
* #### Dimension = 20
    ![](https://i.imgur.com/S8RoZBU.png)
* #### Dimension = 30
    ![](https://i.imgur.com/9utvlm4.png)
* #### Dimension = 40
    ![](https://i.imgur.com/KslgAcR.png)
* #### Dimension = 50
    ![](https://i.imgur.com/YSnKRh9.png)

### 分類器:KNN
* #### Dimension = 10
    ![](https://i.imgur.com/NNU4Jmv.png)
* #### Dimension = 20
    ![](https://i.imgur.com/h0518NI.png)
* #### Dimension = 30
    ![](https://i.imgur.com/4aj0bGg.png)
* #### Dimension = 40
    ![](https://i.imgur.com/XfKvfRx.png)
* #### Dimension = 50
* 
## 結論:
使用SVM分類器的時候比較難看出PCA跟LDA準確度的差異，隨著每一次隨機抽取的樣本不同倆著準確度間的差異都有些許的變化，而使用KNN分類器的後準確度差異值就比較明顯了，即使每一次抽舉的樣本都不一樣，但LDA的準確度都比PCA的準確度來的高。
## 心得感想:
我覺得作業二相較於作業一比較沒有讓我產生太大的困擾，除了前期在了解機器學習中的分類器跟PCA以及LDA這些相關內容時花比較多的時間外，後面開始寫程式後就比較順暢地完成了，其中很大一部份原因是因為我PCA & LDA & SVM & KNN都是直接使用sklearn函式庫的原因，原本我想自己寫但不知道在哪裡出了錯誤一直有error，因為繳交期限將近，所以還是乖乖地用回函式庫，但我還是不會放棄的，在寒假的時候我會繼續研究該如何自己定義，後續若有成功會在做更新。

## 參考資料:
[【SciKit-Learn學習筆記】7：PCA結合SVM做AT&T資料集人物影象分類](https://www.itread01.com/content/1545795842.html)

[混淆矩阵confusion matrix的创建方式（可视化）](https://blog.csdn.net/qq_33590958/article/details/103443215)

[python机器学习-LDA和PCA](https://zhuanlan.zhihu.com/p/352896755)

[fit_transform,fit,transform区别和作用详解](https://blog.csdn.net/weixin_38278334/article/details/82971752)

[Comparison of LDA and PCA 2D projection of Iris dataset](https://scikit-learn.org/stable/auto_examples/decomposition/plot_pca_vs_lda.html)

[【機器學習懶人包】從數據分析到模型整合，各種好用的演算法全都整理給你啦！](https://buzzorange.com/techorange/2019/08/13/machine-learning-algorithm-collection/)

[[python] 混淆矩陣分析圖](https://honglung.pixnet.net/blog/post/214669413-%E6%B7%B7%E6%B7%86%E7%9F%A9%E9%99%A3)

[機器/統計學習:主成分分析(Principal Component Analysis, PCA)](https://chih-sheng-huang821.medium.com/%E6%A9%9F%E5%99%A8-%E7%B5%B1%E8%A8%88%E5%AD%B8%E7%BF%92-%E4%B8%BB%E6%88%90%E5%88%86%E5%88%86%E6%9E%90-principle-component-analysis-pca-58229cd26e71)

[機器學習: 降維(Dimension Reduction)- 線性區別分析( Linear Discriminant Analysis)](https://chih-sheng-huang821.medium.com/%E6%A9%9F%E5%99%A8%E5%AD%B8%E7%BF%92-%E9%99%8D%E7%B6%AD-dimension-reduction-%E7%B7%9A%E6%80%A7%E5%8D%80%E5%88%A5%E5%88%86%E6%9E%90-linear-discriminant-analysis-d4c40c4cf937)