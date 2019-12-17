## Matlab Toolbox EKF/UKF
### CKF
* 包含几个函数：`ckf_predict`, `ckf_transform`, `ckf_update`, `ckf_packed_pc`, `sphericalradial`  
  运行逻辑：predict→transform(SR(f))计算预测均值→transform(SR(pack_pc(f)))计算预测P和C→update→transform(SR(h))计算更新均值→transform(SR(pack_pc(h)))计算更新P和C→predict...
* `ckf_pack_pc`计算P和C，再打包成一个数组
* `sphericalradial`生成容积点，代入函数完成传播，再根据容积准则计算积分值
* 通用套路是用SR准则计算积分值，先算mean，再代入算P和C；先算预测mean和covariance，然后用Kalman计算更新mean和covariance
* Reentry Vehicle示例中，认为噪声是叠加性的，用reentry_f计算轨迹，reentry_h计算测量结果
* 该工具箱函数和原始的CKF定义有差异，主要体现在P和C的计算上，改了一下效果稍有改善