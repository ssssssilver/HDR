# HDR
HighDefinition Render Pipeline下的shadergraph  
新建项目时直接选择创建High Denfinition RP 这样就可以直接使用HDR模式 不需要手动配置  
可以直接使用demoscene场景的默认配置进行操作  
 ![创建](https://github.com/ssssssilver/HDR/blob/master/preview/hdr.jpg)  
 
1.消溶着色器  
对模型空间下的y轴进行操作 将结果作用于alphaclip Threshold中 再将模型的alpha值设置成0.5 这样的alphatest操作能控制物体在模型空间下进行消溶  
为了使消溶效果更加真实 将噪波图的变化与alphatest混合  
对消溶范围与噪点图混合 并对消溶部分的颜色使用HDR效果 最后作用于Emission 让自发光的效果更加鲜明  
![消溶](https://github.com/ssssssilver/HDR/blob/master/preview/dissolve.gif)



