# 深度学习网络结构
  1. VGG
  2. ResNet
  3. GoogleNet
  4. DenseNet
  5. MobileNet
  8. TridentNet
  
# 目标检测
1. yolo
2. SSD
3. Faster R-CNN
   3.1 pvanet
4. CornerNet
   hourglass net
   associative embedding
5. RetinaNet（Focus Loss)
6. Mask R-CNN

# Segmatic Segmentation
1. FCN 
   2014, 深度学习语义分割的开山之作，摒弃了全连接层，提出的全卷积网络的概念
2. SegNet
   2015, 对FCN的改进，发现上采样不必如FCN般使用转置卷积，而只需要使用基于maxpooling index的上采样外加一个卷积层即可达到相似目的。
   这个发现让后续不少方法放弃使用转置卷积而使用固定参数的双线性插值+卷积的方式，降低了参数量
3. UNet   
   2015,对FCN的改进，不像FCN那样仅仅从分辨率最小的特征逐渐上采样，获得分割结果。而是提出skip-connection的概念（element-wise add修改成channel-concat），把每一个stage输出的特征图都引入解码端，提高分割效果。后续收到DenseNet影响，把skip-connection替换成DenseBlock，即UNet++  
   
4. DeepLab
   2015,v1/v2/v3/v3+供四个版本，主要贡献是提出了空洞卷积的概念，摒弃了Pooling层。空洞卷积可以看作Pooling的另一面：Pooling是通过缩小特征图获得较大的“视野”，空洞卷积是通过放大kernel获得较大的“视野”，所以也可以用空洞卷积替代Pooling，实现主流的模型；ASPP模块可以看作是基于空洞卷积的多尺度金字塔

5. RefineNet
   2016,强调每一个尺度对分割都是有帮助的，充分利用每个stage输出的特征图生成最后的分割结果。利用Resnet做backbone，对每个stage输出上采样到输出尺寸，做多通道融合后，最后经过一个级联的Pooling网络输出最终结果
 
6. SPSNet
   2016,强调多尺度对分割结果的重要性，利用Pooling构建一个多尺度金字塔（可以看作一个简化版的，基于Pooling的RefineNet）
   
7. Large Kernel Matters
   2017,考虑到分类和分割是两个矛盾的问题：分类期望使用较大的kernel，全连接，以获得对位置和姿态的鲁棒性，而分割期望使用较小的kernel，仅仅依赖局部信息以获得较高的定位精度。该方法通过分解二维卷积的策略降低了使用大kernel的计算量；每个stage输出的特征图都经过一个大kernel的卷积，然后经过类似残差结构的Boundary Refinement结构，最后类似UNet逐层上采样获得输出结果。
   
8. 速度改进  
   8.1 ENet   
   8.2 ICNet    
    强调分割速度的两个算法，ICNet速度接近ENet而且效果远远好于ENet.   
    ICNet基础的优化思路是：在低分辨率上使用dense convnet获得粗略的分割结果，在高分辨率上使用light convnet，并结合低分辨率分割结果（CFF模块），优化分割细节   
   
# 其他
  1. FPN
