# raywenderlich.com Objective-C编码规范

这篇编码风格指南概括了raywenderlich.com的编码规范，可能有些删减或修改。

## 介绍

我们制定Objective-C编码规范的原因是我们能够在我们的书，教程和初学者工具包的代码保持优雅和一致。即使我们有很多不同的作者来完成不同的书籍。


这里编码规范有可能与你看到的其他Objective-C编码规范不同，因为它主要是为了打印和web的易读性。

## 关于作者

这编码规范的创建是由很多来自raywenderlich.com团队成员在Nicholas Waynik的带领下共同完成的。团队成员有：[Soheil Moayedi Azarpour](https://github.com/moayes), [Ricardo Rendon Cepeda](https://github.com/ricardo-rendoncepeda), [Tony Dahbura](https://github.com/tdahbura), [Colin Eberhardt](https://github.com/ColinEberhardt), [Matt Galloway](https://github.com/mattjgalloway), [Greg Heo](https://github.com/gregheo), [Matthijs Hollemans](https://github.com/hollance), [Christopher LaPollo](https://github.com/elephantronic), [Saul Mora](https://github.com/casademora), [Andy Pereira](https://github.com/macandyp), [Mic Pringle](https://github.com/micpringle), [Pietro Rea](https://github.com/pietrorea), [Cesare Rocchi](https://github.com/funkyboy), [Marin Todorov](https://github.com/icanzilb), [Nicholas Waynik](https://github.com/ndubbs)和[Ray Wenderlich](https://github.com/raywenderlich)

我们也非常感谢[New York Times](https://github.com/NYTimes/objective-c-style-guide) 和[Robots & Pencils'](https://github.com/RobotsAndPencils/objective-c-style-guide)Objective-C编码规范的作者。这两个编码规范为本指南的创建提供很好的起点。

## 背景

这里有些关于编码风格Apple官方文档，如果有些东西没有提及，可以在以下文档来查找更多细节：

* [The Objective-C Programming Language](http://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/ObjectiveC/Introduction/introObjectiveC.html)
* [Cocoa Fundamentals Guide](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CocoaFundamentals/Introduction/Introduction.html)
* [Coding Guidelines for Cocoa](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html)
* [iOS App Programming Guide](http://developer.apple.com/library/ios/#documentation/iphone/conceptual/iphoneosprogrammingguide/Introduction/Introduction.html)

## 目录

* [语言](#language)
* [代码组织](#code-organization)
* [空格](#spacing)
* [注释](#comments)
* [命名](#naming)
  * [下划线](#underscores)
* [方法](#methods)
* [变量](#variables)
* [属性特性](#property-attributes)
* [点符号语法](#dot-notation-syntax)
* [字面值](#literals)
* [常量](#constants)
* [枚举类型](#enumerated-types)
* [Case语句](#case-statements)
* [私有属性](#private-properties)
* [布尔值](#booleans)
* [条件语句](#conditionals)
  * [三元操作符](#ternary-operator)
* [Init方法](#init-methods)
* [类构造方法](#class-constructor-methods)
* [CGRect函数](#cgrect-functions)
* [黄金路径](#golden-path)
* [错误处理](#error-handling)
* [单例模式](#singletons)
* [换行符](#line-breaks)
* [Xcode工程](#xcode-project)

<b id="language"></b>
## 语言

应该使用US英语.

**应该:**

```objc
UIColor *myColor = [UIColor whiteColor];
```

**不应该:**

```objc
UIColor *myColour = [UIColor whiteColor];
```

<b id="code-organization"></b>
## 代码组织

在函数分组和protocol/delegate实现中使用`#pragma mark -`来分类方法，要遵循以下一般结构：

```objc
#pragma mark - Lifecycle

- (instancetype)init {}
- (void)dealloc {}
- (void)viewDidLoad {}
- (void)viewWillAppear:(BOOL)animated {}
- (void)didReceiveMemoryWarning {}

#pragma mark - Custom Accessors

- (void)setCustomProperty:(id)value {}
- (id)customProperty {}

#pragma mark - IBActions

- (IBAction)submitData:(id)sender {}

#pragma mark - Public

- (void)publicMethod {}

#pragma mark - Private

- (void)privateMethod {}

#pragma mark - Protocol conformance
#pragma mark - UITextFieldDelegate
#pragma mark - UITableViewDataSource
#pragma mark - UITableViewDelegate

#pragma mark - NSCopying

- (id)copyWithZone:(NSZone *)zone {}

#pragma mark - NSObject

- (NSString *)description {}
```

<b id="spacing"></b>
## 空格

* 缩进使用**4**个空格，确保在Xcode偏好设置来设置。(raywenderlich.com使用**2**个空格)
* 方法大括号和其他大括号(`if`/`else`/`switch`/`while` 等.)总是在同一行语句打开但在新行中关闭。

**应该:**

```objc
if (user.isHappy) {
    //Do something
} else {
    //Do something else
}
```

**不应该:**

```objc
if (user.isHappy)
{
  //Do something
}
else {
  //Do something else
}
```

* 在方法之间应该有且只有一行，这样有利于在视觉上更清晰和更易于组织。在方法内的空白应该分离功能，但通常都抽离出来成为一个新方法。
* 优先使用auto-synthesis。但如果有必要，`@synthesize` 和 `@dynamic`应该在实现中每个都声明新的一行。
* 应该避免以冒号对齐的方式来调用方法。因为有时方法签名可能有3个以上的冒号和冒号对齐会使代码更加易读。请**不要**这样做，尽管冒号对齐的方法包含代码块，因为Xcode的对齐方式令它难以辨认。

**应该:**

```objc
// blocks are easily readable
[UIView animateWithDuration:1.0 animations:^{
  // something
} completion:^(BOOL finished) {
  // something
}];
```

**不应该:**

```objc
// colon-aligning makes the block indentation hard to read
[UIView animateWithDuration:1.0
                 animations:^{
                     // something
                 }
                 completion:^(BOOL finished) {
                     // something
                 }];
```

<b id="comments"></b>
## 注释

当需要注释时，注释应该用来解释这段特殊代码**为什么**要这样做。任何被使用的注释都必须保持最新或被删除。

一般都避免使用块注释，因为代码尽可能做到自解释，只有当断断续续或几行代码时才需要注释。*例外：这不应用在生成文档的注释*

<b id="naming"></b>
## 命名

Apple命名规则尽可能坚持，特别是与这些相关的[memory management rules](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/MemoryMgmt/Articles/MemoryMgmt.html) ([NARC](http://stackoverflow.com/a/2865194/340508))。

长的，描述性的方法和变量命名是好的。

**应该:**

```objc
UIButton *settingsButton;
```

**不应该:**

```objc
UIButton *setBut;
```

三个字符前缀应该经常用在类和常量命名，但在Core Data的实体名中应被忽略。对于官方的raywenderlich.com书、初学者工具包或教程，前缀'RWT'应该被使用。

常量应该使用驼峰式命名规则，所有的单词首字母大写和加上与类名有关的前缀。

**应该:**

```objc
static NSTimeInterval const RWTTutorialViewControllerNavigationFadeAnimationDuration = 0.3;
```

**不应该:**

```objc
static NSTimeInterval const fadetime = 1.7;
```

属性也是使用驼峰式，但首单词的首字母小写。对属性使用auto-synthesis，而不是手动编写@ synthesize语句，除非你有一个好的理由。

**应该:**

```objc
@property (strong, nonatomic) NSString *descriptiveVariableName;
```

**不应该:**

```objc
id varnm;
```
<b id="underscores"></b>
### 下划线

当使用属性时，实例变量应该使用`self.`来访问和改变。这就意味着所有属性将会视觉效果不同，因为它们前面都有`self.`。

但有一个特例：在初始化方法里，实例变量(例如，_variableName)应该直接被使用来避免getters/setters潜在的副作用。

局部变量不应该包含下划线。

<b id="methods"></b>
## 方法

在方法签名中，应该在方法类型(-/+ 符号)之后有一个空格。在方法各个段之间应该也有一个空格(符合Apple的风格)。在参数之前应该包含一个具有描述性的关键字来描述参数。

"and"这个词的用法应该保留。它不应该用于多个参数来说明，就像`initWithWidth:height`以下这个例子：

**应该:**
```objc
- (void)setExampleText:(NSString *)text image:(UIImage *)image;
- (void)sendAction:(SEL)aSelector to:(id)anObject forAllCells:(BOOL)flag;
- (id)viewWithTag:(NSInteger)tag;
- (instancetype)initWithWidth:(CGFloat)width height:(CGFloat)height;
```

**不应该:**

```objc
-(void)setT:(NSString *)text i:(UIImage *)image;
- (void)sendAction:(SEL)aSelector :(id)anObject :(BOOL)flag;
- (id)taggedView:(NSInteger)tag;
- (instancetype)initWithWidth:(CGFloat)width andHeight:(CGFloat)height;
- (instancetype)initWith:(int)width and:(int)height;  // Never do this.
```
<b id="variables"></b>
## 变量

变量尽量以描述性的方式来命名。单个字符的变量命名应该尽量避免，除了在`for()`循环。

星号表示变量是指针。例如， `NSString *text` 既不是 `NSString* text` 也不是 `NSString * text`，除了一些特殊情况下常量。

[私有变量](#private-properties) 应该尽可能代替实例变量的使用。尽管使用实例变量是一种有效的方式，但更偏向于使用属性来保持代码一致性。

通过使用'back'属性(_variable，变量名前面有下划线)直接访问实例变量应该尽量避免，除了在初始化方法(`init`, `initWithCoder:`, 等…)，`dealloc` 方法和自定义的setters和getters。想了解关于如何在初始化方法和dealloc直接使用Accessor方法的更多信息，查看[这里](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/MemoryMgmt/Articles/mmPractical.html#//apple_ref/doc/uid/TP40004447-SW6)

**应该:**

```objc
@interface RWTTutorial : NSObject

@property (strong, nonatomic) NSString *tutorialName;

@end
```

**不应该:**

```objc
@interface RWTTutorial : NSObject {
  NSString *tutorialName;
}
```

<b id="property-attributes"></b>
## 属性特性

所有属性特性应该显式地列出来，有助于新手阅读代码。属性特性的顺序应该是storage、atomicity，与在Interface Builder连接UI元素时自动生成代码一致。

**应该:**

```objc
@property (weak, nonatomic) IBOutlet UIView *containerView;
@property (strong, nonatomic) NSString *tutorialName;
```

**不应该:**

```objc
@property (nonatomic, weak) IBOutlet UIView *containerView;
@property (nonatomic) NSString *tutorialName;
```

NSString应该使用`copy` 而不是 `strong`的属性特性。

为什么？即使你声明一个`NSString`的属性，有人可能传入一个`NSMutableString`的实例，然后在你没有注意的情况下修改它。 

**应该:**

```objc
@property (copy, nonatomic) NSString *tutorialName;
```

**不应该:**

```objc
@property (strong, nonatomic) NSString *tutorialName;
```不

<b id="dot-notation-syntax"></b>
## 点符号语法

点语法是一种很方便封装访问方法调用的方式。当你使用点语法时，通过使用getter或setter方法，属性仍然被访问或修改。想了解更多，阅读[这里](https://developer.apple.com/library/ios/documentation/cocoa/conceptual/ProgrammingWithObjectiveC/EncapsulatingData/EncapsulatingData.html)

点语法应该**总是**被用来访问和修改属性，因为它使代码更加简洁。[]符号更偏向于用在其他例子。



**应该:**
```objc
NSInteger arrayCount = [self.array count];
view.backgroundColor = [UIColor orangeColor];
[UIApplication sharedApplication].delegate;
```

**不应该:**
```objc
NSInteger arrayCount = self.array.count;
[view setBackgroundColor:[UIColor orangeColor]];
UIApplication.sharedApplication.delegate;
```

<b id="literals"></b>
## 字面值

`NSString`, `NSDictionary`, `NSArray`, 和 `NSNumber`的字面值应该在创建这些类的不可变实例时被使用。请特别注意`nil`值不能传入`NSArray`和`NSDictionary`字面值，因为这样会导致crash。

**应该:**

```objc
NSArray *names = @[@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul"];
NSDictionary *productManagers = @{@"iPhone": @"Kate", @"iPad": @"Kamal", @"Mobile Web": @"Bill"};
NSNumber *shouldUseLiterals = @YES;
NSNumber *buildingStreetNumber = @10018;
```

**不应该:**

```objc
NSArray *names = [NSArray arrayWithObjects:@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul", nil];
NSDictionary *productManagers = [NSDictionary dictionaryWithObjectsAndKeys: @"Kate", @"iPhone", @"Kamal", @"iPad", @"Bill", @"Mobile Web", nil];
NSNumber *shouldUseLiterals = [NSNumber numberWithBool:YES];
NSNumber *buildingStreetNumber = [NSNumber numberWithInteger:10018];
```
<b id="constants"></b>
## 常量

常量是容易重复被使用和无需通过查找和代替就能快速修改值。常量应该使用`static`来声明而不是使用`#define`，除非显式地使用宏。

**应该:**

```objc
static NSString * const RWTAboutViewControllerCompanyName = @"RayWenderlich.com";

static CGFloat const RWTImageThumbnailHeight = 50.0;
```

**不应该:**

```objc
#define CompanyName @"RayWenderlich.com"

#define thumbnailHeight 2
```
<b id="enumerated-types"></b>
## 枚举类型

当使用`enum`时，推荐使用新的固定基本类型规格，因为它有更强的类型检查和代码补全。现在SDK有一个宏`NS_ENUM()`来帮助和鼓励你使用固定的基本类型。

**例如:**

```objc
typedef NS_ENUM(NSInteger, RWTLeftMenuTopItemType) {
  RWTLeftMenuTopItemMain,
  RWTLeftMenuTopItemShows,
  RWTLeftMenuTopItemSchedule
};
```

你也可以显式地赋值(展示旧的k-style常量定义)：

```objc
typedef NS_ENUM(NSInteger, RWTGlobalConstants) {
  RWTPinSizeMin = 1,
  RWTPinSizeMax = 5,
  RWTPinCountMin = 100,
  RWTPinCountMax = 500,
};
```

旧的k-style常量定义应该**避免**除非编写Core Foundation C的代码。

**不应该:**

```objc
enum GlobalConstants {
  kMaxPinSize = 5,
  kMaxPinCount = 500,
};
```

<b id="case-statements"></b>
## Case语句

大括号在case语句中并不是必须的，除非编译器强制要求。当一个case语句包含多行代码时，大括号应该加上。

```objc
switch (condition) {
  case 1:
    // ...
    break;
  case 2: {
    // ...
    // Multi-line example using braces
    break;
  }
  case 3:
    // ...
    break;
  default: 
    // ...
    break;
}

```
有很多次，当相同代码被多个cases使用时，一个fall-through应该被使用。一个fall-through就是在case最后移除'break'语句，这样就能够允许执行流程跳转到下一个case值。为了代码更加清晰，一个fall-through需要注释一下。


```objc
switch (condition) {
  case 1:
    // ** fall-through! **
  case 2:
    // code executed for values 1 and 2
    break;
  default: 
    // ...
    break;
}

```

当在switch使用枚举类型时，'default'是不需要的。例如：

```objc
RWTLeftMenuTopItemType menuType = RWTLeftMenuTopItemMain;

switch (menuType) {
  case RWTLeftMenuTopItemMain:
    // ...
    break;
  case RWTLeftMenuTopItemShows:
    // ...
    break;
  case RWTLeftMenuTopItemSchedule:
    // ...
    break;
}
```

<b id="private-properties"></b>
## 私有属性

私有属性应该在类的实现文件中的类扩展(匿名分类)中声明，命名分类(比如`RWTPrivate `或`private`)应该从不使用除非是扩展其他类。匿名分类应该通过使用<headerfile>+Private.h文件的命名规则暴露给测试。

**例如:**

```objc
@interface RWTDetailViewController ()

@property (strong, nonatomic) GADBannerView *googleAdView;
@property (strong, nonatomic) ADBannerView *iAdView;
@property (strong, nonatomic) UIWebView *adXWebView;

@end
```

<b id="booleans"></b>
## 布尔值

Objective-C使用`YES`和`NO`。因为`true`和`false`应该只在CoreFoundation，C或C++代码使用。既然`nil`解析成`NO`，所以没有必要在条件语句比较。不要拿某样东西直接与`YES`比较，因为`YES`被定义为1和一个`BOOL`能被设置为8位。

这是为了在不同文件保持一致性和在视觉上更加简洁而考虑。

**应该:**

```objc
if (someObject) {}
if (![anotherObject boolValue]) {}
```

**不应该:**

```objc
if (someObject == nil) {}
if ([anotherObject boolValue] == NO) {}
if (isAwesome == YES) {} // Never do this.
if (isAwesome == true) {} // Never do this.
```

如果`BOOL`属性的名字是一个形容词，属性就能忽略"is"前缀，但要指定get访问器的惯用名称。例如：

```objc
@property (assign, getter=isEditable) BOOL editable;
```

文字和例子从这里引用[Cocoa Naming Guidelines](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CodingGuidelines/Articles/NamingIvarsAndTypes.html#//apple_ref/doc/uid/20001284-BAJGIIJE)

<b id="conditionals"></b>
## 条件语句

条件语句主体为了防止出错应该使用大括号包围，即使条件语句主体能够不用大括号编写(如，只用一行代码)。这些错误包括添加第二行代码和期望它成为if语句；还有，[even more dangerous defect](http://programmers.stackexchange.com/a/16530)可能发生在if语句里面一行代码被注释了，然后下一行代码不知不觉地成为if语句的一部分。除此之外，这种风格与其他条件语句的风格保持一致，所以更加容易阅读。

**应该:**

```objc
if (!error) {
  return success;
}
```

**不应该:**

```objc
if (!error)
  return success;
```

或

```objc
if (!error) return success;
```

<b id="ternary-operator"></b>
### 三元操作符

当需要提高代码的清晰性和简洁性时，三元操作符`?:`才会使用。单个条件求值常常需要它。多个条件求值时，如果使用`if`语句或重构成实例变量时，代码会更加易读。一般来说，最好使用三元操作符是在根据条件来赋值的情况下。

Non-boolean的变量与某东西比较，加上括号()会提高可读性。如果被比较的变量是boolean类型，那么就不需要括号。

**应该:**

```objc
NSInteger value = 5;
result = (value != 0) ? x : y;

BOOL isHorizontal = YES;
result = isHorizontal ? x : y;
```

**不应该:**

```objc
result = a > b ? x = c > d ? c : d : y;
```

<b id="init-methods"></b>
## Init方法

Init方法应该遵循Apple生成代码模板的命名规则。返回类型应该使用`instancetype`而不是`id`

```objc
- (instancetype)init {
  self = [super init];
  if (self) {
    // ...
  }
  return self;
}
```

查看关于instancetype的文章[Class Constructor Methods](#class-constructor-methods)

<b id="class-constructor-methods"></b>
## 类构造方法

当类构造方法被使用时，它应该返回类型是`instancetype `而不是`id`。这样确保编译器正确地推断结果类型。


```objc
@interface Airplane
+ (instancetype)airplaneWithType:(RWTAirplaneType)type;
@end
```
关于更多instancetype信息，请查看[NSHipster.com](http://nshipster.com/instancetype/)

<b id="cgrect-functions"></b>
## CGRect函数

当访问`CGRect`里的`x`, `y`, `width`, 或 `height`时，应该使用[`CGGeometry`函数](http://developer.apple.com/library/ios/#documentation/graphicsimaging/reference/CGGeometry/Reference/reference.html)而不是直接通过结构体来访问。引用Apple的`CGGeometry `:

> 在这个参考文档中所有的函数，接受CGRect结构体作为输入，在计算它们结果时隐式地标准化这些rectangles。因此，你的应用程序应该避免直接访问和修改保存在CGRect数据结构中的数据。相反，使用这些函数来操纵rectangles和获取它们的特性。


**应该:**

```objc
CGRect frame = self.view.frame;

CGFloat x = CGRectGetMinX(frame);
CGFloat y = CGRectGetMinY(frame);
CGFloat width = CGRectGetWidth(frame);
CGFloat height = CGRectGetHeight(frame);
CGRect frame = CGRectMake(0.0, 0.0, width, height);
```

**不应该:**

```objc
CGRect frame = self.view.frame;

CGFloat x = frame.origin.x;
CGFloat y = frame.origin.y;
CGFloat width = frame.size.width;
CGFloat height = frame.size.height;
CGRect frame = (CGRect){ .origin = CGPointZero, .size = frame.size };
```

<b id="golden-path"></b>
## 黄金路径

当使用条件语句编码时，左手边的代码应该是"golden" 或 "happy"路径。也就是不要嵌套`if`语句，多个返回语句也是OK。

**应该:**

```objc
- (void)someMethod {
  if (![someOther boolValue]) {
	return;
  }

  //Do something important
}
```

**不应该:**

```objc
- (void)someMethod {
  if ([someOther boolValue]) {
    //Do something important
  }
}
```

<b id="error-handling"></b>
## 错误处理

当方法通过引用来返回一个错误参数，判断返回值而不是错误变量。

**应该:**
```objc
NSError *error;
if (![self trySomethingWithError:&error]) {
  // Handle Error
}
```

**不应该:**
```objc
NSError *error;
[self trySomethingWithError:&error];
if (error) {
  // Handle Error
}
```

在成功的情况下，有些Apple的APIs记录垃圾值(garbage values)到错误参数(如果non-NULL)，那么判断错误值会导致false负值和crash。

<b id="singletons"></b>
## 单例模式

单例对象应该使用线程安全模式来创建共享实例。

```objc
+ (instancetype)sharedInstance {
  static id sharedInstance = nil;

  static dispatch_once_t onceToken;
  dispatch_once(&onceToken, ^{
    sharedInstance = [[self alloc] init];
  });

  return sharedInstance;
}
```

这会防止[possible and sometimes prolific crashes](http://cocoasamurai.blogspot.com/2011/04/singletons-your-doing-them-wrong.html).

<b id="line-breaks"></b>
## 换行符

换行符是一个很重要的主题，因为它的风格指南主要为了打印和网上的可读性。

例如:

```objc
self.productsRequest = [[SKProductsRequest alloc] initWithProductIdentifiers:productIdentifiers];
```

一行很长的代码应该分成两行代码，下一行用两个空格隔开。

```objc
self.productsRequest = [[SKProductsRequest alloc] 
  initWithProductIdentifiers:productIdentifiers];
```

<b id="xcode-project"></b>
## Xcode工程

物理文件应该与Xcode工程文件保持同步来避免文件扩张。任何Xcode分组的创建应该在文件系统的文件体现。代码不仅是根据**类型**来分组，而且还可以根据**功能**来分组，这样代码更加清晰。

尽可能在target的Build Settings打开"Treat Warnings as Errors，和启用以下[additional warnings](http://boredzo.org/blog/archives/2009-11-07/warnings)。如果你需要忽略特殊的警告，使用 [Clang's pragma feature](http://clang.llvm.org/docs/UsersManual.html#controlling-diagnostics-via-pragmas)。


# 其他Objective-C编码规范

If ours doesn't fit your tastes, have a look at some other style guides:

* [Robots & Pencils](https://github.com/RobotsAndPencils/objective-c-style-guide)
* [New York Times](https://github.com/NYTimes/objective-c-style-guide)
* [Google](http://google-styleguide.googlecode.com/svn/trunk/objcguide.xml)
* [GitHub](https://github.com/github/objective-c-conventions)
* [Adium](https://trac.adium.im/wiki/CodingStyle)
* [Sam Soffes](https://gist.github.com/soffes/812796)
* [CocoaDevCentral](http://cocoadevcentral.com/articles/000082.php)
* [Luke Redpath](http://lukeredpath.co.uk/blog/my-objective-c-style-guide.html)
* [Marcus Zarra](http://www.cimgf.com/zds-code-style-guide/)

