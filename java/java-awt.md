# java-awt（桌面应用开发）

## 简介

- GUI（Graphics User Interface）图形用户界面/接口
- AWT（Abstract Window Toolkit）抽象窗口工具集
- AWT是Sun公司最早提供的GUI库，完成布局，渲染由JVM调用平台系统完成
- 因AWT功能比较有限而后又提供了Swing库，Swing基于AWT并使用其事件处理机制
- Java使用AWT和Swing类完成图形用户界面开发（java.awt包）

## 框架窗口（`Frame`）

```java
Frame f = new Frame("测试窗口");
f.setBounds(30, 30, 250, 200);
f.setVisible(true);
```

## 面板（`Panel`）

```java
Panel p = new Panel();
p.add(new TextField(20));
p.add(new Button("测试"));
f.add(p);
```

## 滚动面板（`ScrollPane`）

```java
ScrollPane sp = new ScrollPane(ScrollPane.SCROLLBARS_ALWAYS);
sp.add(new TextField(20));
sp.add(new Button("测试"));
```

## 标签（`Label`）

## 单行文本框（`TextField`）

## 多行文本框（`TextArea`）

## 列表框（`List`）

## 下拉框（`Choice`）

## 复选框（`Checkbox`）

## 单选框（`CheckboxGroup`内`Checkbox`）

## 按钮（`Button`）

## 滚动条（`Scrollbar`）

## 对话框（`Dialog`）

```java
// 模式对话框，关闭后ower才能获得focus
Dialog d1 = new Dialog(ower, title, true);
// 非模式对话框
Dialog d2 = new Dialog(ower, title, false);
```

## 文件对话框（`FileDialog`）

```java
// 打开
FileDialog d1 = new FileDialog(ower, title, FileDialog.LOAD);
// 保存
FileDialog d2 = new FileDialog(ower, title, FileDialog.SAVE);
// 选中的文件路径
d.getDirectory();
// 选中的文件名
d.getFile();
```

## 菜单条（`MenuBar`）

```java
Frame f = new Frame("frame");
MenuBar mb = new MenuBar();
mb.add(memu);
f.setMenuBar(mb);
```

### 菜单（`Menu`）

- 常用构造器：`(名称)`和`(名称,快捷键)`

```java
Menu menu = new Menu("菜单");
menu.add(menuItem);
```

### 右键菜单（`PopupMenu`）

### 菜单项（`MenuItem`）

```java
MenuItem menuItem = new MenuItem("子菜单");
```

### 复选框菜单项（`CheckboxMenuItem`）

### 菜单快捷键（`MenuShortcut`）

```java
// 组合键（CTRL + A）
MenuShortcut ms = new MenuShortcut(KeyEvent.VK_A);
// 组合键（CTRL + SHIFT + A）
MenuShortcut ms = new MenuShortcut(KeyEvent.VK_A, true);
```

## 布局管理（LayoutManager）

### 流布局（`FlowLayout`）

- 顺序布局、遇边界折回换行

```java
f.setLayout(new FlowLayout(FlowLayout.LEFT, 20, 5));
f.add(new Button("测试"));
f.pack(); // 设置窗口为最佳大小
```

### 板块布局（`BorderLayout`）

- 分`EAST`、`SOUTH`、`WEST`、`NORTH`、`CENTER`五个区域
- 区域内组件覆盖

```java
f.setLayout(new BorderLayout(30, 5));
f.add(new Button("测试"), NORTH);
f.pack();
```

### 栅格布局（`GridLayout`）

- 通过设置行/列数、水平/垂直间隙形成网格区域

```java
p.setLayout(new GridLayout(3, 5, 4, 4));
p.add(new Button("测试"));
```

### 灵活栅格布局（`GridBagLayout`）

- 通过设置起始位置、水平/垂直跨越栅格数等，形成栅格组合的区域

```java
GridBagLayout gb = new GridBagLayout();
GridBagConstraints gbc = new GridBagConstraints();
f.setLayout(gb);
//设置栅格伸展方式
gbc.属性 = 值;
Button bt = new Button("测试");
gb.setConstraints(bt, gbc);
f.add(bt);
```

### 卡片布局（`CardLayout`）

- 层叠式布局，仅最上一层可见，通过切换层级显示不同层内容

