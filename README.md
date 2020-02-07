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
  
2.防护罩着色器
参考油管up主的一个视频:https://www.youtube.com/channel/UCtb1s859RTxx-RIgFs5ZVQA  
![防护罩](https://github.com/ssssssilver/HDR/blob/master/preview/guard1.gif)  
球体的模型是使用blener制作 需要在add-on添加Mesh:Tissue这个插件 在创建一个icon sphere时点击组件的convert to dualmesh可以把球体的面变面五边形与六边形组合  
需要注意的是 想要让球体的UV相同部分都重合在一起 需要在创建球体时将generate uvs取消勾选 在将五边形与六边形分开后需要将uv构图导出进行ps处理 以便后期着色器使用  

![blender](https://github.com/ssssssilver/HDR/blob/master/preview/blender.png)  
使用自定义的球体模型 一是能将球体的每一个网格都分离成单独块 用法线与模型位置可以控制每一片的偏移 二是能修改UV 自定义显示效果  
  
将模型导出再放进unity后 创建一个particleSystem组件来呈现这个着色器效果 去粒子的速度跟其他功能 只保留Emission与renderer，并将粒子的显示从公告板换成mesh 用blender创建的圆形来代替

shadergraph的设置比较简单 透明度部分通过用ps修改后的uv图利用它apha值配合hdrcolor来显示  
颜色部分利用fresnel effect+hdrcolor来实现效果  
球体整体向外扩散需要用到法线与模型坐标组合作用于position  
同时因为是用于粒子系统 需要将着色器设置成Addtive  
  
在particlesystem中添加rotate over lifetime可以给模型增加旋转效果   
![旋转](https://github.com/ssssssilver/HDR/blob/master/preview/gurad2.gif)  
  
部分防护罩效果  
将fresnel部分去掉 并且用sphereMask来控制输出的alpha值 可以让防护罩只显示部分 并且能控制显示需要的部分  
![部分](https://github.com/ssssssilver/HDR/blob/master/preview/gurad3.gif)




