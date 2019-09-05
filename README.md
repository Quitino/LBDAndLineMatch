
## LBD_and_LineMatch

#### 依赖项

 - OpenCV
 - Arpack
 - Lapack

#### 实现功能
通过EDlines算法提取图像的线段特征，再用LBD构建线段的描述子信息，并用图匹配的方法进行两张图之间的特征线段的匹配，其中test.hpp用于记录matching的结果和线段提取的结果，库有点老了，不太实用。


