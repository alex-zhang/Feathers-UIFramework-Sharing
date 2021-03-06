# Feathers UI-Framework Sharing

![](https://github.com/alex-zhang/Feathers-UIFramework-Sharing/blob/master/feathers.png)

## UI-Framework Achitecture

**why start here?**

+ Cursor Control
```
System Cursor > Parent Container Cursor[...] > Business Logic Cursor
```
+ DragAndDrop
+ Focus Control
+ PopUp Manager
+ Animation/Effect/Tween
+ System Level Display Layers Sort Division.
+ Asset & Asset Loader
+ Interactive & Event Stream
+ Localization & I18N
+ __Look And Feel (Theme & Style & Font & Skin Support)__
+ __Bounds Size Mode & Layout__
+ __Components Update Mechanism__ 
+ Data-Drive Based Component Design
```
Flex Data-Bindding ArrayList ArrayCollection TreeList    
JS/Html MVVM[Model View ViewModel]
```
+ Low-Level Render Controller(Vector, Bitmap, Canvas...)
+ Vector Graphics
+ Component's Life-Cycle
+ Numerous of Components Support
```
ToolTip Support & Custom ToolTip
Alert
Button
List
Tabel
Tree
CheckBox
DateField
DateChoose
TextInput
TextArea
Slider
ScrollBar
According
TabBar
Image
...
```

## Look And Feel

__Look And Feel 是由若干Style Props支撑起来的外观__

+ CSS (Style Props Table)

```css
global
{
    font-size:12;
    text-align:center;
    color:#CCCCCC;
    background-color:#FFFCCC;
}

Parent
{
    font-size:13;
    color:#FFF;
}

Panel (Class Selector)
{
    color:#123123;
}

.myPanel (StyleName/Id Selector)
{
    text-align:left;
    color:#123123;
}

element.setStyle("text-align", "center");
```

+ Theme

```
Theme 就是这些所有Pre-Design Style Props Table 资源一个集合
```

+ Style Merge Rules

```
inlineStyles > StyleName Styles > Class Styles > Parent Inherited Styles[...] > global Styles > Theme
```

+ Final Computed Style Props Table

```css
runTime
{
    font-size:13;
    text-align:right;
    color:#123123;
    background-color:#FFFCCC;
}

```
上层样式的改变会引起很多的影响到的组件显示方面的更新。这需要一个缓慢、异步的更新过程。
所以关于样式这块，我们的UI框架需要有一种高效和幂等的更新方式来开完成样运行时样式表的更新/刷新

## Bounds Size Mode & Layout

+ Bounds Size Mode

![](https://github.com/alex-zhang/Feathers-UIFramework-Sharing/blob/master/sp_size_properties.png)

```
width 当前实际尺寸(包含缩放)
explicitWidth 显示指定的具体尺寸（不需要依赖父容器的尺寸）
percentWidth 显示指定的百分比尺寸（需要依赖父容器的尺寸）
measureWidth 组件自身度量尺寸
minWidth 最小约束尺寸
maxWidth 最大约束尺寸
padding
margin
border
x
left
scaleX
```

+ Layout

measure    -> layout

![](https://github.com/alex-zhang/Feathers-UIFramework-Sharing/blob/master/view_layout.jpg)

![](https://github.com/alex-zhang/Feathers-UIFramework-Sharing/blob/master/layout-diagram.png)

![](https://github.com/alex-zhang/Feathers-UIFramework-Sharing/blob/master/scroller_bar.jpg)

父容器内任何子容器尺寸的改变都可能会引起本身尺寸的改变，而且还会继续向上传递。这需要一个缓慢、异步的更新过程。
所以关于布局这块，我们的UI框架需要有一种高效和幂等的更新方式来开完成样组件的自身的尺寸度量和内部child的布局

## Components Update Mechanism

+ Asyc-update

invalidate -> validate

![](https://github.com/alex-zhang/Feathers-UIFramework-Sharing/blob/master/update_mechanism.png)

## Feathers

Flex < [Feathers](http://feathersui.com/) < Flash CS Component

+ feathers urls

```
http://feathersui.com
http://forum.starling-framework.org/forum/feathers
http://wiki.starling-framework.org
http://wiki.starling-framework.org/feathers/start
http://wiki.starling-framework.org/feathers/text-renderers
```

+ source code
+ feathers in projects


## Other UI-Framework
+ [Viburnum](https://github.com/alex-zhang/Viburnum-UIFramework)
+ Flex
+ Flash CS UI
+ Feathers
+ [ASWing](https://github.com/alex-zhang/aswing/blob/master/AsWing/src/org/aswing/Component.as)
+ [Android](https://github.com/android/platform_frameworks_base/tree/master/core/java/android)
+ HTML(JQueryUI, KindoUI)
+ Unity/Cocos2d
+ ...

## Flow-Layout & Screen-Adaptation in Starling

+ Design 914X578 UseFor App
![](https://github.com/alex-zhang/Feathers-UIFramework-Sharing/blob/master/screen_adaptation_914_578.png)

__首先不考虑高清、低清资源__

+ 方案1:等比缩放：

![](https://github.com/alex-zhang/Feathers-UIFramework-Sharing/blob/master/Penguflip_scale_up.png)

![](https://github.com/alex-zhang/Feathers-UIFramework-Sharing/blob/master/Penguflip_scale_up_ipad_bars.png)

> 优点：逻辑简单，大部分分辨率下OK，整个app业务逻辑完全基于绝对位置布局(参考 原始914X578)
> 缺点：部分非主流的分辨率会下出现留白，有些很能会很大。

+ 方案2:拉伸缩放：

> 优点：逻辑简单，大部分分辨率下OK，整个app业务逻辑完全基于绝对位置布局(参考 原始914X578)
> 缺点：部分非主流的分辨率会下出现变形，有些很能会严重变形。有些底层不支持。

+ 方案3: 等比缩放 + （轻微）拉伸缩放：
> 针对方案1中的留白情况时，做轻微拉伸，目的是在拉伸不严重的情况下，减少留白的面积

> 优点：是方案1的优化版
> 缺点：有些底层不支持

------------------------------------------------------------------------------

+ 方案3: 流式布局

+ Flow-Layout For 1800X900
![](https://github.com/alex-zhang/Feathers-UIFramework-Sharing/blob/master/screen_adaptation_1416_768.png)

+ Flow-Layout 2149X1107
![](https://github.com/alex-zhang/Feathers-UIFramework-Sharing/blob/master/screen_adaptation_1416_768.png)
screen_adaptation_2149_1107.png

+ Flow-Layout 2880X1536
.....

> 优点：能够完美适应所有分辨率，没有变形和留白
> 缺点：需要在UI层次支持流式布局。在分辨率差异较大时，页面显得太空旷，且有些界面元素变得很小了

+ 方案4: 流式布局 + 等比缩放

> 这就是我们现在使用的解决方案

> 优点：很多
> 缺点：没有

--------------------------------------------------------------------------------

```actionscript
package com.xxx.hippo.screenAdaptation
{
    public class FlowFitScreenAdaptation extends ScreenAdaptation
    {
        public static var DESIGN_MIN_WIDTH:int = 800;
        public static var DESIGN_MAX_WIDTH:int = 1280;
        
        public static var DESIGN_MIN_HEIGHT:int = 768;
        
        public function FlowFitScreenAdaptation()
        {
            super();
        }

        /*
        *          min 800   max 1280
        * ____________|_________|____________________________________________________
        *
        */
        override public function adaptScreenion(deviceWidth:int, deviceHeight:int):void
        {
            //假设设备是横向的，即宽度略大于高度
            //如果设备尺寸的尺寸范围本来就在最小和最大之间则即为该设备的值
            
            var deviceSizeRatio:Number = deviceWidth / deviceHeight;
            var deviceToDesignWidthMultiple:Number = deviceWidth / DESIGN_MIN_WIDTH;
            
            if(deviceWidth <= DESIGN_MAX_WIDTH)//opt for almost device.
            {
                mDesignWidth = deviceWidth;
                mDesignHeight = deviceHeight;
            }
                //如果设备尺寸的尺寸整除后的尺寸在最小和最大之间则即为该设备的整除后的值
            else if(deviceToDesignWidthMultiple >= 2)
            {
                var curDesignWidth:Number = deviceWidth / int(deviceToDesignWidthMultiple);
                if(curDesignWidth >= DESIGN_MIN_WIDTH && curDesignWidth <= DESIGN_MAX_WIDTH)
                {
                    mDesignWidth = curDesignWidth;
                    mDesignHeight = mDesignWidth / deviceSizeRatio;
                }
            }
            else
            {
                //否则返回最大设计尺寸的值。
                mDesignWidth = DESIGN_MIN_WIDTH;
                mDesignHeight = mDesignWidth / deviceSizeRatio;
            }
            
            //we must ensure we have a min height.
            if(mDesignHeight < DESIGN_MIN_HEIGHT)
            {
                mDesignHeight = DESIGN_MIN_HEIGHT;
                mDesignWidth = mDesignHeight * deviceSizeRatio;
            }
            
            mStageViewPort.setTo(0, 0, deviceWidth, deviceHeight);
        }
    }
}
```

--------------------------------------------------------------------------------

```actionscript
package com.xxx.hippo.screenAdaptation
{
	public class ScaleFitScreenAdaptation extends ScreenAdaptation
	{
		public function ScaleFitScreenAdaptation()
		{
			super();
		}
		
		public function set designWidth(value:int):void
		{
			mDesignWidth = value;
		}
		
		public function set designHeight(value:int):void
		{
			mDesignHeight = value;
		}
		
		override public function adaptScreenion(deviceWidth:int, deviceHeight:int):void
		{
			var designWHRatio:Number = designWidth / mDesignHeight;
			var deviceWHRatio:Number = deviceWidth / deviceHeight;
			
			if(designWHRatio > deviceWHRatio)
			{
				mStageViewPort.width = deviceWidth;
				mStageViewPort.height = mStageViewPort.width / designWHRatio;
				
				mStageViewPort.x = 0;
				mStageViewPort.y = (deviceHeight - mStageViewPort.height) >> 1;
			}
			else
			{
				mStageViewPort.height = deviceHeight;
				mStageViewPort.width = mStageViewPort.height * designWHRatio;
				
				mStageViewPort.y = 0;
				mStageViewPort.x = (deviceWidth - mStageViewPort.width) >> 1;
			}
		}
	}
}
```
