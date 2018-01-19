Java初级面试题
96  小二叔 关注
2016.12.23 16:21* 字数 57829 阅读 6180评论 17喜欢 311
1. Java基础部分

基础部分的顺序：基本语法，类相关的语法，内部类的语法，继承相关的语法，异常的语法，线程的语法，集合的语法，io的语法，虚拟机方面的语法。

1、一个".java"源文件中是否可以包括多个类（不是内部类）？有什么限制？

可以有多个类，但只能有一个public的类，并且public的类名必须与文件名相一致。

2、Java有没有goto?

java中的保留字，现在没有在java中使用。

3、说说&和&&的区别。

&和&&都可以用作逻辑与的运算符，表示逻辑与（and），当运算符两边的表达式的结果都为true时，整个运算结果才为true，否则，只要有一方为false，则结果为false。

&&还具有短路的功能，即如果第一个表达式为false，则不再计算第二个表达式，例如，对于if(str != null&& !str.equals(“”))表达式，当str为null时，后面的表达式不会执行，所以不会出现NullPointerException如果将&&改为&，则会抛出NullPointerException异常。If(x==33 &++y>0) y会增长，If(x==33 && ++y>0)不会增长

&还可以用作位运算符，当&操作符两边的表达式不是boolean类型时，&表示按位与操作，我们通常使用0x0f来与一个整数进行&运算，来获取该整数的最低4个bit位，例如，0x31 & 0x0f的结果为0x01。

备注：这道题先说两者的共同点，再说出&&和&的特殊之处，并列举一些经典的例子来表明自己理解透彻深入、实际经验丰富。 f

4、在JAVA中如何跳出当前的多重嵌套循环？

在Java中，要想跳出多重循环，可以在外面的循环语句前定义一个标号，然后在里层循环体的代码中使用带有标号的break语句，即可跳出外层循环。例如，

ok:

for(int i=0;i<10;i++)     {

for(int j=0;j<10;j++)            {

System.out.println(“i=” + i + “,j=” + j);

if(j == 5) break ok;

}

}

另外，我个人通常并不使用标号这种方式，而是让外层的循环条件表达式的结果可以受到里层循环体代码的控制，例如，要在二维数组中查找到某个数字。

int arr[][] ={{1,2,3},{4,5,6,7},{9}};

boolean found = false;

for(int i=0;i

for(int j=0;j

System.out.println(“i=” + i + “,j=” + j);

if(arr[i][j]  ==5) {

found = true;

break;

}

}

}

5、switch语句能否作用在byte上，能否作用在long上，能否作用在String上?

在switch（expr1）中，expr1只能是一个整数表达式或者枚举常量（更大字体），整数表达式可以是int基本类型或Integer包装类型，由于，byte,short,char都可以隐含转换为int，所以，这些类型以及这些类型的包装类型也是可以的。显然，long和String类型都不符合switch的语法规定，并且不能被隐式转换成int类型，所以，它们不能作用于swtich语句中。

6、short s1 = 1; s1 = s1 + 1;有什么错? short s1 = 1; s1 += 1;有什么错?

对于short s1 = 1; s1 = s1 + 1;由于s1+1运算时会自动提升表达式的类型，所以结果是int型，再赋值给short类型s1时，编译器将报告需要强制转换类型的错误。

对于short s1 = 1; s1 += 1;由于 +=是java语言规定的运算符，java编译器会对它进行特殊处理，因此可以正确编译。

7、char型变量中能不能存贮一个中文汉字?为什么?

char型变量是用来存储Unicode编码的字符的，unicode编码字符集中包含了汉字，所以，char型变量中当然可以存储汉字啦。不过，如果某个特殊的汉字没有被包含在unicode编码字符集中，那么，这个char型变量中就不能存储这个特殊汉字。补充说明：unicode编码占用两个字节，所以，char类型的变量也是占用两个字节。

备注：后面一部分回答虽然不是在正面回答题目，但是，为了展现自己的学识和表现自己对问题理解的透彻深入，可以回答一些相关的知识，做到知无不言，言无不尽。

8、用最有效率的方法算出2乘以8等於几?

2 << 3，

因为将一个数左移n位，就相当于乘以了2的n次方，那么，一个数乘以8只要将其左移3位即可，而位运算cpu直接支持的，效率最高，所以，2乘以8等於几的最效率的方法是2 << 3。

9、请设计一个一百亿的计算器

首先要明白这道题目的考查点是什么，一是大家首先要对计算机原理的底层细节要清楚、要知道加减法的位运算原理和知道计算机中的算术运算会发生越界的情况，二是要具备一定的面向对象的设计思想。

首先，计算机中用固定数量的几个字节来存储的数值，所以计算机中能够表示的数值是有一定的范围的，为了便于讲解和理解，我们先以byte类型的整数为例，它用1个字节进行存储，表示的最大数值范围为-128到+127。-1在内存中对应的二进制数据为11111111，如果两个-1相加，不考虑Java运算时的类型提升，运算后会产生进位，二进制结果为1,11111110，由于进位后超过了byte类型的存储空间，所以进位部分被舍弃，即最终的结果为11111110，也就是-2，这正好利用溢位的方式实现了负数的运算。-128在内存中对应的二进制数据为10000000，如果两个-128相加，不考虑Java运算时的类型提升，运算后会产生进位，二进制结果为1,00000000，由于进位后超过了byte类型的存储空间，所以进位部分被舍弃，即最终的结果为00000000，也就是0，这样的结果显然不是我们期望的，这说明计算机中的算术运算是会发生越界情况的，两个数值的运算结果不能超过计算机中的该类型的数值范围。由于Java中涉及表达式运算时的类型自动提升，我们无法用byte类型来做演示这种问题和现象的实验，大家可以用下面一个使用整数做实验的例子程序体验一下：

int a = Integer.MAX_VALUE;

int b = Integer.MAX_VALUE;

int sum = a + b;

System.out.println(“a=”+a+”,b=”+b+”,sum=”+sum);

先不考虑long类型，由于int的正数范围为2的31次方，表示的最大数值约等于2*1000*1000*1000，也就是20亿的大小，所以，要实现一个一百亿的计算器，我们得自己设计一个类可以用于表示很大的整数，并且提供了与另外一个整数进行加减乘除的功能，大概功能如下：

（）这个类内部有两个成员变量，一个表示符号，另一个用字节数组表示数值的二进制数

（）有一个构造方法，把一个包含有多位数值的字符串转换到内部的符号和字节数组中

（）提供加减乘除的功能

public class BigInteger{

int sign;

byte[] val;

public Biginteger(String val) {

sign = ;

val = ;

}

public BigInteger add(BigInteger other)       {

}

public BigInteger subtract(BigInteger other) {

}

public BigInteger multiply(BigInteger other){

}

public BigInteger divide(BigInteger other){

}

}

备注：要想写出这个类的完整代码，是非常复杂的，如果有兴趣的话，可以参看jdk中自带的java.math.BigInteger类的源码。面试的人也知道谁都不可能在短时间内写出这个类的完整代码的，他要的是你是否有这方面的概念和意识，他最重要的还是考查你的能力，所以，你不要因为自己无法写出完整的最终结果就放弃答这道题，你要做的就是你比别人写得多，证明你比别人强，你有这方面的思想意识就可以了，毕竟别人可能连题目的意思都看不懂，什么都没写，你要敢于答这道题，即使只答了一部分，那也与那些什么都不懂的人区别出来，拉开了距离，算是矮子中的高个，机会当然就属于你了。另外，答案中的框架代码也很重要，体现了一些面向对象设计的功底，特别是其中的方法命名很专业，用的英文单词很精准，这也是能力、经验、专业性、英语水平等多个方面的体现，会给人留下很好的印象，在编程能力和其他方面条件差不多的情况下，英语好除了可以使你获得更多机会外，薪水可以高出一千元。

10、使用final关键字修饰一个变量时，是引用不能变，还是引用的对象不能变？

使用final关键字修饰一个变量时，是指引用变量不能变，引用变量所指向的对象中的内容还是可以改变的。例如，对于如下语句：

final StringBuffer a=new StringBuffer("immutable");

执行如下语句将报告编译期错误：

a=new StringBuffer("");

但是，执行如下语句则可以通过编译：

a.append(" broken!");

有人在定义方法的参数时，可能想采用如下形式来阻止方法内部修改传进来的参数对象：

public void method(final  StringBuffer param){

}

实际上，这是办不到的，在该方法内部仍然可以增加如下代码来修改参数对象：

param.append("a");

11、"=="和equals方法究竟有什么区别？

（单独把一个东西说清楚，然后再说清楚另一个，这样，它们的区别自然就出来了，混在一起说，则很难说清楚）

==操作符专门用来比较两个变量的值是否相等，也就是用于比较变量所对应的内存中所存储的数值是否相同，要比较两个基本类型的数据或两个引用变量是否相等，只能用==操作符。

如果一个变量指向的数据是对象类型的，那么，这时候涉及了两块内存，对象本身占用一块内存（堆内存），变量也占用一块内存，例如Objet obj = new Object();变量obj是一个内存，new Object()是另一个内存，此时，变量obj所对应的内存中存储的数值就是对象占用的那块内存的首地址。对于指向对象类型的变量，如果要比较两个变量是否指向同一个对象，即要看这两个变量所对应的内存中的数值是否相等，这时候就需要用==操作符进行比较。

equals方法是用于比较两个独立对象的内容是否相同，就好比去比较两个人的长相是否相同，它比较的两个对象是独立的。例如，对于下面的代码：

String a=new String("foo");

String b=new String("foo");

两条new语句创建了两个对象，然后用a/b这两个变量分别指向了其中一个对象，这是两个不同的对象，它们的首地址是不同的，即a和b中存储的数值是不相同的，所以，表达式a==b将返回false，而这两个对象中的内容是相同的，所以，表达式a.equals(b)将返回true。

在实际开发中，我们经常要比较传递进行来的字符串内容是否等，例如，String input = …;input.equals(“quit”)，许多人稍不注意就使用==进行比较了，这是错误的，随便从网上找几个项目实战的教学视频看看，里面就有大量这样的错误。记住，字符串的比较基本上都是使用equals方法。

如果一个类没有自己定义equals方法，那么它将继承Object类的equals方法，Object类的equals方法的实现代码如下：

boolean equals(Object o){

return this==o;

}

这说明，如果一个类没有自己定义equals方法，它默认的equals方法（从Object类继承的）就是使用==操作符，也是在比较两个变量指向的对象是否是同一对象，这时候使用equals和使用==会得到同样的结果，如果比较的是两个独立的对象则总返回false。如果你编写的类希望能够比较该类创建的两个实例对象的内容是否相同，那么你必须覆盖equals方法，由你自己写代码来决定在什么情况即可认为两个对象的内容是相同的。

12、静态变量和实例变量的区别？

在语法定义上的区别：静态变量前要加static关键字，而实例变量前则不加。

在程序运行时的区别：实例变量属于某个对象的属性，必须创建了实例对象，其中的实例变量才会被分配空间，才能使用这个实例变量。静态变量不属于某个实例对象，而是属于类，所以也称为类变量，只要程序加载了类的字节码，不用创建任何实例对象，静态变量就会被分配空间，静态变量就可以被使用了。总之，实例变量必须创建对象后才可以通过这个对象来使用，静态变量则可以直接使用类名来引用。

例如，对于下面的程序，无论创建多少个实例对象，永远都只分配了一个staticVar变量，并且每创建一个实例对象，这个staticVar就会加1；但是，每创建一个实例对象，就会分配一个instanceVar，即可能分配多个instanceVar，并且每个instanceVar的值都只自加了1次。

public class VariantTest{

public static int staticVar = 0;

public int instanceVar = 0;

public VariantTest(){

staticVar++;

instanceVar++;

System.out.println(“staticVar=” + staticVar + ”,instanceVar=”+ instanceVar);

}

}

备注：这个解答除了说清楚两者的区别外，最后还用一个具体的应用例子来说明两者的差异，体现了自己有很好的解说问题和设计案例的能力，思维敏捷，超过一般程序员，有写作能力！

13、是否可以从一个static方法内部发出对非static方法的调用？

不可以。因为非static方法是要与对象关联在一起的，必须创建一个对象后，才可以在该对象上进行方法调用，而static方法调用时不需要创建对象，可以直接调用。也就是说，当一个static方法被调用时，可能还没有创建任何实例对象，如果从一个static方法中发出对非static方法的调用，那个非static方法是关联到哪个对象上的呢？这个逻辑无法成立，所以，一个static方法内部发出对非static方法的调用。

14、Integer与int的区别

int是java提供的8种原始数据类型之一。Java为每个原始类型提供了封装类，Integer是java为int提供的封装类。int的默认值为0，而Integer的默认值为null，即Integer可以区分出未赋值和值为0的区别，int则无法表达出未赋值的情况，例如，要想表达出没有参加考试和考试成绩为0的区别，则只能使用Integer。在JSP开发中，Integer的默认为null，所以用el表达式在文本框中显示时，值为空白字符串，而int默认的默认值为0，所以用el表达式在文本框中显示时，结果为0，所以，int不适合作为web层的表单数据的类型。

在Hibernate中，如果将OID定义为Integer类型，那么Hibernate就可以根据其值是否为null而判断一个对象是否是临时的，如果将OID定义为了int类型，还需要在hbm映射文件中设置其unsaved-value属性为0。

另外，Integer提供了多个与整数相关的操作方法，例如，将一个字符串转换成整数，Integer中还定义了表示整数的最大值和最小值的常量。

15、Math.round(11.5)等於多少? Math.round(-11.5)等於多少?

Math类中提供了三个与取整有关的方法：ceil、floor、round，这些方法的作用与它们的英文名称的含义相对应，例如，ceil的英文意义是天花板，该方法就表示向上取整，Math.ceil(11.3)的结果为12,Math.ceil(-11.3)的结果是-11；floor的英文意义是地板，该方法就表示向下取整，Math.ceil(11.6)的结果为11,Math.ceil(-11.6)的结果是-12；最难掌握的是round方法，它表示“四舍五入”，算法为Math.floor(x+0.5)，即将原来的数字加上0.5后再向下取整，所以，Math.round(11.5)的结果为12，Math.round(-11.5)的结果为-11。

16、下面的代码有什么不妥之处?

