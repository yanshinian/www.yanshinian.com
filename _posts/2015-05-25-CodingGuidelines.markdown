---
layout: post
title: "Cocoa编码规范【整理】"
description: "Cocoa编码规范"
date: 2015-05-25 02:15:48
category: 效率开发
---
##个人学习心得

命名的心得，那就是多向苹果多学学。学学苹果的命名的方式

* NSString 类，方法的命名。长的跟句子，但是一读便明了，还有它分类的声明与分组。有时候为了方便。把分类写到一起。当然也可以分文件处理。

* UITableViewController类，代理的命名，代理方法的命名。

* UIKit/NSAttributedString.h 类，常量的命名（`能用const就少用#define`）。

* UIButton.h 类，工厂方法创建不同的button。

* UIControl.h 类，学习下枚举的命名方式。

* UINavigationController.h 类，学习下严格的属性声明，能不让外界修改就不让外界修改。

当然出了以上的类，还有其他的类，值得我们去学习，无论是封装还是代码的整洁便于阅读都可看做一个参考标准了。下面是整理的 `Cocoa 编码规范`。

##代码命名的基本知识

###一般原则

####清晰 

```
insertObject:atIndex: // 清晰

insert:at: //不清晰；是什么被插入？at又意味着什么？

removeObjectAtIndex: // 清晰，我们知道根据索引来删除

removeObject; // 清晰，删除相关的对象

remove: // 不清晰；什么被删除？

```

通常，不要缩写一些东西的名称，尽管他们拼写起来很长。

```
destinationselection // 清晰

destsel //不清晰

setBackgroundColor:

setBkgdColor: //不清晰，
```
你可能认为一个缩写是众所周知的，但也不尽然，特别是如果开发者遇到你的方法或函数的名称有着不同的文化和语言背景

有的缩写是公用的而且有了一定的年份。你可以继续使用它们。如果方法名称给人感觉有不同的解释，要避免API命名歧义。

```
sendPort  // 是发送端口？还是返回端口？

displayNmae //是展示一个名称？还是在用户界面接受一个标题呢？
```
####一致性

不同类之间的方法做同样的事情，那么名称也应该一样。

```
- (NSInteger)tag //NSView, NSCell, NSControl中都有定义
- (void)setStringValue:(NSString *) //在Cocoa 一些类中也有定义
```
####不要自我引用

命名不应该自我参照

```
NSString // Okay

NSStringObject // NO，自我参照
```

常数（看做标记，可以进行位运算)例外，用作通知名称。

```
NSUnderlineByWordMask // Okay

NSTableViewColumnDidMoveNotification //Okay
```
###前缀

前缀是在编程接口名称的重要组成部分。能够区分不同的功能模块。通常这一软件封装在一个框架或（如是基础和应用套件的情况下）密切相关的框架。前缀避免了第三方开发者和Apple之间的命名冲突（也防止Apple本身）。

前缀有规定的格式。通常由2/3个大写字母组成。不要使用“下划线”或者“子前缀”。

```
NS	Foundation
NS	Application Kit
AB	Address Book
IB  Interface Builder
```
使用前缀来命名类、协议、函数、常数，自定义数据类型(typedef structures)，不要用前缀来命名方法。方法存在类的命名区域中，不要在这区域里面使用前缀。

###书写约定

对于多个单词组成的名字，不要使用标点符号(下划线、破折号等)作为名称部分或作为分隔符。相反每个单词第一个字母大写并且连着写（例如：`runTheWordsTogether`）--驼峰命名。注意一下几点：

 * 对于方法名字，第一个单词小写字母开头,剩下的首字母大写（小驼峰命名规则）,不要用前缀。例如：`fileExistsAtPath:isDirectory:`。一个例外是，方法名称以通用的缩写开头，例如：TIFFRepresentation (NSImage)。
 
 * 对于函数和常数，和相关类使用相同的前缀，并且大写第一个字母。例：NSRunAlertPanel、NSCellDisabled。
 
    ```
    SRunAlertPanel ,
  	NSCellDisabled
    ```

 * 避免使用下划线作为前缀意义在于会导致方法名称私有的意思（可以用它做实例变量）。Apple保留使用该规则。但在第三方用可能导致命名冲突，他们会不自觉的重写自己已有的一个私有方法。
 
