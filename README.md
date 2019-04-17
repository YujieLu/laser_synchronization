# 倍加福激光同步方案
## 原理分析
设 某一次navigator node 收到激光同步信号的系统时间为t<sup>linux</sup><sub>syn</sub>，该次激光内部raw时钟为 t<sup>raw</sup><sub>syn</sub>,  
设 laser driver node收到一帧数据的系统时间为t<sup>linux</sup><sub>scan</sub>, 激光内部raw时钟为t<sup>raw</sup><sub>scan</sub>  
t0 为激光同步信号的时间间隔，激光同步时间误差为te，则  

t<sup>linux</sup><sub>syn</sub>-t<sup>linux</sup><sub>scan</sub>+t<sup>raw</sup><sub>scan</sub>-te= t<sup>raw</sup><sub>syn</sub>=k * t0

其中，k是整数，且t0较大，默认为4000ms,可以算出来同步误差为：  
te = t - [t/t0] * t0  
其中，t=t<sup>linux</sup><sub>syn</sub>-t<sup>linux</sup><sub>scan</sub>+t<sup>raw</sup><sub>scan</sub>  
[]是四舍五入运算符

需要注意的有：
* navigator node 转发同步信号时，需要确认和单边机的时延不应该太大，否则不应转发
* laser driver node在做计算时需要做好换算
* te 理论分析应为正值，初始值使用0

## 分工
1. 请黄工根据对应的数据手册，设置同步信号，并完成接线，并提前将接线方式告知蔡工。
2. 请蔡工根据接线方式，编写程序，监视激光同步信号；在通讯协议中增加一位，上传激光同步信号，当接收到激光同步信号时上传1，其他时间传0。
3. 请吕工在navigator node中发布一个同步的topic，仅包含navigator node接收到同步信号时的时间戳，具体message 的类型由凯文定
4. 请开问你在laser driver node中，接收同步的topic，并根据该topic调整时间戳。  

*有任何疑问和建议，请同我说。*


## 计划
当前同步对定位的影响不大，但考虑到提高车辆效率的同时保证精度，传感器之间的同步还是要注意的，暂定同步方案开始实施的时间点为5月初，劳动节放假后。

