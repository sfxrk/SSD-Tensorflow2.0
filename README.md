# SSD-Tensorflow2.0
## tensorflow 2.0 ssd
vgg 分类网络
Conv2D 层
MaxPool 层
在 conv5 之后接上flatten 后接上三个全连接层，
前面连个激活函数为relu,最后一层的激活函数为softmax
```
python nets/vgg.py
```
```
model.fit_generator(generator=train_batch_generator,
                                  steps_per_epoch=120,
                                  epochs=10,
                                  verbose=1,
                                  validation_data=test_batch_generator,
                                  validation_steps=1)
```
在测试集上的结果能达到90%
现在讲全连接层改成卷积层，试下效果

```
self.fc6 = Conv2D(4096,(7,7),padding="valid",activation='relu',name='conv6')
self.dropout6 = Dropout(0.5)

self.fc7 = Conv2D(4096,(1,1),activation='relu',name='conv7')
self.dropout7 = Dropout(0.5)

self.fc8 = Conv2D(classes,(1,1),padding='same',activation=None,name='conv8')
```
ssd 对 vgg 做了一点变化
### VGG 层
在fc6层和fc7层与以往的VGG不同的是，使用卷积层来代替以前的全连接层
卷积层使用的是局部信息，全连接层使用的是全局信息
但是在最后fc6 和 fc7 特征尺寸变大，

可以让卷积网络在一张更大的输入图片上滑动，得到每个区域的输出（这样就突破了输入尺寸的限制）。

### Anchor 层 
一共使用 38×38×4 + 19×19×6+ 10×10×6 + 5×5×6 + 3×3×4+ 1×1×4 = 8732

在38*38特征图中，以每个点为中心移动框，还原到原图中如下图,每个点有四种组合方式

![38*38 的 anchor](https://raw.githubusercontent.com/jadehh/SSD-Tensorflow2.0/master/gif/anchor_38.gif)

大特征图检测小物体，因为此时的anchor宽和高比较小,
anchor 高和宽尺寸大小为
```
(300*0.1,300*0.1)
sqrt(0.1*0.2) * 300, sqrt(0.1*0.2) * 300
( 0.1 * 300 * np.sqrt(2)， 0.1 * 300 / np.sqrt(2),)
( 0.1 * 300 * np.sqrt(0.5)， 0.1 * 300 / np.sqrt(0.5),)

(0.1,           0.1）
(0.14142136,0.14142136）
(0.14142136，0.07071068)
(0.07071068，0.14142136)
``` 
anchor 中心点坐标(x,y),根据offset_width 和 step_width = 300/38=8

计算公式
```
 
   np.linspace(offset_width * step_width, (offset_width + feature_map_width - 1) * step_width,
                         feature_map_width)

   (4,12,20, ........) 一共有38 * 38 个 中心坐标


```




在19*19特征图中，以每个点为中心移动框，还原到原图中如下图,

![19*19 的 anchor](https://raw.githubusercontent.com/jadehh/SSD-Tensorflow2.0/master/gif/anchor_19.gif)

在SSD中priorbox的个数与位置是固定的，所以需要通过一个预测值反推出真实框。

整个网络坐标的训练就是为了训练这个预测框


预测框 表达的是真实框与Anchor框之间的关系，公式如下
```
 # 编码公式
    cx(predict) = (cx(gt) - cx(anchor)) / w(anchor) / cx_variance
    cy(predict) = (cy(gt) - cy(anchor)) / h(anchor) / cy_variance
    cw(predict)= ln(w(gt) / w(anchor)) / w_variance
    ch(predict) = ln(h(gt) / h(anchor)) / h_variance

```

由预测框的值可以反推出真实框的值，

SSD经过网络求得的结果是预测框的值，所以需要解码
```
    # 解码公式
    cx(gt) = cx(predict) * cx_variance * w(anchor) + cx(anchor)
    cy(gt) = cy(predict) * cy_variance * h(anchor) + cy(anchor)
    w(gt) = exp(cw(predict)*w_variance)*w(anchor)
    h(gt) = exp(ch(predict)*h_variance)*h(anchor)
```

SSD Encode代码
```
python utils/ss_input_encode.py
encode 的结果为 [self.num_classes+1,predictions,anchor_boxes,variances]
predictions =  [p_xmin,p_ymin,p_xmax,p_ymax]
anchor_boxes = [a_xmin,a_ymin,a_xmax,a_ymax], 固定值
variances = [0.1,0.1,0.2,0.2]
```

   