###类和协议命名

一个类名应该包含一个名词，这个名词清晰的表示这个类是代表什么，是做什么的。 这个类名还应该包含一个前缀（参见“前缀”）。Foundation跟应用框架有很多这样的例子。`NSString,NSDate,NSScanner,NSApplication`等等

协议的命名应该根据使用协议的相应类行为命名 

* 大多数协议包含的相关方法，不与任何特定的类关联。这种协议的应该命名为使协议与类不能混淆。一个通常的规则是用动名词(...ing),比如：`NSCopying`、`NSCoding`等。
 	
	```
NSLocking  Good
NSLock     一看就是类名称
 	```

* 有的协议包含一些没什么联系的方法（而不是创建多个独立的小协议）。这些协议跟一个类的联系很大，这个类主要体现了这个协议。这种情况下，命名规则为协议名跟类名字一样。一个例子是NSObject 协议，这个协议包含一些方法可以查询任何类在父类中的层次位置等。因为NSObject类实现了协议的大部分方法，所以协议可以以类名命名。
 
##代理的命名
自定义的代理命名方式`名字＋delegate`就好比苹果的tableview的代理`UITableViewDelegate`。

##头文件

怎么命名你的头文件非常重要。因为你的命名表明了类中的内容：

* 声明一个独立的类/协议：如果一个类/协议不是一个文件中的一部分，将其声明独立成一个文件，这个文件的名字表明了该类/协议；

	```
	NSLocale.h  NSLocale类。	
	```

* 声明联系的类/协议：如果有一些联系的声明（类、协议、分类），将它们声明放到一个文件中，文件的命名根据基础的类、协议、分类；

	```
    NSString.h	NSString和NSSMutableString
    NSLock.h      NSLocking协议、NSLock、NSConditionLock、NSRecursive类
	```
* 包含框架的头文件:所有的框架都有一个头文件，以框架命名，包含框架里所有公开的头文件。

	```
	Foundation.h  Foundation.framwork。
	```
* 为别的框架中类增加API：如果你在一个框架中声明的方法，是另一个框架中类的分类，名字为原来类的名字拼接上“Additions”。一个例子为Applicatiion kit 的NSBuddleAdditions.h头文件。 --相联系的函数和数据类型：如果你有一些相联系的函数、常数、结构体等其他数据类型，将它们放到合适命名的头文件中。例如NSGraphics.h(Applicatiion kit )。

##方法命名

###基本规则

* 方法名采用小驼峰命名。不使用前缀。有两个情况是例外的，方法用到了众所周知的缩写(例如TIFF或PDF)，还有就是你可能定义一些私有的方法
* 如果方法代表对象的某个动作，方法用动词开头：

	```
	- (void)invokeWithTarget:(id)target;

	- (void)selectTabViewItem:(NSTabViewItem *)tabViewItem
	```
	
	不要使用`do`或`does`，它们没有什么含义，并且不要在动词之前使用副词或形容词
* 如果方法返回的是消息发送者(对象)的属性，用属性命名方法。get这个词不需要，除非有多个间接返回的值。

	```
	- (NSSize)cellSize;        正确

	- (NSSize)calcCellSize;    错误

	- (NSSize)getCellSize;	  错误
	```
* 在所有的参数前使用关键词

	```
    - (void)sendAction:(SEL)aSelector toObject:(id)anObject forAllCells:(BOOL)flag; 	正确
    - (void)sendAction:(SEL)aSelector :(id)anObject :(BOOL)flag; 	错误
	```
* 参数前的单词描述参数的意义

	```
     - (id)viewWithTag:(NSInteger)aTag; 	正确
     - (id)taggedView:(int)aTag; 	错误
	```
	
* 当你创建一个基于现有方法的新方法，在一个已有的方法上添加关键词

	```
     - (id)initWithFrame:(CGRect)frameRect; 	NSView,UIView
     - (id)initWithFrame:(NSRect)frameRect mode:(int)aMode cellClass:(Class)factoryId numberOfRows:(int)rowsHigh numberOfColumns:(int)colsWide; 	NSMatrix,NSView的一个子类
```
* 不要使用and去连接多个参数的关键词(对象属性名)

	```
    - (int)runModalForDirectory:(NSString *)path file:(NSString *) name types:(NSArray *)fileTypes; 	正确
    - (int)runModalForDirectory:(NSString *)path andFile:(NSString *)name andTypes:(NSArray *)fileTypes; 	错误
	```
