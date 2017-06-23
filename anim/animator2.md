看代码，这个基本都很熟悉

>     ObjectAnimator   
>     	.ofFloat(imageView, "translationX", 1, 100)   
>     	.setDuration(200)   
>     	.start();   

拿 ofFloat 举例子
> ofFloat(Object target, String propertyName, float... values)   

- 正常情况下 ofFloat 的第一个参数 target 你会放个View进去，但一看源码他是个Object类型的，你可能会纠结为什么不是View 类型呢？

- 第二个参数 propertyName String类型，可以参照 [属性动画 Animator ( 一 )](http://www.wttzero.cn/wordpress/index.php/2017/06/21/animator_one/) 里面的参数 translationX、translationY... ,但你可能回想怎么每个枚举或者一个静态类来调用这些参数呢？

- 第三个参数 values 是个float... 类型，可以理解成float数组，这个应该都知道


### 举个栗子 ###
第一个数不放 View 放别的类会怎样   

一个简单的Date类 里面只有一个 time 字段跟get set 方法，在set里面加个打印

	public class Date {
	
	    private float time;
	
	    public float getTime() {
	        return time;
	    }
	
	    public void setTime(float time) {
	        this.time = time;
	        KLog.i("   " + time);
	    }
	}

看 ObjectAnimator 

	Date date = new Date();
     ObjectAnimator
           .ofFloat(date, "time", 0, 12)
           .setDuration(200)
           .start();

看下运行结果 Date 里面 setTime 的打印

>  [ (Date.java:19)#setTime ]    0.0   
>  [ (Date.java:19)#setTime ]    0.0   
>  [ (Date.java:19)#setTime ]    0.18850136   
>  [ (Date.java:19)#setTime ]    0.7882104   
>  [ (Date.java:19)#setTime ]    1.6912422   
>  [ (Date.java:19)#setTime ]    2.9457521   
>  [ (Date.java:19)#setTime ]    4.3260527   
>  [ (Date.java:19)#setTime ]    5.905756   
>  [ (Date.java:19)#setTime ]    7.400673   
>  [ (Date.java:19)#setTime ]    8.890524   
>  [ (Date.java:19)#setTime ]    10.107283   
>  [ (Date.java:19)#setTime ]    11.115842   
>  [ (Date.java:19)#setTime ]    11.734757   
>  [ (Date.java:19)#setTime ]    11.997039   
>  [ (Date.java:19)#setTime ]    12.0   


上面 ObjectAnimator.ofFloat    

第一个参数 Object类型 ，我们放入的是 Date 对象   
第二个参数 String类型 ，我们放入的是 Date 对象里面的 time 字段   
打印是从 0 - 12 ，对上ofFloat 的第三个参数 values   

回头看
>     ObjectAnimator   
>     	.ofFloat(imageView, "translationX", 1, 100)   
>     	.setDuration(200)   
>     	.start(); 


translationX 是 View类的字段，ImageView继承View   

ObjectAnimator动画是通过 修改 imageView 的 translationX 字段值 实现动画效果

translationX、translationY、rotation、rotationX、rotationY、pivotX 等... 同上理论