```java
CardLayout c = new CardLayout();
p.setLayout(c);
p.add(new Button("测试1"));
p.add(new Button("测试2"));
c.previous(p);
c.next(p);
c.first(p);
c.last(p);
c.show(p, 组件);
```

### 盒子布局（`BoxLayout`）

- Swing库中新增该布局，功能与CardLayout相似但简化设置过程

## 绘图

### 组件类（`Component`）

- `paint(Graphics g)` 绘图
- `update(Graphics g)` 刷新
- `repaint()` 刷新重绘

### 画笔类（`Graphics`）

draw`Xxxx`() 方法

- `Line` 直线
- `String` 字符串
- `Rect` 矩形
- `RoundRect` 圆角矩形
- `Oval` 椭圆
- `Polygon` 多边形
- `Arc` 圆弧
- `Polyline` 折线
- `Image` 位图

```java
// 位图刷
BufferedImage(width,height,type);
// 位图文件
ImageIO.read(jpg、png);
```

fill`Xxxx`() 方法

- `Rect`
- `RoundRect`
- `Oval`
- `Polygon`
- `Arc`

set`Xxxx`() 方法

- `Color` 颜色
- `Font` 字体

### 画布类（`Canvas`）

- 创建其子类并重写`paint()`方法实现绘图
- `Timer(int, ActionListener)`处理事件
- `actionPerformed()`方法实现动画

## 事件

### 事件处理模型

- `Event Source` 事件源
- `Event` 事件
- `Event Listener` 事件监听器

### 组件事件（`ComponentEvent`）

```java
class MyListener implements ComponentListener { }
```

- `componentHidden` 组件隐藏
- `componentMoved` 组件移动
- `componentResized` 组件缩放
- `componentShown` 组件显示

### 容器事件（`ContainerEvent`）

```java
class MyListener implements ContainerListener { }
```

- `componentAdded` 添加组件
- `componentRemoved` 删除组件

### 窗口事件（`WindowEvent`）

```java
class MyListener implements WindowListener { }
```

- windowActivated
- windowClosed
- windowClosing
- windowDeactivated
- windowDeiconified
- windowIconified
- windowOpened

### 焦点事件（`FocusEvent`）

```java
class MyListener implements FocusListener { }
```

- `focusGained` 获得焦点
- `focusLost` 失去焦点

### 键盘事件（`KeyEvent`）

```java
class MyListener implements KeyListener { }
```

- `keyPressed` 按下
- `keyReleased` 松开
- `keyTyped` 单击按键

### 鼠标事件（`MouseEvent`）

```java
class MyListener implements MouseListener { }
```

- `mouseClicked` 单击
- `mouseEntered` 移入
- `mouseExited` 离开
- `mousePressed` 按下
- `mouseReleased` 松开鼠标

```java
class MyListener implements MouseMotionListener { }
```

- `mouseDragged` 按下移动
- `mouseMoved` 松开移动

### 组件绘制事件（`PaintEvent`）

### 动作事件（`ActionEvent`）

```java
class MyListener implements ActionListener { }
```

- `actionPerformed` 按钮、文本框、菜单项被单击

### 调节事件（`AdjustmentEvent`）

```java
class MyListener implements AdjustmentListener { }
```

- `adjustmentValueChanged` 滑块位置发生改变

### 选项事件（`ItemEvent`）

```java
class MyListener implements ItemListener { }
```

- `itemStateChanged` 选中或取消选中

### 文本事件（`TextEvent`）

```java
class MyListener implements TextListener { }
```

- `textValueChanged` 文本内容改变

## 事件适配器

- 提供了空方法来实现相应接口
- 按需重写方法即可，不用实现接口的所有方法
- ContainerAdapter
- FocusAdapter
- ComponentAdapter
- KeyAdapter
- MouseAdapter
- MouseMotionAdapter
- WindowAdapter

## 事件示例

```java
Frame f = new Frame("测试");
f.addWindowListener(new MyListener());

// 实现接口所有方法
class MyListener implements WindowListener { ... }

// 仅重写所需方法
class MyListener extends WindowAdapter {
    public void windowClosing(WindowEvent e) { System.exit(0); }
}

// 匿名内部类
f.addWindowListener(new WindowAdapter() {
    public void windowClosing(WindowEvent e) { System.exit(0); }
});
```