尽管在这个例子中and看起来还不错，但是当方法中有许多参数的时候，再用and就不行了。 

* 如果方法包含着俩个分开的动作，用and去连接它们；

	```
	- (BOOL)openFile:(NSString *)fullPath withApplication:(NSString *)appName andDeactivate:(BOOL)flag;   NSWorkspace
	```
	
###存取器（Set，Get）方法

存取器放方法是指那些读/写对象属性的方法，根据属性意义的不同，它们有不同的通用格式。(备注：不同格式代表不同对应实例变量的写法，存取器方法形式就是intanceVariables 和 setIntanceVariables俩种形式) 

* 如果属性表示的是名词意思，格式如：
   
	\- (type)noun; 
	
	\- (void)setNoun:(type)aNoun; 
   
	```
    - (NSString *)title;
    - (void)setTitle:(NSString *)aTitle;
	```
   
* 如果属性表示的是形容词意思，格式如：
 
	\- (BOOL)isAdjective;
  
	\- (void)setAdjective:(BOOL)flag; (注意type是BOOL) 
   
	```
    - (BOOL)isEditable; 
    - (void)setEditable:(BOOL)flag;
	```
   
* 如果属性表示的是动词意思 ， 格式如：

	\- (BOOL)verbObject; 
	
	\- (void)setVerbObject:(BOOL)flag; (注意type为BOOL)
   
	```
    - (BOOL)showsAlpha; 
    - (void)setShowsAlpha:(BOOL)flag; 
	```
   动词是现在时；    
* 在属性的名称中，不要通过用分词形式将动词转换为形容词；

	```
	- (void)setAcceptsGlyphInfo:(BOOL)flag; 	正确
	- (BOOL)acceptsGlyphInfo; 	正确
	- (void)setGlyphInfoAccepted:(BOOL)flag; 	错误
	- (BOOL)glyphInfoAccepted; 	错误
	```
* 可以使用情态动词(动词前面“can”、“should”、“will”等)进一步说明属性意思，但不要使用'do'或'does'。

	```
	- (void)setCanHide:(BOOL)flag; 	正确
	- (BOOL)canHide; 	正确
	- (void)setShouldCloseDocument:(BOOL)flag; 正确
	- (BOOL)shouldCloseDocument; 	正确
	- (void)setDoesAcceptGlyphInfo:(BOOL)flag; 错误
	- (BOOL)doesAcceptGlyphInfo; 	错误
	```

* 当使用get这个词时，只有当方法间接返回多个对象/值。

	```
	- (void)getLineDash:(float *)pattern count:(int *)count phase:(float *)phase; 
	注意，这种形式的方法，其中的引用型参数应该能接收NULL，因为方法调用者可能并不需要多个返回值。
	``` 
	
###代理方法

代理方法是那些当发生特定事件对象使用它delegate调用的方法(如果delegate实现了它)，它们有着特定的格式，这些格式也适用于对象的`data source`方法。

* 名字的开头指明发消息的对象类型。

	```
	- (void)tableView:(UITableView *)tableView didSelectRowAtIndexPath:(NSIndexPath *)indexPath;
	- (BOOL)application:(UIApplication *)application handleOpenURL:(NSURL *)
	```
	类名省略了它的前缀并且小写开头。 

* 如果方法只有一个参数，格式为：冒号+类名(调用代理的对象)+sender；

	```
	- (BOOL)applicationOpenUntitledFile:(NSApplication *)sender; 
	```

* 一个例外是方法用来发送通知，如果这样的话，方法参数为通知对象；

	```
	- (void)windowDidChangeScreen:(NSNotification *)notification; 
	```

* 命名中使用did或will这类词，告诉delegate某些事情已经发生或将要发生；

	```
	- (void)tableView:(UITableView *)tableView willDisplayCell:(UITableViewCell *)cell forRowAtIndexPath:(NSIndexPath *)indexPath; 
	- (void)tableView:(UITableView *)tableView didSelectRowAtIndexPath:(NSIndexPath *)indexPath;
	```
