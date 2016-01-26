# zbbj
i am zb
- 有模拟器的程序的启动过程:先进入程序的入口main函数中，在main中，实现了跳转代理的类，在代理的类中，打包并指定程序的主入口(main.storyBoard)。然后加载箭头指向的视图控制器，然后再加载视图控制器里面的view，从而显示人们眼中能看到view上面的东西.view上能加载好多子视图(subview）,这时view对于子视图来说就是superview
- 只有实现代码中声明的名称和界面上控件的关系，就可以在代码上对该控件进行控制和设置了
- 强烈注意：self理解成视图控制器的对象(类型为UIViewController类型的指针)
- 技巧:在UI中以后只要对象前面有遇见self，就可以直接忽略self，直接理解成对象就行

![](http://images.cnblogs.com/cnblogs_com/crazysea/780725/o_a.png)
- 代码分成两页的快捷键:alt+command+Enter

- 375*667  iphone6s尺寸
- 每一个界面就是一个控制器 例如，打开一个页面A，返回，退回到初始的界面B,这里面就是两个控制器(A和B)


- IBAction:响应方法(通俗:连接方法,和方法相关).即点击按钮,就会执行返回值类型为IBAction的方法 注意:写上IBAction，并且还得用鼠标把故事版的控件和方法通过拖动线条的形式来进行关联
IBOutlet:获取对象的属性的修饰词(通俗:连接属性,和属性相关)。从而实现代码中声明的名称和界面上控件的关系，就可以在代码上对该控件进行控制和设置了.例如:如果仅仅是在故事版上放置了UILabel控件,肯定不能获取到控件的textColor属性。 注意:写上IBOutlet，并且还得用鼠标把故事版的控件和声明的属性通过拖动线条的形式来进行关联
故事版中的控件,右击控件，若有Sent Events,则能发送事件,即能和方法关联。亦即,则可以和返回值类型为IBOutlet的数据进行拖动关联
规律:继承于UIControl的类产生的对象都能和IBOutlet进行连线(事件交互)。反之,则不能进行连线

- 视图控制器包括两部分：一部分是视图，一部分是控制器。即一个是View，一个是Controller

        /*
        frame: 用来设置控件的位置和尺寸
        bounds:用来设置控件的尺寸(x,y一般为0),因为bounds以自身左上角的坐标为原点（0，0）所以只需要设只width喝height的值.
        center: 用来设置控件的位置
        frame以父控件的左上角为原点，bounds以自身左上角的坐标为原点（0，0）
         */
         redView.frame=CGRectMake(<#CGFloat x#>, <#CGFloat y#>, <#CGFloat width#>, <#CGFloat height#>);



        注意
        凡是继承于UIControl类产生的对象都能连线(进行事件交互,和返回值类型为IBAction的方法进行连接),反之,则不能
        在storyboard中右击查看有没有sentEvents,有,一定能够连线;
        没有,则一定不能连线
        Demo演示: UISwitch; ---> 继承UIControl
        UIStepper;---> 继承UIControl
        UISlider;---> 继承UIControl
        UIImageView;---> 不是继承UIControl



---
/*
 两个经典的错误:
 1.错误1
  - 描述:
  reason: '[<MainViewController 0x7f9529d16850> setValue:forUndefinedKey:]: this class is not key value coding-compliant for the key testLabel.'
  - 原因: 在storyboard中的控件有多余的连线
  - 解决: 删除多余的连线

 2. 错误2
  - 描述:
  reason: '-[MainViewController testClick]: unrecognized selector sent to instance 0x7fb9b8629060'
  - 原因: 在storyboard中的控件有多余的连线
  - 解决: 删除多余的连线 或者  添加新的方法
 */
