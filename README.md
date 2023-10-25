#南華大學跨領域-人工智慧期中報告
主題:初學者的 TensorFlow 2.0 教程
組員: 11118111李遠樵
#作業流程
1、首先将 TensorFlow 導入程序：
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
![image](
