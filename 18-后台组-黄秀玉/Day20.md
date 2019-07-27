[toc]
# GUI（图形用户界面）

计算机与用户进行交互的两种方式：GUI和CLI
- GUI
  - Graphical User Interface（图形用户接口）
  - 用图形的方式，来显示计算机操作的界面，这样更方便更直观。
- CLI
  - Command line User Interface（命令行用户接口）
  - Dos命令行操作，需要记忆一些常用的命令，操作不直观。
 
Java为GUI提供的对象都存在java.Awt和javax.Swing两个包中。   
- java.Awt：Abstract Window ToolKit（抽象窗口工具包），需要调用本地系统方法实现功能。跨平台性不是很好，属于重量级控件。
- javax.Swing：在Awt的基础上，建立的一套图形界面系统，其中提供了更多的组件，而且完全由java实现。增强了移植性，属于轻量级控件。  

## GUI布局
容器中的组件的排放方式就是布局。   
常见的布局管理器：
- Flow Layout(流式布局管理器)
  - 从左到右的顺序排列。
  - Panel默认的布局管理器。
- BorderLayout(边界布局管理器)
  -  东西南北中
  -  Frame默认的布局管理器。
- GridLayout(网格布局管理器)
  - 规则的矩阵 
- CardLayout(卡片布局管理器)
  - 选项卡 
- GridBagLayout(网格布局管理器)
  - 非规则的矩阵 
 
## 事件监听机制 
组成：事件源（组件）、事件（Event)、监听器（listener）、事件处理（引发事件后处理方式） 

要实现相应的事件监听器接口，就必须实现其中的所有方法，有的接口中包含多个方法，而我们只需要其中的一两个，这时候其他方法就只是空实现。JDK针对大多数事件监听器接口定义了相应的实现类，称之为事件**适配器**（Adapter）类。在适配器类中，实现了相应监听器接口的所有方法，但不做任何事情，即这些Adapter类中的方法都是空的。只要继承适配器类，就等于实现了相应的监听器接口。如果要对某类事件的某种情况进行处理，只要覆盖相应的方法就可以了。   

## 窗体事件
构造函数  
Frame()：构造一个最初不可见的Frame新实例。  

父类component中组件的共性方法：    
1）void **setVisible**(boolean b) 
根据参数 b 的值显示或隐藏此组件。  

2）void **setBounds**(int x, int y, int width, int height)：移动组件并调整其大小。  

3）void **setLocation**(int x, int y)：将组件移到新位置。   

窗体事件示例：
```
public static void main(String[] args) 
{
    Frame f = new Frame("my awt");
    f.setSize(500,400);  
    f.setLocation(300,200);   
    f.setLayout(new FlowLayout());
    Button b = new Button("我是一个按钮");
    f.add(b);  
    f.addWindowListener(new WindowAdapter()
    {
        public void windowClosing(WindowEvent e)
        {
            System.exit(0);
        }
    });
    f.setVisible(true);
}
```

## 鼠标事件
接口MouseListener中的方法：    
1）void	**mouseClicked**(MouseEvent e)：鼠标按键在组件上单击（按下并释放）时调用。     
2）void	**mouseEntered**(MouseEvent e)：鼠标进入到组件上时调用。      
3）void	**mouseExited**(MouseEvent e)：鼠标离开组件时调用。    
4）void	**mousePressed**(MouseEvent e)：鼠标按键在组件上按下时调用。    
5）void	**mouseReleased**(MouseEvent e)：鼠标按钮在组件上释放时调用。

方法超过三个，使用配适器和匿名内部类。

MouseEvent中的方法：
int **getClickCount**()：返回与此事件关联的鼠标单击次数。

鼠标事件示例：

```
but.addMouseListener(new MouseAdapter()
{
    private int count = 1;
    private int clickCount = 1;
    public void mouseEntered(MouseEvent e)
    {
        System.out.println("鼠标进入到该组件"+count++);
    }
    public void mouseClicked(MouseEvent e)
    {
        if(e.getClickCount()==2)
            System.out.println("双击动作"+clickCount++);
    }
```

## 键盘事件  
接口KeyListener中的方法：    
1）void **keyPressed**(KeyEvent e) ：按下某个键时调用此方法。     
2）void **keyReleased**(KeyEvent e)：释放某个键时调用此方法。    
3）void **keyTyped**(KeyEvent e) ：键入某个键时调用此方法。

类KeyEvent中的方法：  
1）char **getKeyChar**() ：返回与此事件中的键关联的字符。      
2）int **getKeyCode**() ：返回与此事件中的键关联的整数 keyCode。 

键盘事件示例：

```
but.addKeyListener(new KeyAdapter()
{
    public void keyPressed(KeyEvent e)
    {
        System.out.println(e.getKeyChar());
    }
});
```
## TextField和TextArea
TextField构造函数：     
1）TextField()：构造新文本字段。      
2）TextField(int columns)：构造具有指定列数的新空文本字段。       
3）TextField(String text) ：构造使用指定文本初始化的新文本字段。

TextArea构造函数：        
1）TextArea()：构造一个将空字符串作为文本的新文本区。      
2）TextArea(int rows, int columns)：构造一个新文本区，该文本区具有指定的行数和列数，并将空字符串作为文本。

TextArea的方法：    
1）void **append**(String str)：将给定文本追加到文本区的当前文本。

## 菜单
MenuBar（菜单栏）     
Menu（菜单）    
MenuItem（菜单项）      
示例：
```
class MyMenuDemo
{
    private Frame f;//定义窗体
    private MenuBar mb;//定义菜单栏
    private Menu m,subMenu;//定义"文件"和"子菜单"菜单
    private MenuItem closeItem,subItem;//定义条目“退出”和“子条目”菜单项
    MyMenuDemo()
    {
        init();
    }
    
/*图形用户界面组件初始化*/
public void init()
{
    f=new Frame("my window");//创建窗体对象
    f.setBounds(300,100,500,600);//设置窗体位置和大小
    f.setLayout(new FlowLayout());//设置窗体布局为流式布局
    mb=new MenuBar();//创建菜单栏
    m=new Menu("文件");//创建“文件”菜单    
    subMenu = new Menu("子菜单");//创建“子菜单”菜单
    subItem=new MenuItem("子条目");//创建“子条目”菜单项
    closeItem=new MenuItem("退出");//创建“退出"菜单项
    m.add(subMenu);//将“子菜单”菜单添加到“文件”菜单上
    m.add(closeItem);//将“退出”菜单项添加到“文件”菜单上
    subMenu.add(subItem);//"子条目"菜单项添加到"子菜单"菜单项中
    mb.add(m);//将文件添加到菜单栏上
    f.setMenuBar(mb);//将此窗体的菜单栏设置为指定的菜单栏。
    myEvent();//加载事件处理
    f.setVisible(true);//设置窗体可见
}  
private void myEvent()
{
// 窗体关闭监听
    f.addWindowListener(new WindowAdapter() 
    {
        public void windowClosing(WindowEvent e) 
        {
            System.exit(0);
        }
    });
            
//退出菜单项监听
    closeItem.addActionListener(new ActionListener()
    {
        public void actionPerformed(ActionEvent e)
        {
            System.exit(0);
        }
    });
}

public static void main(String[] args)
{
    new MyMenuDemo();
}
}
```
