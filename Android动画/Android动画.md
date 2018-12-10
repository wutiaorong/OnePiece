### Android动画
安卓主要有三种动画
1. 补间动画，又称View动画
2. 帧动画，又称Drawable动画
3. 属性动画

**下面逐个来描述下**
#### 一. 补间动画
补间动画主要有四个类型
* 平移动画（Translate）:TranslateAnimation
* 缩放动画（scale）:ScaleAnimation
* 旋转动画（rotate）:RotateAnimation
* 透明度动画（alpha）:AlphaAnimation

具体的使用方式分为两种：在XML代码或者Java 代码里设置。具体怎么使用这里不做详细描述。都是一些API的使用。主要要注意下面几个点

**1. 补间动画只适用于View，也就是只能对View做动画，这就是为什么它也叫视图动画，View的原因。**  

**2. View做在做补间动画的时候，它并没有真正的移动它的位置，只是画它的时候进行了Matrix处理，使得它看起来变化了，所以我们点击动画后的位置，并没有用**  

**3. 调用setFillAfter方法可以使动画执行后停留在动画执行后的位置，不然动画执行以后又会恢复动画一开始的样子**

#### 二. 帧动画

帧动画主要通过设置多张图片，由android来控制依次显示这些静态图片，来达到动画的效果。同样可以通过XML代码或者Java代码来设置。

#### 三. 属性动画

 Android 3.0（API 11）以后才提供的属性动画。  
 
 **为什么要提供属性动画呢**
 **因为逐帧动画和补间动画存在一定的缺点** 
 
 **1. 补间动画无法对非View对象进行操作**  
 **2. 补间动画没有改变View的属性，只是改变视觉效果**
* 补间动画只是改变了View的视觉效果，而不会真正去改变View的属性。如，将屏幕左上角的按钮 通过补间动画 移动到屏幕的右下角
* 点击当前按钮位置（屏幕右下角）是没有效果的，因为实际上按钮还是停留在屏幕左上角，补间动画只是将这个按钮绘制到屏幕右下角，改变了视觉效果而已。 

**3. 补间动画只能实现平移、旋转、缩放和 透明度这些简单的动画需求，动画效果单一**

**属性动画原理：在一定时间间隔内，通过不断对值进行改变，并不断将该值赋给对象的属性，从而实现该对象在该属性上的动画效果**

属性动画主要有两个重要的类：ValueAnimator类 和 ObjectAnimator类

**1. ValueAnimator**  
主要有
* ValueAnimator.ofInt（）
* ValueAnimator.ofFloat（）
* ValueAnimator.ofObject（） 

分别对应将将初始值 以整型数值，浮点型数值，对象的形式 过渡到结束值。

我们在设置完动画以后，调用addUpdateListener来在每次值变化的时候进行相应的处理。

**2. ObjectAnimator**  
和ValueAnimator的不同是，它直接对对象的属性值进行改变操作，从而实现动画效果。它继承自ValueAnimator类，即底层的动画实现机制是基于ValueAnimator类。  
使用例子

```
ObjectAnimator animator = ObjectAnimator.ofFloat(mButton, "alpha", 1f, 0f, 1f);
```
ObjectAnimator.ofFloat（）的第二个参数传入值的作用是：让ObjectAnimator类根据传入的属性名 去寻找 该对象对应属性名的 set（）和 get（）方法，从而进行对象属性值的赋值

