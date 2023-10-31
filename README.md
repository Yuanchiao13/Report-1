#南華大學跨領域-人工智慧期中報告

主題:初學者的 TensorFlow 2.0 教程

組員: 11118111李遠樵、11115022陳廷羽、11115004林彥佑

#作業流程

1、首先将 TensorFlow 導入程序：

```python
import tensorflow as tf
```

2、加载 MNIST 數據集。將樣本數據從整數轉換為浮點數：
```python
mnist = tf.keras.datasets.mnist

(x_train, y_train), (x_test, y_test) = mnist.load_data()
x_train, x_test = x_train / 255.0, x_test / 255.0
```
Downloading data from https://storage.googleapis.com/tensorflow/tf-keras-datasets/mnist.npz
11490434/11490434 [==============================] - 1s 0us/step

3、通過堆疊層来構建 tf.keras.Sequential 模型:

```python
model = tf.keras.models.Sequential([
  tf.keras.layers.Flatten(input_shape=(28, 28)),
  tf.keras.layers.Dense(128, activation='relu'),
  tf.keras.layers.Dropout(0.2),
  tf.keras.layers.Dense(10)
])
```

4、對於每个样本，模型都會返回一个包含 logits 或 log-odds 分数的向量，每個類一個:
```python
predictions = model(x_train[:1]).numpy()
```
array([[-0.40544653,  0.21649133,  0.21764778, -0.4033628 ,  0.1971823 ,
        -0.967962  ,  0.21890277, -0.55331427, -0.25738302, -1.103743  ]],
      dtype=float32)
      
5、tf.nn.softmax 函数將這些 logits 轉換為每個類的概率：
```python
tf.nn.softmax(predictions).numpy()
```
array([[0.07991948, 0.14885277, 0.149025  , 0.08008619, 0.14600612,
        0.04553604, 0.14921214, 0.06893417, 0.09267356, 0.03975451]],
      dtype=float32)
      
6、使用 losses.SparseCategoricalCrossentropy 為训练定義损失函数，它會接受 logits 向量和 True 索引，並為每个樣本返回一个標量损失:
```python
loss_fn = tf.keras.losses.SparseCategoricalCrossentropy(from_logits=True)
```

7、此损失等於 true 類的負對數概率：如果模型确定類正确，则损失為零。這個未經訓练的模型给出的概率接近隨機（每個類為 1/10），因此初始损失應該接近 -tf.math.log(1/10) ~= 2.3:

```python
loss_fn(y_train[:1], predictions).numpy()
```
3.089251

8、在开始训练之前，使用 Keras Model.compile 配置和編譯模型。将 optimizer 類設置為 adam，将 loss 设置為您之前定義的 loss_fn 函数，並通過将 metrics 參數设置為 accuracy 来指定要為模型评估的指標:
```python
model.compile(optimizer='adam',
              loss=loss_fn,
              metrics=['accuracy'])
     
```

9、使用 Model.fit 方法调整模型参数並最小化损失：
```python
model.fit(x_train, y_train, epochs=5)
```
Epoch 1/5
1875/1875 [==============================] - 11s 5ms/step - loss: 0.2951 - accuracy: 0.9143
Epoch 2/5
1875/1875 [==============================] - 9s 5ms/step - loss: 0.1450 - accuracy: 0.9577
Epoch 3/5
1875/1875 [==============================] - 10s 5ms/step - loss: 0.1090 - accuracy: 0.9664
Epoch 4/5
1875/1875 [==============================] - 10s 5ms/step - loss: 0.0887 - accuracy: 0.9725
Epoch 5/5
1875/1875 [==============================] - 10s 5ms/step - loss: 0.0760 - accuracy: 0.9763
<keras.src.callbacks.History at 0x78e24aa04eb0>

10、Model.evaluate 通常會在 "Validation-set" 或 "Test-set" 上檢查模型的性能:
```python
model.evaluate(x_test,  y_test, verbose=2)
```
313/313 - 1s - loss: 0.0723 - accuracy: 0.9774 - 1s/epoch - 4ms/step
[0.07230165600776672, 0.977400004863739]

11、在完成上述的步驟後這個照片分類器的准确度已经達到 98%。這個機械學習模型也完成了

##參考資料:https://tensorflow.google.cn/tutorials/quickstart/beginner?hl=zh_cn



