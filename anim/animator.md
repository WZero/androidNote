**属性动画里涉及的一些属性值：**   

- translationX和translationY: 这两个属性作为一种增量来控制着View对象从它布局容器的左上角坐标偏移的位置   
- rotation、rotationX和rotationY：这三个属性控制着View对象围绕支点进行2D和3D旋转   
- scaleX和scaleY：这两个属性控制着View对象围绕支点进行2D缩放   
- pivotX和pivotY：这两个属性控制着View对象的支点位置，围绕这个位置进行旋转和缩放的变化处理，默认情况下，该支点为View对象的中心点。   
- x和y：这是两个简单实用的属性，它描述了View对象在它的容器中最终的位置，它是最初的左上角坐标和translationX、translationY值的累计和。   
- alpha：它表示View对象的alpha透明值，默认1不透明，0为完全透明   




### Animator ###

**常用方法**   
- Animator.setStartDelay() 延迟处理动画   
- Animator.setInterpolator() 动画插值器 Interpolator


### ValueAnimator ###





### ObjectAnimator ###
ObjectAnimator 继承自 ValueAnimator


**常用方法**   
- ObjectAnimator.ofInt()   
- ObjectAnimator.ofArgb()   
- ObjectAnimator.ofFloat()   
- ObjectAnimator.ofObject()   
- ObjectAnimator.ofPropertyValuesHolder()   


### AnimatorSet ###

**常用方法**   
- new AnimatorSet().playTogether();   
- new AnimatorSet().playSequentially();   
- new AnimatorSet().play().with()   
- new AnimatorSet().play().before()   
- new AnimatorSet().play().after()   





### 插值器 - Interpolator ###

- AccelerateDecelerateInterpolator 在动画开始与结束的地方速率改变比较慢，在中间的时候加速
- AccelerateInterpolator  在动画开始的地方速率改变比较慢，然后开始加速
- AnticipateInterpolator 开始的时候向后然后向前甩
- AnticipateOvershootInterpolator 开始的时候向后然后向前甩一定值后返回最后的值
- BounceInterpolator   动画结束的时候弹起
- CycleInterpolator 动画循环播放特定的次数，速率改变沿着正弦曲线
- DecelerateInterpolator 在动画开始的地方快然后慢
- LinearInterpolator   以常量速率改变
- OvershootInterpolator    向前甩一定值后再回到原来位置



