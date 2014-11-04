# Feathers UI-Framework Sharing

Flex < [Feathers](http://feathersui.com/) < Flash CS Component

## UI-Framework Achitecture
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
+ Interactive Event
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
+ Component's Life-Cycle
+ Numerous of Components Support
```
ToolTip Support & Custom ToolTip
Alert
...
```

## Look And Feel
+ CSS (Style Props Table)

```
global
{
    fontSize:12;
    text-align:center;
    color:#CCCCCC;
    background-color:#FFFCCC;
}

Parent
{
    fontSize:13;
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
Theme 就是这些所有Pre-Design Style Props Table 已经资源一个集合
```

+ Style Merge Rules

```
inlineStyles > StyleName Styles > Class Styles > Parent Inherited Styles[...] > global Styles > Theme
```

+ Final Computed Style Props Table

```
runTime
{
    fontSize:13;
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
```

+ Layout

![](https://github.com/alex-zhang/Feathers-UIFramework-Sharing/blob/master/view_layout.jpg)

![](https://github.com/alex-zhang/Feathers-UIFramework-Sharing/blob/master/layout-diagram.png)

![](https://github.com/alex-zhang/Feathers-UIFramework-Sharing/blob/master/scroller_bar.jpg)

父容器内任何子容器尺寸的改变都可能会引起本身尺寸的改变，而且还会继续向上传递。这需要一个缓慢、异步的更新过程。
所以关于布局这块，我们的UI框架需要有一种高效和幂等的更新方式来开完成样组件的自身的尺寸度量和内部child的布局

## Components Update Mechanism

+ Asyc-update

invalidate -> validate
measure    -> layout

![](https://github.com/alex-zhang/Feathers-UIFramework-Sharing/blob/master/update_mechanism.png)

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

+ Design 914X578
![](https://github.com/alex-zhang/Feathers-UIFramework-Sharing/blob/master/screen_adaptation_914_578.png)

+ IN PC 1800X900
![](https://github.com/alex-zhang/Feathers-UIFramework-Sharing/blob/master/screen_adaptation_1416_768.png)



