# imagewatcher
仿朋友圈查看图片

### horizontal的移动
```java
    /**
     *  横向滚动条移动的算法,计算dx是关键
     *  通过position找到选中的RadioButton
     */
    public void moveHsv(int position){
        //横向滚动条移动到指定屏幕中可以显示的位置
        // 通过smoothScrollBy将滚动条移动到指定的位置 (dx需要计算的,dy不需要改变)
        /**
         * 准备条件
         * 1.屏幕的宽度
         * 2.选中项的宽度
         * 3.选中项的左侧的x坐标点
         */
        DisplayMetrics outMetrics = new DisplayMetrics();
        getWindowManager().getDefaultDisplay().getMetrics(outMetrics);
        int sceenWidth= outMetrics.widthPixels;
        //选中项的RadioButton
        RadioButton rbTitle = (RadioButton) rg.getChildAt(position);
        //千万不要在onCreate里调用view.getWidth或者view.getHeight方法,都是0,
        // 因为还没有测出View真是的大小
        final int rbTitleWidth = rbTitle.getWidth();
        Log.i("123", "rbTitle的宽度-->"+rbTitleWidth); final int rbTitleLeftX = rbTitle.getLeft(); //上下左右的坐标点都可以的

        //计算出要移动的中心位置 (最后目标参考的位置可以根据需求自己设定)
        int offset = (sceenWidth - rbTitleWidth) / 2;
        final int dx = rbTitleLeftX - offset;
        Log.i("123", "rbTitleLeftX-->" +rbTitleLeftX);
        Log.i("123", "dx-->" + dx);
        //直接使用ScrollTo,ScrollBy对上次移动dx继续累加
        hsv.smoothScrollTo(dx, 0);
        
    }
```