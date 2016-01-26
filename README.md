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
# 第二天
- 你遇到的问题，你老是忘记写这句代码   _imageView=imageView;这句其实就一个作用，就是把局部变量赋给全局变量，因为局部变量出了{}就被销毁了，必须用赋给一个全局变量,这样的话，即使出了{},也能在外面使用

-  利用@property来生成setter/getter方法，我们可以不写成员变量，系统会自动给我们生成一个_开头的私有的成员变量.
也就是说是在.m文件中生成的，而不是在在.h文件中生成的 在.m文件中我们不用写出来这个私有的成员变量，因为它使存在的，不过是隐形的罢了.   UI代理中，经常用到这个.m文件中的这个以下划线私有成员变量，即实例变量



        1.2 把NSString类型转为NSInteger
        NSInteger num1 = [num1String integerValue];
        NSInteger num2 = [num2String integerValue];

        1.4 把结果转成NSString类型,显示到resultLabel上面
        self.resultLabel.text = [NSString
        stringWithFormat:@"%zd", result];

![](http://images.cnblogs.com/cnblogs_com/crazysea/780725/o_b.png)

- 有些方法新版本的xcode摒弃了以前的旧方法，可以通过适配旧版本来使用旧方法仍然可以使用 将高版本改为低版本

![](http://images.cnblogs.com/cnblogs_com/crazysea/780725/o_d.png)
![](http://images.cnblogs.com/cnblogs_com/crazysea/780725/o_c.png)


- 若不适配，则会如下图提示警告


](http://images.cnblogs.com/cnblogs_com/crazysea/780725/o_e副本.png)

- 子控件加载到父控件上，在故事版中无法加载，只有通过代码加载。下面将Button控件的对象button1加载到视图控制器的图视图中  [self.imageView addSubview:button1];


            // 第一种:
    /*
     UIImageView *imageView = [[UIImageView alloc] init];
     imageView.frame = CGRectMake(10, 100, 400, 198); //等价于imageView.frame=(CGRect){{10,100},{400,198}};  (CGRect)是强制类型转换
     // 设置图片
     imageView.image = [UIImage imageNamed:@"a"];
     [self.view addSubview:imageView];
    */
    // 第二种:
    /*
     UIImage *image = [UIImage imageNamed:@"a"];
     UIImageView *imageView = [[UIImageView alloc] initWithFrame:CGRectMake(10, 10, image.size.width, image.size.height)];
     imageView.image = image;
     [self.view addSubview:imageView];
     */

    // 第三种 ---> 注意: 如果用initWithImage:创建,控件的尺寸默认就是图片的尺寸
    /*
     UIImageView *imageView = [[UIImageView alloc] initWithImage:[UIImage imageNamed:@"a"]];
     #warning 注意 - 要单独设置控件的位置
     imageView.center = CGPointMake(100, 100);
     [self.view addSubview:imageView];

     }*/
    //第四种
    /*
    UIImage *image=[UIImage imageNamed:@"a"];
    UIImageView *imageView=[[UIImageView alloc]initWithFrame:CGRectMake(100, 100, image.size.width, image.size.height)];
    imageView.image=image;//易忘:将UIImage的对象image赋给图片视图的image属性，使用图片视图上拥有了名为a的图片
    [self.view addSubview:imageView];
    */

-

        //技巧:逆推法 根据参数的类型,你就知道你还要创建哪个类型的对象。
        NSString *path=[NSBundle mainBundle] pathForResource:<#(nullable NSString *)#> ofType:<#(nullable NSString *)#>];//4
        NSURL *url=NSURL URLWithString:<#(nonnull NSString *)#>];//3
        AVPlayerItem *Item=[AVPlayerItem playerItemWithURL:<#(nonnull NSURL *)#>];//2
        AVPlayer *player=[AVPlayer playerWithPlayerItem:<#(nonnull AVPlayerItem *)#>];//1

---
        //逆推法+将很多图片依次放入数组
        //1.创建存放图片的动态数组
    NSMutableArray<UIImage *> *arr=[NSMutableArray array];
    //2.利用循环,实现图片按序号依次放入数组中
    for (int i=1; i<39; i++) {
        //获取到图片的名字
        NSString *imageN=[NSString stringWithFormat:<#(nonnull NSString *), ...#>];//3
        //获取到图片
        UIImage *imag=[UIImage imageNamed:<#(nonnull NSString *)#>];//2
        //依次将图片放入数组
        [arr addObject:<#(nonnull UIImage *)#>];//1

- 模拟器上的效果显示不全的解决办法:
- 1.在故事板中将ImageView的Mode设置为Aspect Fill
- 2.将模拟器的6s plus改为6s





- 在打断点的情况下,可以得知 self代表的是ViewController类型的一个对象(对象即保存地址的指针)。如下图所示


![](http://images.cnblogs.com/cnblogs_com/crazysea/780725/o_f.png)

![](http://images.cnblogs.com/cnblogs_com/crazysea/780725/o_g.png)






- 超级精华:打断点，鼠标悬停在self上，从而判断self代表的地址

        @interface ViewController ()

        @property (weak,nonatomic) IBOutlet UIImageView *imageView;
        @end
ViewController后面的()没有名字,所以是匿名扩展(即匿名类别).可以用@property声明属性,并且自动生成setter和getter方法以及以下划线开头的实例变量_imageView，其实是类型为UIImageView类型的指针(即对象),下面的周杰伦图片是鼠标悬停在_imageView上自动产生的，因为在故事版的UIImageView控件上加了这张图片。又因为_imageView实例变量(对象)代表了这个UIImageView,所以会显示出这张图片
![](http://images.cnblogs.com/cnblogs_com/crazysea/780725/o_h副本.png)
---
若ViewController后面的()有名称，这里是非匿名类别,所以用@property声明的属性不会自动生成实例变量_imageView，只会自动生成setter和getter方法

---
实例变量:声明在{}中,如果变量的数据类型是一个类,则这个变量就是实例变量.例如 UIButton *myButton; 其实,实例变量是成员变量的特殊形式.实例变量是类内部使用的,无需于外界接触,即类私有变量.只要在同一个类,无论类中有多少个方法,都能在方法中使用这个实例变量,此时实例变量作为全局变量来使用.而局部变量,只要出了方法的花括号{},就被销毁了，就不能再同一个类的其他方法中使用

        @property (nonatomic, strong) AVPlayer *player;
        //_player此时是个指针(即对象)，保存了右边传过来的地址.从这可以验证实例变量就是个对象
        _player = [[AVPlayer alloc] initWithPlayerItem:playerItem];//等价 AVPlayer *player= [[AVPlayer alloc] initWithPlayerItem:playerItem]; 
        
- ####强烈注意:_imageView是实例变量,也叫做对象。UIImageView既叫控件,也叫类.所以可以有[_imageView UIImageView中的对象方法];
####


---




        //精华:右边的self代表了ViewController的对象。因为你看一下左边的一栏,可以看到这些方法都是在ViewController.m文件中的即都是在ViewController类中  对象调用对象方法很正常啊。
        //因为loadImagesWithImageCount:kStandImageCount imageNamePrefix:@"stand"方法是对象方法，谁能调用？ 图片视图UIImageView的对象_imageView？很显然不是.因为这个对象方法是自己自定义的.在UIImageView类中根本没有这个方法.这个方法是在ViewController.m类中的。很显然,self代表了ViewController的对象

        self.standImagesArray = [self loadImagesWithImageCount:kStandImageCount imageNamePrefix:@"stand"];//右边的返回值类型是NSMutableArray类型的，所以可以用_standImagesArray对象接收。因为_standImagesArray对象也是NSMutableArray类型的





         Bundle就是包(package)的意思，其实就是一个Bundle文件夹
         imageNamed:加载图片,就算没有强指针指向,也不会从内存中被干掉 (默认带有缓存)
         imageWithContentFile:加载图片,如果没有强指针指向,就会被从内存中被干掉 (默认不带有缓存)
         
         放到Assets.xcassets中的图片默认就带有缓存
         使用场景:
        imageNamed: 1)图片经常会被使用  2)少量的图片
         imageWithContentFile: 1)图片不经常被使用  2)大批量的图片
         
        图片的加载方式:

        方式1:  imageNamed:       方式2:  imageWithContentsOfFile:
        
        a:图片放在Assets.xcassets中:
        1.图片在资源包中的Assets.car的内部,且无法看到里面的图片，所以无法获取到路径，最多只能看到Assets.xcassets文件的路径
        2.只能通过imageNamed:这种方式来加载图片m不能通过imageWithContentsOfFile:这种方式来加载图片
 
        b:图片放到放到项目目录中:
        1.图片资源会被打包到MainBundle中,所以能够获取到图片的路径
        2.能通过imageWithContentsOfFile:的方式和imageNamed:两种方式来加载图片

        - (void)viewDidLoad {
        [super viewDidLoad];
    
        // 图片的两种加载方式  选方式二虽然麻烦，但还是选方式二，是因为涉及缓存问题
    
        // 方式一:既可以加载Assets.xcassets内部的图片,也能够加载Assets.xcassets外面的图片
        //self.imageView.image = [UIImage imageNamed:@"1.jpg"];
    
        // 方式二:
        // 不可取。不能加载Assets.xcassets内部的图片
        self.imageView.image = [UIImage imageWithContentsOfFile:@"/Users/xiaomage/Desktop/课堂共享/01-UI基础/Day2/代码/07-资源存放问题/07-资源存放问题/Assets.xcassets/kb.imageset/kb.jpg"];
        // 方式二:从资源包中加载图片，获取资源包的路径(前提条件，不能将图片放在Assets.xcassets中,只需放在Assets.xcassets的外面就行)  方式二只能加载Assets.xcassets的外面的图片,不能加载Assets.xcassets内部的图片
        // 精华:只要执行了[NSBundle mainBundle]，就已经进入了资源包
        NSString *path = [[NSBundle mainBundle] pathForResource:@"1.jpg" ofType:nil];
        self.imageView.image = [UIImage imageWithContentsOfFile:path];
        }
        
        
        以上总结:
        imageNamed:方法 加载图片，既可以Assets.xcassets内部，也可以放在Assets.xcassets外部的图片。默认带有缓存。
        imageWithContentsOfFile:方法 加载图片，不能将图片放在以Assets.xcassets内部，只能放在以Assets.xcassets内部外部。默认不带有缓存



- 从下面的文档中可知imageNamed：方法是从 main bundle中加载
- 
![](http://images.cnblogs.com/cnblogs_com/crazysea/780725/o_Snip20160121_9.png)

![](http://images.cnblogs.com/cnblogs_com/crazysea/780725/o_i.png)
![](http://images.cnblogs.com/cnblogs_com/crazysea/780725/o_j.png)
![](http://images.cnblogs.com/cnblogs_com/crazysea/780725/o_k.png)
---

     
        // size属性是结构体类型.并且被readonly修饰.说明size属性只有getter方法没有setter方法.即:只能获取值，不能赋值
        @property(nonatomic,readonly) CGSize size; 


 

# 第六天

-  你遇到的问题，你老是忘记写这句代码   _imageView=imageView;这句其实就一个作用，就是把局部变量赋给全局变量，因为局部变量出了{}就被销毁了，必须用赋给一个全局变量,这样的话，即使出了{},也能在外面使用

滚动前提:设置contenSize的尺寸+scrollEnabled属性设置为YES(是否能够滚动,默认为YES)/userInteractionEnabled属性设置为YES(是否能够能够跟用户进行交互默认为YES)
scrollEnabled和userInteractionEnabledquiet区别:userInteractionEnabled设置为NO时,模拟器接界面上任何控件或者子控件都不能点击(都不能和用户进行交互)
可滚动的尺寸:contentSize的尺寸减去scrollView的尺寸。如果contentSize的尺寸小于或者等于scrollView的尺寸,则不能滚动.contentSize决定图片滚动的范围


- 通过打印%@类型的 self.scrollView.subViews 可以看到scrollView上有几个子控件  subViews数组. 
- 箭头指向的地方表示3scrollView上有3个子控件,分别是一个imageView上的image+两个滚动条.强烈注意:image是加载到imageView上的，所以imageView多大，image就有多大。又因为imageView是加载到UIScrollView上的,因为有image->imageView->scrollView这层关系,所以最终,scrollView多大,那么image就有多大。因为scrollView是510x510，所以image的大小也是510x510
![](06-01.png)


- 是contentView滚动而不是scrollView滚动.scrollView里面存放的是UIImageView中的image。切记:scrollView是固定不动的.动的是contenView
![](06-02.png)

- contentOffset是scrollView的属性. 
- 偏移量的的值：contentView的左上角的值与scrollView的左上角的值之差，就是contentOffset   偏移量(有正负)


![](06-03.png)

- 代理方法就是协议里的方法
- 
任何oc对象都可以作为代理，一般情况下是控制器

![](06-09.png)
![](06-10.png)
        #import "ViewController.h"
        #import "Car.h"
        @interface ViewController ()
        @property(nonatomic,strong) Car *car;
        @end
        
        @implementation ViewController
        
        - (void)viewDidLoad {
            //1.UIScrollView
            UIScrollView *scrollView=[[UIScrollView alloc]init];
            scrollView.backgroundColor=[UIColor redColor];
            scrollView.frame=CGRectMake(20, 20, 300, 200);
            [self.view addSubview:scrollView];
            //2.UIImageView
            UIImageView *imageView=[[UIImageView alloc]initWithImage:[UIImage imageNamed:@"minion"]];
           [scrollView addSubview:imageView];
            //3.contenSize
           scrollView.contentSize=CGSizeMake(510, 510);
            //设置代理
            /*之所以会提示警告是因为,[[Car alloc]init]返回的地址是用一个等号左边的弱指针保存的.
             点击delegate，进入文档,可以看到@property (nonatomic, weak, nullable) id <UITableViewDelegate> delegate;
             所以可以知道,delegate是一个weak，即弱指针,所以这一行代码执行完毕之后,就立刻被销毁了。
             若不想被销毁,左边必须用一个强指针,可以在最上方敲@property(nonatomic,strong) Car *car;用car这个强指针指向[[Car alloc]init].
             只要控制器UIViewController在,那么Car类的对象在，Car类的对象在，那么等号左边一定是一个强指针保存等号右边的地址。
           */
             scrollView.delegate=[[Car alloc]init];//1   将1用两行2替代
            
        //    self.car=[[Car alloc]init];//2
        //    scrollView.delegate=self.car;//2
        }

---
                //
        //  Car.h
        //  a
        //
        //  Created by zhangbin on 16/1/26.
        //  Copyright © 2016年 zhangbin. All rights reserved.
        //
        
        #import <UIKit/UIKit.h>//头文件必须是UIKit/UIKit.h,框架若是UIScrollViewDelegate,则<UIScrollViewDelegate>添加不了
        
        @interface Car : NSObject<UIScrollViewDelegate>
        
        @end
        
        
                //
        //  Car.m
        //  a
        //
        //  Created by zhangbin on 16/1/26.
        //  Copyright © 2016年 zhangbin. All rights reserved.
        //
        
        #import "Car.h"
        
        @implementation Car
        
        -(void)scrollViewDidScroll:(UIScrollView *)scrollView{
         NSLog(@"%s",__func__);
        }
        @end

-面试必问: 苹果为什么设计代理属性为weak？

4条实线构成了一个循环,不会被销毁,所以会发生内存泄露,即内存释放不了。 代理属性设置为weak，为了防止循环引用.
![](06-04.png)
![](06-05.png)

详细解释:
![](06-11.png)



- NSInteger是根据系统的类型来决定是长整形还是整形,所以如果出现警告,可以用ld，zd格式符来解决警告的问题
- addTarget:<#(nullable id)#> action:<#(nonnull SEL)#> forControlEvents:<#(UIControlEvents)#>以下简写为addTarget方法.
- 
只要继承于UIControl的类(例如UIButton)，就可以利用addTarget方法来监该听类的对象的行为,把触发addTarget事件的对象传递进来作为addTarget方法中的参数。并且再跳转至@selector后面的另一个方法中

- 因为UIButton直接继承于UIControl,而UIControl里面有addTarget方法，方法中的参数就是促发该方法的对象，一般是UIButton的对象，所以可以利用addTarget方法来监该听类的对象的行为.
- 因为UIScrollView继承于UIView，不继承于UIButton，所以不能用UIButton里面的addTarget的方法. 而UIView里面有代理方法 delegate，所以可以用代理方法.
![](06-06.png)

- 局部变量,只要出了大括号,局部变量就不复存在,就会被销毁.

- 以下两张图片的内容等价。即 通过故事版连线.实现让控制器成为scrollView的代理 等价于代码self.scrollView=self;
![](06-07.png)
![](06-08.png)

rootViewController-->UIViewController的view-->UIView的subViews数组-->

         //CGSizeMake:设置宽高
        scrollView.contentSize=CGSizeMake(510, 510);
        //CGRectMake:设置坐标以及宽和高
        imageView.frame=CGRectMake(0, 0, 300, 500);
        
        
---
- 分页的标准:以scrollView的尺寸为一页
- 

- 
- UIEdgeInsetsMake(20,30,40,50)代表的具体含义如下图。 （上坐下右）其实就是距离上边距可以多出20的像素，向左多出30的像素，向下多出40的像素,向右多出50的像素。但是多出的部分不能加任何东西，仅仅作为多出的空白区域，并且如果拖动到了多出的空白区域的时候，并不会使那个空白的区域消失，即使加了弹簧效果。
![](06-12.png)


![](06-13.png)



- 计算contentSize的偏移量（加精） 核心:就看对应的左上角的坐标即可。
![](06-14.png)

            ////用四舍五入算法实现 当进入视野的图片(第二页)的范围大于将要消失的图片(第一页)的范围的时候，页码自动显示为第二页，而不是当第二页的图片全部进入视野，才才显示第二页。即在滚动的过程中显示页码
            - (void)scrollViewDidScroll:(UIScrollView *)scrollView
            {
                // 四舍五入 (int)(小数 + 0.5)  即+0.5是别人总结出来的公式   +0.5的形式实现了四舍五入算法。
                // 0.3->0  (int)(0.3 + 0.5)= 0.8 -> 0
                // 0.4->0  (int)(0.4 + 0.5)= 0.9 -> 0
                // 1.4->1  (int)(1.4 + 0.5)= 1.9 -> 1
                // 1.6->2  (int)(1.6 + 0.5)= 2.1 -> 2
                // 四舍五入算法技巧总结: scrollView的尺寸等于每张图片的大小，所以假设尺寸为1.
                //                   当前x的偏移量0.3+0.5=0.8，0.8/1 ->0, 0.3根据四舍五入，得0。而0.8是通过加0.5的形式实现了四舍五入算法。
                //                   当前x的偏移量0.4+0.5=0.9，0.9/1 ->0, 0.4根据四舍五入,得0。而0.9是通过加0.5的形式实现了四舍五入算法。
                //                   当前x的偏移量1.4+0.5=1.9，1.9/1 ->1, 1.4根据四舍五入,得1。而1.9是通过加0.5的形式实现了四舍五入算法。
                //                   当前x的偏移量1.6+0.5=0.9，2.1/1 ->2, 1.6根据四舍五入,得2。而2.1是通过加0.5的形式实现了四舍五入算法。
                // 计算页码
                int page = (int)(scrollView.contentOffset.x / scrollView.frame.size.width + 0.5);
                
                // 设置页码
                self.pageControl.currentPage = page;
            }

---
            //以下两个方法实现了，当停止滚动时，页码才显示，而不是在滚动的过程中就显示页码

            - (void)scrollViewDidEndDragging:(UIScrollView *)scrollView willDecelerate:(BOOL)decelerate
            {
                if (decelerate == NO) {
                    // 计算页码
                    int page = scrollView.contentOffset.x / scrollView.frame.size.width;
                    
                    // 设置页码
                    self.pageControl.currentPage = page;
                }
                
            }
            
            - (void)scrollViewDidEndDecelerating:(UIScrollView *)scrollView
            {
                // 计算页码
                int page = scrollView.contentOffset.x / scrollView.frame.size.width;
                
                // 设置页码
                self.pageControl.currentPage = page;
            }


