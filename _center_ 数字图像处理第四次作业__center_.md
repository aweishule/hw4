#<center> 数字图像处理第四次作业</center>

------

<center>自动化少61</center>

<center>魏俊哲</center>

<center>2140506024</center>

<center>2019.3.19</center>

### 摘要：
本次作业学习了空域滤波器的使用，学习了如何产生高斯函数。通过对实验结果的分析可以发现高斯函数对于高斯噪声优化效果较好，而中值滤波对大噪声有一定的优化效果。后面的边缘提取作业中，学习了4种常用的算法，对数字图像处理的理解更加深入。

> 1.空域低通滤波器：分别用高斯滤波器和中值滤波器去平滑测试图像test1和2，模板大小分别是3x3 ， 5x5 ，7x7； 分析各自优缺点；

### 原理说明
中值滤波器的想法很简单，如果一个信号是平缓变化的，那么某一点的输出值可以用这点的某个大小的邻域内的所有值的统计中值来代替。这个邻域在信号处理领域称之为窗（window）。窗开的越大，输出的结果就越平滑，但也可能会把我们有用的信号特征给抹掉。所以窗的大小要根据实际的信号和噪声特性来确定。
通常我们会选择窗的大小使得窗内的数据个数为奇数个，之所以这么选是因为奇数个数据才有唯一的中间值。
高斯滤波是一种线性平滑滤波，适用于消除高斯噪声，广泛应用于图像处理的减噪过程。通俗的讲，高斯滤波就是对整幅图像进行加权平均的过程，每一个像素点的值，都由其本身和邻域内的其他像素值经过加权平均后得到。高斯滤波的具体操作是：用一个模板（或称卷积、掩模）扫描图像中的每一个像素，用模板确定的邻域内像素的加权平均灰度值去替代模板中心像素点的值。
### 处理结果
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/guass.jpg)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/t2guass.jpg)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/zzz.jpg)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/test2zzz.jpg)

### 结果分析
发现中值滤波后的图像更加模糊，对孤立点噪声的屏蔽效果好很多，高斯滤波则对高斯噪声屏蔽效果好，两者各有优劣，应视情况选择合适滤波器。
> 2.-利用固定方差 sigma=1.5产生高斯滤波器. 附件有产生高斯滤波器的方法； 分析各自优缺点；

此题与上题重合，实现方法见代码。

> 3.利用高通滤波器滤波测试图像test3,4：包括unsharp masking, Sobel edge detector, and Laplace edge detection；Canny algorithm.分析各自优缺点；

### 1.UnSharp Masking
### 原理说明
线性反锐化掩模（UnSharp Masking，UM）算法。首先将原图像低通滤波后产生一个钝化模糊图像，将原图像与这模糊图像相减得到保留高频成份的图像，再将高频图像用一个参数放大后与原图像叠加，这就产生一个增强了边缘的图像。最初将原图像通过低通滤波器后，因为高频成份受到抑制，从而使图像模糊，所以模糊图像中高频成份有很大削弱。将原图像与模糊图像相减的结果就会使f(x、y)的低频成份损失很多，而高频成份较完整地被保留下来。因此，再将高频成份的图像用一个参数放大后与原图像f(x、y)叠加后，就提升了高频成份，而低频成份几乎不受影响。
### 处理结果
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/sharp3.jpg)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/sharp4.jpg)
### 结果分析
结果得到了边缘更加清晰的图像，与预期改进效果一致。
### 2.Sobel edge detector
### 原理说明
Sobel算法关注2维图像上的变化程度测量，特别强调变化频率高的区域以确定边界。典型的应用是寻找输入的灰度图像中每个点的绝对变化量。这里使用matlab中的edge函数调用sobel算子进行处理。
### 处理结果
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/sobel3.jpg)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/blob/master/sobel4.jpg)
### 结果分析
结果观察：在在图像的任何一点使用此算子，将会产生对应的梯度矢量或是其法矢量。由于Sobel算子是滤波算子的形式，用于提取边缘，可以利用快速卷积函数，简单有效，因此应用广泛。美中不足的是，Sobel算子并没有将图像的主体与背景严格地区分开来，换言之就是Sobel算子没有基于图像灰度进行处理，由于Sobel算子没有严格地模拟人的视觉生理特征，所以提取的图像轮廓有时并不能令人满意。从图像观察，可以看出索贝尔算子并没有将图像边缘完全分离出来。

### 3.Laplace edge detection
### 原理说明
拉普拉斯算子是最简单的各向同性微分算子，具有旋转不变性。这里使用matlab中的edge函数调用laplacian算子进行处理。

### 处理结果
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/laplacian3.jpg)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/laplacian4.jpg)
### 结果分析
拉普拉斯是一种微分算子，其应用强调的是图像中灰度的突变，并不强调灰度级缓慢变化的区域。这将产生把浅灰色边线和突变点叠加到暗色背景中的图像。结合处理后的图像观察，拉普拉斯算子对于test3 的边沿检测较为理想，而对于test4的边缘检测不是很理想，因为test4图片整体处于灰色，所以完全没有提取出来边缘。
### 4.Canny algorithm
### 原理说明
在图像边缘检测中，抑制噪声和边缘精确定位是无法同时满足的。边缘检测算法通过平滑滤波去除图像噪声的同时，也增加了边缘定位的不确定性；反之，提高边缘检测算子对边缘敏感性的同时，也提高了对噪声的敏感性。Canny算子力图在抗噪声干扰和精确定位边缘之间寻求最佳折中方案。
这里使用matlab中的edge函数调用Canny算子进行处理。
### 处理结果
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/canny3.jpg)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/canny4.jpg)
### 结果分析
canny算子的边缘提取效果还是比较理想的，虽然test4存在一些不连续的问题，但是还是能够得到一定边缘的。与前面的方法对比可以看出,canny虽然更加复杂，但是效果也更好。
### 附录
参考文献：Rafael C. Gonzalez., et al. 数字图像处理（第三版）, 电子工业出版社，2011.