* 虽然你可以在命名中是使用did或will这类词，告诉delegate去做某些事情，但有时“should”更合适；

	```
	- (BOOL)tableView:(UITableView *)tableView shouldIndentWhileEditingRowAtIndexPath:(NSIndexPath *)indexPath;
	```
	
###集合方法(`Array、Set、Dictionary`等)

要管理对象(每一个叫做对象的元素)的集合，命名方法以下格式：

\- (void)addObject:(id)anObject;

\- (void)removeObjectAtIndex:(NSUInteger)index;


例如：

	- (void)addLayoutManager:(NSLayoutManager *)obj;
	- (void)removeLayoutManager:(NSLayoutManager *)obj;
	

以下是一些重要、有用的的规格： 

* 如果集合没有顺序，返回NSSet比NSArray更好； 
* 如果在集合中插入元素，位置很重要的话，使用以下的格式比前面提到的更好： 

	```
	- (void)insertLayoutManager:(NSLayoutManager *)obj atIndex:(int)index; 
	- (void)removeLayoutManagerAtIndex:(int)index; 
	```
 
以下一些实现细节要注意： 

* 这些方法通常暗含插入对象的拥有权(ownership)的管理，所以添加/插入元素的时候retain它们，移除的时候remove它们；

* 如 果插入对象想保持它原来的持有的对象，通常对该对象的setter方法不用retain，例如insertLayoutManager:atIndex: method方法。NSLayoutManager类在以下的方法中同样这样处理：

	```
	- (void)setTextStorage:(NSTextStorage *)textStorage; 
	- (NSTextStorage *)textStorage; 
	```

	通常你不用调用setTextStorage方法，但是你可能需要重写它。 

另一个关于集合约定的例子来自 NSWindow 类：

```
	- (void)addChildWindow:(NSWindow *)childWin ordered:(NSWindowOrderingMode)place;
	- (void)removeChildWindow:(NSWindow *)childWin;
	- (NSArray *)childWindows;
	- (NSWindow *)parentWindow;
	- (void)setParentWindow:(NSWindow *)window;
```


###方法参数

在命名方法参数时候有几个基本规则： ----参数的名字也是骆驼风格 ----不要使用“pointer”或ptr这些词，参数的类型比参数的名字更能说明它是否是指针。 ----避免一俩个字母做参数的名字 ----避免缩写，参数名不差多这几个字母。 一般来讲，以下的一些方法中的关键词通常跟固定的参数搭配：

```
	...action:(SEL)aSelector
	...alignment:(int)mode
	...atIndex:(int)index
	...content:(NSRect)aRect
	...doubleValue:(double)aDouble
	...floatValue:(float)aFloat
	...font:(NSFont *)fontObj
	...frame:(NSRect)frameRect
	...intValue:(int)anInt
	...keyEquivalent:(NSString *)charCode
	...length:(int)numBytes
	...point:(NSPoint)aPoint
	...stringValue:(NSString *)aString
	...tag:(int)anInt
	...target:(id)anObject
```

###私有方法

在大多数情况下，私有的方法名称一般跟公共方法的名称都遵循同样的规则作为。然而，还有一个普遍的规则是给私有方法一个前缀，所以很容易区分他们跟公共方法。

即使遵循这些规则，私有方法名称还是可以引起一些特殊问题。当你你编写的Cocoa框架类的子类，你不知道你的私有方法是否无意中重写方法里同名称的私有方法。 在Cocoa框架中命名大多数私有的方法用下划线前缀开头（例如，_foodata），标记方法为私有。对于这条规则，有两个建议： 

* 对于你自己的私有方法，不要使用下划线前缀。Apple约定了这条规则； 
* 如果是一个大cocoa框架类（如NSView）的子类，你要绝对确保你的私有的方法不同于父类的方法，您可以通过添加你自己独有的前缀来区分。前缀应尽可能的唯一的，也许是一个基于在你公司或项目的形式”xx_”。所以如果你的项目被称为Byte Flogger，前缀可以是BF_addobject； 
	
	虽然之前建议用前缀给私有方法命名，这看起来跟之前说的规则矛盾。但这块情况特殊，我们必须确保子类无意间重写父类的私有方法。 


