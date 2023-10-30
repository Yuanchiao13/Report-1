#南華大學跨領域-人工智慧期中報告
主題:初學者的 TensorFlow 2.0 教程
組員: 11118111李遠樵
#作業流程
1、首先将 TensorFlow 導入程序：
python
import tensorflow as tf
![image](https://github.com/Yuanchiao13/Report-1/blob/main/1698201427621.jpg)
2、加载 MNIST 數據集。將樣本數據從整數轉換為浮點數：
![image](https://github.com/Yuanchiao13/Report-1/blob/main/2.jpg)
3、通過堆疊層来構建 tf.keras.Sequential 模型。
![image](https://github.com/Yuanchiao13/Report-1/blob/main/3.jpg)
4、對於每个样本，模型都會返回一个包含 logits 或 log-odds 分数的向量，每個類一個。
![image](https://github.com/Yuanchiao13/Report-1/blob/main/4.jpg)
5、tf.nn.softmax 函数將這些 logits 轉換為每個類的概率：
![image](https://github.com/Yuanchiao13/Report-1/blob/main/5.jpg)
6、使用 losses.SparseCategoricalCrossentropy 為训练定義损失函数，它會接受 logits 向量和 True 索引，並為每个樣本返回一个標量损失。
![image](https://github.com/Yuanchiao13/Report-1/blob/main/6.jpg)
7、此损失等於 true 類的負對數概率：如果模型确定類正确，则损失為零。這個未經訓练的模型给出的概率接近隨機（每個類為 1/10），因此初始损失應該接近 -tf.math.log(1/10) ~= 2.3。
![image](https://github.com/Yuanchiao13/Report-1/blob/main/7.jpg)
8、在开始训练之前，使用 Keras Model.compile 配置和編譯模型。将 optimizer 類設置為 adam，将 loss 设置為您之前定義的 loss_fn 函数，並通過将 metrics 參數设置為 accuracy 来指定要為模型评估的指標。
![image](https://github.com/Yuanchiao13/Report-1/blob/main/8.jpg)
9、使用 Model.fit 方法调整模型参数並最小化损失：
![image](https://github.com/Yuanchiao13/Report-1/blob/main/9.jpg)
10、Model.evaluate 通常會在 "Validation-set" 或 "Test-set" 上檢查模型的性能。
![image](https://github.com/Yuanchiao13/Report-1/blob/main/10.jpg)
11、在完成上述的步驟後這個照片分類器的准确度已经達到 98%。這個機械學習模型也完成了
##參考資料:https://tensorflow.google.cn/tutorials/quickstart/beginner?hl=zh_cn



