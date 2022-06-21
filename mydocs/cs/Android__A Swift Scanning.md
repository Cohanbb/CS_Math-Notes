<p align="center">
    <font size="6"><strong>Android__A Swift Scanning</strong></font>
</p>

- [Android 简介](#android-简介)
  - [Android 项目目录结构](#android-项目目录结构)
  - [Android 四大组件](#android-四大组件)
- [UI 设计](#ui-设计)
  - [基本概念](#基本概念)
  - [Widgets](#widgets)
    - [基础控件](#基础控件)
    - [高级控件](#高级控件)
  - [Layout](#layout)
    - [线性布局 LinearLayout](#线性布局-linearlayout)
    - [相对布局 RelativeLayout](#相对布局-relativelayout)
    - [帧布局 FrameLayout](#帧布局-framelayout)
    - [表格布局 TableLayout](#表格布局-tablelayout)
    - [网格布局 GridLayout](#网格布局-gridlayout)
    - [约束布局 ConstraintLayout](#约束布局-constraintlayout)
- [事件监听](#事件监听)
  - [事件监听方式](#事件监听方式)
    - [使用匿名内部类](#使用匿名内部类)
    - [使用内部类](#使用内部类)
    - [使用 Activity 作为事件监听器](#使用-activity-作为事件监听器)
  - [Handler 消息传递机制](#handler-消息传递机制)
- [Activity](#activity)
  - [Activity 生命周期](#activity-生命周期)
  - [创建 Activity](#创建-activity)
  - [Intent](#intent)
  - [启动 Activity](#启动-activity)
    - [显式调用](#显式调用)
    - [隐式调用](#隐式调用)
  - [Activity 间的数据传递](#activity-间的数据传递)
    - [Intent 机制](#intent-机制)
    - [Bundle 机制](#bundle-机制)
- [数据存储](#数据存储)
  - [SharedPreference](#sharedpreference)
  - [文件存储](#文件存储)
  - [Content Provider](#content-provider)
  - [SQLite 存储](#sqlite-存储)
  - [SD 卡](#sd-卡)
- [Content Provider](#content-provider-1)
- [BroadcastReceiver](#broadcastreceiver)
- [Service](#service)

# Android 简介

## Android 项目目录结构

## Android 四大组件

1. Activity

2. Content Provider

3. Broadcast Receiver

4. Service

# UI 设计

Android 提供了使用 XML 文件构建 UI 布局和控件，这些文件存放在 `/res/layout` 目录下。

`android.view` 类中定义了所有 UI 控件的基类 `View` 以及容纳这些控件的容器 `ViewGroup`。

## 基本概念

**长度的表示方法：**

* px
* dp
* sp
* in
* pt
* mm

**颜色的表示方法：**

* Java 中使用 Android 系统封装好的 `Color` 类常量
* Java 中使用十六进制 0x 开头的十六进制

```java
int color = 0xff00ff00;
```

* Java 中使用 `Color` 类的 `argb` 方法创建颜色

```java
int color = Color.argb(127.255.0.255);
```

* Java 中将十六进制颜色值转为 `int`

```java
int color = Color.parseColor("#00CCFF"); 
```

* XML  文件中定义颜色

```xml
<resource>
    <color name = "colorPrimary">#3F5185</color>
</resource>
```

**盒子模型**

![](https://www.runoob.com/images/box-model.gif)

## Widgets

`android.view.View` 类的派生类包含了所有的 Widget。

### 基础控件

* Button 按钮

```xml
<Button
    android:layout_width=""
    android:layout_height=""
    android:text=""
    android:onClick=""/>
```

* TextView 文本视图

```xml
<TextView
    android:layout_width=""
    android:layout_height=""
    android:text=""
    android:textSize=""/>
```

* EditText 编辑文本视图

```xml
<EditText
    ...
    android:inputType=""/>
```

* RadioGroup 单选按钮

```xml
<RadioGroup
    ...>

    <RadioButton
        ...
    />

    <RadioButton
        ...
    />

</RadioGroup>
```

* CheckBox 复选框

```xml
<selector
    ...>
    
    <item
        ...
    />

    <item
        ...
    />

</selector>
```

* ImageView 图片视图

```xml
<ImageView
    ...
    android:background=""
    android:src=""/>
```

### 高级控件

* Spinner
* ProgressBar
* SeekBar
* RatingBar
* TextClock
* DatePicker
* ListView
* GridView

## Layout

`ViewGroup` 类的派生类有六个：

* LinearLayout
* RelativeLayout
* FrameLayout
* AdapterView
* AbsoluteLayout
* SlidingDrawer

### 线性布局 LinearLayout

线性布局中控件只能沿垂直方向或水平方向摆放。

```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="horizontal">
    
    <!-- android:orientation 表示布局的方向，vertical 代表垂直方向，horizontal 代表水平方向 -->
    
    <LinearLayout
        android:id="@+id/LinearLayout1"
        android:layout_width="0dp"
        android:layout_height="match_parent"
        android:background="#ADFF2F"
        android:layout_weight="1"/>
    
    <LinearLayout
        android:id="@+id/LinearLayout2"
        android:layout_width="0dp"
        android:layout_height="match_parent"
        android:background="#DA70D6"
        android:layout_weight="2"/>

    <!-- 
    android:id 代表控件的 ID，@id 表明后面的内容被解析为 ID，+ 表明这是一个新创建的 ID
    0dp 代表长度由权重决定，match_parent 代表填充满父容器，wrap_content 表示强制将视图扩展以显示完整的内容
    android:layout_weight 代表布局的权重，在本例中LinearLayout1 权重为 1，
    LinearLayout2 权重为 2，故前者占布局的 1/3，后者占 2/3
    -->

</LinearLayout>
```

![](media/16557256967517.jpg)


### 相对布局 RelativeLayout

相对布局中一个控件使用其他的控件作为参考进行摆放，其常用属性：

```xml
<!--
    <RelativeLayout
        android:layout_below 放在指定控件的下边
        android:layout_toLeftOf 放在指定控件的左边
        android:layout_toRightOf 放在指定控件的右边
        android:layout_alignTop 上边界与指定控件的上边界对齐
        android:layout_alignBottom 下边界与指定控件的下边界对齐
        android:layout_alignLeft 左边界与指定控件的左边界对齐
        android:layout_alignRight 左边界与指定控件的左边界对齐
    />
-->
```

### 帧布局 FrameLayout

帧布局又叫框架布局，会在屏幕的左上角开辟一个区域放置控件。

```xml
<FrameLayout xmlns:android=""
    xmlns:tools=""
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    
    <TextView
        android:layout_width="200dp"
        android:layout_height="200dp"
        android:background="#FF6143"/>
    
    <TextView
        android:layout_width="150dp"
        android:layout_height="150dp"
        android:background="#7BFE00"/>
    
    <TextView
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:background="#FFFF00"/>
    
</FrameLayout>

<!--
    帧布局中可以使用 android:layout_gravity 来控制在父容器中的位置：
        top：将控件放到父容器顶端
        bottom：将控件放到父容器底端
        left：将控件放到父容器左端
        right：将控件放到父容器右端
        center_vertical：将控件垂直居中
        center_horizontal：将控件水平居中
        center：将控件水平和垂直居中
-->
```

![](media/16557263884508.jpg)


### 表格布局 TableLayout

### 网格布局 GridLayout

### 约束布局 ConstraintLayout

约束布局与相对布局类似，以其他控件作为参考来摆放控件。

约束布局的出现是为了解决布局嵌套过多的问题。

一些约束：

```xml
<!--
    <ConstraintLayout
        app:layout_constraintLeft_toLeftOf 左边界与指定控件左边界对齐
        app:layout_constraintLeft_toRightOf 左边界与指定控件有边界对齐
        app:layout_constraintRight_toLeftOf 右边界与指定控件左边界对齐
        app:layout_constraintRight_toRightOf 右边界与指定控件右边界对齐
        app:layout_constraintTop_toTopOf 上边界与指定控件上边界对齐
        app:layout_constraintTop_toBottomOf 上边界与指定控件下边界对齐
        app:layout_constraintBottom_toTopOf 下边界与指定控件上边界对齐
        app:layout_constraintBottom_toBottomOf 下边界与指定控件下边界对齐
        app:layout_constraintBaseline_toBaselineOf Baseline 与指定控件 Baseline 对齐
        app:layout_constraintStart_toEndOf
        app:layout_constraintStart_toStartOf
        app:layout_constraintEnd_toStartOf
        app:layout_constraintEnd_toEndOf
        
        
        app:layout_constraintWidth_percent  占指定控件宽度百分比
        app:layout_constraintHeight_percent 占指定控件高度百分比
        
        
        app:layout_constraintCirecle 表明参考的对象
        app:layout_constraintCirecle_Angle 控件中心与参考对象中心的夹角
        app:layout_constraintCirecle_Radius 控件中心与参考对象中心的距离
        
        
        app:layout_constraintHorizontal_bias 水平偏移
        app:layout_constraintVertical_bias 垂直偏移
    </ConstraintLayout>
-->
```

**边距**

```xml
<!--
    android:layout_marginStart与开头的边距
    android:layout_marginEnd 与末尾的边距
    android:layout_marginLeft 左边距
    android:layout_marginTop 上边距
    android:layout_marginRight 右边距
    android:layout_marginBottom 下边距
-->
```

在约束布局中想要设置 margin，必须约束好该控件 ConstraintLayout 中的位置。

**goneMargin**

goneMargin主要用于约束的控件可见性被设置为gone的时候使用的margin值。

```xml
<!--
    layout_goneMarginStart
    layout_goneMarginEnd
    layout_goneMarginLeft
    layout_goneMarginTop
    layout_goneMarginRight
    layout_goneMarginBottom
-->
```

**居中和偏移**

水平居中

```xml
    app:layout_constraintLeft_toLeftOf="parent"
    app:layout_constraintRight_toRightOf="parent"
```

垂直居中

```xml
    app:layout_constraintTop_toTopOf="parent"
    app:layout_constraintBottom_toBottomOf="parent"
```

水平+垂直居中

```xml
    app:layout_constraintLeft_toLeftOf="parent"
    app:layout_constraintRight_toRightOf="parent"
    app:layout_constraintTop_toTopOf="parent"
    app:layout_constraintBottom_toBottomOf="parent"
```

在居中的基础上设置 margin 可实现偏移，另一种偏移方式

```xml
    app:layout_constraintLeft_toLeftOf="parent"
    app:layout_constraintRight_toRightOf="parent"
    app:layout_constraintTop_toTopOf="parent"
    app:layout_constraintBottom_toBottomOf="parent
    app:layout_constraintHorizontal_bias 水平偏移
    app:layout_constraintVertical_bias 垂直偏移
```

**尺寸约束**

控件的尺寸可以使用四种方式约束

1. 直接指定具体的数值

2. 设置为 `wrap_content`，然后可设置最大最小尺寸

3. 设置为 0dp，则依照约束设定尺寸。

4. 当宽和高至少一个被设置成 0dp，可通过 `layout_constraintDimensionRatio` 设置宽高比。

# 事件监听

## 事件监听方式

### 使用匿名内部类

```java
public class MainActivity extends Activity {
    private Button btnshow;
    
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        btnshow = (Button) findViewById(R.id.btnshow);
        btnshow.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View v) {
                /*响应代码*/
            }
        });
    }
}
```

### 使用内部类

```java
public class MainActivity extends Activity {
    private Button btnshow;
    
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        btnshow = (Button) findViewById(R.id.btnshow);
        btnshow.setOnClickListener(new BtnClickListener);
    }
    
    class BtnClickListener implements View.OnClickListener {
        @Override
        public void onClick(View v) {
            /*响应代码*/
        }
    }
}
```

### 使用 Activity 作为事件监听器

```java
public class MainActivity extends Activity {
    private Button btwshow;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        btnshow = (Button) findViewById(R.id.btnshow);
        btnshow.setOnClickListener(this);
    }

    @Override
    public void onClick(View v) {
        /*响应代码*/
    }
}
```

## Handler 消息传递机制

Handler 的主要工作就是为了满足UI线程和工作线程间（子线程）的通信，主要作用有两个：

* 在新启动的线程发送消息

* 在主线程中获取、处理消息

由三部分构成：

* Handler
* MessageQueue
* Looper

新线程将消息发送至 MessageQueue，然后 Handler 不断从 MessageQueue 中获取并处理消息。Handler 从 MessageQueue 中读取消息就要用到 Looper，Looper 的 loop 方法负责读取 MessageQueue 中的消息，读取消息之后把消息发送给 Handler 来处理。

# Activity

## Activity 生命周期

## 创建 Activity

在 AndroidManifest.xml 文件中注册 Activity，在 `<application>` 标签下添加 `<activity>` 标签：

```xml
<manifest ...>
    <application ...>
        <activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN"/>
                <category android:name="android.intent.category.LAUNCHER"/>
            </intent-filter>
        </activity>
    </application>
</manifest>
```
创建布局文件 activity_main.xml：

```xml
<!-- 布局文件 -->
```

创建 MainActivity 类：

```java
public class MainActivity extends Activity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
}
```

## Intent

Intent 机制用来协助应用进行交互和通信，不仅可用于应用程序之间，也可以用于应用程序内部的 Activity 和 Service。

Intent 中的属性有：

* Action
* Data 
* Category
* Type
* Component
* Extras
* Flag

## 启动 Activity

### 显式调用

```java
    /*1.*/
    Intent intent = new Intent(当前的活动.this, 启动的活动.class);
    startActivity(intent);
    
    /*2.*/
    ComponentName cn = new ComponentName("当前活动的全限定类名", "启动活动的全限定类名");
    Intent intent = new Intent();
    intent.setComponent(cn);
    startActivity(intent);
    
    /*3.*/
    Intent intent = new Intent();
    intent.setClassName(this, "启动的类名");
    startActivity(intent);
```

### 隐式调用

```java
    Intent intent = new Intent;
    intent.setAction("myaction");
    intent.setCategory("mycategory");
    startActivity(intent);
```

在 Manifest.xml 文件中找到调用的 Activity，设置 <intent-filter> 中的 action 和 category 属性。

## Activity 间的数据传递

### Intent 机制

```java
    Intent intent = new Intent;
    
```

### Bundle 机制

```java

```

# 数据存储

## SharedPreference

## 文件存储

## Content Provider

## SQLite 存储

## SD 卡

# Content Provider

# BroadcastReceiver

# Service