###函数命名
Objective-c中实现一个功能可以通过函数和方法。当你的对象是单实例或者处理一个子功能时候，更适合用函数。 函数命名有几下基本原则：

* 函数名类似方法名，但有一些例外： 
	
	* 它们用你在类/常数中的前缀开头
	* 前缀后的首字母大写。 

* 许多函数名字已动词开头，描述函数实现的功能：

```
NSHighlightRect 
NSDeallocateObject
```

函数如果是查询一些属性，命名有一些特别的规定：

* 如果函数返回第一个参数的属性，省略动词：

	```
	unsigned int NSEventMaskFromType(NSEventType type) float 	NSHeight(NSRect aRect) 
	```
* 如果函数返回值是指针，使用Get：

	```
	const char *NSGetSizeAndAlignment(const char *typePtr, unsigned int *sizep, unsigned int *alignp) 
	```

* 如果函数返回值是布尔型，函数名用变化的(inflected)动词开头：
	
	```
	BOOL NSDecimalIsNotANumber(const NSDecimal *decimal) 
	```

##属性和数据类型命名

这部分讲命名属性、实例变量、常数、通知、异常。

###属性和实例变量命名

因为属性和存取器方法的对应性质(get方法和set后那部分名称即是属性名字，对应实例变量)，所以对于属性的命名基本类似存取器方法的名字，参考存取器方法小节。 

如果属性是名称/动词意思，格式是：@property (…) type nounOrVerb 

例如：

```
@property (strong) NSString *title;
@property (assign) BOOL showsAlpha; 
```

如果属性是形容词意思，属性名称省略is前缀，并且指定存取器get方法的命名。例如：

```
@property (assign, getter=isEditable) BOOL editable; 
```
在许多情况，当你声明一个了属性，你同时也确定(synthesize)了相应的实例变量。 确保实例变量简明的描述存储的属性，通常你不直接访问实例变量，而是通过存取器方法(在类内部直接访问)，为了区别，用下划线前缀；例：

```
@implementation MyClass {
	BOOL _showsTitle;
}
```

如果你想用某实例变量对应某个属性，在@synthesize中说明：
		
```
@implementation MyClass 
@synthesize showsTitle=_showsTitle; 
```
当添加实例变量的时候，有以下几条规则： 

* 避免显示的声明公共的实例变量。开发者只会关心对象的接口，不关心实现的细节。通过声明属性和相应的(synthesizing)实例变量，避免显示声明实例变量。

* 如果需要声明实例变量，用@private 或者 @protected声明。如要继承的实例变量用@protected声明。 
* 如果一个实例变量是实例的访问属性(accessible attribute)，确保你已经写了相应的存取器方法。

###常数
常数的命名规则跟常数是怎么产生的息息相关。

####枚举常数

* 对于有取值相联系的常数集合，使用枚举(说什么情况使用枚举，跟命名没关系)
* 枚举常数和typedef后面枚举名的命名跟函数的命名规则类似，参考函数命名小节。例：

	```
	typedef enum _NSMatrixMode {
		NSRadioModeMatrix = 0,
		NSHighlightModeMatrix = 1,
		NSListModeMatrix = 2,
		NSTrackModeMatrix = 3
	} NSMatrixMode;
	```
	注意上文中_NSMatrixMode 在typedef中没有用。

 

* 你也可以使用不命名的枚举，比如位掩码(bit masks)，例如：

	```
	enum {
		NSBorderlessWindowMask = 0,
		NSTitledWindowMask = 1 << 0,
		NSClosableWindowMask = 1 << 1,
		NSMiniaturizableWindowMask = 1 << 2,
		NSResizableWindowMask = 1 << 3
	};
	```
 
####const修饰的常数

* 使用const去创建浮点型常量。可以创建整形常量，如果各整形常量之间没有什么联系，否则，使用枚举。

* const修饰的常数命名规则，举例说明：const float NSLightGray; 命名规则类似函数，参考函数命名小节。

####其他类型常数

* 通常不使用`#define`预编译命令去创建常数。像上文说的，整形常数用枚举，浮点型常数用`const`修饰。