1. if(username.equals(“zxx”){}

username可能为NULL,会报空指针错误；改为"zxx".equals(username)

2.intx = 1;

return x==1?true:false;  这个改成return x==1;就可以!

17、请说出作用域public，private，protected，以及不写时的区别

这四个作用域的可见范围如下表所示。

说明：如果在修饰的元素上面没有写任何访问修饰符，则表示friendly。

作用域    当前类同一package子孙类其他package

public    √    √         √      √

protected  √    √         √     ×

friendly   √    √         ×     ×

private    √    ×         ×     ×

备注：只要记住了有4种访问权限，4个访问范围，然后将全选和范围在水平和垂直方向上分别按排从小到大或从大到小的顺序排列，就很容易画出上面的图了。

18、Overload和Override的区别。Overloaded的方法是否可以改变返回值的类型?

Overload是重载的意思，Override是覆盖的意思，也就是重写。

重载Overload表示同一个类中可以有多个名称相同的方法，但这些方法的参数列表各不相同（即参数个数或类型不同）。

重写Override表示子类中的方法可以与父类中的某个方法的名称和参数完全相同，通过子类创建的实例对象调用这个方法时，将调用子类中的定义方法，这相当于把父类中定义的那个完全相同的方法给覆盖了，这也是面向对象编程的多态性的一种表现。子类覆盖父类的方法时，只能比父类抛出更少的异常，或者是抛出父类抛出的异常的子异常，因为子类可以解决父类的一些问题，不能比父类有更多的问题。子类方法的访问权限只能比父类的更大，不能更小。如果父类的方法是private类型，那么，子类则不存在覆盖的限制，相当于子类中增加了一个全新的方法。

至于Overloaded的方法是否可以改变返回值的类型这个问题，要看你倒底想问什么呢？这个题目很模糊。如果几个Overloaded的方法的参数列表不一样，它们的返回者类型当然也可以不一样。但我估计你想问的问题是：如果两个方法的参数列表完全一样，是否可以让它们的返回值不同来实现重载Overload。这是不行的，我们可以用反证法来说明这个问题，因为我们有时候调用一个方法时也可以不定义返回结果变量，即不要关心其返回结果，例如，我们调用map.remove(key)方法时，虽然remove方法有返回值，但是我们通常都不会定义接收返回结果的变量，这时候假设该类中有两个名称和参数列表完全相同的方法，仅仅是返回类型不同，java就无法确定编程者倒底是想调用哪个方法了，因为它无法通过返回结果类型来判断。

override可以翻译为覆盖，从字面就可以知道，它是覆盖了一个方法并且对其重写，以求达到不同的作用。对我们来说最熟悉的覆盖就是对接口方法的实现，在接口中一般只是对方法进行了声明，而我们在实现时，就需要实现接口声明的所有方法。除了这个典型的用法以外，我们在继承中也可能会在子类覆盖父类中的方法。在覆盖要注意以下的几点：

1、覆盖的方法的标志必须要和被覆盖的方法的标志完全匹配，才能达到覆盖的效果；

2、覆盖的方法的返回值必须和被覆盖的方法的返回一致；

3、覆盖的方法所抛出的异常必须和被覆盖方法的所抛出的异常一致，或者是其子类；

4、被覆盖的方法不能为private，否则在其子类中只是新定义了一个方法，并没有对其进行覆盖。

overload对我们来说可能比较熟悉，可以翻译为重载，它是指我们可以定义一些名称相同的方法，通过定义不同的输入参数来区分这些方法，然后再调用时，VM就会根据不同的参数样式，来选择合适的方法执行。在使用重载要注意以下的几点：

1、在使用重载时只能通过不同的参数样式。例如，不同的参数类型，不同的参数个数，不同的参数顺序（当然，同一方法内的几个参数类型必须不一样，例如可以是fun(int,float)，但是不能为fun(int,int)）；

2、不能通过访问权限、返回类型、抛出的异常进行重载；

3、方法的异常类型和数目不会对重载造成影响；

4、对于继承来说，如果某一方法在父类中是访问权限是priavte，那么就不能在子类对其进行重载，如果定义的话，也只是定义了一个新方法，而不会达到重载的效果。

19、构造器Constructor是否可被override?

构造器Constructor不能被继承，因此不能重写Override，但可以被重载Overload。

20、接口是否可继承接口?抽象类是否可实现(implements)接口?抽象类是否可继承具体类(concrete class)?抽象类中是否可以有静态的main方法？

接口可以继承接口。抽象类可以实现(implements)接口，抽象类可以继承具体类。抽象类中可以有静态的main方法。

备注：只要明白了接口和抽象类的本质和作用，这些问题都很好回答，你想想，如果你是java语言的设计者，你是否会提供这样的支持，如果不提供的话，有什么理由吗？如果你没有道理不提供，那答案就是肯定的了。

只有记住抽象类与普通类的唯一区别就是不能创建实例对象和允许有abstract方法。

21、写clone()方法时，通常都有一行代码，是什么？

clone 有缺省行为，super.clone();因为首先要把父类中的成员复制到位，然后才是复制自己的成员。

22、面向对象的特征有哪些方面

计算机软件系统是现实生活中的业务在计算机中的映射，而现实生活中的业务其实就是一个个对象协作的过程。面向对象编程就是按现实业务一样的方式将程序代码按一个个对象进行组织和编写，让计算机系统能够识别和理解用对象方式组织和编写的程序代码，这样就可以把现实生活中的业务对象映射到计算机系统中。

面向对象的编程语言有4个主要的特征。

1封装：

封装是保证软件部件具有优良的模块性的基础，封装的目标就是要实现软件部件的“高内聚、低耦合”，防止程序相互依赖性而带来的变动影响。在面向对象的编程语言中，对象是封装的最基本单位，面向对象的封装比传统语言的封装更为清晰、更为有力。面向对象的封装就是把描述一个对象的属性和行为的代码封装在一个“模块”中，也就是一个类中，属性用变量定义，行为用方法进行定义，方法可以直接访问同一个对象中的属性。通常情况下，只要记住让变量和访问这个变量的方法放在一起，将一个类中的成员变量全部定义成私有的，只有这个类自己的方法才可以访问到这些成员变量，这就基本上实现对象的封装，就很容易找出要分配到这个类上的方法了，就基本上算是会面向对象的编程了。把握一个原则：把对同一事物进行操作的方法和相关的方法放在同一个类中，把方法和它操作的数据放在同一个类中。

例如，人要在黑板上画圆，这一共涉及三个对象：人、黑板、圆，画圆的方法要分配给哪个对象呢？由于画圆需要使用到圆心和半径，圆心和半径显然是圆的属性，如果将它们在类中定义成了私有的成员变量，那么，画圆的方法必须分配给圆，它才能访问到圆心和半径这两个属性，人以后只是调用圆的画圆方法、表示给圆发给消息而已，画圆这个方法不应该分配在人这个对象上，这就是面向对象的封装性，即将对象封装成一个高度自治和相对封闭的个体，对象状态（属性）由这个对象自己的行为（方法）来读取和改变。一个更便于理解的例子就是，司机将火车刹住了，刹车的动作是分配给司机，还是分配给火车，显然，应该分配给火车，因为司机自身是不可能有那么大的力气将一个火车给停下来的，只有火车自己才能完成这一动作，火车需要调用内部的离合器和刹车片等多个器件协作才能完成刹车这个动作，司机刹车的过程只是给火车发了一个消息，通知火车要执行刹车动作而已。

抽象：

抽象就是找出一些事物的相似和共性之处，然后将这些事物归为一个类，这个类只考虑这些事物的相似和共性之处，并且会忽略与当前主题和目标无关的那些方面，将注意力集中在与当前目标有关的方面。例如，看到一只蚂蚁和大象，你能够想象出它们的相同之处，那就是抽象。抽象包括行为抽象和状态抽象两个方面。例如，定义一个Person类，如下：

Class Person{

String name;

int age;

}

人本来是很复杂的事物，有很多方面，但因为当前系统只需要了解人的姓名和年龄，所以上面定义的类中只包含姓名和年龄这两个属性，这就是一种抽像，使用抽象可以避免考虑一些与目标无关的细节。我对抽象的理解就是不要用显微镜去看一个事物的所有方面，这样涉及的内容就太多了，而是要善于划分问题的边界，当前系统需要什么，就只考虑什么。

继承：

在定义和实现一个类的时候，可以在一个已经存在的类的基础之上来进行，把这个已经存在的类所定义的内容作为自己的内容，并可以加入若干新的内容，或修改原来的方法使之更适合特殊的需要，这就是继承。继承是子类自动共享父类数据和方法的机制，这是类之间的一种关系，提高了软件的可重用性和可扩展性。

多态：

多态是指程序中定义的引用变量所指向的具体类型和通过该引用变量发出的方法调用在编程时并不确定，而是在程序运行期间才确定，即一个引用变量倒底会指向哪个类的实例对象，该引用变量发出的方法调用到底是哪个类中实现的方法，必须在由程序运行期间才能决定。因为在程序运行时才确定具体的类，这样，不用修改源程序代码，就可以让引用变量绑定到各种不同的类实现上，从而导致该引用调用的具体方法随之改变，即不修改程序代码就可以改变程序运行时所绑定的具体代码，让程序可以选择多个运行状态，这就是多态性。多态性增强了软件的灵活性和扩展性。例如，下面代码中的UserDao是一个接口，它定义引用变量userDao指向的实例对象由daofactory.getDao()在执行的时候返回，有时候指向的是UserJdbcDao这个实现，有时候指向的是UserHibernateDao这个实现，这样，不用修改源代码，就可以改变userDao指向的具体类实现，从而导致userDao.insertUser()方法调用的具体代码也随之改变，即有时候调用的是UserJdbcDao的insertUser方法，有时候调用的是UserHibernateDao的insertUser方法：

UserDao userDao =daofactory.getDao();

userDao.insertUser(user);

比喻：人吃饭，你看到的是左手，还是右手？

23、java中实现多态的机制是什么？

靠的是父类或接口定义的引用变量可以指向子类或具体实现类的实例对象，而程序调用的方法在运行期才动态绑定，就是引用变量所指向的具体实例对象的方法，也就是内存里正在运行的那个对象的方法，而不是引用变量的类型中定义的方法。

24、abstract class和interface有什么区别?

含有abstract修饰符的class即为抽象类，abstract类不能创建实例对象。含有abstract方法的类必须定义为abstract class，abstract class类中的方法不必是抽象的。abstract class类中定义抽象方法必须在具体(Concrete)子类中实现，所以，不能有抽象构造方法或抽象静态方法。如果的子类没有实现抽象父类中的所有抽象方法，那么子类也必须定义为abstract类型。

接口（interface）可以说成是抽象类的一种特例，接口中的所有方法都必须是抽象的。接口中的方法定义默认为public abstract类型，接口中的成员变量类型默认为public static final。

下面比较一下两者的语法区别：

1.抽象类可以有构造方法，接口中不能有构造方法。

2.抽象类中可以有普通成员变量，接口中没有普通成员变量

3.抽象类中可以包含非抽象的普通方法，接口中的所有方法必须都是抽象的，不能有非抽象的普通方法。

4.抽象类中的抽象方法的访问类型可以是public，protected和（默认类型,虽然

eclipse下不报错，但应该也不行），但接口中的抽象方法只能是public类型的，并且默认即为public abstract类型。

5.抽象类中可以包含静态方法，接口中不能包含静态方法

6.抽象类和接口中都可以包含静态成员变量，抽象类中的静态成员变量的访问类型可以任意，但接口中定义的变量只能是public static final类型，并且默认即为public static final类型。

7. 一个类可以实现多个接口，但只能继承一个抽象类。

下面接着再说说两者在应用上的区别：

接口更多的是在系统架构设计方法发挥作用，主要用于定义模块之间的通信契约。而抽象类在代码实现方面发挥作用，可以实现代码的重用，例如，模板方法设计模式是抽象类的一个典型应用，假设某个项目的所有Servlet类都要用相同的方式进行权限判断、记录访问日志和处理异常，那么就可以定义一个抽象的基类，让所有的Servlet都继承这个抽象基类，在抽象基类的service方法中完成权限判断、记录访问日志和处理异常的代码，在各个子类中只是完成各自的业务逻辑代码，伪代码如下：

public abstract classBaseServlet extends HttpServlet{

public final void service(HttpServletRequest request,HttpServletResponse response) throws IOExcetion,ServletException       {

记录访问日志

进行权限判断

if(具有权限){

try{

doService(request,response);

}

catch(Excetpion e)  {

记录异常信息

}

}

}

protected abstract void doService(HttpServletRequest request,HttpServletResponse response) throws IOExcetion,ServletException;

//注意访问权限定义成protected，显得既专业，又严谨，因为它是专门给子类用的

}

public class MyServlet1 extendsBaseServlet

{

protected voiddoService(HttpServletRequest request, HttpServletResponse response) throwsIOExcetion,ServletException

{

本Servlet只处理的具体业务逻辑代码

}

}

父类方法中间的某段代码不确定，留给子类干，就用模板方法设计模式。

备注：这道题的思路是先从总体解释抽象类和接口的基本概念，然后再比较两者的语法细节，最后再说两者的应用区别。比较两者语法细节区别的条理是：先从一个类中的构造方法、普通成员变量和方法（包括抽象方法），静态变量和方法，继承性等6个方面逐一去比较回答，接着从第三者继承的角度的回答，特别是最后用了一个典型的例子来展现自己深厚的技术功底。

25、abstract的method是否可同时是static,是否可同时是native，是否可同时是synchronized?

abstract的method不可以是static的，因为抽象的方法是要被子类实现的，而static与子类扯不上关系！

native方法表示该方法要用另外一种依赖平台的编程语言实现的，不存在着被子类实现的问题，所以，它也不能是抽象的，不能与abstract混用。例如，FileOutputSteam类要硬件打交道，底层的实现用的是操作系统相关的api实现，例如，在windows用c语言实现的，所以，查看jdk的源代码，可以发现FileOutputStream的open方法的定义如下：

private native void open(Stringname) throws FileNotFoundException;

如果我们要用java调用别人写的c语言函数，我们是无法直接调用的，我们需要按照java的要求写一个c语言的函数，又我们的这个c语言函数去调用别人的c语言函数。由于我们的c语言函数是按java的要求来写的，我们这个c语言函数就可以与java对接上，java那边的对接方式就是定义出与我们这个c函数相对应的方法，java中对应的方法不需要写具体的代码，但需要在前面声明native。

关于synchronized与abstract合用的问题，我觉得也不行，因为在我几年的学习和开发中，从来没见到过这种情况，并且我觉得synchronized应该是作用在一个具体的方法上才有意义。而且，方法上的synchronized同步所使用的同步锁对象是this，而抽象方法上无法确定this是什么。

26、什么是内部类？Static Nested Class和Inner Class的不同。

内部类就是在一个类的内部定义的类，内部类中不能定义静态成员（静态成员不是对象的特性，只是为了找一个容身之处，所以需要放到一个类中而已，这么一点小事，你还要把它放到类内部的一个类中，过分了啊！提供内部类，不是为让你干这种事情，无聊，不让你干。我想可能是既然静态成员类似c语言的全局变量，而内部类通常是用于创建内部对象用的，所以，把“全局变量”放在内部类中就是毫无意义的事情，既然是毫无意义的事情，就应该被禁止），内部类可以直接访问外部类中的成员变量，内部类可以定义在外部类的方法外面，也可以定义在外部类的方法体中，如下所示：

public class Outer

{

int out_x  = 0;

public void method()

{

Inner1 inner1 = new Inner1();

public class Inner2  //在方法体内部定义的内部类

{

public method()

{

out_x = 3;

}

}

Inner2 inner2 = new Inner2();

}

public class Inner1  //在方法体外面定义的内部类

{

}

}

在方法体外面定义的内部类的访问类型可以是public,protecte,默认的，private等4种类型，这就好像类中定义的成员变量有4种访问类型一样，它们决定这个内部类的定义对其他类是否可见；对于这种情况，我们也可以在外面创建内部类的实例对象，创建内部类的实例对象时，一定要先创建外部类的实例对象，然后用这个外部类的实例对象去创建内部类的实例对象，代码如下：

Outer outer = new Outer();

Outer.Inner1 inner1 = outer.new Innner1();

在方法内部定义的内部类前面不能有访问类型修饰符，就好像方法中定义的局部变量一样，但这种内部类的前面可以使用final或abstract修饰符。这种内部类对其他类是不可见的其他类无法引用这种内部类，但是这种内部类创建的实例对象可以传递给其他类访问。这种内部类必须是先定义，后使用，即内部类的定义代码必须出现在使用该类之前，这与方法中的局部变量必须先定义后使用的道理也是一样的。这种内部类可以访问方法体中的局部变量，但是，该局部变量前必须加final修饰符。

对于这些细节，只要在eclipse写代码试试，根据开发工具提示的各类错误信息就可以马上了解到。

在方法体内部还可以采用如下语法来创建一种匿名内部类，即定义某一接口或类的子类的同时，还创建了该子类的实例对象，无需为该子类定义名称：

public class Outer

{

public void start()

{

new Thread(

new Runable(){

public void run(){};

}

).start();

}

}

最后，在方法外部定义的内部类前面可以加上static关键字，从而成为Static Nested Class，它不再具有内部类的特性，所有，从狭义上讲，它不是内部类。Static Nested Class与普通类在运行时的行为和功能上没有什么区别，只是在编程引用时的语法上有一些差别，它可以定义成public、protected、默认的、private等多种类型，而普通类只能定义成public和默认的这两种类型。在外面引用Static Nested Class类的名称为“外部类名.内部类名”。在外面不需要创建外部类的实例对象，就可以直接创建Static Nested Class，例如，假设Inner是定义在Outer类中的Static Nested Class，那么可以使用如下语句创建Inner类：

Outer.Inner inner = new Outer.Inner();

由于static Nested Class不依赖于外部类的实例对象，所以，static Nested Class能访问外部类的非static成员变量(不能直接访问，需要创建外部类实例才能访问非静态变量)。当在外部类中访问Static Nested Class时，可以直接使用Static Nested Class的名字，而不需要加上外部类的名字了，在Static Nested Class中也可以直接引用外部类的static的成员变量，不需要加上外部类的名字。

在静态方法中定义的内部类也是Static Nested Class，这时候不能在类前面加static关键字，静态方法中的Static Nested Class与普通方法中的内部类的应用方式很相似，它除了可以直接访问外部类中的static的成员变量，还可以访问静态方法中的局部变量，但是，该局部变量前必须加final修饰符。

备注：首先根据你的印象说出你对内部类的总体方面的特点：例如，在两个地方可以定义，可以访问外部类的成员变量，不能定义静态成员，这是大的特点。然后再说一些细节方面的知识，例如，几种定义方式的语法区别，静态内部类，以及匿名内部类。

27、内部类可以引用它的包含类的成员吗？有没有什么限制？

完全可以。如果不是静态内部类，那没有什么限制！

如果你把静态嵌套类当作内部类的一种特例，那在这种情况下不可以访问外部类的普通成员变量，而只能访问外部类中的静态成员，例如，下面的代码：

class Outer

{

static int x;

static class Inner

{

void test()

{

syso(x);

}

}

}

答题时，也要能察言观色，揣摩提问者的心思，显然人家希望你说的是静态内部类不能访问外部类的成员，但你一上来就顶牛，这不好，要先顺着人家，让人家满意，然后再说特殊情况，让人家吃惊。

28、Anonymous Inner Class (匿名内部类)是否可以extends(继承)其它类，是否可以implements(实现)interface(接口)?

可以继承其他类或实现其他接口。不仅是可以，而是必须!

29、super.getClass()方法调用

下面程序的输出结果是多少？

Import java.util.Date;

publicclassTestextendsDate{

public static voidmain(String[] args) {

newTest().test();

}

public voidtest(){

System.out.println(super.getClass().getName());

}

}

很奇怪，结果是Test

这属于脑筋急转弯的题目，在一个qq群有个网友正好问过这个问题，我觉得挺有趣，就研究了一下，没想到今天还被你面到了，哈哈。

在test方法中，直接调用getClass().getName()方法，返回的是Test类名

由于getClass()在Object类中定义成了final，子类不能覆盖该方法，所以，在

test方法中调用getClass().getName()方法，其实就是在调用从父类继承的getClass()方法，等效于调用super.getClass().getName()方法，所以，super.getClass().getName()方法返回的也应该是Test。

如果想得到父类的名称，应该用如下代码：

getClass().getSuperClass().getName();

30、String是最基本的数据类型吗?

基本数据类型包括byte、int、char、long、float、double、boolean和short。

java.lang.String类是final类型的，因此不可以继承这个类、不能修改这个类。为了提高效率节省空间，我们应该用StringBuffer类

31、String s = "Hello";s = s + " world!";这两行代码执行后，原始的String对象中的内容到底变了没有？

没有。因为String被设计成不可变(immutable)类，所以它的所有对象都是不可变对象。在这段代码中，s原先指向一个String对象，内容是 "Hello"，然后我们对s进行了+操作，那么s所指向的那个对象是否发生了改变呢？答案是没有。这时，s不指向原来那个对象了，而指向了另一个 String对象，内容为"Hello world!"，原来那个对象还存在于内存之中，只是s这个引用变量不再指向它了。

通过上面的说明，我们很容易导出另一个结论，如果经常对字符串进行各种各样的修改，或者说，不可预见的修改，那么使用String来代表字符串的话会引起很大的内存开销。因为 String对象建立之后不能再改变，所以对于每一个不同的字符串，都需要一个String对象来表示。这时，应该考虑使用StringBuffer类，它允许修改，而不是每个不同的字符串都要生成一个新的对象。并且，这两种类的对象转换十分容易。

同时，我们还可以知道，如果要使用内容相同的字符串，不必每次都new一个String。例如我们要在构造器中对一个名叫s的String引用变量进行初始化，把它设置为初始值，应当这样做：

public class Demo {

private String s;

...

public Demo {

s = "Initial Value";

}

...

}

而非

s = new String("Initial Value");

后者每次都会调用构造器，生成新对象，性能低下且内存开销大，并且没有意义，因为String对象不可改变，所以对于内容相同的字符串，只要一个String对象来表示就可以了。也就说，多次调用上面的构造器创建多个对象，他们的String类型属性s都指向同一个对象。

上面的结论还基于这样一个事实：对于字符串常量，如果内容相同，Java认为它们代表同一个String对象。而用关键字new调用构造器，总是会创建一个新的对象，无论内容是否相同。

至于为什么要把String类设计成不可变类，是它的用途决定的。其实不只String，很多Java标准类库中的类都是不可变的。在开发一个系统的时候，我们有时候也需要设计不可变类，来传递一组相关的值，这也是面向对象思想的体现。不可变类有一些优点，比如因为它的对象是只读的，所以多线程并发访问也不会有任何问题。当然也有一些缺点，比如每个不同的状态都要一个对象来代表，可能会造成性能上的问题。所以Java标准类库还提供了一个可变版本，即 StringBuffer。

32、是否可以继承String类?

String类是final类故不可以继承。

33、String s = new String("xyz");创建了几个String Object?二者之间有什么区别？

两个或一个，”xyz”对应一个对象，这个对象放在字符串常量缓冲区，常量”xyz”不管出现多少遍，都是缓冲区中的那一个。New String每写一遍，就创建一个新的对象，它一句那个常量”xyz”对象的内容来创建出一个新String对象。如果以前就用过’xyz’，这句代表就不会创建”xyz”自己了，直接从缓冲区拿。

34、String和StringBuffer的区别

JAVA平台提供了两个类：String和StringBuffer，它们可以储存和操作字符串，即包含多个字符的字符数据。这个String类提供了数值不可改变的字符串。而这个StringBuffer类提供的字符串进行修改。当你知道字符数据要改变的时候你就可以使用StringBuffer。典型地，你可以使用StringBuffers来动态构造字符数据。另外，String实现了equals方法，new String(“abc”).equals(newString(“abc”)的结果为true,而StringBuffer没有实现equals方法，所以，new StringBuffer(“abc”).equals(newStringBuffer(“abc”)的结果为false。

接着要举一个具体的例子来说明，我们要把1到100的所有数字拼起来，组成一个串。

StringBuffer sbf = new StringBuffer();

for(int i=0;i<100;i++)

{

sbf.append(i);

}

上面的代码效率很高，因为只创建了一个StringBuffer对象，而下面的代码效率很低，因为创建了101个对象。

String str = new String();

for(int i=0;i<100;i++)

{

str = str + i;

}

在讲两者区别时，应把循环的次数搞成10000，然后用endTime-beginTime来比较两者执行的时间差异，最后还要讲讲StringBuilder与StringBuffer的区别。

String覆盖了equals方法和hashCode方法，而StringBuffer没有覆盖equals方法和hashCode方法，所以，将StringBuffer对象存储进Java集合类中时会出现问题。

35、如何把一段逗号分割的字符串转换成一个数组?

如果不查jdk api，我很难写出来！我可以说说我的思路：

1用正则表达式，代码大概为：String [] result = orgStr.split(“,”);

2用 StingTokenizer ,代码为：StringTokenizer  tokener = StringTokenizer(orgStr,”,”);

String [] result =new String[tokener .countTokens()];

Int i=0;

while(tokener.hasNext(){

result[i++]=toker.nextToken();

}

36、数组有没有length()这个方法? String有没有length()这个方法？

数组没有length()这个方法，有length的属性。String有有length()这个方法。

37、下面这条语句一共创建了多少个对象：String s="a"+"b"+"c"+"d";

答：对于如下代码：

String s1 = "a";

String s2 = s1 + "b";

String s3 = "a" + "b";

System.out.println(s2 == "ab");

System.out.println(s3 == "ab");

第一条语句打印的结果为false，第二条语句打印的结果为true，这说明javac编译可以对字符串常量直接相加的表达式进行优化，不必要等到运行期去进行加法运算处理，而是在编译时去掉其中的加号，直接将其编译成一个这些常量相连的结果。

题目中的第一行代码被编译器在编译时优化后，相当于直接定义了一个”abcd”的字符串，所以，上面的代码应该只创建了一个String对象。写如下两行代码，

String s ="a" + "b" + "c" + "d";

System.out.println(s== "abcd");

最终打印的结果应该为true。

38、try {}里有一个return语句，那么紧跟在这个try后的finally {}里的code会不会被执行，什么时候被执行，在return前还是后?

也许你的答案是在return之前，但往更细地说，我的答案是在return中间执行，请看下面程序代码的运行结果：

publicclassTest {

/**

*@paramargs add by zxx ,Dec 9, 2008

*/

public static voidmain(String[] args) {

//TODOAuto-generated method stub

System.out.println(newTest().test());;

}

staticinttest()

{

intx = 1;

try

{

returnx;

}

finally

{

++x;

}

}

}

---------执行结果 ---------

1

运行结果是1，为什么呢？主函数调用子函数并得到结果的过程，好比主函数准备一个空罐子，当子函数要返回结果时，先把结果放在罐子里，然后再将程序逻辑返回到主函数。所谓返回，就是子函数说，我不运行了，你主函数继续运行吧，这没什么结果可言，结果是在说这话之前放进罐子里的。

39、下面的程序代码输出的结果是多少？

public classsmallT

{

public staticvoid  main(String args[])

{

smallT t  = new smallT();

int  b =  t.get();

System.out.println(b);

}

public int  get()

{

try

{

return1 ;

}

finally

{

return2 ;

}

}

}

返回的结果是2。

我可以通过下面一个例子程序来帮助我解释这个答案，从下面例子的运行结果中可以发现，try中的return语句调用的函数先于finally中调用的函数执行，也就是说return语句先执行，finally语句后执行，所以，返回的结果是2。Return并不是让函数马上返回，而是return语句执行后，将把返回结果放置进函数栈中，此时函数并不是马上返回，它要执行finally语句后才真正开始返回。

在讲解答案时可以用下面的程序来帮助分析：

publicclassTest {

/**

*@paramargs add by zxx ,Dec 9, 2008

*/

public static voidmain(String[] args) {

//TODOAuto-generated method stub

System.out.println(newTest().test());;

}

inttest()

{

try

{

returnfunc1();

}

finally

{

returnfunc2();

}

}

intfunc1()

{

System.out.println("func1");

return1;

}

intfunc2()

{

System.out.println("func2");

return2;

}

}

-----------执行结果-----------------

func1

func2

2

结论：finally中的代码比return和break语句后执行

40、final, finally, finalize的区别。

final 用于声明属性，方法和类，分别表示属性不可变，方法不可覆盖，类不可继承。

内部类要访问局部变量，局部变量必须定义成final类型，例如，一段代码……

finally是异常处理语句结构的一部分，表示总是执行。

finalize是Object类的一个方法，在垃圾收集器执行的时候会调用被回收对象的此方法，可以覆盖此方法提供垃圾收集时的其他资源回收，例如关闭文件等。JVM不保证此方法总被调用

41、运行时异常与一般异常有何异同？

异常表示程序运行过程中可能出现的非正常状态，运行时异常表示虚拟机的通常操作中可能遇到的异常，是一种常见运行错误。java编译器要求方法必须声明抛出可能发生的非运行时异常，但是并不要求必须声明抛出未被捕获的运行时异常。

42、error和exception有什么区别?

error 表示恢复不是不可能但很困难的情况下的一种严重问题。比如说内存溢出。不可能指望程序能处理这样的情况。 exception表示一种设计或实现问题。也就是说，它表示如果程序运行正常，从不会发生的情况。

43、Java中的异常处理机制的简单原理和应用。

异常是指java程序运行时（非编译）所发生的非正常情况或错误，与现实生活中的事件很相似，现实生活中的事件可以包含事件发生的时间、地点、人物、情节等信息，可以用一个对象来表示，Java使用面向对象的方式来处理异常，它把程序中发生的每个异常也都分别封装到一个对象来表示的，该对象中包含有异常的信息。

Java对异常进行了分类，不同类型的异常分别用不同的Java类表示，所有异常的根类为java.lang.Throwable，Throwable下面又派生了两个子类：Error和Exception，Error表示应用程序本身无法克服和恢复的一种严重问题，程序只有死的份了，例如，说内存溢出和线程死锁等系统问题。Exception表示程序还能够克服和恢复的问题，其中又分为系统异常和普通异常，系统异常是软件本身缺陷所导致的问题，也就是软件开发人员考虑不周所导致的问题，软件使用者无法克服和恢复这种问题，但在这种问题下还可以让软件系统继续运行或者让软件死掉，例如，数组脚本越界（ArrayIndexOutOfBoundsException），空指针异常（NullPointerException）、类转换异常（ClassCastException）；普通异常是运行环境的变化或异常所导致的问题，是用户能够克服的问题，例如，网络断线，硬盘空间不够，发生这样的异常后，程序不应该死掉。

java为系统异常和普通异常提供了不同的解决方案，编译器强制普通异常必须try..catch处理或用throws声明继续抛给上层调用方法处理，所以普通异常也称为checked异常，而系统异常可以处理也可以不处理，所以，编译器不强制用try..catch处理或用throws声明，所以系统异常也称为unchecked异常。

提示答题者：就按照三个级别去思考：虚拟机必须宕机的错误，程序可以死掉也可以不死掉的错误，程序不应该死掉的错误；

44、请写出你最常见到的5个runtime exception。

这道题主要考你的代码量到底多大，如果你长期写代码的，应该经常都看到过一些系统方面的异常，你不一定真要回答出5个具体的系统异常，但你要能够说出什么是系统异常，以及几个系统异常就可以了，当然，这些异常完全用其英文名称来写是最好的，如果实在写不出，那就用中文吧，有总比没有强！

所谓系统异常，就是…..，它们都是RuntimeException的子类，在jdk doc中查RuntimeException类，就可以看到其所有的子类列表，也就是看到了所有的系统异常。我比较有印象的系统异常有：NullPointerException、ArrayIndexOutOfBoundsException、ClassCastException。

45、JAVA语言如何进行异常处理，关键字：throws,throw,try,catch,finally分别代表什么意义？在try块中可以抛出异常吗？

46、java中有几种方法可以实现一个线程？用什么关键字修饰同步方法? stop()和suspend()方法为何不推荐使用？

java5以前，有如下两种：

第一种：

new Thread(){}.start();这表示调用Thread子类对象的run方法，new Thread(){}表示一个Thread的匿名子类的实例对象，子类加上run方法后的代码如下：

new Thread(){

public void run(){

}

}.start();

第二种：

new Thread(new Runnable(){}).start();这表示调用Thread对象接受的Runnable对象的run方法，new Runnable(){}表示一个Runnable的匿名子类的实例对象,runnable的子类加上run方法后的代码如下：

new Thread(new Runnable(){

public voidrun(){

}

}

).start();

从java5开始，还有如下一些线程池创建多线程的方式：

ExecutorService pool = Executors.newFixedThreadPool(3)

for(int i=0;i<10;i++)

{

pool.execute(newRunable(){public void run(){}});

}

Executors.newCachedThreadPool().execute(new Runable(){publicvoid run(){}});

Executors.newSingleThreadExecutor().execute(new Runable(){publicvoid run(){}});

有两种实现方法，分别使用new Thread()和new Thread(runnable)形式，第一种直接调用thread的run方法，所以，我们往往使用Thread子类，即new SubThread()。第二种调用runnable的run方法。

有两种实现方法，分别是继承Thread类与实现Runnable接口

用synchronized关键字修饰同步方法

反对使用stop()，是因为它不安全。它会解除由线程获取的所有锁定，而且如果对象处于一种不连贯状态，那么其他线程能在那种状态下检查和修改它们。结果很难检查出真正的问题所在。suspend()方法容易发生死锁。调用suspend()的时候，目标线程会停下来，但却仍然持有在这之前获得的锁定。此时，其他任何线程都不能访问锁定的资源，除非被"挂起"的线程恢复运行。对任何线程来说，如果它们想恢复目标线程，同时又试图使用任何一个锁定的资源，就会造成死锁。所以不应该使用suspend()，而应在自己的Thread类中置入一个标志，指出线程应该活动还是挂起。若标志指出线程应该挂起，便用wait()命其进入等待状态。若标志指出线程应当恢复，则用一个notify()重新启动线程。

47、sleep()和 wait()有什么区别?

（网上的答案：sleep是线程类（Thread）的方法，导致此线程暂停执行指定时间，给执行机会给其他线程，但是监控状态依然保持，到时后会自动恢复。调用sleep不会释放对象锁。 wait是Object类的方法，对此对象调用wait方法导致本线程放弃对象锁，进入等待此对象的等待锁定池，只有针对此对象发出notify方法（或notifyAll）后本线程才进入对象锁定池准备获得对象锁进入运行状态。）

sleep就是正在执行的线程主动让出cpu，cpu去执行其他线程，在sleep指定的时间过后，cpu才会回到这个线程上继续往下执行，如果当前线程进入了同步锁，sleep方法并不会释放锁，即使当前线程使用sleep方法让出了cpu，但其他被同步锁挡住了的线程也无法得到执行。wait是指在一个已经进入了同步锁的线程内，让自己暂时让出同步锁，以便其他正在等待此锁的线程可以得到同步锁并运行，只有其他线程调用了notify方法（notify并不释放锁，只是告诉调用过wait方法的线程可以去参与获得锁的竞争了，但不是马上得到锁，因为锁还在别人手里，别人还没释放。如果notify方法后面的代码还有很多，需要这些代码执行完后才会释放锁，可以在notfiy方法后增加一个等待和一些代码，看看效果），调用wait方法的线程就会解除wait状态和程序可以再次得到锁后继续向下运行。对于wait的讲解一定要配合例子代码来说明，才显得自己真明白。

packagecom.huawei.interview;

publicclassMultiThread {

/**

*@paramargs

*/

public static voidmain(String[] args) {

//TODOAuto-generated method stub

newThread(newThread1()).start();

try{

Thread.sleep(10);

}catch(InterruptedException e) {

//TODOAuto-generated catchblock

e.printStackTrace();

}

newThread(newThread2()).start();

}

private static classThread1implementsRunnable

{

@Override

public voidrun() {

//TODOAuto-generated methodstub

//由于这里的Thread1和下面的Thread2内部run方法要用同一对象作为监视器，我们这里不能用this，因为在Thread2里面的this和这个Thread1的this不是同一个对象。我们用MultiThread.class这个字节码对象，当前虚拟机里引用这个变量时，指向的都是同一个对象。

synchronized(MultiThread.class){

System.out.println("enterthread1...");

System.out.println("thread1is waiting");

try{

//释放锁有两种方式，第一种方式是程序自然离开监视器的范围，也就是离开了synchronized关键字管辖的代码范围，另一种方式就是在synchronized关键字管辖的代码内部调用监视器对象的wait方法。这里，使用wait方法释放锁。

MultiThread.class.wait();

}catch(InterruptedException e) {

//TODOAuto-generatedcatch block

e.printStackTrace();

}

System.out.println("thread1is going on...");

System.out.println("thread1is being over!");

}

}

}

private static classThread2implementsRunnable

{

@Override

public voidrun() {

//TODOAuto-generated methodstub

synchronized(MultiThread.class){

System.out.println("enterthread2...");

System.out.println("thread2notify other thread can release wait status..");

//由于notify方法并不释放锁，即使thread2调用下面的sleep方法休息了10毫秒，但thread1仍然不会执行，因为thread2没有释放锁，所以Thread1无法得不到锁。

MultiThread.class.notify();

System.out.println("thread2is sleeping ten millisecond...");

try{

Thread.sleep(10);

}catch(InterruptedExceptione) {

//TODOAuto-generatedcatch block

e.printStackTrace();

}

System.out.println("thread2is going on...");

System.out.println("thread2is being over!");

}

}

}

}

48、同步和异步有何异同，在什么情况下分别使用他们？举例说明。

如果数据将在线程间共享。例如正在写的数据以后可能被另一个线程读到，或者正在读的数据可能已经被另一个线程写过了，那么这些数据就是共享数据，必须进行同步存取。

当应用程序在对象上调用了一个需要花费很长时间来执行的方法，并且不希望让程序等待方法的返回时，就应该使用异步编程，在很多情况下采用异步途径往往更有效率。

49. 下面两个方法同步吗？（自己发明）

class Test

{

synchronizedstatic voidsayHello3()

{

}

synchronizedvoidgetX(){}

}

50、多线程有几种实现方法?同步有几种实现方法?

多线程有两种实现方法，分别是继承Thread类与实现Runnable接口

同步的实现方面有两种，分别是synchronized,wait与notify

wait():使一个线程处于等待状态，并且释放所持有的对象的lock。

sleep():使一个正在运行的线程处于睡眠状态，是一个静态方法，调用此方法要捕捉InterruptedException异常。

notify():唤醒一个处于等待状态的线程，注意的是在调用此方法的时候，并不能确切的唤醒某一个等待状态的线程，而是由JVM确定唤醒哪个线程，而且不是按优先级。

Allnotity():唤醒所有处入等待状态的线程，注意并不是给所有唤醒线程一个对象的锁，而是让它们竞争。

51、启动一个线程是用run()还是start()? .

启动一个线程是调用start()方法，使线程就绪状态，以后可以被调度为运行状态，一个线程必须关联一些具体的执行代码，run()方法是该线程所关联的执行代码。

52、当一个线程进入一个对象的一个synchronized方法后，其它线程是否可进入此对象的其它方法?

分几种情况：

1.其他方法前是否加了synchronized关键字，如果没加，则能。

2.如果这个方法内部调用了wait，则可以进入其他synchronized方法。

3.如果其他个方法都加了synchronized关键字，并且内部没有调用wait，则不能。

4.如果其他方法是static，它用的同步锁是当前类的字节码，与非静态的方法不能同步，因为非静态的方法用的是this。

53、线程的基本概念、线程的基本状态以及状态之间的关系

一个程序中可以有多条执行线索同时执行，一个线程就是程序中的一条执行线索，每个线程上都关联有要执行的代码，即可以有多段程序代码同时运行，每个程序至少都有一个线程，即main方法执行的那个线程。如果只是一个cpu，它怎么能够同时执行多段程序呢？这是从宏观上来看的，cpu一会执行a线索，一会执行b线索，切换时间很快，给人的感觉是a,b在同时执行，好比大家在同一个办公室上网，只有一条链接到外部网线，其实，这条网线一会为a传数据，一会为b传数据，由于切换时间很短暂，所以，大家感觉都在同时上网。

状态：就绪，运行，synchronize阻塞，wait和sleep挂起，结束。wait必须在synchronized内部调用。

调用线程的start方法后线程进入就绪状态，线程调度系统将就绪状态的线程转为运行状态，遇到synchronized语句时，由运行状态转为阻塞，当synchronized获得锁后，由阻塞转为运行，在这种情况可以调用wait方法转为挂起状态，当线程关联的代码执行完后，线程变为结束状态。

54、简述synchronized和java.util.concurrent.locks.Lock的异同？

主要相同点：Lock能完成synchronized所实现的所有功能

主要不同点：Lock有比synchronized更精确的线程语义和更好的性能。synchronized会自动释放锁，而Lock一定要求程序员手工释放，并且必须在finally从句中释放。Lock还有更强大的功能，例如，它的tryLock方法可以非阻塞方式去拿锁。

举例说明（对下面的题用lock进行了改写）：

packagecom.huawei.interview;

importjava.util.concurrent.locks.Lock;

importjava.util.concurrent.locks.ReentrantLock;

publicclassThreadTest {

/**

*@paramargs

*/

private intj;

privateLock lock =newReentrantLock();

public static voidmain(String[] args) {

//TODOAuto-generated method stub

ThreadTest tt =newThreadTest();

for(inti=0;i<2;i++)

{

newThread(tt.newAdder()).start();

newThread(tt.newSubtractor()).start();

}

}

private classSubtractorimplementsRunnable

{

@Override

public voidrun() {

//TODOAuto-generated methodstub

while(true)

{

/*synchronized (ThreadTest.this) {

System.out.println("j--="+ j--);

//这里抛异常了，锁能释放吗？

}*/

lock.lock();

try

{

System.out.println("j--="+ j--);

}finally

{

lock.unlock();

}

}

}

}

private classAdderimplementsRunnable

{

@Override

public voidrun() {

//TODOAuto-generated methodstub

while(true)

{

/*synchronized (ThreadTest.this) {

System.out.println("j++="+ j++);

}*/

lock.lock();

try

{

System.out.println("j++="+ j++);

}finally

{

lock.unlock();

}

}

}

}

}

55、设计4个线程，其中两个线程每次对j增加1，另外两个线程对j每次减少1。写出程序。

以下程序使用内部类实现线程，对j增减的时候没有考虑顺序问题。

public class ThreadTest1

{

private int j;

public static void main(String args[]){

ThreadTest1 tt=newThreadTest1();

Inc inc=tt.new Inc();

Dec dec=tt.new Dec();

for(inti=0;i<2;i++){

Thread t=newThread(inc);

t.start();

t=new Thread(dec);

t.start();

}

}

private synchronized void inc(){

j++;

System.out.println(Thread.currentThread().getName()+"-inc:"+j);

}

private synchronized void dec(){

j--;

System.out.println(Thread.currentThread().getName()+"-dec:"+j);

}

class Inc implements Runnable{

public void run(){

for(inti=0;i<100;i++){

inc();

}

}

}

class Dec implements Runnable{

public void run(){

for(inti=0;i<100;i++){

dec();

}

}

}

}

----------随手再写的一个-------------

class A

{

JManger j =new JManager();

main()

{

new A().call();

}

void call

{

for(int i=0;i<2;i++)

{

new Thread(

newRunnable(){ public void run(){while(true){j.accumulate()}}}

).start();

new Thread(newRunnable(){ public void run(){while(true){j.sub()}}}).start();

}

}

}

class JManager

{

private j = 0;

public synchronized voidsubtract()

{

j--

}

public synchronized voidaccumulate()

{

j++;

}

}

56、子线程循环10次，接着主线程循环100，接着又回到子线程循环10次，接着再回到主线程又循环100，如此循环50次，请写出程序。

最终的程序代码如下：

publicclassThreadTest {

/**

*@paramargs

*/

public static voidmain(String[] args) {

//TODOAuto-generated method stub

newThreadTest().init();

}

public voidinit()

{

finalBusiness business =newBusiness();

newThread(

newRunnable()

{

public voidrun() {

for(inti=0;i<50;i++)

{

business.SubThread(i);

}

}

}

).start();

for(inti=0;i<50;i++)

{

business.MainThread(i);

}

}

private classBusiness

{

booleanbShouldSub =true;//这里相当于定义了控制该谁执行的一个信号灯

public synchronized voidMainThread(inti)

{

if(bShouldSub)

try{

this.wait();

}catch(InterruptedException e) {

//TODOAuto-generatedcatch block

e.printStackTrace();

}

for(intj=0;j<5;j++)

{

System.out.println(Thread.currentThread().getName()+ ":i=" + i +",j=" + j);

}

bShouldSub =true;

this.notify();

}

public synchronized voidSubThread(inti)

{

if(!bShouldSub)

try{

this.wait();

}catch(InterruptedExceptione) {

//TODOAuto-generatedcatch block

e.printStackTrace();

}

for(intj=0;j<10;j++)

{

System.out.println(Thread.currentThread().getName()+ ":i=" + i +",j=" + j);

}

bShouldSub =false;

this.notify();

}

}

}

备注：不可能一上来就写出上面的完整代码，最初写出来的代码如下，问题在于两个线程的代码要参照同一个变量，即这两个线程的代码要共享数据，所以，把这两个线程的执行代码搬到同一个类中去：

packagecom.huawei.interview.lym;

publicclassThreadTest {

private static booleanbShouldMain=false;

public static voidmain(String[]args) {

//TODOAuto-generated method stub

/*new Thread(){

public void run()

{

for(int i=0;i<50;i++)

{

for(int j=0;j<10;j++)

{

System.out.println("i="+ i + ",j=" + j);

}

}

}

}.start();*/

//final String str = newString("");

newThread(

newRunnable()

{

public voidrun()

{

for(inti=0;i<50;i++)

{

synchronized(ThreadTest.class) {

if(bShouldMain)

{

try{

ThreadTest.class.wait();}

catch(InterruptedException e) {

e.printStackTrace();

}

}

for(intj=0;j<10;j++)

{

System.out.println(

Thread.currentThread().getName()+

"i="+ i + ",j=" + j);

}

bShouldMain=true;

ThreadTest.class.notify();

}

}

}

}

).start();

for(inti=0;i<50;i++)

{

synchronized(ThreadTest.class){

if(!bShouldMain)

{

try{

ThreadTest.class.wait();}

catch(InterruptedException e) {

e.printStackTrace();

}

}

for(intj=0;j<5;j++)

{

System.out.println(

Thread.currentThread().getName()+

"i=" + i +",j=" + j);

}

bShouldMain=false;

ThreadTest.class.notify();

}

}

}

}

下面使用jdk5中的并发库来实现的：

import java.util.concurrent.Executors;

import java.util.concurrent.ExecutorService;

import java.util.concurrent.locks.Lock;

import java.util.concurrent.locks.ReentrantLock;

import java.util.concurrent.locks.Condition;

public class ThreadTest

{

private static Locklock = new ReentrantLock();

private staticCondition subThreadCondition = lock.newCondition();

private staticboolean bBhouldSubThread = false;

public static voidmain(String [] args)

{

ExecutorServicethreadPool = Executors.newFixedThreadPool(3);

threadPool.execute(newRunnable(){

publicvoid run()

{

for(inti=0;i<50;i++)

{

lock.lock();

try

{

if(!bBhouldSubThread)

subThreadCondition.await();

for(intj=0;j<10;j++)

{

System.out.println(Thread.currentThread().getName()+ ",j=" + j);

}

bBhouldSubThread= false;

subThreadCondition.signal();

}catch(Exceptione)

{

}

finally

{

lock.unlock();

}

}

}

});

threadPool.shutdown();

for(inti=0;i<50;i++)

{

lock.lock();

try

{

if(bBhouldSubThread)

subThreadCondition.await();

for(intj=0;j<10;j++)

{

System.out.println(Thread.currentThread().getName()+ ",j=" + j);

}

bBhouldSubThread= true;

subThreadCondition.signal();

}catch(Exceptione)

{

}

finally

{

lock.unlock();

}

}

}

}

57、介绍Collection框架的结构

答：随意发挥题，天南海北谁便谈，只要让别觉得你知识渊博，理解透彻即可。

58、Collection框架中实现比较要实现什么接口

comparable/comparator

59、ArrayList和Vector的区别

答：

这两个类都实现了List接口（List接口继承了Collection接口），他们都是有序集合，即存储在这两个集合中的元素的位置都是有顺序的，相当于一种动态的数组，我们以后可以按位置索引号取出某个元素，，并且其中的数据是允许重复的，这是HashSet之类的集合的最大不同处，HashSet之类的集合不可以按索引号去检索其中的元素，也不允许有重复的元素（本来题目问的与hashset没有任何关系，但为了说清楚ArrayList与Vector的功能，我们使用对比方式，更有利于说明问题）。

接着才说ArrayList与Vector的区别，这主要包括两个方面：.

（1）同步性：

Vector是线程安全的，也就是说是它的方法之间是线程同步的，而ArrayList是线程序不安全的，它的方法之间是线程不同步的。如果只有一个线程会访问到集合，那最好是使用ArrayList，因为它不考虑线程安全，效率会高些；如果有多个线程会访问到集合，那最好是使用Vector，因为不需要我们自己再去考虑和编写线程安全的代码。

备注：对于Vector&ArrayList、Hashtable&HashMap，要记住线程安全的问题，记住Vector与Hashtable是旧的，是java一诞生就提供了的，它们是线程安全的，ArrayList与HashMap是java2时才提供的，它们是线程不安全的。所以，我们讲课时先讲老的。

（2）数据增长：

ArrayList与Vector都有一个初始的容量大小，当存储进它们里面的元素的个数超过了容量时，就需要增加ArrayList与Vector的存储空间，每次要增加存储空间时，不是只增加一个存储单元，而是增加多个存储单元，每次增加的存储单元的个数在内存空间利用与程序效率之间要取得一定的平衡。Vector默认增长为原来两倍，而ArrayList的增长策略在文档中没有明确规定（从源代码看到的是增长为原来的1.5倍）。ArrayList与Vector都可以设置初始的空间大小，Vector还可以设置增长的空间大小，而ArrayList没有提供设置增长空间的方法。

总结：即Vector增长原来的一倍，ArrayList增加原来的0.5倍。

60、HashMap和Hashtable的区别

（条理上还需要整理，也是先说相同点，再说不同点）

HashMap是Hashtable的轻量级实现（非线程安全的实现），他们都完成了Map接口，主要区别在于HashMap允许空（null）键值（key）,由于非线程安全，在只有一个线程访问的情况下，效率要高于Hashtable。

HashMap允许将null作为一个entry的key或者value，而Hashtable不允许。

HashMap把Hashtable的contains方法去掉了，改成containsvalue和containsKey。因为contains方法容易让人引起误解。

Hashtable继承自Dictionary类，而HashMap是Java1.2引进的Map interface的一个实现。

最大的不同是，Hashtable的方法是Synchronize的，而HashMap不是，在多个线程访问Hashtable时，不需要自己为它的方法实现同步，而HashMap就必须为之提供外同步。

Hashtable和HashMap采用的hash/rehash算法都大概一样，所以性能不会有很大的差异。

就HashMap与HashTable主要从三方面来说。

一.历史原因:Hashtable是基于陈旧的Dictionary类的，HashMap是Java 1.2引进的Map接口的一个实现

二.同步性:Hashtable是线程安全的，也就是说是同步的，而HashMap是线程序不安全的，不是同步的

三.值：只有HashMap可以让你将空值作为一个表的条目的key或value

61、List和 Map区别?

一个是存储单列数据的集合，另一个是存储键和值这样的双列数据的集合，List中存储的数据是有顺序，并且允许重复；Map中存储的数据是没有顺序的，其键是不能重复的，它的值是可以有重复的。

62、List, Set, Map是否继承自Collection接口?

List，Set是，Map不是

63、List、Map、Set三个接口，存取元素时，各有什么特点？

这样的题属于随意发挥题：这样的题比较考水平，两个方面的水平：一是要真正明白这些内容，二是要有较强的总结和表述能力。如果你明白，但表述不清楚，在别人那里则等同于不明白。

首先，List与Set具有相似性，它们都是单列元素的集合，所以，它们有一个功共同的父接口，叫Collection。Set里面不允许有重复的元素，所谓重复，即不能有两个相等（注意，不是仅仅是相同）的对象，即假设Set集合中有了一个A对象，现在我要向Set集合再存入一个B对象，但B对象与A对象equals相等，则B对象存储不进去，所以，Set集合的add方法有一个boolean的返回值，当集合中没有某个元素，此时add方法可成功加入该元素时，则返回true，当集合含有与某个元素equals相等的元素时，此时add方法无法加入该元素，返回结果为false。Set取元素时，没法说取第几个，只能以Iterator接口取得所有的元素，再逐一遍历各个元素。

List表示有先后顺序的集合，注意，不是那种按年龄、按大小、按价格之类的排序。当我们多次调用add(Obj e)方法时，每次加入的对象就像火车站买票有排队顺序一样，按先来后到的顺序排序。有时候，也可以插队，即调用add(int index,Obj e)方法，就可以指定当前对象在集合中的存放位置。一个对象可以被反复存储进List中，每调用一次add方法，这个对象就被插入进集合中一次，其实，并不是把这个对象本身存储进了集合中，而是在集合中用一个索引变量指向这个对象，当这个对象被add多次时，即相当于集合中有多个索引指向了这个对象，如图x所示。List除了可以以Iterator接口取得所有的元素，再逐一遍历各个元素之外，还可以调用get(index i)来明确说明取第几个。

Map与List和Set不同，它是双列的集合，其中有put方法，定义如下：put(obj key,objvalue)，每次存储时，要存储一对key/value，不能存储重复的key，这个重复的规则也是按equals比较相等。取则可以根据key获得相应的value，即get(Object key)返回值为key所对应的value。另外，也可以获得所有的key的结合，还可以获得所有的value的结合，还可以获得key和value组合成的Map.Entry对象的集合。

List 以特定次序来持有元素，可有重复元素。Set无法拥有重复元素,内部排序。Map保存key-value值，value可多值。

HashSet按照hashcode值的某种运算方式进行存储，而不是直接按hashCode值的大小进行存储。例如，"abc"---> 78，"def" ---> 62，"xyz" ---> 65在hashSet中的存储顺序不是62,65,78，这些问题感谢以前一个叫崔健的学员提出，最后通过查看源代码给他解释清楚，看本次培训学员当中有多少能看懂源码。LinkedHashSet按插入的顺序存储，那被存储对象的hashcode方法还有什么作用呢？学员想想!hashset集合比较两个对象是否相等，首先看hashcode方法是否相等，然后看equals方法是否相等。new两个Student插入到HashSet中，看HashSet的size，实现hashcode和equals方法后再看size。

同一个对象可以在Vector中加入多次。往集合里面加元素，相当于集合里用一根绳子连接到了目标对象。往HashSet中却加不了多次的。

64、说出ArrayList,Vector, LinkedList的存储性能和特性

ArrayList和Vector都是使用数组方式存储数据，此数组元素数大于实际存储的数据以便增加和插入元素，它们都允许直接按序号索引元素，但是插入元素要涉及数组元素移动等内存操作，所以索引数据快而插入数据慢，Vector由于使用了synchronized方法（线程安全），通常性能上较ArrayList差，而LinkedList使用双向链表实现存储，按序号索引数据需要进行前向或后向遍历，但是插入数据时只需要记录本项的前后项即可，所以插入速度较快。

LinkedList也是线程不安全的，LinkedList提供了一些方法，使得LinkedList可以被当作堆栈和队列来使用。

65、去掉一个Vector集合中重复的元素

Vector newVector = new Vector();

For (int i=0;i

{

Object obj = vector.get(i);

if(!newVector.contains(obj);

newVector.add(obj);

}

还有一种简单的方式，HashSet set = new HashSet(vector);

66、Collection和 Collections的区别。

Collection是集合类的上级接口，继承与他的接口主要有Set和List.

Collections是针对集合类的一个帮助类，他提供一系列静态方法实现对各种集合的搜索、排序、线程安全化等操作。

67、Set里的元素是不能重复的，那么用什么方法来区分重复与否呢?是用==还是equals()?它们有何区别?

Set里的元素是不能重复的，元素重复与否是使用equals()方法进行判断的。

equals()和==方法决定引用值是否指向同一对象equals()在类中被覆盖，为的是当两个分离的对象的内容和类型相配的话，返回真值。


68、你所知道的集合类都有哪些？主要方法？

最常用的集合类是 List 和 Map。 List的具体实现包括 ArrayList和 Vector，它们是可变大小的列表，比较适合构建、存储和操作任何类型对象的元素列表。 List适用于按数值索引访问元素的情形。

Map 提供了一个更通用的元素存储方法。 Map集合类用于存储元素对（称作"键"和"值"），其中每个键映射到一个值。

ArrayList/VectoràList

àCollection

HashSet/TreeSetàSet

PropetiesàHashTable

àMap

Treemap/HashMap

我记的不是方法名，而是思想，我知道它们都有增删改查的方法，但这些方法的具体名称，我记得不是很清楚，对于set，大概的方法是add,remove, contains；对于map，大概的方法就是put,remove，contains等，因为，我只要在eclispe下按点操作符，很自然的这些方法就出来了。我记住的一些思想就是List类会有get(int index)这样的方法，因为它可以按顺序取元素，而set类中没有get(int index)这样的方法。List和set都可以迭代出所有元素，迭代时先要得到一个iterator对象，所以，set和list类都有一个iterator方法，用于返回那个iterator对象。map可以返回三个集合，一个是返回所有的key的集合，另外一个返回的是所有value的集合，再一个返回的key和value组合成的EntrySet对象的集合，map也有get方法，参数是key，返回值是key对应的value。

69、两个对象值相同(x.equals(y) == true)，但却可有不同的hash code，这句话对不对?

对。

如果对象要保存在HashSet或HashMap中，它们的equals相等，那么，它们的hashcode值就必须相等。

如果不是要保存在HashSet或HashMap，则与hashcode没有什么关系了，这时候hashcode不等是可以的，例如arrayList存储的对象就不用实现hashcode，当然，我们没有理由不实现，通常都会去实现的。

70、TreeSet里面放对象，如果同时放入了父类和子类的实例对象，那比较时使用的是父类的compareTo方法，还是使用的子类的compareTo方法，还是抛异常！

（应该是没有针对问题的确切的答案，当前的add方法放入的是哪个对象，就调用哪个对象的compareTo方法，至于这个compareTo方法怎么做，就看当前这个对象的类中是如何编写这个方法的）

实验代码：

publicclassParentimplementsComparable {

private intage = 0;

publicParent(intage){

this.age = age;

}

public intcompareTo(Object o){

//TODOAuto-generated method stub

System.out.println("method ofparent");

Parent o1 = (Parent)o;

returnage>o1.age?1:age

}

}

publicclassChildextendsParent {

publicChild(){

super(3);

}

public intcompareTo(Object o){

//TODOAuto-generated methodstub

System.out.println("methodof child");

//Child o1 = (Child)o;

return1;

}

}

publicclassTreeSetTest {

/**

*@paramargs

*/

public static voidmain(String[] args) {

//TODOAuto-generated method stub

TreeSet set =newTreeSet();

set.add(newParent(3));

set.add(newChild());

set.add(newParent(4));

System.out.println(set.size());

}

}

71、说出一些常用的类，包，接口，请各举5个

要让人家感觉你对java ee开发很熟，所以，不能仅仅只列core java中的那些东西，要多列你在做ssh项目中涉及的那些东西。就写你最近写的那些程序中涉及的那些类。

常用的类：BufferedReaderBufferedWriter  FileReader FileWirter  String  Integer

java.util.Date，System，Class，List,HashMap

常用的包：java.langjava.io java.util  java.sql,javax.servlet,org.apache.strtuts.action,org.hibernate

常用的接口：RemoteList Map  Document  NodeList,Servlet,HttpServletRequest,HttpServletResponse,Transaction(Hibernate)、Session(Hibernate),HttpSession

72、java中有几种类型的流？JDK为每种类型的流提供了一些抽象类以供继承，请说出他们分别是哪些类？

字节流，字符流。字节流继承于InputStream OutputStream，字符流继承于InputStreamReaderOutputStreamWriter。在java.io包中还有许多其他的流，主要是为了提高性能和使用方便。

73、字节流与字符流的区别

要把一片二进制数据数据逐一输出到某个设备中，或者从某个设备中逐一读取一片二进制数据，不管输入输出设备是什么，我们要用统一的方式来完成这些操作，用一种抽象的方式进行描述，这个抽象描述方式起名为IO流，对应的抽象类为OutputStream和InputStream，不同的实现类就代表不同的输入和输出设备，它们都是针对字节进行操作的。

在应用中，经常要完全是字符的一段文本输出去或读进来，用字节流可以吗？计算机中的一切最终都是二进制的字节形式存在。对于“中国”这些字符，首先要得到其对应的字节，然后将字节写入到输出流。读取时，首先读到的是字节，可是我们要把它显示为字符，我们需要将字节转换成字符。由于这样的需求很广泛，人家专门提供了字符流的包装类。

底层设备永远只接受字节数据，有时候要写字符串到底层设备，需要将字符串转成字节再进行写入。字符流是字节流的包装，字符流则是直接接受字符串，它内部将串转成字节，再写入底层设备，这为我们向IO设别写入或读取字符串提供了一点点方便。

字符向字节转换时，要注意编码的问题，因为字符串转成字节数组，

其实是转成该字符的某种编码的字节形式，读取也是反之的道理。

讲解字节流与字符流关系的代码案例：

import java.io.BufferedReader;

import java.io.FileInputStream;

import java.io.FileOutputStream;

import java.io.FileReader;

import java.io.FileWriter;

import java.io.InputStreamReader;

import java.io.PrintWriter;

public class IOTest {

public static void main(String[]args) throws Exception {

String str = "中国人";

/*FileOutputStreamfos  = newFileOutputStream("1.txt");

fos.write(str.getBytes("UTF-8"));

fos.close();*/

/*FileWriter fw =new FileWriter("1.txt");

fw.write(str);

fw.close();*/

PrintWriter pw =new PrintWriter("1.txt","utf-8");

pw.write(str);

pw.close();

/*FileReader fr =new FileReader("1.txt");

char[] buf = newchar[1024];

int len =fr.read(buf);

String myStr = newString(buf,0,len);

System.out.println(myStr);*/

/*FileInputStreamfr = new FileInputStream("1.txt");

byte[] buf = newbyte[1024];

int len =fr.read(buf);

String myStr = newString(buf,0,len,"UTF-8");

System.out.println(myStr);*/

BufferedReader br =new BufferedReader(

newInputStreamReader(

newFileInputStream("1.txt"),"UTF-8"

)

);

String myStr =br.readLine();

br.close();

System.out.println(myStr);

}

}

74、什么是java序列化，如何实现java序列化？或者请解释Serializable接口的作用。

我们有时候将一个java对象变成字节流的形式传出去或者从一个字节流中恢复成一个java对象，例如，要将java对象存储到硬盘或者传送给网络上的其他计算机，这个过程我们可以自己写代码去把一个java对象变成某个格式的字节流再传输，但是，jre本身就提供了这种支持，我们可以调用OutputStream的writeObject方法来做，如果要让java帮我们做，要被传输的对象必须实现serializable接口，这样，javac编译时就会进行特殊处理，编译的类才可以被writeObject方法操作，这就是所谓的序列化。需要被序列化的类必须实现Serializable接口，该接口是一个mini接口，其中没有需要实现的方法，implementsSerializable只是为了标注该对象是可被序列化的。

例如，在web开发中，如果对象被保存在了Session中，tomcat在重启时要把Session对象序列化到硬盘，这个对象就必须实现Serializable接口。如果对象要经过分布式系统进行网络传输或通过rmi等远程调用，这就需要在网络上传输对象，被传输的对象就必须实现Serializable接口。

75、描述一下JVM加载class文件的原理机制?

JVM中类的装载是由ClassLoader和它的子类来实现的,Java ClassLoader是一个重要的Java运行时系统组件。它负责在运行时查找和装入类文件的类。

76、heap和stack有什么区别。

java的内存分为两类，一类是栈内存，一类是堆内存。栈内存是指程序进入一个方法时，会为这个方法单独分配一块私属存储空间，用于存储这个方法内部的局部变量，当这个方法结束时，分配给这个方法的栈会释放，这个栈中的变量也将随之释放。

堆是与栈作用不同的内存，一般用于存放不放在当前方法栈中的那些数据，例如，使用new创建的对象都放在堆里，所以，它不会随方法的结束而消失。方法中的局部变量使用final修饰后，放在堆中，而不是栈中。

77、GC是什么?为什么要有GC?

GC是垃圾收集的意思（Gabage Collection）,内存处理是编程人员容易出现问题的地方，忘记或者错误的内存回收会导致程序或系统的不稳定甚至崩溃，Java提供的GC功能可以自动监测对象是否超过作用域从而达到自动回收内存的目的，Java语言没有提供释放已分配内存的显示操作方法。

78、垃圾回收的优点和原理。并考虑2种回收机制。

Java语言中一个显著的特点就是引入了垃圾回收机制，使c++程序员最头疼的内存管理的问题迎刃而解，它使得Java程序员在编写程序的时候不再需要考虑内存管理。由于有个垃圾回收机制，Java中的对象不再有"作用域"的概念，只有对象的引用才有"作用域"。垃圾回收可以有效的防止内存泄露，有效的使用可以使用的内存。垃圾回收器通常是作为一个单独的低级别的线程运行，不可预知的情况下对内存堆中已经死亡的或者长时间没有使用的对象进行清楚和回收，程序员不能实时的调用垃圾回收器对某个对象或所有对象进行垃圾回收。回收机制有分代复制垃圾回收和标记垃圾回收，增量垃圾回收。

79、垃圾回收器的基本原理是什么？垃圾回收器可以马上回收内存吗？有什么办法主动通知虚拟机进行垃圾回收？

对于GC来说，当程序员创建对象时，GC就开始监控这个对象的地址、大小以及使用情况。通常，GC采用有向图的方式记录和管理堆(heap)中的所有对象。通过这种方式确定哪些对象是"可达的"，哪些对象是"不可达的"。当GC确定一些对象为"不可达"时，GC就有责任回收这些内存空间。可以。程序员可以手动执行System.gc()，通知GC运行，但是Java语言规范并不保证GC一定会执行。

80、什么时候用assert。

assertion(断言)在软件开发中是一种常用的调试方式，很多开发语言中都支持这种机制。在实现中，assertion就是在程序中的一条语句，它对一个boolean表达式进行检查，一个正确程序必须保证这个boolean表达式的值为true；如果该值为false，说明程序已经处于不正确的状态下，assert将给出警告或退出。一般来说，assertion用于保证程序最基本、关键的正确性。assertion检查通常在开发和测试时开启。为了提高性能，在软件发布后，assertion检查通常是关闭的。

packagecom.huawei.interview;

publicclassAssertTest {

/**

*@paramargs

*/

public static voidmain(String[] args) {

//TODOAuto-generated method stub

inti = 0;

for(i=0;i<5;i++)

{

System.out.println(i);

}

//假设程序不小心多了一句--i;

--i;

asserti==5;

}

}

81、java中会存在内存泄漏吗，请简单描述。

所谓内存泄露就是指一个不再被程序使用的对象或变量一直被占据在内存中。java中有垃圾回收机制，它可以保证一对象不再被引用的时候，即对象编程了孤儿的时候，对象将自动被垃圾回收器从内存中清除掉。由于Java使用有向图的方式进行垃圾回收管理，可以消除引用循环的问题，例如有两个对象，相互引用，只要它们和根进程不可达的，那么GC也是可以回收它们的，例如下面的代码可以看到这种情况的内存回收：

packagecom.huawei.interview;

importjava.io.IOException;

publicclassGarbageTest {

/**

*@paramargs

*@throwsIOException

*/

public static voidmain(String[] args)throwsIOException {

//TODOAuto-generated method stub

try{

gcTest();

}catch(IOException e) {

//TODOAuto-generated catch block

e.printStackTrace();

}

System.out.println("hasexited gcTest!");

System.in.read();

System.in.read();

System.out.println("out begingc!");

for(inti=0;i<100;i++)

{

System.gc();

System.in.read();

System.in.read();

}

}

private static voidgcTest()throwsIOException {

System.in.read();

System.in.read();

Person p1 =newPerson();

System.in.read();

System.in.read();

Person p2 =newPerson();

p1.setMate(p2);

p2.setMate(p1);

System.out.println("beforeexit gctest!");

System.in.read();

System.in.read();

System.gc();

System.out.println("exitgctest!");

}

private static classPerson

{

byte[] data =new byte[20000000];

Person mate =null;

public voidsetMate(Personother)

{

mate = other;

}

}

}

java中的内存泄露的情况：长生命周期的对象持有短生命周期对象的引用就很可能发生内存泄露，尽管短生命周期对象已经不再需要，但是因为长生命周期对象持有它的引用而导致不能被回收，这就是java中内存泄露的发生场景，通俗地说，就是程序员可能创建了一个对象，以后一直不再使用这个对象，这个对象却一直被引用，即这个对象无用但是却无法被垃圾回收器回收的，这就是java中可能出现内存泄露的情况，例如，缓存系统，我们加载了一个对象放在缓存中(例如放在一个全局map对象中)，然后一直不再使用它，这个对象一直被缓存引用，但却不再被使用。

检查java中的内存泄露，一定要让程序将各种分支情况都完整执行到程序结束，然后看某个对象是否被使用过，如果没有，则才能判定这个对象属于内存泄露。

如果一个外部类的实例对象的方法返回了一个内部类的实例对象，这个内部类对象被长期引用了，即使那个外部类实例对象不再被使用，但由于内部类持久外部类的实例对象，这个外部类对象将不会被垃圾回收，这也会造成内存泄露。

下面内容来自于网上（主要特点就是清空堆栈中的某个元素，并不是彻底把它从数组中拿掉，而是把存储的总数减少，本人写得可以比这个好，在拿掉某个元素时，顺便也让它从数组中消失，将那个元素所在的位置的值设置为null即可）：

我实在想不到比那个堆栈更经典的例子了,以致于我还要引用别人的例子，下面的例子不是我想到的，是书上看到的，当然如果没有在书上看到，可能过一段时间我自己也想的到，可是那时我说是我自己想到的也没有人相信的。

public class Stack {

private Object[] elements=new Object[10];

private int size = 0;

public void push(Object e){

ensureCapacity();

elements[size++] = e;

}

public Object pop(){

if( size == 0)

throw new EmptyStackException();

return elements[--size];

}

private void ensureCapacity(){

if(elements.length == size){

Object[] oldElements = elements;

elements = new Object[2 * elements.length+1];

System.arraycopy(oldElements,0, elements, 0, size);

}

}

}

上面的原理应该很简单，假如堆栈加了10个元素，然后全部弹出来，虽然堆栈是空的，没有我们要的东西，但是这是个对象是无法回收的，这个才符合了内存泄露的两个条件：无用，无法回收。

但是就是存在这样的东西也不一定会导致什么样的后果，如果这个堆栈用的比较少，也就浪费了几个K内存而已，反正我们的内存都上G了，哪里会有什么影响，再说这个东西很快就会被回收的，有什么关系。下面看两个例子。

例子1

public class Bad{

public static Stack s=Stack();

static{

s.push(new Object());

s.pop(); //这里有一个对象发生内存泄露

s.push(new Object()); //上面的对象可以被回收了，等于是自愈了

}

}

因为是static，就一直存在到程序退出，但是我们也可以看到它有自愈功能，就是说如果你的Stack最多有100个对象，那么最多也就只有100个对象无法被回收其实这个应该很容易理解，Stack内部持有100个引用，最坏的情况就是他们都是无用的，因为我们一旦放新的进取，以前的引用自然消失！

内存泄露的另外一种情况：当一个对象被存储进HashSet集合中以后，就不能修改这个对象中的那些参与计算哈希值的字段了，否则，对象修改后的哈希值与最初存储进HashSet集合中时的哈希值就不同了，在这种情况下，即使在contains方法使用该对象的当前引用作为的参数去HashSet集合中检索对象，也将返回找不到对象的结果，这也会导致无法从HashSet集合中单独删除当前对象，造成内存泄露。

82、能不能自己写个类，也叫java.lang.String？

可以，但在应用的时候，需要用自己的类加载器去加载，否则，系统的类加载器永远只是去加载jre.jar包中的那个java.lang.String。由于在tomcat的web应用程序中，都是由webapp自己的类加载器先自己加载WEB-INF/classess目录中的类，然后才委托上级的类加载器加载，如果我们在tomcat的web应用程序中写一个java.lang.String，这时候Servlet程序加载的就是我们自己写的java.lang.String，但是这么干就会出很多潜在的问题，原来所有用了java.lang.String类的都将出现问题。

虽然java提供了endorsed技术，可以覆盖jdk中的某些类，具体做法是….。但是，能够被覆盖的类是有限制范围，反正不包括java.lang这样的包中的类。

（下面的例如主要是便于大家学习理解只用，不要作为答案的一部分，否则，人家怀疑是题目泄露了）例如，运行下面的程序：

packagejava.lang;

publicclassString {

/**

*@paramargs

*/

public static voidmain(String[] args) {

//TODOAuto-generated method stub

System.out.println("string");

}

}

报告的错误如下：

java.lang.NoSuchMethodError:main

Exception inthread "main"

这是因为加载了jre自带的java.lang.String，而该类中没有main方法。

83. Java代码查错

1.

abstract class Name {

private String name;

public abstract boolean isStupidName(String name) {}

}

大侠们，这有何错误?

答案: 错。abstract method必须以分号结尾，且不带花括号。

2.

public class Something {

void doSomething () {

private String s = "";

int l = s.length();

}

}

有错吗?

答案: 错。局部变量前不能放置任何访问修饰符 (private，public，和protected)。final可以用来修饰局部变量

(final如同abstract和strictfp，都是非访问修饰符，strictfp只能修饰class和method而非variable)。

3.

abstract class Something {

private abstract String doSomething ();

}

这好像没什么错吧?

答案: 错。abstract的methods不能以private修饰。abstract的methods就是让子类implement(实现)具体细节的，怎么可以用private把abstract

method封锁起来呢? (同理，abstract method前不能加final)。

4.

public class Something {

public int addOne(final int x) {

return ++x;

}

}

这个比较明显。

答案: 错。int x被修饰成final，意味着x不能在addOne method中被修改。

5.

public class Something {

public static void main(String[] args) {

Other o = new Other();

new Something().addOne(o);

}

public void addOne(final Other o) {

o.i++;

}

}

class Other {

public int i;

}

和上面的很相似，都是关于final的问题，这有错吗?

答案: 正确。在addOne method中，参数o被修饰成final。如果在addOne method里我们修改了o的reference

(比如: o = new Other();)，那么如同上例这题也是错的。但这里修改的是o的member vairable

(成员变量)，而o的reference并没有改变。

6.

class Something {

int i;

public void doSomething() {

System.out.println("i = "+ i);

}

}

有什么错呢? 看不出来啊。

答案: 正确。输出的是"i = 0"。int i属於instant variable (实例变量，或叫成员变量)。instant variable有default value。int的default value是0。

7.

class Something {

final int i;

public void doSomething() {

System.out.println("i = "+ i);

}

}

和上面一题只有一个地方不同，就是多了一个final。这难道就错了吗?

答案: 错。final int i是个final的instant variable (实例变量，或叫成员变量)。final的instant variable没有default value，必须在constructor (构造器)结束之前被赋予一个明确的值。可以修改为"final int i =0;"。

8.

public class Something {

public static void main(String[] args) {

Something s = new Something();

System.out.println("s.doSomething() returns " + doSomething());

}

public String doSomething() {

return "Do something ...";

}

}

看上去很完美。

答案: 错。看上去在main里call doSomething没有什么问题，毕竟两个methods都在同一个class里。但仔细看，main是static的。static method不能直接call non-staticmethods。可改成"System.out.println("s.doSomething()returns " + s.doSomething());"。同理，static method不能访问non-static instant variable。

9.

此处，Something类的文件名叫OtherThing.java

class Something {

private static void main(String[] something_to_do){

System.out.println("Dosomething ...");

}

}

这个好像很明显。

答案: 正确。从来没有人说过Java的Class名字必须和其文件名相同。但public class的名字必须和文件名相同。

10．

interface  A{

int x = 0;

}

class B{

int x =1;

}

class C extends B implements A {

public void pX(){

System.out.println(x);

}

public static void main(String[] args) {

new C().pX();

}

}

答案：错误。在编译时会发生错误(错误描述不同的JVM有不同的信息，意思就是未明确的x调用，两个x都匹配（就象在同时import java.util和java.sql两个包时直接声明Date一样）。对于父类的变量,可以用super.x来明确，而接口的属性默认隐含为 public staticfinal.所以可以通过A.x来明确。

11.

interface Playable {

void play();

}

interface Bounceable {

void play();

}

interface Rollable extends Playable, Bounceable {

Ball ball = new Ball("PingPang");

}

class Ball implements Rollable {

private String name;

public String getName() {

return name;

}

public Ball(String name) {

this.name =name;

}

public void play() {

ball = newBall("Football");

System.out.println(ball.getName());

}

}

这个错误不容易发现。

答案: 错。"interfaceRollable extends Playable, Bounceable"没有问题。interface可继承多个interfaces，所以这里没错。问题出在interface Rollable里的"Ball ball =new Ball("PingPang");"。任何在interface里声明的interface variable (接口变量，也可称成员变量)，默认为public static final。也就是说"Ball ball = new Ball("PingPang");"实际上是"public staticfinal Ball ball = new Ball("PingPang");"。在Ball类的Play()方法中，"ball = newBall("Football");"改变了ball的reference，而这里的ball来自Rollable interface，Rollable interface里的ball是public static final的，final的object是不能被改变reference的。因此编译器将在"ball = newBall("Football");"这里显示有错。

二.算法与编程

1、编写一个程序，将a.txt文件中的单词与b.txt文件中的单词交替合并到c.txt文件中，a.txt文件中的单词用回车符分隔，b.txt文件中用回车或空格进行分隔。

答：

packagecn.itcast;

import java.io.File;

import java.io.FileReader;

import java.io.FileWriter;

public class MainClass{

public static voidmain(String[] args) throws Exception{

FileManager a= new FileManager("a.txt",new char[]{'\n'});

FileManager b= new FileManager("b.txt",new char[]{'\n',' '});

FileWriter c= new FileWriter("c.txt");

String aWord= null;

String bWord= null;

while((aWord= a.nextWord()) !=null ){

c.write(aWord+ "\n");

bWord= b.nextWord();

if(bWord!= null)

c.write(bWord+ "\n");

}

while((bWord= b.nextWord()) != null){

c.write(bWord+ "\n");

}

c.close();

}

}

class FileManager{

String[] words =null;

int pos = 0;

Public FileManager(String filename,char[] seperators) throws Exception{

File f = new File(filename);

FileReader reader = new FileReader(f);

char[] buf =new char[(int)f.length()];

int len =reader.read(buf);

Stringresults = new String(buf,0,len);

String regex= null;

if(seperators.length>1 ){

regex= "" + seperators[0] + "|" + seperators[1];

}else{

regex= "" + seperators[0];

}

words =results.split(regex);

}

public StringnextWord(){

if(pos ==words.length)

returnnull;

returnwords[pos++];

}

}

2、编写一个程序，将d:\java目录下的所有.java文件复制到d:\jad目录下，并将原来文件的扩展名从.java改为.jad。

（大家正在做上面这道题，网上迟到的朋友也请做做这道题，找工作必须能编写这些简单问题的代码！）

答：listFiles方法接受一个FileFilter对象，这个FileFilter对象就是过虑的策略对象，不同的人提供不同的FileFilter实现，即提供了不同的过滤策略。

import java.io.File;

import java.io.FileInputStream;

import java.io.FileOutputStream;

import java.io.FilenameFilter;

import java.io.IOException;

import java.io.InputStream;

import java.io.OutputStream;

public class Jad2Java {

public static voidmain(String[] args) throws Exception {

File srcDir =new File("java");

if(!(srcDir.exists()&& srcDir.isDirectory()))

thrownew Exception("目录不存在");

File[] files= srcDir.listFiles(

newFilenameFilter(){

publicboolean accept(File dir, String name) {

returnname.endsWith(".java");

}

}

);

System.out.println(files.length);

File destDir= new File("jad");

if(!destDir.exists())destDir.mkdir();

for(File f:files){

FileInputStream  fis = new FileInputStream(f);

StringdestFileName = f.getName().replaceAll("\\.java$", ".jad");

FileOutputStreamfos = new FileOutputStream(new File(destDir,destFileName));

copy(fis,fos);

fis.close();

fos.close();

}

}

private static voidcopy(InputStream ips,OutputStream ops) throws Exception{

int len = 0;

byte[] buf =new byte[1024];

while((len =ips.read(buf)) != -1){

ops.write(buf,0,len);

}

}

}

由本题总结的思想及策略模式的解析：

1.

class jad2java{

1.得到某个目录下的所有的java文件集合

1.1得到目录 File srcDir = newFile("d:\\java");

1.2得到目录下的所有java文件：File[] files =srcDir.listFiles(new MyFileFilter());

1.3只想得到.java的文件： class MyFileFilterimplememyts FileFilter{

publicboolean accept(File pathname){

returnpathname.getName().endsWith(".java")

}

}

2.将每个文件复制到另外一个目录，并改扩展名

2.1得到目标目录，如果目标目录不存在，则创建之

2.2根据源文件名得到目标文件名，注意要用正则表达式，注意.的转义。

2.3根据表示目录的File和目标文件名的字符串，得到表示目标文件的File。

//要在硬盘中准确地创建出一个文件，需要知道文件名和文件的目录。

2.4将源文件的流拷贝成目标文件流，拷贝方法独立成为一个方法，方法的参数采用抽象流的形式。

//方法接受的参数类型尽量面向父类，越抽象越好，这样适应面更宽广。

}

分析listFiles方法内部的策略模式实现原理

File[] listFiles(FileFilter filter){

File[] files =listFiles();

//ArraylistacceptedFilesList = new ArrayList();

File[] acceptedFiles= new File[files.length];

int pos = 0;

for(File file:files){

booleanaccepted = filter.accept(file);

if(accepted){

//acceptedFilesList.add(file);

acceptedFiles[pos++]= file;

}

}

Arrays.copyOf(acceptedFiles,pos);

//return(File[])accpetedFilesList.toArray();

}

3、编写一个截取字符串的函数，输入为一个字符串和字节数，输出为按字节截取的字符串，但要保证汉字不被截取半个，如“我ABC”，4，应该截取“我AB”，输入“我ABC汉DEF”，6，应该输出“我ABC”，而不是“我ABC+汉的半个”。

答：

首先要了解中文字符有多种编码及各种编码的特征。

假设n为要截取的字节数。

public static voidmain(String[] args) throws Exception{

String str ="我a爱中华abc我爱传智def';

String str ="我ABC汉";

int num =trimGBK(str.getBytes("GBK"),5);

System.out.println(str.substring(0,num));

}

public staticint  trimGBK(byte[] buf,int n){

int num = 0;

booleanbChineseFirstHalf = false;

for(inti=0;i

{

if(buf[i]<0&& !bChineseFirstHalf){

bChineseFirstHalf= true;

}else{

num++;

bChineseFirstHalf= false;

}

}

return num;

}

4、有一个字符串，其中包含中文字符、英文字符和数字字符，请统计和打印出各个字符的个数。

答：哈哈，其实包含中文字符、英文字符、数字字符原来是出题者放的烟雾弹。

String content = “中国aadf的111萨bbb菲的zz萨菲”;

HashMap map = new HashMap();

for(int i=0;i

{

char c =content.charAt(i);

Integer num =map.get(c);

if(num == null)

num = 1;

else

num = num +1;

map.put(c,num);

}

for(Map.EntrySet entry : map)

{

system.out.println(entry.getkey()+ “:” + entry.getValue());

}

估计是当初面试的那个学员表述不清楚，问题很可能是：

如果一串字符如"aaaabbc中国1512"要分别统计英文字符的数量，中文字符的数量，和数字字符的数量，假设字符中没有中文字符、英文字符、数字字符之外的其他特殊字符。

int engishCount;

int chineseCount;

int digitCount;

for(int i=0;i

{

charch = str.charAt(i);

if(ch>=’0’&& ch<=’9’)

{

digitCount++

}

elseif((ch>=’a’&& ch<=’z’) || (ch>=’A’ && ch<=’Z’))

{

engishCount++;

}

else

{

chineseCount++;

}

}

System.out.println(……………);

5、说明生活中遇到的二叉树，用java实现二叉树

这是组合设计模式。

我有很多个(假设10万个)数据要保存起来，以后还需要从保存的这些数据中检索是否存在某个数据，（我想说出二叉树的好处，该怎么说呢？那就是说别人的缺点），假如存在数组中，那么，碰巧要找的数字位于99999那个地方，那查找的速度将很慢，因为要从第1个依次往后取，取出来后进行比较。平衡二叉树（构建平衡二叉树需要先排序，我们这里就不作考虑了）可以很好地解决这个问题，但二叉树的遍历（前序，中序，后序）效率要比数组低很多，原理如下图：

代码如下：

packagecom.huawei.interview;

publicclassNode {

public intvalue;

publicNode left;

publicNode right;

public voidstore(intvalue)

{

if(value<this.value)

{

if(left ==null)

{

left =newNode();

left.value=value;

}

else

{

left.store(value);

}

}

else if(value>this.value)

{

if(right ==null)

{

right =newNode();

right.value=value;

}

else

{

right.store(value);

}

}

}

public booleanfind(intvalue)

{

System.out.println("happen" +this.value);

if(value ==this.value)

{

return true;

}

else if(value>this.value)

{

if(right ==null)returnfalse;

returnright.find(value);

}else

{

if(left ==null)returnfalse;

returnleft.find(value);

}

}

public  voidpreList()

{

System.out.print(this.value+ ",");

if(left!=null)left.preList();

if(right!=null) right.preList();

}

public voidmiddleList()

{

if(left!=null)left.preList();

System.out.print(this.value+ ",");

if(right!=null)right.preList();

}

public voidafterList()

{

if(left!=null)left.preList();

if(right!=null)right.preList();

System.out.print(this.value+ ",");

}

public static voidmain(String [] args)

{

int[] data =new int[20];

for(inti=0;i

{

data[i] = (int)(Math.random()*100)+ 1;

System.out.print(data[i] +",");

}

System.out.println();

Node root =newNode();

root.value = data[0];

for(inti=1;i

{

root.store(data[i]);

}

root.find(data[19]);

root.preList();

System.out.println();

root.middleList();

System.out.println();

root.afterList();

}

}

-----------------又一次临场写的代码---------------------------

importjava.util.Arrays;

importjava.util.Iterator;

public class Node{

private Node left;

private Node right;

private int value;

//private int num;

public Node(int value){

this.value = value;

}

public void add(int value){

if(value > this.value)

{

if(right != null)

right.add(value);

else

{

Node node = new Node(value);

right = node;

}

}

else{

if(left != null)

left.add(value);

else

{

Node node = new Node(value);

left = node;

}

}

}

public boolean find(int value){

if(value == this.value) return true;

else if(value > this.value){

if(right == null) return false;

else return right.find(value);

}else{

if(left == null) return false;

else return left.find(value);

}

}

public void display(){

System.out.println(value);

if(left != null) left.display();

if(right != null) right.display();

}

/*public Iterator iterator(){

}*/

public static void main(String[] args){

int[] values = new int[8];

for(int i=0;i<8;i++){

int num = (int)(Math.random() * 15);

//System.out.println(num);

//if(Arrays.binarySearch(values,num)<0)

if(!contains(values,num))

values[i] = num;

else

i--;

}

System.out.println(Arrays.toString(values));

Node root = new Node(values[0]);

for(int i=1;i

root.add(values[i]);

}

System.out.println(root.find(13));

root.display();

}

public static boolean contains(int [] arr,int value){

int i = 0;

for(;i

if(arr[i] == value) return true;

}

return false;

}

}

6、从类似如下的文本文件中读取出所有的姓名，并打印出重复的姓名和重复的次数，并按重复次数排序：

1,张三,28

2,李四,35

3,张三,28

4,王五,35

5,张三,28

6,李四,35

7,赵六,28

8,田七,35

程序代码如下（答题要博得用人单位的喜欢，包名用该公司，面试前就提前查好该公司的网址，如果查不到，现场问也是可以的。还要加上实现思路的注释）：

packagecom.huawei.interview;

importjava.io.BufferedReader;

importjava.io.IOException;

importjava.io.InputStream;

importjava.io.InputStreamReader;

importjava.util.Comparator;

importjava.util.HashMap;

importjava.util.Iterator;

importjava.util.Map;

importjava.util.TreeSet;

publicclassGetNameTest {

/**

*@paramargs

*/

public static voidmain(String[] args) {

//TODOAuto-generated method stub

//InputStream ips =GetNameTest.class.getResourceAsStream("/com/huawei/interview/info.txt");

//用上一行注释的代码和下一行的代码都可以，因为info.txt与GetNameTest类在同一包下面，所以，可以用下面的相对路径形式

Map results =newHashMap();

InputStream ips = GetNameTest.class.getResourceAsStream("info.txt");

BufferedReader in =newBufferedReader(newInputStreamReader(ips));

String line =null;

try{

while((line=in.readLine())!=null)

{

dealLine(line,results);

}

sortResults(results);

}catch(IOException e) {

//TODOAuto-generated catchblock

e.printStackTrace();

}

}

static classUser

{

publicString name;

publicInteger value;

publicUser(String name,Integervalue)

{

this.name = name;

this.value = value;

}

@Override

public booleanequals(Object obj) {

//TODOAuto-generated methodstub

//下面的代码没有执行，说明往treeset中增加数据时，不会使用到equals方法。

booleanresult =super.equals(obj);

System.out.println(result);

returnresult;

}

}

private static voidsortResults(Map results) {

//TODOAuto-generated method stub

TreeSet sortedResults =newTreeSet(

newComparator(){

public intcompare(Object o1, Object o2) {

//TODOAuto-generated method stub

User user1 = (User)o1;

User user2 = (User)o2;

/*如果compareTo返回结果0，则认为两个对象相等，新的对象不会增加到集合中去

*所以，不能直接用下面的代码，否则，那些个数相同的其他姓名就打印不出来。

* */

//returnuser1.value-user2.value;

//returnuser1.value

if(user1.value

{

return-1;

}else if(user1.value>user2.value)

{

return1;

}else

{

returnuser1.name.compareTo(user2.name);

}

}

}

);

Iterator iterator =results.keySet().iterator();

while(iterator.hasNext())

{

String name = (String)iterator.next();

Integer value =(Integer)results.get(name);

if(value > 1)

{

sortedResults.add(newUser(name,value));

}

}

printResults(sortedResults);

}

private static voidprintResults(TreeSet sortedResults)

{

Iterator iterator  = sortedResults.iterator();

while(iterator.hasNext())

{

User user = (User)iterator.next();

System.out.println(user.name +":" + user.value);

}

}

public static voiddealLine(String line,Map map)

{

if(!"".equals(line.trim()))

{

String [] results =line.split(",");

if(results.length == 3)

{

String name = results[1];

Integer value =(Integer)map.get(name);

if(value ==null)value = 0;

map.put(name,value + 1);

}

}

}

}

7、写一个Singleton出来。

第一种：饱汉模式

public classSingleTon {

private SingleTon(){

}

//实例化放在静态代码块里可提高程序的执行效率，但也可能更占用空间

private final static SingleTon instance =new SingleTon();

public static SingleTon getInstance(){

return instance;

}

}

第二种：饥汉模式

public classSingleTon {

private SingleTon(){}

private static instance = null;//newSingleTon();

public static synchronized SingleTongetInstance(){

if(instance == null)

instance = new SingleTon();

return instance;

}

}

第三种：用枚举

public enum SingleTon{

ONE;

}

第三：更实际的应用（在什么情况用单例）

public classSequenceGenerator{

//下面是该类自身的业务功能代码

private int count = 0;

public synchronized int getSequence(){

++count;

}

//下面是把该类变成单例的代码

private SequenceGenerator(){}

private final static instance = newSequenceGenerator();

public static SingleTon getInstance(){

return instance;

}

}

第四：

public class MemoryDao

{

private HashMap map = new HashMap();

publicvoid add(Student stu1){

map.put(SequenceGenerator.getInstance().getSequence(),stu1);

}

//把MemoryDao变成单例

}

Singleton模式主要作用是保证在Java应用程序中，一个类Class只有一个实例存在。

一般Singleton模式通常有几种种形式:

第一种形式: 定义一个类，它的构造函数为private的，它有一个static的private的该类变量，在类初始化时实例话，通过一个public的getInstance方法获取对它的引用,继而调用其中的方法。

public class Singleton {

private Singleton(){}

//在自己内部定义自己一个实例，是不是很奇怪？

//注意这是private只供内部调用

private staticSingleton instance = new Singleton();

//这里提供了一个供外部访问本class的静态方法，可以直接访问

public staticSingleton getInstance() {

return instance;

}

}

第二种形式:

public class Singleton {

private static Singleton instance = null;

public static synchronized Singleton getInstance() {

//这个方法比上面有所改进，不用每次都进行生成对象，只是第一次

//使用时生成实例，提高了效率！

if (instance==null)

instance＝new Singleton();

return instance;

}

}

其他形式:

定义一个类，它的构造函数为private的，所有方法为static的。

一般认为第一种形式要更加安全些

8、递归算法题1

一个整数，大于0，不用循环和本地变量，按照n，2n，4n，8n的顺序递增，当值大于5000时，把值按照指定顺序输出来。

例：n=1237

则输出为：

1237，

2474，

4948，

9896，

9896，

4948，

2474，

1237，

提示：写程序时，先致谢按递增方式的代码，写好递增的以后，再增加考虑递减部分。

public static void doubleNum(int n)

{

System.out.println(n);

if(n<=5000)

doubleNum(n*2);

System.out.println(n);

}

Gaibaota(N) = Gaibaota(N-1) + n

9、递归算法题2

第1个人10，第2个比第1个人大2岁，依次递推，请用递归方式计算出第8个人多大？

packagecn.itcast;

importjava.util.Date;

publicclassA1 {

public static voidmain(String [] args)

{

System.out.println(computeAge(8));

}

public static intcomputeAge(intn)

{

if(n==1)return10;

returncomputeAge(n-1) + 2;

}

}

public static voidtoBinary(intn,StringBuffer result)

{

if(n/2 != 0)

toBinary(n/2,result);

result.append(n%2);

}

10、排序都有哪几种方法？请列举。用JAVA实现一个快速排序。

本人只研究过冒泡排序、选择排序和快速排序，下面是快速排序的代码：

public class QuickSort {

/**

* 快速排序

* @param strDate

* @param left

* @param right

*/

public void quickSort(String[] strDate,int left,int right){

String middle,tempDate;

int i,j;

i=left;

j=right;

middle=strDate[(i+j)/2];

do{

while(strDate[i].compareTo(middle)<0&& i

i++; //找出左边比中间值大的数

while(strDate[j].compareTo(middle)>0&& j>left)

j--; //找出右边比中间值小的数

if(i<=j){ //将左边大的数和右边小的数进行替换

tempDate=strDate[i];

strDate[i]=strDate[j];

strDate[j]=tempDate;

i++;

j--;

}

}while(i<=j); //当两者交错时停止

if(i

quickSort(strDate,i,right);//从

}

if(j>left){

quickSort(strDate,left,j);

}

}

/**

* @param args

*/

public static void main(String[] args){

String[] strVoid=newString[]{"11","66","22","0","55","22","0","32"};

QuickSort sort=new QuickSort();

sort.quickSort(strVoid,0,strVoid.length-1);

for(int i=0;i

System.out.println(strVoid[i]+" ");

}

}

}

11、有数组a[n]，用java代码将数组元素顺序颠倒

//用下面的也可以

//for(inti=0,int j=a.length-1;i

importjava.util.Arrays;

public classSwapDemo{

public static void main(String[] args){

int [] a = new int[]{

(int)(Math.random() *1000),

(int)(Math.random() * 1000),

(int)(Math.random() *1000),

(int)(Math.random() *1000),

(int)(Math.random() * 1000)

};

System.out.println(a);

System.out.println(Arrays.toString(a));

swap(a);

System.out.println(Arrays.toString(a));

}

public static void swap(int a[]){

int len = a.length;

for(int i=0;i

int tmp = a[i];

a[i] = a[len-1-i];

a[len-1-i] = tmp;

}

}

}

12．金额转换，阿拉伯数字的金额转换成中国传统的形式如：（￥1011）－>（一千零一拾一元整）输出。

去零的代码：

returnsb.reverse().toString().replaceAll("零[拾佰仟]","零").replaceAll("零+万","万").replaceAll("零+元","元").replaceAll("零+","零");

public class RenMingBi {

/**

* @param args add by zxx ,Nov 29, 2008

*/

private static finalchar[] data = new char[]{

'零','壹','贰','叁','肆','伍','陆','柒','捌','玖'

};

private static finalchar[] units = new char[]{

'元','拾','佰','仟','万','拾','佰','仟','亿'

};

public static voidmain(String[] args) {

// TODOAuto-generated method stub

System.out.println(

convert(135689123));

}

public static Stringconvert(int money)

{

StringBuffersbf = new StringBuffer();

int unit = 0;

while(money!=0)

{

sbf.insert(0,units[unit++]);

intnumber = money%10;

sbf.insert(0,data[number]);

money/= 10;

}

returnsbf.toString();

}

}

三. html&JavaScript&ajax部分

1. 判断第二个日期比第一个日期大

如何用脚本判断用户输入的的字符串是下面的时间格式2004-11-21必须要保证用户的输入是此格式，并且是时间，比如说月份不大于12等等，另外我需要用户输入两个，并且后一个要比前一个晚，只允许用JAVASCRIPT，请详细帮助作答，,

//这里可用正则表达式判断提前判断一下格式，然后按下提取各时间字段内容

window.onload =function()

{

//这么写是为了实现js代码与html代码的分离，当我修改js时，不能影响html代码。

document.getElementById("frm1").onsubmit=

function(){

vard1 = this.d1.value;

vard2 = this.d2.value;

if(!verifyDate(d1)) {alert("第一个日期格式不对");return false;}

if(!verifyDate(d2)) {alert("第二个日期格式不对");return false;}

if(!compareDate(d1,d2)){alert("第二个日期比第一日期小");return false;}

};

}

functioncompareDate(d1,d2)

{

var arrayD1= d1.split("-");

var date1 =new Date(arrayD1[0],arrayD1[1],arrayD1[2]);

var arrayD2= d2.split("-");

var date2 =new Date(arrayD2[0],arrayD2[1],arrayD2[2]);

if(date1> date2) return false;

return true;

}

functionverifyDate(d)

{

vardatePattern = /^\d{4}-(0?[1-9]|1[0-2])-(0?[1-9]|[1-2]\d|3[0-1])$/;

returndatePattern.test(d);

}

2. 用table显示n条记录，每3行换一次颜色，即1，2，3用红色字体，4，5，6用绿色字体，7，8，9用红颜色字体。

1

2

3

4

5

6

7

8

9

10

window.onload=function()

{

var tbl =document.getElementById("tbl");

rows =tbl.getElementsByTagName("tr");

for(i=0;i

{

var j= parseInt(i/3);

if(j%2==0)rows[i].style.backgroundColor="#f00";

else  rows[i].style.backgroundColor="#0f0";

}

}

3、HTML的 form提交之前如何验证数值文本框的内容全部为数字?否则的话提示用户并终止提交?

function chkForm(this)

{

var value = thist.d1.value;

var len =value.length;

for(vari=0;i

{

if(value.charAt(i)>"9"|| value.charAt(i)<"0")

{

alert("含有非数字字符");

returnfalse;

}

}

return true;

}

4、请写出用于校验HTML文本框中输入的内容全部为数字的javascript代码

function chkNumber(eleText)

{

var value =eleText.value;

var len =value.length;

for(vari=0;i

{

if(value.charAt(i)>"9"|| value.charAt(i)<"0")

{

alert("含有非数字字符");

eleText.focus();

break;

}

}

}

除了写完代码，还应该在网页上写出实验步骤和在代码中加入实现思路，让面试官一看就明白你的意图和检查你的结果。

5、说说你用过那些ajax技术和框架，说说它们的区别

四. Java web部分

1、Tomcat的优化经验

答:去掉对web.xml的监视，把jsp提前编辑成Servlet。

有富余物理内存的情况，加大tomcat使用的jvm的内存

2、HTTP请求的GET与POST方式的区别

答:servlet有良好的生存期的定义，包括加载和实例化、初始化、处理请求以及服务结束。这个生存期由javax.servlet.Servlet接口的init,service和destroy方法表达。

3、解释一下什么是servlet;

答:servlet有良好的生存期的定义，包括加载和实例化、初始化、处理请求以及服务结束。这个生存期由javax.servlet.Servlet接口的init,service和destroy方法表达。

4、说一说Servlet的生命周期?

答:servlet有良好的生存期的定义，包括加载和实例化、初始化、处理请求以及服务结束。这个生存期由javax.servlet.Servlet接口的init,service和destroy方法表达。

Servlet被服务器实例化后，容器运行其init方法，请求到达时运行其service方法，service方法自动派遣运行与请求对应的doXXX方法（doGet，doPost）等，当服务器决定将实例销毁的时候调用其destroy方法。

web容器加载servlet，生命周期开始。通过调用servlet的init()方法进行servlet的初始化。通过调用service()方法实现，根据请求的不同调用不同的do***()方法。结束服务，web容器调用servlet的destroy()方法。

5、Servlet的基本架构

public class ServletName extends HttpServlet {

public void doPost(HttpServletRequest request,HttpServletResponse response) throws

ServletException, IOException {

}

public void doGet(HttpServletRequest request,HttpServletResponse response) throws

ServletException, IOException {

}

}

6、SERVLET API中forward()与redirect()的区别？

答:前者仅是容器中控制权的转向，在客户端浏览器地址栏中不会显示出转向后的地址；后者则是完全的跳转，浏览器将会得到跳转的地址，并重新发送请求链接。这样，从浏览器的地址栏中可以看到跳转后的链接地址。所以，前者更加高效，在前者可以满足需要时，尽量使用forward()方法，并且，这样也有助于隐藏实际的链接。在有些情况下，比如，需要跳转到一个其它服务器上的资源，则必须使用

sendRedirect()方法。

7、什么情况下调用doGet()和doPost()？

Jsp页面中的FORM标签里的method属性为get时调用doGet()，为post时调用doPost()。

8、Request对象的主要方法：

setAttribute(String name,Object)：设置名字为name的request的参数值

getAttribute(String name)：返回由name指定的属性值

getAttributeNames()：返回request对象所有属性的名字集合，结果是一个枚举的实例

getCookies()：返回客户端的所有Cookie对象，结果是一个Cookie数组

getCharacterEncoding()：返回请求中的字符编码方式

getContentLength()：返回请求的Body的长度

getHeader(String name)：获得HTTP协议定义的文件头信息

getHeaders(String name)：返回指定名字的request Header的所有值，结果是一个枚举的实例

getHeaderNames()：返回所以request Header的名字，结果是一个枚举的实例

getInputStream()：返回请求的输入流，用于获得请求中的数据

getMethod()：获得客户端向服务器端传送数据的方法

getParameter(String name)：获得客户端传送给服务器端的有name指定的参数值

getParameterNames()：获得客户端传送给服务器端的所有参数的名字，结果是一个枚举的实例

getParametervalues(String name)：获得有name指定的参数的所有值

getProtocol()：获取客户端向服务器端传送数据所依据的协议名称

getQueryString()：获得查询字符串

getRequestURI()：获取发出请求字符串的客户端地址

getRemoteAddr()：获取客户端的IP地址

getRemoteHost()：获取客户端的名字

getSession([Boolean create])：返回和请求相关Session

getServerName()：获取服务器的名字

getServletPath()：获取客户端所请求的脚本文件的路径

getServerPort()：获取服务器的端口号

removeAttribute(String name)：删除请求中的一个属性

9、forward和redirect的区别

forward是服务器请求资源，服务器直接访问目标地址的URL，把那个URL的响应内容读取过来，然后把这些内容再发给浏览器，浏览器根本不知道服务器发送的内容是从哪儿来的，所以它的地址栏中还是原来的地址。

redirect就是服务端根据逻辑,发送一个状态码,告诉浏览器重新去请求那个地址，一般来说浏览器会用刚才请求的所有参数重新请求，所以session,request参数都可以获取。

10、request.getAttribute()和 request.getParameter()有何区别?

11. jsp有哪些内置对象?作用分别是什么?分别有什么方法？

答:JSP共有以下9个内置的对象：

request 用户端请求，此请求会包含来自GET/POST请求的参数

response 网页传回用户端的回应

pageContext 网页的属性是在这里管理

session 与请求有关的会话期

application servlet 正在执行的内容

out 用来传送回应的输出

configservlet的构架部件

page JSP网页本身

exception 针对错误网页，未捕捉的例外

request表示HttpServletRequest对象。它包含了有关浏览器请求的信息，并且提供了几个用于获取cookie, header,和session数据的有用的方法。

response表示HttpServletResponse对象，并提供了几个用于设置送回浏览器的响应的方法（如cookies,头信息等）

out对象是javax.jsp.JspWriter的一个实例，并提供了几个方法使你能用于向浏览器回送输出结果。

pageContext表示一个javax.servlet.jsp.PageContext对象。它是用于方便存取各种范围的名字空间、servlet相关的对象的API，并且包装了通用的servlet相关功能的方法。

session表示一个请求的javax.servlet.http.HttpSession对象。Session可以存贮用户的状态信息

applicaton表示一个javax.servle.ServletContext对象。这有助于查找有关servlet引擎和servlet环境的信息

config表示一个javax.servlet.ServletConfig对象。该对象用于存取servlet实例的初始化参数。

page表示从该页面产生的一个servlet实例

12. jsp有哪些动作?作用分别是什么?

（这个问题似乎不重要，不明白为何有此题）

答:JSP共有以下6种基本动作

jsp:include：在页面被请求的时候引入一个文件。

jsp:useBean：寻找或者实例化一个JavaBean。

jsp:setProperty：设置JavaBean的属性。

jsp:getProperty：输出某个JavaBean的属性。

jsp:forward：把请求转到一个新的页面。

jsp:plugin：根据浏览器类型为Java插件生成OBJECT或EMBED标记

13、JSP的常用指令

isErrorPage(是否能使用Exception对象)，isELIgnored(是否忽略表达式)

14. JSP中动态INCLUDE与静态INCLUDE的区别？

答：动态INCLUDE用jsp:include动作实现

它总是会检查所含文件中的变化，适合用于包含动态页面，并且可以带参数 静态INCLUDE用include伪码实现,定不会检查所含文件的变化，适用于包含静态页面 <%@include file=included.htm %>

15、两种跳转方式分别是什么?有什么区别?

（下面的回答严重错误，应该是想问forward和sendRedirect的区别，毕竟出题的人不是专业搞文字艺术的人，可能表达能力并不见得很强，用词不一定精准，加之其自身的技术面也可能存在一些问题，不一定真正将他的意思表达清楚了，严格意思上来讲，一些题目可能根本就无人能答，所以，答题时要掌握主动，只要把自己知道的表达清楚就够了，而不要去推敲原始题目的具体含义是什么，不要一味想着是在答题）

答：有两种，分别为：

前者页面不会转向include所指的页面，只是显示该页的结果，主页面还是原来的页面。执行完后还会回来，相当于函数调用。并且可以带参数.后者完全转向新页面，不会再回来。相当于go to 语句。

16、页面间对象传递的方法

request，session，application，cookie等

17、JSP和Servlet有哪些相同点和不同点，他们之间的联系是什么？

JSP是Servlet技术的扩展，本质上是Servlet的简易方式，更强调应用的外表表达。JSP编译后是"类servlet"。Servlet和JSP最主要的不同点在于，Servlet的应用逻辑是在Java文件中，并且完全从表示层中的HTML里分离开来。而JSP的情况是Java和HTML可以组合成一个扩展名为.jsp的文件。JSP侧重于视图，Servlet主要用于控制逻辑。

18、MVC的各个部分都有那些技术来实现?如何实现?

答:MVC是Model－View－Controller的简写。Model代表的是应用的业务逻辑（通过JavaBean，EJB组件实现），View是应用的表示面（由JSP页面产生），Controller是提供应用的处理过程控制（一般是一个Servlet），通过这种设计模型把应用逻辑，处理过程和显示逻辑分成不同的组件实现。这些组件可以进行交互和重用。

19、我们在web应用开发过程中经常遇到输出某种编码的字符，如iso8859-1等，如何输出一个某种编码的字符串？

Public String translate(String str) {

String tempStr ="";

try {

tempStr = newString(str.getBytes("ISO-8859-1"), "GBK");

tempStr =tempStr.trim();

}

catch (Exception e) {

System.err.println(e.getMessage());

}

return tempStr;

}

20．现在输入n个数字，以逗号，分开；然后可选择升或者降序排序；按提交键就在另一页面显示按什么排序，结果为，提供reset

五.数据库部分

1、用两种方式根据部门号从高到低，工资从低到高列出每个员工的信息。

employee:

eid,ename,salary,deptid;

select * from employeeorder by deptid desc,salary

2、列出各个部门中工资高于本部门的平均工资的员工数和部门号，并按部门号排序

创建表：

mysql> createtable employee921(id int primary key auto_increment,name varchar(5

0),salary bigint,deptid int);

插入实验数据：

mysql> insert into employee921values(null,'zs',1000,1),(null,'ls',1100,1),(null

,'ww',1100,1),(null,'zl',900,1) ,(null,'zl',1000,2), (null,'zl',900,2),(null,'z

l',1000,2) , (null,'zl',1100,2);

编写sql语句：

（）select avg(salary) from employee921 group by deptid;

（）mysql> selectemployee921.id,employee921.name,employee921.salary,employee921.dep

tid tid fromemployee921where salary > (select avg(salary) from employee921 where  deptid = tid);

效率低的一个语句，仅供学习参考使用（在group by之后不能使用where，只能使用having，在group by之前可以使用where，即表示对过滤后的结果分组）：

mysql> selectemployee921.id,employee921.name,employee921.salary,employee921.dep

tid tid fromemployee921where salary > (select avg(salary) from employee921 group by deptid havingdeptid = tid);

（）select count(*) ,tid

from (

selectemployee921.id,employee921.name,employee921.salary,employee921.deptid tid

from      employee921

where salary>

(selectavg(salary) from employee921 where deptid = tid)

) as t

group by tid ;

另外一种方式：关联查询

select a.ename,a.salary,a.deptid

from emp a,

(selectdeptd,avg(salary) avgsal from emp group by deptid ) b

where a.deptid=b.deptidand a.salary>b.avgsal;

3、存储过程与触发器必须讲，经常被面试到?

create procedure insert_Student (_name varchar(50),_age int ,out_id int)

begin

insert into studentvalue(null,_name,_age);

select max(stuId)into _id from student;

end;

call insert_Student('wfz',23,@id);

select @id;

mysql> create trigger update_Student BEFORE update on studentFOR EACH ROW

-> select * from student;

触发器不允许返回结果

create trigger update_StudentBEFORE update on student FOR EACH ROW

insert intostudent value(null,'zxx',28);

mysql的触发器目前不能对当前表进行操作

create trigger update_StudentBEFORE update on student FOR EACH ROW

delete from articleswhere id=8;

这个例子不是很好，最好是用删除一个用户时，顺带删除该用户的所有帖子

这里要注意使用OLD.id

触发器用处还是很多的，比如校内网、开心网、Facebook，你发一个日志，自动通知好友，其实就是在增加日志时做一个后触发，再向通知表中写入条目。因为触发器效率高。而UCH没有用触发器，效率和数据处理能力都很低。

存储过程的实验步骤：

mysql> delimiter |

mysql> create procedure insertArticle_Procedure (pTitle varchar(50),pBid int,out

pId int)

-> begin

-> insert into article1value(null,pTitle,pBid);

-> select max(id) into pId fromarticle1;

-> end;

-> |

Query OK, 0 rows affected (0.05sec)

mysql> callinsertArticle_Procedure('传智播客',1,@pid);

-> |

Query OK, 0 rows affected (0.00sec)

mysql> delimiter ;

mysql> select @pid;

+------+

| @pid |

+------+

| 3|

+------+

1 row in set (0.00 sec)

mysql> select * fromarticle1;

+----+--------------+------+

| id | title| bid |

+----+--------------+------+

| 1| test        | 1    |

| 2| chuanzhiboke | 1    |

| 3|传智播客| 1    |

+----+--------------+------+

3 rows in set (0.00 sec)

触发器的实验步骤：

create table board1(id intprimary key auto_increment,name varchar(50),ar

ticleCount int);

create table article1(id intprimary key auto_increment,title varchar(50)

,bid int referencesboard1(id));

delimiter |

create triggerinsertArticle_Trigger after insert on article1 for each ro

w begin

-> update board1 setarticleCount=articleCount+1 where id= NEW.bid;

-> end;

-> |

delimiter ;

insert into board1 value(null,'test',0);

insert into article1value(null,'test',1);

还有，每插入一个帖子，都希望将版面表中的最后发帖时间，帖子总数字段进行同步更新，用触发器做效率就很高。下次课设计这样一个案例，写触发器时，对于最后发帖时间可能需要用declare方式声明一个变量，或者是用NEW.posttime来生成。

4、数据库三范式是什么?

第一范式（1NF）：字段具有原子性,不可再分。所有关系型数据库系统都满足第一范式）

数据库表中的字段都是单一属性的，不可再分。例如，姓名字段，其中的姓和名必须作为一个整体，无法区分哪部分是姓，哪部分是名，如果要区分出姓和名，必须设计成两个独立的字段。

第二范式（2NF）：

第二范式（2NF）是在第一范式（1NF）的基础上建立起来的，即满足第二范式（2NF）必须先满足第一范式（1NF）。

要求数据库表中的每个实例或行必须可以被惟一地区分。通常需要为表加上一个列，以存储各个实例的惟一标识。这个惟一属性列被称为主关键字或主键。

第二范式（2NF）要求实体的属性完全依赖于主关键字。所谓完全依赖是指不能存在仅依赖主关键字一部分的属性，如果存在，那么这个属性和主关键字的这一部分应该分离出来形成一个新的实体，新实体与原实体之间是一对多的关系。为实现区分通常需要为表加上一个列，以存储各个实例的惟一标识。简而言之，第二范式就是非主属性非部分依赖于主关键字。

第三范式的要求如下：

满足第三范式（3NF）必须先满足第二范式（2NF）。简而言之，第三范式（3NF）要求一个数据库表中不包含已在其它表中已包含的非主关键字信息。

所以第三范式具有如下特征：

1，每一列只有一个值

2，每一行都能区分。

3，每一个表都不包含其他表已经包含的非主关键字信息。

例如，帖子表中只能出现发帖人的id，而不能出现发帖人的id，还同时出现发帖人姓名，否则，只要出现同一发帖人id的所有记录，它们中的姓名部分都必须严格保持一致，这就是数据冗余。

5、说出一些数据库优化方面的经验?

用PreparedStatement一般来说比Statement性能高：一个sql发给服务器去执行，涉及步骤：语法检查、语义分析，编译，缓存

“inert into user values(1,1,1)”-à二进制

“inert into user values(2,2,2)”-à二进制

“inert into user values(?,?,?)”-à二进制

有外键约束会影响插入和删除性能，如果程序能够保证数据的完整性，那在设计数据库时就去掉外键。（比喻：就好比免检产品，就是为了提高效率，充分相信产品的制造商）

（对于hibernate来说，就应该有一个变化：empleyee->Deptment对象，现在设计时就成了employeeàdeptid）

看mysql帮助文档子查询章节的最后部分，例如，根据扫描的原理，下面的子查询语句要比第二条关联查询的效率高：

1.select e.name,e.salarywhere e.managerid=(select id from employee where name='zxx');

2.select e.name,e.salary,m.name,m.salary fromemployees e,employees m where

e.managerid = m.id andm.name='zxx';

表中允许适当冗余，譬如，主题帖的回复数量和最后回复时间等

将姓名和密码单独从用户表中独立出来。这可以是非常好的一对一的案例哟！

sql语句全部大写，特别是列名和表名都大写。特别是sql命令的缓存功能，更加需要统一大小写，sql语句à发给oracle服务器à语法检查和编译成为内部指令à缓存和执行指令。根据缓存的特点，不要拼凑条件，而是用?和PreparedStatment

还有索引对查询性能的改进也是值得关注的。

备注：下面是关于性能的讨论举例

4航班 3个城市

m*n

select * from flight,city where flight.startcityid=city.cityidand city.name='beijing';

m + n

select * from flight where startcityid = (select cityid fromcity where cityname='beijing');

select flight.id,'beijing',flight.flightTime from flight wherestartcityid = (select cityid from city where cityname='beijing')

6、union和union all有什么不同?

假设我们有一个表Student，包括以下字段与数据：

drop table student;

create table student

(

id int primary key,

name nvarchar2(50) not null,

score number not null

);

insert into student values(1,'Aaron',78);

insert into student values(2,'Bill',76);

insert into student values(3,'Cindy',89);

insert into student values(4,'Damon',90);

insert into student values(5,'Ella',73);

insert into student values(6,'Frado',61);

insert into student values(7,'Gill',99);

insert into student values(8,'Hellen',56);

insert into student values(9,'Ivan',93);

insert into student values(10,'Jay',90);

commit;

Union和Union All的区别。

select *

from student

where id < 4

union

select *

from student

where id > 2 and id < 6

结果将是

1    Aaron    78

2    Bill    76

3    Cindy    89

4    Damon    90

5    Ella    73

如果换成Union All连接两个结果集，则返回结果是：

1    Aaron    78

2    Bill    76

3    Cindy    89

3    Cindy    89

4    Damon    90

5    Ella    73

可以看到，Union和Union All的区别之一在于对重复结果的处理。

UNION在进行表链接后会筛选掉重复的记录，所以在表链接后会对所产生的结果集进行排序运算，删除重复的记录再返回结果。实际大部分应用中是不会产生重复的记录，最常见的是过程表与历史表UNION。如：

select * from gc_dfys

union

select * from ls_jg_dfys

这个SQL在运行时先取出两个表的结果，再用排序空间进行排序删除重复的记录，最后返回结果集，如果表数据量大的话可能会导致用磁盘进行排序。

而UNION ALL只是简单的将两个结果合并后就返回。这样，如果返回的两个结果集中有重复的数据，那么返回的结果集就会包含重复的数据了。

从效率上说，UNION ALL要比UNION快很多，所以，如果可以确认合并的两个结果集中不包含重复的数据的话，那么就使用UNION ALL，

7.分页语句

取出sql表中第31到40的记录（以自动增长ID为主键）

sql server方案1：

selecttop 10 * from t where id not in (select top 30 id from t order by id ) orde byid

sql server方案2：

selecttop 10 * from t where id in (select top 40 id from t order by id) order by iddesc

mysql方案：select * from t order by idlimit 30,10

oracle方案：select * from (select rownum r,* from t where r<=40) wherer>30

--------------------待整理进去的内容-------------------------------------

pageSize=20;

pageNo = 5;

1.分页技术1（直接利用sql语句进行分页，效率最高和最推荐的）

mysql:sql = "select * from articles limit " +(pageNo-1)*pageSize + "," + pageSize;

oracle: sql = "select * from " +

"(selectrownum r,* from " +

"(select* from articles order by postime desc)" +

"whererownum<= " + pageNo*pageSize +") tmp " +

"wherer>" + (pageNo-1)*pageSize;

注释：第7行保证rownum的顺序是确定的，因为oracle的索引会造成rownum返回不同的值

简洋提示：没有order by时，rownum按顺序输出，一旦有了order by，rownum不按顺序输出了，这说明rownum是排序前的编号。如果对order by从句中的字段建立了索引，那么，rownum也是按顺序输出的，因为这时候生成原始的查询结果集时会参照索引表的顺序来构建。

sqlserver:sql = "select top 10 * from id not id(select top" + (pageNo-1)*pageSize + "id from articles)"

DataSource ds = new InitialContext().lookup(jndiurl);

Connection cn = ds.getConnection();

//"select * from user where id=?"--->binary directive

PreparedStatement pstmt = cn.prepareSatement(sql);

ResultSet rs = pstmt.executeQuery()

while(rs.next())

{

out.println(rs.getString(1));

}

2.不可滚动的游标

pageSize=20;

pageNo = 5;

cn = null

stmt = null;

rs = null;

try

{

sqlserver:sql = "select* from articles";

DataSource ds = new InitialContext().lookup(jndiurl);

Connection cn = ds.getConnection();

//"select * from user where id=?"--->binary directive

PreparedStatement pstmt = cn.prepareSatement(sql);

ResultSet rs = pstmt.executeQuery()

for(int j=0;j<(pageNo-1)*pageSize;j++)

{

rs.next();

}

int i=0;

while(rs.next() && i<10)

{

i++;

out.println(rs.getString(1));

}

}

cacth(){}

finnaly

{

if(rs!=null)try{rs.close();}catch(Exceptione){}

if(stm.........

if(cn............

}

3.可滚动的游标

pageSize=20;

pageNo = 5;

cn = null

stmt = null;

rs = null;

try

{

sqlserver:sql = "select* from articles";

DataSource ds = new InitialContext().lookup(jndiurl);

Connection cn = ds.getConnection();

//"select * from user where id=?"--->binary directive

PreparedStatement pstmt = cn.prepareSatement(sql,ResultSet.TYPE_SCROLL_INSENSITIVE,...);

//根据上面这行代码的异常SQLFeatureNotSupportedException，就可判断驱动是否支持可滚动游标

ResultSet rs = pstmt.executeQuery()

rs.absolute((pageNo-1)*pageSize)

int i=0;

while(rs.next() && i<10)

{

i++;

out.println(rs.getString(1));

}

}

cacth(){}

finnaly

{

if(rs!=null)try{rs.close();}catch(Exceptione){}

if(stm.........

if(cn............

}

8.用一条SQL语句查询出每门课都大于80分的学生姓名

name   kecheng   fenshu

张三    语文      81

张三    数学      75

李四    语文      76

李四    数学      90

王五    语文      81

王五    数学      100

王五    英语      90

准备数据的sql代码：

create table score(id int primary key auto_increment,namevarchar(20),subject varchar(20),score int);

insert into score values

(null,'张三','语文',81),

(null,'张三','数学',75),

(null,'李四','语文',76),

(null,'李四','数学',90),

(null,'王五','语文',81),

(null,'王五','数学',100),

(null,'王五 ','英语',90);

提示：当百思不得其解时，请理想思维，把小变成大做，把大变成小做，

答案：

A: select distinct name from score  where  name not in (selectdistinct name from score where score<=80)

B:select distince name t1 from score where 80< all (selectscore from score where name=t1);

9.所有部门之间的比赛组合

一个叫department的表，里面只有一个字段name,一共有4条纪录，分别是a,b,c,d,对应四个球对，现在四个球对进行比赛，用一条sql语句显示所有可能的比赛组合.

答：select a.name,b.name

from team a, team b

where a.name < b.name

10.每个月份的发生额都比101科目多的科目

请用SQL语句实现：从TestDB数据表中查询出所有月份的发生额都比101科目相应月份的发生额高的科目。请注意：TestDB中有很多科目，都有1－12月份的发生额。

AccID：科目代码，Occmonth：发生额月份，DebitOccur：发生额。

数据库名：JcyAudit，数据集：Select * from TestDB

准备数据的sql代码：

drop table if exists TestDB;

create table TestDB(id int primary key auto_increment,AccIDvarchar(20), Occmonth date, DebitOccur bigint);

insert into TestDB values

(null,'101','1988-1-1',100),

(null,'101','1988-2-1',110),

(null,'101','1988-3-1',120),

(null,'101','1988-4-1',100),

(null,'101','1988-5-1',100),

(null,'101','1988-6-1',100),

(null,'101','1988-7-1',100),

(null,'101','1988-8-1',100);

--复制上面的数据，故意把第一个月份的发生额数字改小一点

insert into TestDB values

(null,'102','1988-1-1',90),

(null,'102','1988-2-1',110),

(null,'102','1988-3-1',120),

(null,'102','1988-4-1',100),

(null,'102','1988-5-1',100),

(null,'102','1988-6-1',100),

(null,'102','1988-7-1',100),

(null,'102','1988-8-1',100);

--复制最上面的数据，故意把所有发生额数字改大一点

insert into TestDB values

(null,'103','1988-1-1',150),

(null,'103','1988-2-1',160),

(null,'103','1988-3-1',180),

(null,'103','1988-4-1',120),

(null,'103','1988-5-1',120),

(null,'103','1988-6-1',120),

(null,'103','1988-7-1',120),

(null,'103','1988-8-1',120);

--复制最上面的数据，故意把所有发生额数字改大一点

insert into TestDB values

(null,'104','1988-1-1',130),

(null,'104','1988-2-1',130),

(null,'104','1988-3-1',140),

(null,'104','1988-4-1',150),

(null,'104','1988-5-1',160),

(null,'104','1988-6-1',170),

(null,'104','1988-7-1',180),

(null,'104','1988-8-1',140);

--复制最上面的数据，故意把第二个月份的发生额数字改小一点

insert into TestDB values

(null,'105','1988-1-1',100),

(null,'105','1988-2-1',80),

(null,'105','1988-3-1',120),

(null,'105','1988-4-1',100),

(null,'105','1988-5-1',100),

(null,'105','1988-6-1',100),

(null,'105','1988-7-1',100),

(null,'105','1988-8-1',100);

答案：

select distinct AccID from TestDB

where AccID not in

(selectTestDB.AccIDfrom TestDB,

(select * from TestDB where AccID='101') asdb101

whereTestDB.Occmonth=db101.Occmonth and TestDB.DebitOccur<=db101.DebitOccur

);

11.统计每年每月的信息

year  monthamount

1991   1     1.1

1991   2     1.2

1991   3     1.3

1991   4     1.4

1992   1     2.1

1992   2     2.2

1992   3     2.3

1992   4     2.4

查成这样一个结果

year m1  m2  m3  m4

1991 1.1 1.2 1.3 1.4

1992 2.1 2.2 2.3 2.4

提示：这个与工资条非常类似，与学生的科目成绩也很相似。

准备sql语句：

drop table if existssales;

create table sales(idint auto_increment primary key,year varchar(10), month varchar(10), amountfloat(2,1));

insert into salesvalues

(null,'1991','1',1.1),

(null,'1991','2',1.2),

(null,'1991','3',1.3),

(null,'1991','4',1.4),

(null,'1992','1',2.1),

(null,'1992','2',2.2),

(null,'1992','3',2.3),

(null,'1992','4',2.4);

答案一、

select sales.year ,

(select t.amount fromsales t where t.month='1' and t.year= sales.year) '1',

(select t.amount fromsales t where t.month='1' and t.year= sales.year) '2',

(select t.amount fromsales t where t.month='1' and t.year= sales.year) '3',

(select t.amount fromsales t where t.month='1' and t.year= sales.year) as '4'

from salesgroup by year;

12.显示文章标题，发帖人、最后回复时间

表：id,title,postuser,postdate,parentid

准备sql语句：

drop table if exists articles;

create table articles(id int auto_increment primary key,titlevarchar(50), postuser varchar(10), postdate datetime,parentid int referencesarticles(id));

insert into articles values

(null,'第一条','张三','1998-10-10 12:32:32',null),

(null,'第二条','张三','1998-10-10 12:34:32',null),

(null,'第一条回复1','李四','1998-10-10 12:35:32',1),

(null,'第二条回复1','李四','1998-10-10 12:36:32',2),

(null,'第一条回复2','王五','1998-10-10 12:37:32',1),

(null,'第一条回复3','李四','1998-10-10 12:38:32',1),

(null,'第二条回复2','李四','1998-10-10 12:39:32',2),

(null,'第一条回复4','王五','1998-10-10 12:39:40',1);

答案：

select a.title,a.postuser,

(selectmax(postdate) from articles where parentid=a.id) reply

from articles a where a.parentid is null;

注释：子查询可以用在选择列中，也可用于where的比较条件中，还可以用于from从句中。

13.删除除了id号不同,其他都相同的学生冗余信息

2.学生表如下:

id号   学号   姓名课程编号课程名称分数

1        2005001  张三 0001     数学    69

2        2005002  李四 0001     数学    89

3        2005001  张三 0001     数学    69

A: delete from tablename where id号 not in(select min(id号) from tablename group by学号,姓名,课程编号,课程名称,分数)

实验：

create table student2(id int auto_increment primary key,codevarchar(20),name varchar(20));

insert into student2 values(null,'2005001','张三'),(null,'2005002','李四'),(null,'2005001','张三');

//如下语句，mysql报告错误，可能删除依赖后面统计语句，而删除又导致统计语句结果不一致。

delete from student2 where id not in(select min(id) fromstudent2 group by name);

//但是，如下语句没有问题：

select *from student2where id not in(select min(id) from student2 group by name);

//于是，我想先把分组的结果做成虚表，然后从虚表中选出结果，最后再将结果作为删除的条件数据。

delete from student2 where id not in(select mid from (selectmin(id) mid

from student2 group by name) as t);

或者：

delete from student2 where id not in(select min(id) from (select* from s

tudent2) as t group by t.name);

14.航空网的几个航班查询题：

表结构如下：

flight{flightID,StartCityID ,endCityID,StartTime}

city{cityID, CityName)

实验环境：

create table city(cityID int auto_increment primary key,cityNamevarchar(20));

create table flight (flightID int auto_increment primary key,

StartCityID intreferences city(cityID),

endCityID  int references city(cityID),

StartTimetimestamp);

//航班本来应该没有日期部分才好，但是下面的题目当中涉及到了日期

insert into city values(null,'北京'),(null,'上海'),(null,'广州');

insert into flight values

(null,1,2,'9:37:23'),(null,1,3,'9:37:23'),(null,1,2,'10:37:23'),(null,2,3,'10:37:23');

1、查询起飞城市是北京的所有航班，按到达城市的名字排序

参与运算的列是我起码能够显示出来的那些列，但最终我不一定把它们显示出来。各个表组合出来的中间结果字段中必须包含所有运算的字段。

select  * from flight f,city c

where f.endcityid =c.cityid and startcityid =

(select c1.cityidfrom city c1 where c1.cityname = "北京")

order by c.citynameasc;

mysql> select flight.flightid,'北京' startcity, e.cityname from flight,city e wh

ere flight.endcityid=e.cityid and flight.startcityid=(selectcityid from city wh

ere cityname='北京');

mysql> select flight.flightid,s.cityname,e.cityname fromflight,city s,city e wh

ere flight.startcityid=s.cityid and s.cityname='北京' andflight.endCityId=e.cit

yID order by e.cityName desc;

2、查询北京到上海的所有航班纪录（起飞城市，到达城市，起飞时间，航班号）

select c1.CityName,c2.CityName,f.StartTime,f.flightID

from city c1,city c2,flight f

where f.StartCityID=c1.cityID

and f.endCityID=c2.cityID

and c1.cityName='北京'

and c2.cityName='上海'

3、查询具体某一天（2005-5-8）的北京到上海的的航班次数

select count(*) from

(select c1.CityName,c2.CityName,f.StartTime,f.flightID

from city c1,city c2,flight f

where f.StartCityID=c1.cityID

and f.endCityID=c2.cityID

and c1.cityName='北京'

and c2.cityName='上海'

and 查帮助获得的某个日期处理函数(startTime) like '2005-5-8%'

mysql中提取日期部分进行比较的示例代码如下：

select * from flight wheredate_format(starttime,'%Y-%m-%d')='1998-01-02'

15.查出比经理薪水还高的员工信息：

Drop table if not exists employees;

create table employees(id int primary key auto_increment,namevarchar(50)

,salary int,managerid intreferences employees(id));

insert into employees values (null,' lhm',10000,null), (null,'zxx',15000,1

),(null,'flx',9000,1),(null,'tg',10000,2),(null,'wzg',10000,3);

Wzg大于flx,lhm大于zxx

解题思路：

根据sql语句的查询特点，是逐行进行运算，不可能两行同时参与运算。

涉及了员工薪水和经理薪水，所有，一行记录要同时包含两个薪水，所有想到要把这个表自关联组合一下。

首先要组合出一个包含有各个员工及该员工的经理信息的长记录，譬如，左半部分是员工，右半部分是经理。而迪卡尔积会组合出很多垃圾信息，先去除这些垃圾信息。

select e.* from employees e,employees m where e.managerid=m.idand e.sala

ry>m.salary;

16、求出小于45岁的各个老师所带的大于12岁的学生人数

数据库中有3个表 teacher表，student表，tea_stu关系表。

teacher 表 teaID name age

student 表 stuID name age

teacher_student表 teaID stuID

要求用一条sql查询出这样的结果

1.显示的字段要有老师name, age每个老师所带的学生人数

2 只列出老师age为40以下，学生age为12以上的记录

预备知识：

1.sql语句是对每一条记录依次处理，条件为真则执行动作（select,insert,delete,update）

2.只要是迪卡尔积，就会产生“垃圾”信息，所以，只要迪卡尔积了，我们首先就要想到清除“垃圾”信息

实验准备：

drop table if exists tea_stu;

drop table if exists teacher;

drop table if exists student;

create table teacher(teaID int primarykey,name varchar(50),age int);

create table student(stuID int primarykey,name varchar(50),age int);

create table tea_stu(teaID int referencesteacher(teaID),stuID int references student(stuID));

insertinto teacher values(1,'zxx',45), (2,'lhm',25) , (3,'wzg',26) , (4,'tg',27);

insertinto student values(1,'wy',11), (2,'dh',25) , (3,'ysq',26) , (4,'mxc',27);

insertinto tea_stu values(1,1), (1,2), (1,3);

insertinto tea_stu values(2,2), (2,3), (2,4);

insert into tea_stu values(3,3), (3,4), (3,1);

insertinto tea_stu values(4,4), (4,1), (4,2) , (4,3);

结果：2à3,3à2,4à3

解题思路：（真实面试答题时，也要写出每个分析步骤，如果纸张不够，就找别人要）

1要会统计分组信息，统计信息放在中间表中：

selectteaid,count(*) from tea_stu group by teaid;

2接着其实应该是筛除掉小于12岁的学生，然后再进行统计，中间表必须与student关联才能得到12岁以下学生和把该学生记录从中间表中剔除，代码是：

selecttea_stu.teaid,count(*) total from student,tea_stu

wherestudent.stuid=tea_stu.stuid and student.age>12 group by tea_stu.teaid

3.接着把上面的结果做成虚表与teacher进行关联，并筛除大于45的老师

selectteacher.teaid,teacher.name,total from teacher ,(select tea_stu.tea

id,count(*)total from student,tea_stu where student.stuid=tea_stu.stuid and stu

dent.age>12group by tea_stu.teaid) as tea_stu2where teacher.teaid=tea_stu2.tea

idand teacher.age<45;

17.求出发帖最多的人：

select authorid,count(*) total from articles

group by authorid

having total=

(select max(total2) from(select count(*) total2 from articles group by authorid) as t);

select t.authorid,max(t.total) from

（select authorid,count(*) total from articles）as t

这条语句不行，因为max只有一列，不能与其他列混淆。

select authorid,count(*) total from articles

group by authorid having total=max(total)也不行。

18、一个用户表中有一个积分字段，假如数据库中有100多万个用户，若要在每年第一天凌晨将积分清零，你将考虑什么，你将想什么办法解决?

alter table drop column score;

alter table add colunm score int;

可能会很快，但是需要试验，试验不能拿真实的环境来操刀，并且要注意，

这样的操作时无法回滚的，在我的印象中，只有inert update delete等DML语句才能回滚，

对于create table,drop table ,alter table等DDL语句是不能回滚。

解决方案一，update user set score=0;

解决方案二，假设上面的代码要执行好长时间，超出我们的容忍范围，那我就alter table user drop columnscore;alter table user add column score int。

下面代码实现每年的那个凌晨时刻进行清零。

Runnable runnable =

new Runnable(){

public voidrun(){

clearDb();

schedule(this,newDate(new Date().getYear()+1,0,0));

}

};

schedule(runnable,

new Date(newDate().getYear()+1,0,1));

19、一个用户具有多个角色，请查询出该表中具有该用户的所有角色的其他用户。

select count(*) as num,tb.id

from

tb,

(select role from tbwhere id=xxx) as t1

where

tb.role = t1.role andtb.id != t1.id

group by tb.id

having

num = select count(role)from tb where id=xxx;

20. xxx公司的sql面试

TableEMPLOYEESStructure:

EMPLOYEE_IDNUMBER        Primary Key,

FIRST_NAMEVARCHAR2(25),

LAST_NAMEVARCHAR2(25),

Salary number(8,2),

HiredDate DATE,

Departmentid number(2)

TableDepartmentsStructure:

Departmentid number(2)Primary Key,

DepartmentNameVARCHAR2(25).

(2）基于上述EMPLOYEES表写出查询：写出雇用日期在今年的，或者工资在[1000,2000]之间的，或者员工姓名（last_name）以’Obama’打头的所有员工，列出这些员工的全部个人信息。（4分）

select* from employees

whereYear(hiredDate) = Year(date())

or (salary between 1000 and 200)

or left(last_name,3)='abc';

(3) 基于上述EMPLOYEES表写出查询：查出部门平均工资大于1800元的部门的所有员工，列出这些员工的全部个人信息。（4分）

mysql>select id,name,salary,deptid did from employee1 where (select avg(salary)

from employee1 where deptid = did) > 1800;

(4) 基于上述EMPLOYEES表写出查询：查出个人工资高于其所在部门平均工资的员工，列出这些员工的全部个人信息及该员工工资高出部门平均工资百分比。（5分）

selectemployee1.*,(employee1.salary-t.avgSalary)*100/employee1.salary

fromemployee1,

(select deptid,avg(salary) avgSalary fromemployee1 group by deptid) as t

whereemployee1.deptid = t.deptid and employee1.salary>t.avgSalary;

21、注册Jdbc驱动程序的三种方式

22、用JDBC如何调用存储过程

代码如下：

packagecom.huawei.interview.lym;

importjava.sql.CallableStatement;

importjava.sql.Connection;

importjava.sql.DriverManager;

importjava.sql.SQLException;

importjava.sql.Types;

publicclassJdbcTest {

/**

*@paramargs

*/

public static voidmain(String[] args) {

//TODOAuto-generated method stub

Connection cn =null;

CallableStatement cstmt =null;

try{

//这里最好不要这么干，因为驱动名写死在程序中了

Class.forName("com.mysql.jdbc.Driver");

//实际项目中，这里应用DataSource数据，如果用框架，

//这个数据源不需要我们编码创建，我们只需Datasource ds =context.lookup()

//cn = ds.getConnection();

cn = DriverManager.getConnection("jdbc:mysql:///test","root","root");

cstmt = cn.prepareCall("{callinsert_Student(?,?,?)}");

cstmt.registerOutParameter(3,Types.INTEGER);

cstmt.setString(1,"wangwu");

cstmt.setInt(2, 25);

cstmt.execute();

//get第几个，不同的数据库不一样，建议不写

System.out.println(cstmt.getString(3));

}catch(Exception e) {

//TODOAuto-generated catchblock

e.printStackTrace();

}

finally

{

/*try{cstmt.close();}catch(Exceptione){}

try{cn.close();}catch(Exceptione){}*/

try{

if(cstmt !=null)

cstmt.close();

if(cn !=null)

cn.close();

}catch(SQLException e) {

//TODOAuto-generatedcatch block

e.printStackTrace();

}

}

}

23、JDBC中的PreparedStatement相比Statement的好处

答：一个sql命令发给服务器去执行的步骤为：语法检查，语义分析，编译成内部指令，缓存指令，执行指令等过程。

select * from student where id =3----缓存--àxxxxx二进制命令

select * from student where id =3----直接取-àxxxxx二进制命令

select * from student where id =4--- -à会怎么干？

如果当初是select * from student where id =?--- -à又会怎么干？

上面说的是性能提高

可以防止sql注入。

24. 写一个用jdbc连接并访问oracle数据的程序代码

25、Class.forName的作用?为什么要用?

答：按参数中指定的字符串形式的类名去搜索并加载相应的类，如果该类字节码已经被加载过，则返回代表该字节码的Class实例对象，否则，按类加载器的委托机制去搜索和加载该类，如果所有的类加载器都无法加载到该类，则抛出ClassNotFoundException。加载完这个Class字节码后，接着就可以使用Class字节码的newInstance方法去创建该类的实例对象了。

有时候，我们程序中所有使用的具体类名在设计时（即开发时）无法确定，只有程序运行时才能确定，这时候就需要使用Class.forName去动态加载该类，这个类名通常是在配置文件中配置的，例如，spring的ioc中每次依赖注入的具体类就是这样配置的，jdbc的驱动类名通常也是通过配置文件来配置的，以便在产品交付使用后不用修改源程序就可以更换驱动类名。

26、大数据量下的分页解决方法。

答：最好的办法是利用sql语句进行分页，这样每次查询出的结果集中就只包含某页的数据内容。再sql语句无法实现分页的情况下，可以考虑对大的结果集通过游标定位方式来获取某页的数据。

sql语句分页，不同的数据库下的分页方案各不一样，下面是主流的三种数据库的分页sql：

sql server:

String sql =

"select top" + pageSize + " * from students where id not in" +

"(select top "+ pageSize * (pageNumber-1) + " id from students order by id)" +

"order by id";

mysql:

String sql =

"select * fromstudents order by id limit " + pageSize*(pageNumber-1) + "," +pageSize;

oracle:

String sql =

"select * from " +

(select *,rownum rid from (select * fromstudents order by postime desc) where rid<=" + pagesize*pagenumber +") as t" +

"where t>" +pageSize*(pageNumber-1);

27、用 JDBC查询学生成绩单,把主要代码写出来（考试概率极大）.

Connection cn = null;

PreparedStatement pstmt =null;

Resultset rs = null;

try

{

Class.forname(driveClassName);

cn =  DriverManager.getConnection(url,username,password);

pstmt =cn.prepareStatement(“select  score.* fromscore ,student “ +

“wherescore.stuId = student.id and student.name = ?”);

pstmt.setString(1,studentName);

Resultset rs =pstmt.executeQuery();

while(rs.next())

{

system.out.println(rs.getInt(“subject”)  +  “    ” + rs.getFloat(“score”) );

}

}catch(Exception e){e.printStackTrace();}

finally

{

if(rs != null) try{rs.close() }catch(exception e){}

if(pstmt != null)try{pstmt.close()}catch(exception e){}

if(cn != null) try{cn.close() }catch(exception e){}

}

28、这段代码有什么不足之处?

try {

Connection conn = ...;

Statement stmt = ...;

ResultSet rs =stmt.executeQuery("select * from table1");

while(rs.next()) {

}

} catch(Exception ex) {

}

答：没有finally语句来关闭各个对象，另外，使用finally之后，要把变量的定义放在try语句块的外面，以便在try语句块之外的finally块中仍可以访问这些变量。

29、说出数据连接池的工作机制是什么?

J2EE服务器启动时会建立一定数量的池连接，并一直维持不少于此数目的池连接。客户端程序需要连接时，池驱动程序会返回一个未使用的池连接并将其表记为忙。如果当前没有空闲连接，池驱动程序就新建一定数量的连接，新建连接的数量有配置参数决定。当使用的池连接调用完成后，池驱动程序将此连接表记为空闲，其他调用就可以使用这个连接。

实现方式，返回的Connection是原始Connection的代理，代理Connection的close方法不是真正关连接，而是把它代理的Connection对象还回到连接池中。

30、为什么要用 ORM? 和 JDBC有何不一样?

orm是一种思想，就是把object转变成数据库中的记录，或者把数据库中的记录转变成objecdt，我们可以用jdbc来实现这种思想，其实，如果我们的项目是严格按照oop方式编写的话，我们的jdbc程序不管是有意还是无意，就已经在实现orm的工作了。

现在有许多orm工具，它们底层调用jdbc来实现了orm工作，我们直接使用这些工具，就省去了直接使用jdbc的繁琐细节，提高了开发效率，现在用的较多的orm工具是hibernate。也听说一些其他orm工具，如toplink,ojb等。

六. XML部分

1、xml有哪些解析技术?区别是什么?

答:有DOM,SAX,STAX等

DOM:处理大型文件时其性能下降的非常厉害。这个问题是由DOM的树结构所造成的，这种结构占用的内存较多，而且DOM必须在解析文件之前把整个文档装入内存,适合对XML的随机访问SAX:不现于DOM,SAX是事件驱动型的XML解析方式。它顺序读取XML文件，不需要一次全部装载整个文件。当遇到像文件开头，文档结束，或者标签开头与标签结束时，它会触发一个事件，用户通过在其回调事件中写入处理代码来处理XML文件，适合对XML的顺序访问

STAX:Streaming API for XML (StAX)

讲解这些区别是不需要特别去比较，就像说传智播客与其他培训机构的区别时，我们只需说清楚传智播客有什么特点和优点就行了，这就已经间接回答了彼此的区别。

2、你在项目中用到了xml技术的哪些方面?如何实现的?

答:用到了数据存贮，信息配置两方面。在做数据交换平台时，将不能数据源的数据组装成XML文件，然后将XML文件压缩打包加密后通过网络传送给接收者，接收解密与解压缩后再同XML文件中还原相关信息进行处理。在做软件配置时，利用XML可以很方便的进行，软件的各种配置参数都存贮在XML文件中。

3、用jdom解析xml文件时如何解决中文问题?如何解析?

答:看如下代码,用编码方式加以解决

package test;

import java.io.*;

public class DOMTest

{

private String inFile = "c:\\people.xml"

private String outFile = "c:\\people.xml"

public static void main(String args[])

{

new DOMTest();

}

public DOMTest()

{

try

{

javax.xml.parsers.DocumentBuilder builder =

javax.xml.parsers.DocumentBuilderFactory.newInstance().newDocumentBuilder();

org.w3c.dom.Document doc = builder.newDocument();

org.w3c.dom.Element root = doc.createElement("老师");

org.w3c.dom.Element wang = doc.createElement("王");

org.w3c.dom.Element liu = doc.createElement("刘");

wang.appendChild(doc.createTextNode("我是王老师"));

root.appendChild(wang);

doc.appendChild(root);

javax.xml.transform.Transformer transformer =

javax.xml.transform.TransformerFactory.newInstance().newTransformer();

transformer.setOutputProperty(javax.xml.transform.OutputKeys.ENCODING,"gb2312");

transformer.setOutputProperty(javax.xml.transform.OutputKeys.INDENT,"yes");

transformer.transform(newjavax.xml.transform.dom.DOMSource(doc),

new

javax.xml.transform.stream.StreamResult(outFile));

}

catch (Exception e)

{

System.out.println (e.getMessage());

}

}

}

4、编程用JAVA解析XML的方式.

答:用SAX方式解析XML，XML文件如下：



王小明

信息学院

6258113

男,1955年生,博士，95年调入海南大学

事件回调类SAXHandler.java

import java.io.*;

import java.util.Hashtable;

import org.xml.sax.*;

public class SAXHandler extends HandlerBase

{

private Hashtable table = new Hashtable();

private String currentElement = null;

private String currentValue = null;

public void setTable(Hashtable table)

{

this.table = table;

}

public Hashtable getTable()

{

return table;

}

public void startElement(String tag, AttributeList attrs)

throws SAXException

{

currentElement = tag;

}

public void characters(char[] ch, int start, int length)

throws SAXException

{

currentValue = new String(ch, start, length);

}

public void endElement(String name) throws SAXException

{

if (currentElement.equals(name))

table.put(currentElement, currentValue);

}

}

JSP内容显示源码,SaxXml.jsp:

剖析XML文件people.xml

<%@ page errorPage=ErrPage.jsp

contentType=text/html;charset=GB2312 %>

<%@ page import=java.io.* %>

<%@ page import=java.util.Hashtable %>

<%@ page import=org.w3c.dom.* %>

<%@ page import=org.xml.sax.* %>

<%@ page import=javax.xml.parsers.SAXParserFactory %>

<%@ page import=javax.xml.parsers.SAXParser %>

<%@ page import=SAXHandler %>

<%

File file = new File(c:\people.xml);

FileReader reader = new FileReader(file);

Parser parser;

SAXParserFactory spf = SAXParserFactory.newInstance();

SAXParser sp = spf.newSAXParser();

SAXHandler handler = new SAXHandler();

sp.parse(new InputSource(reader), handler);

Hashtable hashTable = handler.getTable();

out.println();教师信息表

姓名 +

(String)hashTable.get(new String(name)) +);

学院 +

(String)hashTable.get(newString(college))+);

电话 +

(String)hashTable.get(new String(telephone)) +);

备注 +

(String)hashTable.get(new String(notes)) +);

out.println();

%>

5、XML文档定义有几种形式？它们之间有何本质区别？解析XML文档有哪几种方式？

a: 两种形式 dtdschema，b:本质区别:schema本身是xml的，可以被XML解析器解析(这也是从DTD上发展schema的根本目的)，c:有DOM,SAX,STAX等

DOM:处理大型文件时其性能下降的非常厉害。这个问题是由DOM的树结构所造成的，这种结构占用的内存较多，而且DOM必须在解析文件之前把整个文档装入内存,适合对XML的随机访问

SAX:不现于DOM,SAX是事件驱动型的XML解析方式。它顺序读取XML文件，不需要一次全部装载整个文件。当遇到像文件开头，文档结束，或者标签开头与标签结束时，它会触发一个事件，用户通过在其回调事件中写入处理代码来处理XML文件，适合对XML的顺序访问

STAX:Streaming API forXML (StAX)

七.流行的框架与新技术

1、谈谈你对Struts的理解。

答:

1. struts是一个按MVC模式设计的Web层框架，其实它就是一个大大的servlet，这个Servlet名为ActionServlet，或是ActionServlet的子类。我们可以在web.xml文件中将符合某种特征的所有请求交给这个Servlet处理，这个Servlet再参照一个配置文件（通常为/WEB-INF/struts-config.xml）将各个请求分别分配给不同的action去处理。

一个扩展知识点：struts的配置文件可以有多个，可以按模块配置各自的配置文件，这样可以防止配置文件的过度膨胀；

2.ActionServlet把请求交给action去处理之前，会将请求参数封装成一个formbean对象（就是一个java类，这个类中的每个属性对应一个请求参数），封装成一个什么样的formbean对象呢？看配置文件。

3.要说明的是， ActionServlet把formbean对象传递给action的execute方法之前，可能会调用formbean的validate方法进行校验，只有校验通过后才将这个formbean对象传递给action的execute方法，否则，它将返回一个错误页面，这个错误页面由input属性指定，（看配置文件）作者为什么将这里命名为input属性，而不是error属性，我们后面结合实际的运行效果进行分析。

4.action执行完后要返回显示的结果视图，这个结果视图是用一个ActionForward对象来表示的，actionforward对象通过struts-config.xml配置文件中的配置关联到某个jsp页面，因为程序中使用的是在struts-config.xml配置文件为jsp页面设置的逻辑名，这样可以实现action程序代码与返回的jsp页面名称的解耦。

你对struts可能还有自己的应用方面的经验，那也要一并说出来。

2、谈谈你对Hibernate的理解。

答:

1. 面向对象设计的软件内部运行过程可以理解成就是在不断创建各种新对象、建立对象之间的关系，调用对象的方法来改变各个对象的状态和对象消亡的过程，不管程序运行的过程和操作怎么样，本质上都是要得到一个结果，程序上一个时刻和下一个时刻的运行结果的差异就表现在内存中的对象状态发生了变化。

2.为了在关机和内存空间不够的状况下，保持程序的运行状态，需要将内存中的对象状态保存到持久化设备和从持久化设备中恢复出对象的状态，通常都是保存到关系数据库来保存大量对象信息。从Java程序的运行功能上来讲，保存对象状态的功能相比系统运行的其他功能来说，应该是一个很不起眼的附属功能，java采用jdbc来实现这个功能，这个不起眼的功能却要编写大量的代码，而做的事情仅仅是保存对象和恢复对象，并且那些大量的jdbc代码并没有什么技术含量，基本上是采用一套例行公事的标准代码模板来编写，是一种苦活和重复性的工作。

3.通过数据库保存java程序运行时产生的对象和恢复对象，其实就是实现了java对象与关系数据库记录的映射关系，称为ORM（即Object RelationMapping），人们可以通过封装JDBC代码来实现了这种功能，封装出来的产品称之为ORM框架，Hibernate就是其中的一种流行ORM框架。使用Hibernate框架，不用写JDBC代码，仅仅是调用一个save方法，就可以将对象保存到关系数据库中，仅仅是调用一个get方法，就可以从数据库中加载出一个对象。

4.使用Hibernate的基本流程是：配置Configuration对象、产生SessionFactory、创建session对象，启动事务，完成CRUD操作，提交事务，关闭session。

5.使用Hibernate时，先要配置hibernate.cfg.xml文件，其中配置数据库连接信息和方言等，还要为每个实体配置相应的hbm.xml文件，hibernate.cfg.xml文件中需要登记每个hbm.xml文件。

6.在应用Hibernate时，重点要了解Session的缓存原理，级联，延迟加载和hql查询。

3、AOP的作用。

4、你对Spring的理解。

1.Spring实现了工厂模式的工厂类（在这里有必要解释清楚什么是工厂模式），这个类名为BeanFactory（实际上是一个接口），在程序中通常BeanFactory的子类ApplicationContext。Spring相当于一个大的工厂类，在其配置文件中通过元素配置用于创建实例对象的类名和实例对象的属性。

2. Spring提供了对IOC良好支持，IOC是一种编程思想，是一种架构艺术，利用这种思想可以很好地实现模块之间的解耦。IOC也称为DI（Depency Injection），什么叫依赖注入呢？

譬如，Class Programmer

{

Computer computer =null;

public void code()

{

//Computercomputer = new IBMComputer();

//Computercomputer = beanfacotry.getComputer();

computer.write();

}

public voidsetComputer(Computer computer)

{

this.computer= computer;

}

}

另外两种方式都由依赖，第一个直接依赖于目标类，第二个把依赖转移到工厂上，第三个彻底与目标和工厂解耦了。在spring的配置文件中配置片段如下：

3. Spring提供了对AOP技术的良好封装， AOP称为面向切面编程，就是系统中有很多各不相干的类的方法，在这些众多方法中要加入某种系统功能的代码，例如，加入日志，加入权限判断，加入异常处理，这种应用称为AOP。实现AOP功能采用的是代理技术，客户端程序不再调用目标，而调用代理类，代理类与目标类对外具有相同的方法声明，有两种方式可以实现相同的方法声明，一是实现相同的接口，二是作为目标的子类在，JDK中采用Proxy类产生动态代理的方式为某个接口生成实现类，如果要为某个类生成子类，则可以用CGLI B。在生成的代理类的方法中加入系统功能和调用目标类的相应方法，系统功能的代理以Advice对象进行提供，显然要创建出代理对象，至少需要目标类和Advice类。spring提供了这种支持，只需要在spring配置文件中配置这两个元素即可实现代理和aop功能，例如，

5、谈谈Struts中的Action servlet。

6、Struts优缺点

优点：

1.实现MVC模式，结构清晰,使开发者只关注业务逻辑的实现.

2．有丰富的tag可以用 ,Struts的标记库(Taglib)，如能灵活动用，则能大大提高开发效率

3. 页面导航

使系统的脉络更加清晰。通过一个配置文件，即可把握整个系统各部分之间的联系，这对于后期的维护有着莫大的好处。尤其是当另一批开发者接手这个项目时，这种优势体现得更加明显。

4. 提供Exception处理机制 .

5. 数据库链接池管理

6. 支持I18N

缺点

一、   转到展示层时，需要配置forward，如果有十个展示层的jsp，需要配置十次struts，而且还不包括有时候目录、文件变更，需要重新修改forward，注意，每次修改配置之后，要求重新部署整个项目，而tomcate这样的服务器，还必须重新启动服务器

二、   二、 Struts的Action必需是thread－safe方式，它仅仅允许一个实例去处理所有的请求。所以action用到的所有的资源都必需统一同步，这个就引起了线程安全的问题。

三、    测试不方便. Struts的每个Action都同Web层耦合在一起，这样它的测试依赖于Web容器，单元测试也很难实现。不过有一个Junit的扩展工具Struts TestCase可以实现它的单元测试。

四、    类型的转换. Struts的FormBean把所有的数据都作为String类型，它可以使用工具Commons-Beanutils进行类型转化。但它的转化都是在Class级别，而且转化的类型是不可配置的。类型转化时的错误信息返回给用户也是非常困难的。

五、   对Servlet的依赖性过强. Struts处理Action时必需要依赖ServletRequest和ServletResponse，所有它摆脱不了Servlet容器。

六、    前端表达式语言方面.Struts集成了JSTL，所以它主要使用JSTL的表达式语言来获取数据。可是JSTL的表达式语言在Collection和索引属性方面处理显得很弱。

七、    对Action执行的控制困难. Struts创建一个Action，如果想控制它的执行顺序将会非常困难。甚至你要重新去写Servlet来实现你的这个功能需求。

八、    对Action执行前和后的处理. Struts处理Action的时候是基于class的hierarchies，很难在action处理前和后进行操作。

九、    对事件支持不够.在struts中，实际是一个表单Form对应一个Action类(或DispatchAction)，换一句话说：在Struts中实际是一个表单只能对应一个事件，struts这种事件方式称为application event，application event和component event相比是一种粗粒度的事件

7、STRUTS的应用(如STRUTS架构)

Struts是采用Java Servlet/JavaServer Pages技术，开发Web应用程序的开放源码的framework。采用Struts能开发出基于MVC(Model-View-Controller)设计模式的应用构架。 Struts有如下的主要功能：一.包含一个controller servlet，能将用户的请求发送到相应的Action对象。二.JSP自由tag库，并且在controller servlet中提供关联支持，帮助开发员创建交互式表单应用。三.提供了一系列实用对象：XML处理、通过Java reflection APIs自动处理JavaBeans属性、国际化的提示和消息。

8、说说struts1与struts2的区别。

1.都是MVC的WEB框架,

2 struts1的老牌框架，应用很广泛，有很好的群众基础，使用它开发风险很小，成本更低！struts2虽然基于这个框架，但是应用群众并多，相对不成熟，未知的风险和变化很多，开发人员相对不好招，使用它开发项目的风险系数更大，用人成本更高！

3.struts2毕竟是站在前辈的基础设计出来，它会改善和完善struts1中的一些缺陷，struts1中一些悬而未决问题在struts2得到了解决。

4.struts1的前端控制器是一个Servlet，名称为ActionServlet，struts2的前端控制器是一个filter，在struts2.0中叫FilterDispatcher，在struts2.1中叫StrutsPrepareAndExecuteFilter。

5.struts1的action需要继承Action类，struts2的action可以不继承任何类；struts1对同一个路径的所有请求共享一个Action实例，struts2对同一个路径的每个请求分别使用一个独立Action实例对象，所有对于struts2的Action不用考虑线程安全问题。

6.在struts1中使用formbean封装请求参数，在struts2中直接使用action的属性来封装请求参数。

7.struts1中的多个业务方法放在一个Action中时（即继承DispatchAction时），要么都校验，要么都不校验；对于struts2，可以指定只对某个方法进行校验，当一个Action继承了ActionSupport且在这个类中只编写了validateXxx()方法，那么则只对Xxx()方法进行校验。

（一个请求来了的执行流程进行分析，struts2是自动支持分模块开发，并可以不同模块设置不同的url前缀，这是通过package的namespace来实现的；struts2是支持多种类型的视图；struts2的视图地址可以是动态的，即视图的名称是支持变量方式的，举例，论坛发帖失败后回来还要传递boardid。视图内容显示方面：它的标签用ognl，要el强大很多，在国际化方面支持分模块管理，两个模块用到同样的key，对应不同的消息；）

与Struts1不同，Struts2对用户的每一次请求都会创建一个Action，所以Struts2中的Action是线程安全的。

给我印象最深刻的是：struts配置文件中的redirect视图的url不能接受参数，而struts2配置文件中的redirect视图可以接受参数。

9、hibernate中的update()和saveOrUpdate()的区别，session的load()和get()的区别。

10、简述 Hibernate和 JDBC的优缺点?如何书写一个 one to many配置文件.

11、iBatis与Hibernate有什么不同?

相同点：屏蔽jdbc api的底层访问细节，使用我们不用与jdbc api打交道，就可以访问数据。

jdbc api编程流程固定，还将sql语句与java代码混杂在了一起，经常需要拼凑sql语句，细节很繁琐。

ibatis的好处：屏蔽jdbc api的底层访问细节；将sql语句与java代码进行分离;提供了将结果集自动封装称为实体对象和对象的集合的功能，queryForList返回对象集合，用queryForObject返回单个对象；提供了自动将实体对象的属性传递给sql语句的参数。

Hibernate是一个全自动的orm映射工具，它可以自动生成sql语句,ibatis需要我们自己在xml配置文件中写sql语句，hibernate要比ibatis功能负责和强大很多。因为hibernate自动生成sql语句，我们无法控制该语句，我们就无法去写特定的高效率的sql。对于一些不太复杂的sql查询，hibernate可以很好帮我们完成，但是，对于特别复杂的查询，hibernate就很难适应了，这时候用ibatis就是不错的选择，因为ibatis还是由我们自己写sql语句。

12、写Hibernate的一对多和多对一双向关联的orm配置?

9、hibernate的inverse属性的作用?

解决方案一，按照Object[]数据取出数据，然后自己组bean

解决方案二，对每个表的bean写构造函数，比如表一要查出field1,field2两个字段，那么有一个构造函数就是Bean(type1filed1,type2

field2) ，然后在hql里面就可以直接生成这个bean了。

13、在DAO中如何体现DAO设计模式?

解决方案一，按照Object[]数据取出数据，然后自己组bean

解决方案二，对每个表的bean写构造函数，比如表一要查出field1,field2两个字段，那么有一个构造函数就是Bean(type1filed1,type2

field2) ，然后在hql里面就可以直接生成这个bean了。

14、spring+Hibernate中委托方案怎么配置?

解决方案一，按照Object[]数据取出数据，然后自己组bean

解决方案二，对每个表的bean写构造函数，比如表一要查出field1,field2两个字段，那么有一个构造函数就是Bean(type1filed1,type2

field2) ，然后在hql里面就可以直接生成这个bean了。

15、spring+Hibernate中委托方案怎么配置?

解决方案一，按照Object[]数据取出数据，然后自己组bean

解决方案二，对每个表的bean写构造函数，比如表一要查出field1,field2两个字段，那么有一个构造函数就是Bean(type1filed1,type2

field2) ，然后在hql里面就可以直接生成这个bean了。

16. hibernate进行多表查询每个表中各取几个字段，也就是说查询出来的结果集没有一个实体类与之对应如何解决；

解决方案一，按照Object[]数据取出数据，然后自己组bean

解决方案二，对每个表的bean写构造函数，比如表一要查出field1,field2两个字段，那么有一个构造函数就是Bean(type1filed1,type2

field2) ，然后在hql里面就可以直接生成这个bean了。

17.介绍一下Hibernate的二级缓存

按照以下思路来回答：（1）首先说清楚什么是缓存，（2）再说有了hibernate的Session就是一级缓存，即有了一级缓存，为什么还要有二级缓存，（3）最后再说如何配置Hibernate的二级缓存。

（1）缓存就是把以前从数据库中查询出来和使用过的对象保存在内存中（一个数据结构中），这个数据结构通常是或类似Hashmap，当以后要使用某个对象时，先查询缓存中是否有这个对象，如果有则使用缓存中的对象，如果没有则去查询数据库，并将查询出来的对象保存在缓存中，以便下次使用。下面是缓存的伪代码：

引出hibernate的第二级缓存，用下面的伪代码分析了Cache的实现原理

Dao

{

hashmap map = newmap();

User getUser(integerid)

{

User user =map.get(id)

if(user ==null)

{

user =session.get(id);

map.put(id,user);

}

return user;

}

}

Dao

{

Cache cache = null

setCache(Cachecache)

{

this.cache =cache

}

User getUser(int id)

{

if(cache!=null)

{

Useruser = cache.get(id);

if(user==null)

{

user= session.get(id);

cache.put(id,user);

}

returnuser;

}

returnsession.get(id);

}

}

（2）Hibernate的Session就是一种缓存，我们通常将之称为Hibernate的一级缓存，当想使用session从数据库中查询出一个对象时，Session也是先从自己内部查看是否存在这个对象，存在则直接返回，不存在才去访问数据库，并将查询的结果保存在自己内部。由于Session代表一次会话过程，一个Session与一个数据库连接相关连，所以Session最好不要长时间保持打开，通常仅用于一个事务当中，在事务结束时就应关闭。并且Session是线程不安全的，被多个线程共享时容易出现问题。通常只有那种全局意义上的缓存才是真正的缓存应用，才有较大的缓存价值，因此，Hibernate的Session这一级缓存的缓存作用并不明显，应用价值不大。Hibernate的二级缓存就是要为Hibernate配置一种全局缓存，让多个线程和多个事务都可以共享这个缓存。我们希望的是一个人使用过，其他人也可以使用，session没有这种效果。

（3）二级缓存是独立于Hibernate的软件部件，属于第三方的产品，多个厂商和组织都提供有缓存产品，例如，EHCache和OSCache等等。在Hibernate中使用二级缓存，首先就要在hibernate.cfg.xml配置文件中配置使用哪个厂家的缓存产品，接着需要配置该缓存产品自己的配置文件，最后要配置Hibernate中的哪些实体对象要纳入到二级缓存的管理中。明白了二级缓存原理和有了这个思路后，很容易配置起Hibernate的二级缓存。扩展知识：一个SessionFactory可以关联一个二级缓存，也即一个二级缓存只能负责缓存一个数据库中的数据，当使用Hibernate的二级缓存后，注意不要有其他的应用或SessionFactory来更改当前数据库中的数据，这样缓存的数据就会与数据库中的实际数据不一致。

18、Spring的依赖注入是什么意思?给一个 Bean 的 message属性,字符串类型,注入值为"Hello"的 XML配置文件该怎么写?

19、Jdo是什么?

JDO是Java对象持久化的新的规范，为java data object的简称,也是一个用于存取某种数据仓库中的对象的标准化API。JDO提供了透明的对象存储，因此对开发人员来说，存储数据对象完全不需要额外的代码（如JDBC API的使用）。这些繁琐的例行工作已经转移到JDO产品提供商身上，使开发人员解脱出来，从而集中时间和精力在业务逻辑上。另外，JDO很灵活，因为它可以在任何数据底层上运行。JDBC只是面向关系数据库（RDBMS）JDO更通用，提供到任何数据底层的存储功能，比如关系数据库、文件、XML以及对象数据库（ODBMS）等等，使得应用可移植性更强。

20、什么是spring的IOCAOP

21、STRUTS的工作流程！

22、spring与EJB的区别！！

八.软件工程与设计模式

1、UML方面

标准建模语言UML。用例图,静态图(包括类图、对象图和包图),行为图,交互图(顺序图,合作图),实现图。

2、j2ee常用的设计模式？说明工厂模式。

总共23种，分为三大类：创建型，结构型，行为型

我只记得其中常用的6、7种，分别是：

创建型（工厂、工厂方法、抽象工厂、单例）

结构型（包装、适配器，组合，代理）

行为（观察者，模版，策略）

然后再针对你熟悉的模式谈谈你的理解即可。

Java中的23种设计模式：

Factory（工厂模式），Builder（建造模式），Factory Method（工厂方法模式），

Prototype（原始模型模式），Singleton（单例模式），Facade（门面模式），

Adapter（适配器模式），Bridge（桥梁模式），Composite（合成模式），

Decorator（装饰模式），Flyweight（享元模式），Proxy（代理模式），

Command（命令模式），Interpreter（解释器模式）， Visitor（访问者模式），

Iterator（迭代子模式），Mediator（调停者模式），Memento（备忘录模式），

Observer（观察者模式），State（状态模式），Strategy（策略模式），

Template Method（模板方法模式）， Chain Of Responsibleity（责任链模式）

工厂模式：工厂模式是一种经常被使用到的模式，根据工厂模式实现的类可以根据提供的数据生成一组类中某一个类的实例，通常这一组类有一个公共的抽象父类并且实现了相同的方法，但是这些方法针对不同的数据进行了不同的操作。首先需要定义一个基类，该类的子类通过不同的方法实现了基类中的方法。然后需要定义一个工厂类，工厂类可以根据条件生成不同的子类实例。当得到子类的实例后，开发人员可以调用基类中的方法而不必考虑到底返回的是哪一个子类的实例。

3、开发中都用到了那些设计模式?用在什么场合?

每个模式都描述了一个在我们的环境中不断出现的问题，然后描述了该问题的解决方案的核心。通过这种方式，你可以无数次地使用那些已有的解决方案，无需在重复相同的工作。主要用到了MVC的设计模式。用来开发JSP/Servlet或者J2EE的相关应用。简单工厂模式等。

九. j2ee部分

1、BS与CS的联系与区别。

C/S是Client/Server的缩写。服务器通常采用高性能的PC、工作站或小型机，并采用大型数据库系统，如Oracle、Sybase、InFORMix或 SQL Server。客户端需要安装专用的客户端软件。

B/Ｓ是Brower/Server的缩写，客户机上只要安装一个浏览器（Browser），如Netscape Navigator或Internet Explorer，服务器安装Oracle、Sybase、InFORMix或 SQL Server等数据库。在这种结构下，用户界面完全通过WWW浏览器实现，一部分事务逻辑在前端实现，但是主要事务逻辑在服务器端实现。浏览器通过Ｗeb Server同数据库进行数据交互。

C/S 与 B/S区别：

１．硬件环境不同:

C/S 一般建立在专用的网络上,小范围里的网络环境,局域网之间再通过专门服务器提供连接和数据交换服务.

B/S 建立在广域网之上的,不必是专门的网络硬件环境,例与电话上网,租用设备.信息自己管理.有比C/S更强的适应范围,一般只要有操作系统和浏览器就行

２．对安全要求不同

C/S 一般面向相对固定的用户群,对信息安全的控制能力很强.一般高度机密的信息系统采用C/S结构适宜.可以通过B/S发布部分可公开信息.

B/S 建立在广域网之上,对安全的控制能力相对弱,可能面向不可知的用户。

３．对程序架构不同

C/S 程序可以更加注重流程,可以对权限多层次校验,对系统运行速度可以较少考虑.

B/S 对安全以及访问速度的多重的考虑,建立在需要更加优化的基础之上.比C/S有更高的要求 B/S结构的程序架构是发展的趋势,从MS的.Net系列的BizTalk 2000Exchange 2000等,全面支持网络的构件搭建的系统. SUN和IBM推的JavaBean构件技术等,使 B/S更加成熟.

４．软件重用不同

C/S 程序可以不可避免的整体性考虑,构件的重用性不如在B/S要求下的构件的重用性好.

B/S 对的多重结构,要求构件相对独立的功能.能够相对较好的重用.就入买来的餐桌可以再利用,而不是做在墙上的石头桌子

５．系统维护不同

C/S 程序由于整体性,必须整体考察,处理出现的问题以及系统升级.升级难.可能是再做一个全新的系统

B/S 构件组成,方面构件个别的更换,实现系统的无缝升级.系统维护开销减到最小.用户从网上自己下载安装就可以实现升级.

６．处理问题不同

C/S 程序可以处理用户面固定,并且在相同区域,安全要求高需求,与操作系统相关.应该都是相同的系统

B/S 建立在广域网上,面向不同的用户群,分散地域,这是C/S无法作到的.与操作系统平台关系最小.

７．用户接口不同

C/S 多是建立的Window平台上,表现方法有限,对程序员普遍要求较高

B/S 建立在浏览器上,有更加丰富和生动的表现方式与用户交流.并且大部分难度减低,减低开发成本.

８．信息流不同

C/S 程序一般是典型的中央集权的机械式处理,交互性相对低

B/S 信息流向可变化, B-B B-C B-G等信息、流向的变化,更像交易中心。

2、应用服务器与WEB SERVER的区别？

应用服务器：Weblogic、Tomcat、Jboss

WEB SERVER：IIS、 Apache

3、应用服务器有那些？

BEA WebLogic Server，IBM WebSphere Application Server，Oracle9i ApplicationServer，jBoss，Tomcat

4、J2EE是什么？

答:Je22是Sun公司提出的多层(multi-diered),分布式(distributed),基于组件(component-base)的企业级应用模型(enterpriese applicationmodel).在这样的一个应用系统中，可按照功能划分为不同的组件，这些组件又可在不同计算机上，并且处于相应的层次(tier)中。所属层次包括客户层(clietn tier)组件,web层和组件,Business层和组件,企业信息系统(EIS)层。

一个另类的回答：j2ee就是增删改查。

5、J2EE是技术还是平台还是框架？什么是J2EE

J2EE本身是一个标准，一个为企业分布式应用的开发提供的标准平台。

J2EE也是一个框架，包括JDBC、JNDI、RMI、JMS、EJB、JTA等技术。

6、请对以下在J2EE中常用的名词进行解释(或简单描述)

web容器：给处于其中的应用程序组件（JSP，SERVLET）提供一个环境，使JSP,SERVLET直接更容器中的环境变量接口交互，不必关注其它系统问题。主要有WEB服务器来实现。例如：TOMCAT,WEBLOGIC,WEBSPHERE等。该容器提供的接口严格遵守J2EE规范中的WEB APPLICATION 标准。我们把遵守以上标准的WEB服务器就叫做J2EE中的WEB容器。

EJB容器：Enterprise java bean容器。更具有行业领域特色。他提供给运行在其中的组件EJB各种管理功能。只要满足J2EE规范的EJB放入该容器，马上就会被容器进行高效率的管理。并且可以通过现成的接口来获得系统级别的服务。例如邮件服务、事务管理。

JNDI：（Java Naming & Directory Interface）JAVA命名目录服务。主要提供的功能是：提供一个目录系统，让其它各地的应用程序在其上面留下自己的索引，从而满足快速查找和定位分布式应用程序的功能。

JMS：（Java Message Service）JAVA消息服务。主要实现各个应用程序之间的通讯。包括点对点和广播。

JTA：（Java Transaction API）JAVA事务服务。提供各种分布式事务服务。应用程序只需调用其提供的接口即可。

JAF：（Java Action FrameWork）JAVA安全认证框架。提供一些安全控制方面的框架。让开发者通过各种部署和自定义实现自己的个性安全控制策略。

RMI/IIOP:（Remote Method Invocation /internet对象请求中介协议）他们主要用于通过远程调用服务。例如，远程有一台计算机上运行一个程序，它提供股票分析服务，我们可以在本地计算机上实现对其直接调用。当然这是要通过一定的规范才能在异构的系统之间进行通信。RMI是JAVA特有的。

7、如何给weblogic指定大小的内存?

（这个问题不作具体回答，列出来只是告诉读者可能会遇到什么问题，你不需要面面俱到，什么都精通。）

在启动Weblogic的脚本中（位于所在Domian对应服务器目录下的startServerName），增加set MEM_ARGS=-Xms32m-Xmx200m，可以调整最小内存为32M，最大200M

8、如何设定的weblogic的热启动模式(开发模式)与产品发布模式?

可以在管理控制台中修改对应服务器的启动模式为开发或产品模式之一。或者修改服务的启动文件或者commenv文件，增加setPRODUCTION_MODE=true。

9、如何启动时不需输入用户名与密码?

修改服务启动文件，增加 WLS_USER和WLS_PW项。也可以在boot.properties文件中增加加密过的用户名和密码.

10、在weblogic管理制台中对一个应用域(或者说是一个网站,Domain)进行jms及ejb或连接池等相关信息进行配置后,实际保存在什么文件中?

保存在此Domain的config.xml文件中，它是服务器的核心配置文件。

11、说说weblogic中一个Domain的缺省目录结构?比如要将一个简单的helloWorld.jsp放入何目录下,然的在浏览器上就可打入http://主机:端口号//helloword.jsp就可以看到运行结果了?又比如这其中用到了一个自己写的javaBean该如何办?

Domain目录服务器目录applications，将应用目录放在此目录下将可以作为应用访问，如果是Web应用，应用目录需要满足Web应用目录要求，jsp文件可以直接放在应用目录中，Javabean需要放在应用目录的WEB-INF目录的classes目录中，设置服务器的缺省应用将可以实现在浏览器上无需输入应用名。

12、在weblogic中发布ejb需涉及到哪些配置文件

不同类型的EJB涉及的配置文件不同，都涉及到的配置文件包括ejb-jar.xml,weblogic-ejb-jar.xmlCMP实体Bean一般还需要weblogic-cmp-rdbms-jar.xml

13、如何在weblogic中进行ssl配置与客户端的认证配置或说说j2ee(标准)进行ssl的配置?

缺省安装中使用DemoIdentity.jks和DemoTrust.jksKeyStore实现SSL，需要配置服务器使用Enable SSL，配置其端口，在产品模式下需要从CA获取私有密钥和数字证书，创建identity和trust keystore，装载获得的密钥和数字证书。可以配置此SSL连接是单向还是双向的。

14、如何查看在weblogic中已经发布的EJB?

可以使用管理控制台，在它的Deployment中可以查看所有已发布的EJB

十. EBJ部分

1、EJB是基于哪些技术实现的？并说出SessionBean和EntityBean的区别，StatefulBean和StatelessBean的区别。

EJB包括Session Bean、Entity Bean、Message Driven Bean，基于JNDI、RMI、JAT等技术实现。

SessionBean在J2EE应用程序中被用来完成一些服务器端的业务操作，例如访问数据库、调用其他EJB组件。EntityBean被用来代表应用系统中用到的数据。

对于客户机，SessionBean是一种非持久性对象，它实现某些在服务器上运行的业务逻辑。

对于客户机，EntityBean是一种持久性对象，它代表一个存储在持久性存储器中的实体的对象视图，或是一个由现有企业应用程序实现的实体。

Session Bean 还可以再细分为 Stateful Session Bean与 Stateless SessionBean，这两种的 Session Bean都可以将系统逻辑放在 method之中执行，不同的是 Stateful SessionBean可以记录呼叫者的状态，因此通常来说，一个使用者会有一个相对应的 Stateful SessionBean的实体。Stateless SessionBean虽然也是逻辑组件，但是他却不负责记录使用者状态，也就是说当使用者呼叫 Stateless SessionBean的时候，EJB Container并不会找寻特定的 Stateless SessionBean的实体来执行这个 method。换言之，很可能数个使用者在执行某个 Stateless SessionBean的 methods时，会是同一个 Bean的 Instance在执行。从内存方面来看， Stateful SessionBean与Stateless SessionBean比较， Stateful SessionBean会消耗 J2EE Server较多的内存，然而 Stateful SessionBean的优势却在于他可以维持使用者的状态。

2、简要讲一下 EJB的 7个 Transaction Level?

3、EJB与JAVA BEAN的区别？

Java Bean 是可复用的组件，对Java Bean并没有严格的规范，理论上讲，任何一个Java类都可以是一个Bean。但通常情况下，由于Java Bean是被容器所创建（如Tomcat）的，所以Java Bean应具有一个无参的构造器，另外，通常Java Bean还要实现Serializable接口用于实现Bean的持久性。Java Bean实际上相当于微软COM模型中的本地进程内COM组件，它是不能被跨进程访问的。Enterprise Java Bean相当于DCOM，即分布式组件。它是基于Java的远程方法调用（RMI）技术的，所以EJB可以被远程访问（跨进程、跨计算机）。但EJB必须被布署在诸如Webspere、WebLogic这样的容器中，EJB客户从不直接访问真正的EJB组件，而是通过其容器访问。EJB容器是EJB组件的代理，EJB组件由容器所创建和管理。客户通过容器来访问真正的EJB组件。

4、EJB包括（SessionBean,EntityBean）说出他们的生命周期，及如何管理事务的？

SessionBean：Stateless Session Bean的生命周期是由容器决定的，当客户机发出请求要建立一个Bean的实例时，EJB容器不一定要创建一个新的Bean的实例供客户机调用，而是随便找一个现有的实例提供给客户机。当客户机第一次调用一个Stateful SessionBean 时，容器必须立即在服务器中创建一个新的Bean实例，并关联到客户机上，以后此客户机调用Stateful SessionBean的方法时容器会把调用分派到与此客户机相关联的Bean实例。

EntityBean：Entity Beans能存活相对较长的时间，并且状态是持续的。只要数据库中的数据存在，Entity beans就一直存活。而不是按照应用程序或者服务进程来说的。即使EJB容器崩溃了，Entity beans也是存活的。Entity Beans生命周期能够被容器或者 Beans自己管理。

EJB通过以下技术管理实务：对象管理组织（OMG）的对象实务服务（OTS），Sun Microsystems的Transaction Service（JTS）、Java Transaction API（JTA），开发组（X/Open）的XA接口。

5、EJB容器提供的服务

主要提供声明周期管理、代码产生、持续性管理、安全、事务管理、锁和并发行管理等服务。

6、EJB的激活机制

以Stateful Session Bean为例：其Cache大小决定了内存中可以同时存在的Bean实例的数量，根据MRU或NRU算法，实例在激活和去激活状态之间迁移，激活机制是当客户端调用某个EJB实例业务方法时，如果对应EJB Object发现自己没有绑定对应的Bean实例则从其去激活Bean存储中（通过序列化机制存储实例）回复（激活）此实例。状态变迁前会调用对应的ejbActive和ejbPassivate方法。

7、EJB的几种类型

会话（Session）Bean，实体（Entity）Bean消息驱动的（Message Driven）Bean

会话Bean又可分为有状态（Stateful）和无状态（Stateless）两种

实体Bean可分为Bean管理的持续性（BMP）和容器管理的持续性（CMP）两种

8、客服端调用EJB对象的几个基本步骤

设置JNDI服务工厂以及JNDI服务地址系统属性，查找Home接口，从Home接口调用Create方法创建Remote接口，通过Remote接口调用其业务方法。

十一. webservice部分

1、WEB SERVICE名词解释。JSWDL开发包的介绍。JAXP、JAXM的解释。SOAP、UDDI,WSDL解释。

Web ServiceWeb Service是基于网络的、分布式的模块化组件，它执行特定的任务，遵守具体的技术规范，这些规范使得Web Service能与其他兼容的组件进行互操作。

JAXP(Java API for XML Parsing) 定义了在Java中使用DOM, SAX, XSLT的通用的接口。这样在你的程序中你只要使用这些通用的接口，当你需要改变具体的实现时候也不需要修改代码。

JAXM(Java API for XML Messaging) 是为SOAP通信提供访问方法和传输机制的API。

WSDL是一种 XML格式，用于将网络服务描述为一组端点，这些端点对包含面向文档信息或面向过程信息的消息进行操作。这种格式首先对操作和消息进行抽象描述，然后将其绑定到具体的网络协议和消息格式上以定义端点。相关的具体端点即组合成为抽象端点（服务）。

SOAP即简单对象访问协议(Simple Object Access Protocol)，它是用于交换XML编码信息的轻量级协议。

UDDI 的目的是为电子商务建立标准；UDDI是一套基于Web的、分布式的、为Web Service提供的、信息注册中心的实现标准规范，同时也包含一组使企业能将自身提供的Web Service注册，以使别的企业能够发现的访问协议的实现标准。

2、CORBA是什么?用途是什么?

CORBA 标准是公共对象请求代理结构(Common Object Request Broker Architecture)，由对象管理组织 (Object ManagementGroup，缩写为 OMG)标准化。它的组成是接口定义语言(IDL),语言绑定(binding:也译为联编)和允许应用程序间互操作的协议。其目的为：用不同的程序设计语言书写在不同的进程中运行，为不同的操作系统开发。

3. Linux

4、LINUX下线程，GDI类的解释。

LINUX实现的就是基于核心轻量级进程的"一对一"线程模型，一个线程实体对应一个核心轻量级进程，而线程之间的管理在核外函数库中实现。

GDI类为图像设备编程接口类库。

5. 问得稀里糊涂的题

6、四种会话跟踪技术

会话作用域ServletsJSP页面描述

page否是代表与一个页面相关的对象和属性。一个页面由一个编译好的 Java servlet类（可以带有任何的include指令，但是没有 include动作）表示。这既包括 servlet又包括被编译成 servlet的 JSP页面

request是是代表与 Web客户机发出的一个请求相关的对象和属性。一个请求可能跨越多个页面，涉及多个Web组件（由于 forward指令和 include动作的关系）

session是是代表与用于某个 Web客户机的一个用户体验相关的对象和属性。一个 Web会话可以也经常会跨越多个客户机请求

application是是代表与整个 Web应用程序相关的对象和属性。这实质上是跨越整个 Web应用程序，包括多个页面、请求和会话的一个全局作用域

7、简述逻辑操作(&,|,^)与条件操作(&&,||)的区别。

区别主要答两点：a.条件操作只能操作布尔型的,而逻辑操作不仅可以操作布尔型,而且可以操作数值型

b.逻辑操作不会产生短路

十二.其他

1、请用英文简单介绍一下自己.

4、WEB SERVICE名词解释。JSWDL开发包的介绍。JAXP、JAXM的解释。SOAP、UDDI,WSDL解释。

2、请把http://tomcat.apache.org/首页的这一段话用中文翻译一下?

Apache Tomcat is the servlet container that is used in the officialReference Implementation for theJava ServletandJavaServerPagestechnologies. The Java Servlet and JavaServer Pagesspecifications are developed by Sun under theJavaCommunity Process.

Apache Tomcat is developed in an open andparticipatory environment and released under theApacheSoftware License. Apache Tomcat is intended to be a collaboration ofthe best-of-breed developers from around the world. We invite you toparticipate in this open development project. To learn more about gettinginvolved,click here.

ApacheTomcat powers numerous large-scale, mission-critical web applications across adiverse range of industries and organizations. Some of these users and theirstories are listed on thePoweredBywiki page.

3、美资软件公司JAVA工程师电话面试题目

1. Talk about overriding, overloading.

2. Talk about JAVA design patterns you known.

3. Talk about the difference between LinkList, ArrayList and Victor.

4. Talk about the difference between an Abstract class and an Interface.

5. Class a = new Class(); Class b = new Class();

if(a == b) returns true or false, why?

6. Why we use StringBuffer when concatenating strings?

7. Try to explain Singleton to us? Is it thread safe? If no, how to make itthread safe?

8. Try to explain Ioc?

9. How to set many-to-many relationship in Hibernate?

10. Talk about the difference between INNER JOIN and LFET JOIN.

11. Why we use index in database? How many indexes is the maximum in one tableas your suggestion?

12. When ‘Final’ is used in class, method and property, what dose it mean?

13. Do you have any experience on XML? Talk about any XML tool youused ,e.g. JAXB, JAXG.

14. Do you have any experience on Linux?

15. In OOD what is the reason when you create a Sequence diagram?

Administrator 10:34:20

1，堆和栈的区别，有一个64k的字符串，是放到堆上，还是放到栈上，为什么？

2，什么时候用到接口，什么时候用到抽象类，二者区别

3，有一个100万的数组，里边有两个市重复的，如何设计算法找到。

4，设计数据库时，n维，如何设计。

例如[省份][城市][网吧]，这是三维关系，它的表也应该有三个，网吧有外键引用城市，城市有外键应用省份，这个规律就是下层的要有一外键去引用上层。

