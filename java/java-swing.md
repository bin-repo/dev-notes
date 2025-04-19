# Java 桌面应用开发基础

- AWT 用于编写图形界面应用程序的抽象窗口组件
- Swing 基于AWT接口进行升级和优化的图形界面应用程序的开发包

## 包依赖

```java
import java.awt.*;
import javax.swing.*;
```

## 组件类

- JFrame 窗体（组件容器）
- JPanel 面板（组件容器）
- JLabel 标签
- JTextField 文本框
- JTextArea 多行文本框
- JPasswordField 密码框
- JButton 按钮
- JCheckBox 多选框
- JRadioButton 单选框
- JComboBox 下拉框
- JList 列表框
- JScrollPane 滚动面板
- JSplitPane 拆分面板
- JTabbedPane 选项卡
- JToolBar 工具栏
- JMenuBar 菜单栏
- JMenu 菜单
- JMenuItem 菜单项

## 示例

```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.InputEvent;
import java.awt.event.KeyEvent;

public void demo() {
    JFrame jFrame = new JFrame();
    JFrame jFrame = new JFrame("窗体标题");
    // 窗体关闭按钮模式操作
    jFrame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    // 窗体大小（宽,高）
    jFrame.setSize(400, 300);
    // 窗体位置（top,left）
    jFrame.setLocation(10, 10);
    // 窗体布局
    jFrame.setLayout(new FlowLayout()); // 流式布局
    jFrame.setLayout(new GridLayout(3, 3)); // 栅格布局
    // 显示窗体
    jFrame.setVisible(true);

    JPanel jPanel = new JPanel();

    JLabel jLabel1 = new JLabel("用户名");
    JLabel jLabel2 = new JLabel(new ImageIcon("images/1.jpg"));
    JLabel jLabel3 = new JLabel("<html><a href='example.com'>exam</a></html>");
    jLabel3.setCursor(Cursor.getPredefinedCursor(Cursor.HAND_CURSOR));

    JTextField jTextField = new JTextField(16);
    JTextArea jTextArea = new JTextArea(10, 16);

    JPasswordField jPasswordField = new JPasswordField(6);

    JCheckBox jCheckBox1 = new JCheckBox("足球");
    JCheckBox jCheckBox2 = new JCheckBox("蓝球");

    JRadioButton jRadioButton1 = new JRadioButton("男");
    JRadioButton jRadioButton2 = new JRadioButton("女");
    ButtonGroup buttonGroup = new ButtonGroup();
    buttonGroup.add(jRadioButton1);
    buttonGroup.add(jRadioButton2);

    String[] options = {"北京", "上海", "广州", "深圳"};
    JComboBox<String> jComboBox = new JComboBox<>(options);

    JList<String> jList = new JList<>(options);
    jList.setVisibleRowCount(1);
    // 滚动面板
    JScrollPane jScrollPane = new JScrollPane(jList);
    // 拆分面板
    JPanel jPanel1 = new JPanel();
    JPanel jPanel2 = new JPanel();
    JSplitPane jSplitPane = new JSplitPane(JSplitPane.HORIZONTAL_SPLIT, jPanel1, jPanel2);
    // 选项卡
    JTabbedPane jTabbedPane = new JTabbedPane();
    jTabbedPane.add("选项卡1", jPanel1);
    jTabbedPane.add("选项卡2", jPanel2);
    // 工具栏
    JButton jButton1 = new JButton(new ImageIcon("images/1.png"));
    jButton1.setToolTipText("按钮1");
    JButton jButton2 = new JButton(new ImageIcon("images/2.png"));
    jButton1.setToolTipText("按钮2");
    JToolBar jToolBar = new JToolBar();
    jToolBar.add(jButton1);
    jToolBar.add(jButton2);
    // 菜单栏
    JMenuBar jMenuBar = new JMenuBar();
    JMenu menu1 = new JMenu("文件（F）");
    menu1.setMnemonic('F'); // 助记符
    JMenu menu2 = new JMenu("新建");
    JMenuItem jMenuItem1 = new JMenuItem("文件");
    jMenuItem1.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_F, InputEvent.ALT_DOWN_MASK));
    JMenuItem jMenuItem2 = new JMenuItem("工程");
    menu2.add(jMenuItem1);
    menu2.addSeparator();
    menu2.add(jMenuItem2);
    jMenuBar.add(menu1);
    jMenuBar.add(menu2);
    jFrame.setJMenuBar(jMenuBar);
    // 按钮事件
    JButton jButton = new JButton("提交");
    jButton.addActionListener(e -> {
        // todo
    });
}
```