* 使用大写字母符号让编译器决定某段代码是否编译。例如：

	```
	#ifdef DEBUG
	```
	
* 注意由编译器定义的宏，有前后各俩个下划线。例如：

	```
	__FUNCTION__
	__FILE__
	__LINE__
	__VA_ARGS__
	```

* 定义字符串常数，例如作方法名或字典的key等，你要确保编译器识别字符串常数(编译语法检查)。Cocoa提供了许多字符串常量例子，如：

	```
	APPKIT_EXTERN NSString *NSPrintCopies; 
	```

	字符串的值被指定了常量（注意APPKIT_EXTERN 宏在Objective-C中的像extern声明的作用）


###通知和异常

通知和异常的命名规则基本相同，但它们有各自特点

####通知

如果一个类有delegate，许多通知都会被delegate接收通过delegate方法。这些通知的名称应该反应相应的delegate方法。例如，一个全局的NSApplication类对象自动注册去接收applicationDidBecomeActive消息，当应用程序发送NSApplicationDidBecomeActiveNotification.消息的时候。通知通过全局的字符串对象定义，格式如下：[Name of associated class] + [Did | Will] + [UniquePartOfName] + Notification； 例：

NSApplicationDidBecomeActiveNotification
NSWindowDidMiniaturizeNotification
NSTextViewDidChangeSelectionNotification
NSColorPanelColorDidChangeNotification

 
####异常

尽管你可以为了一些目的自由的使用异常(由NSException类和相关函数提供)，Cocoa将编程中出现错误，例如数组越界，看做异常。Cocoa不使用异常去处理常规的、预料的错误情况，例如，返回值为`nil、NULL、NO`或一些错误代码。详细参考`《Error Handling Programming Guide》`。

异常通过全局的字符串对象定义，格式如下：

```
[Prefix] + [UniquePartOfName] + Exception； 
```

其中unique part of the name是由单词组合而成，每个首字母大写。例如：

```
NSColorListIOException
NSColorListNotEditableException
NSDraggingException
NSFontUnavailableException
NSIllegalSelectorException
```

###通用的缩写和简称

通常你不用缩写你的命名，当你编写接口时候。参考基本命名规则章节。然而，下面所列举的缩写都是众所周知的，你可以继续使用它们。有以下几点需要注意：

* 缩写的替代格式使用在标准C语音库中被允许。例如：`“alloc” `and `“getc”`。
* 你可以在参数中更自由的使用缩写。例如：`“imageRep”`, `“col”` (for `“column”`),`“obj”`, and `“otherWin”`


缩写 	意义

alloc 	Allocate

alt 	Alternate

app 	应用程序，例, NSApp全局应用程序对象。 “application” 全拼在delegate方法、通知中等

calc 	Calculate.

dealloc 	Deallocate.

func 	Function.

horiz 	Horizontal.

info 	Information

init 	Initialize

max/min 	Maximum/Minimum.

msg 	Message

nib 	Interface Builder archive.

pboard 	Pasteboard (but only in constants

rect 	Rectangle.

Rep 	Representation (used in class name such as NSBitmapImageRep

temp 	Temporary.

vert 	Vertical.

你也可以使用一些计算机行业通用的缩写，例：

ASCII、PDF、XML、HTML、URL、RTF、
HTTP、TIFF、JPG、PNG、GIF、LZW、ROM、RGB、CMYK、MIDI、FTP




参考资料：

* iOS开发规范[http://blog.csdn.net/pjk1129/article/details/45146955](http://blog.csdn.net/pjk1129/article/details/45146955)

* Coding Guidelines for Cocoa[https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/CodingGuidelines/Articles/NamingBasics.html#//apple_ref/doc/uid/20001281-BBCHBFAH ](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/CodingGuidelines/Articles/NamingBasics.html#//apple_ref/doc/uid/20001281-BBCHBFAH )

* iOS:Cocoa编码规范 -[译]Coding Guidelines for Cocoa  [http://www.2cto.com/kf/201406/305877.html](http://www.2cto.com/kf/201406/305877.html)

* [Cocoa]苹果 Cocoa 编码规范 [http://blog.csdn.net/kesalin/article/details/6928929](http://blog.csdn.net/kesalin/article/details/6928929)