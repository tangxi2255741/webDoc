# 常用Java注释标签（Java comment tags）

## @author  作者

适用范围：文件、类、方法

（*多个作者使用多个@author标签标识，java doc中显示按输入时间顺序罗列。）*
例：* @author Leo. Yao

## @param  输入参数的名称  说明

适用范围：方法

例：* @param str the String用来存放输出信息。

##  @return 输出参数说明

适用范围：方法

例：    * @return    <code>true</code>执行成功;

​               <code>false</code>执行失败.

## @since JDK版本

用于标识编译该文件所需要的JDK环境。

适用范围：文件、类

例：     * @since JDK1.6

## @version 版本号

用于标识注释对象的版本号
适用范围：文件、类、方法
例：     * @version 1.0

## @see 链接目标

表示参考。会在java 文档中生成一个超链接，链接到参考的类容。
**用法**
   @see #field
   @see #Constructor(Type, Type...)
   @see #Constructor(Type id, Type id...)
   @see #method(Type, Type,...)
   @see #method(Type id, Type, id...)
   @see Class
   @see Class#field
   @see Class#Constructor(Type, Type...)
   @see Class#Constructor(Type id, Type id)
   @see Class#method(Type, Type,...)
   @see Class#method(Type id, Type id,...)
   @see package.Class
   @see package.Class#field
   @see package.Class#Constructor(Type, Type...)
   @see package.Class#Constructor(Type id, Type id)
   @see package.Class#method(Type, Type,...)
   @see package.Class#method(Type id, Type, id)
   @see package

## @throws 异常

标识出方法可能抛出的异常

适用范围：方法

例：     * @throws IOException  If an input or output exception occurred

## @deprecated废弃

标注此类/接口、方法、字段已经被废止

适用范围：文件、类、方法

## @link 链接地址

链接到一个目标，用法类似@see。但常放在注释的解释中形如{@link …}

``` java
/**
    - @deprecated      As of JDK 1.1, replaced by
    - {@link #setBounds(int,int,int,int)}
 */

```



# Java注释的使用顺序

* @author      (classes and interfaces only, required)
* @version     (classes and interfaces only, required. See footnote 1)
* @param       (methods and constructors only)
* @return      (methods only)
* @exception   (@throws is a synonym added in Javadoc 1.2)
* @see        
* @since      
* @serial      (or @serialField or @serialData)
* @deprecated  (see How and When To Deprecate APIs)



# 简单常见的HTML嵌入

<P> 用于分段
<code>  标签用于表示计算机源代码或者其他机器可以阅读的文本内容。<code> 标签就是为软件代码的编写者设计的。包含在该标签内的文本将用等宽、类似电传打字机样式的字体（Courier）显示出来只应该在表示计算机程序源代码或者其他机器可以阅读的文本内容上使用 <code> 标签。虽然 <code> 标签通常只是把文本变成等宽字体，但它暗示着这段文本是源程序代码。将来的浏览器有可能会加入其他显示效果。例如，程序员的浏览器可能会寻找 <code> 片段，并执行某些额外的文本格式化处理，如循环和条件判断语句的特殊缩进等。
```java
/**

- Graphics is the abstract base class for all graphics contexts
- which allow an application to draw onto components realized on
- various devices or onto off-screen images.
- A Graphics object encapsulates the state information needed
- for the various rendering operations that Java supports.  This
- state information includes:
- <ul>
- <li>The Component to draw on
- <li>A translation origin for rendering and clipping coordinates
- <li>The current clip
- <li>The current color
- <li>The current font
- <li>The current logical pixel operation function (XOR or Paint)
- <li>The current XOR alternation color
- (see setXORMode)
- </ul>
- <p>
- Coordinates are infinitely thin and lie between the pixels of the
- output device.
- Operations which draw the outline of a figure operate by traversing
- along the infinitely thin path with a pixel-sized pen that hangs
- down and to the right of the anchor point on the path.
- Operations which fill a figure operate by filling the interior
- of the infinitely thin path.
- Operations which render horizontal text render the ascending
- portion of the characters entirely above the baseline coordinate.
- <p>
- Some important points to consider are that drawing a figure that
- covers a given rectangle will occupy one extra row of pixels on
- the right and bottom edges compared to filling a figure that is
- bounded by that same rectangle.
- Also, drawing a horizontal line along the same y coordinate as
- the baseline of a line of text will draw the line entirely below
- the text except for any descenders.
- Both of these properties are due to the pen hanging down and to
- the right from the path that it traverses.
- <p>
- All coordinates which appear as arguments to the methods of this
- Graphics object are considered relative to the translation origin
- of this Graphics object prior to the invocation of the method.
- All rendering operations modify only pixels which lie within the
- area bounded by both the current clip of the graphics context
- and the extents of the Component used to create the Graphics object.
*
- @author      Sami Shaio
- @author      Arthur van Hoff
- @version     %I%, %G%
- @since       1.0
*/
public abstract class Graphics {
  /**
  - Draws as much of the specified image as is currently available
  - with its northwest corner at the specified coordinate (x, y).
  - This method will return immediately in all cases, even if the
  - entire image has not yet been scaled, dithered and converted
  - for the current output device.
  - <p>
  - If the current output representation is not yet complete then
  - the method will return false and the indicated
  - {@link ImageObserver} object will be notified as the
  - conversion process progresses.
*
  - @param img       the image to be drawn
  - @param x         the x-coordinate of the northwest corner
  - of the destination rectangle in pixels
  - @param y         the y-coordinate of the northwest corner
  - of the destination rectangle in pixels
  - @param observer  the image observer to be notified as more
  - of the image is converted.  May be
  - null
  - @return          true if the image is completely
  - loaded and was painted successfully;
  - false otherwise.
  - @see             Image
  - @see             ImageObserver
  - @since           1.0
*/
public abstract boolean drawImage(Image img, int x, int y,
                    ImageObserver observer)
 }
}

```



# 常见注释模板

## 类（接口）注释

```java
/**

- 类的描述
- @author Administrator
- @Time 2012-11-2014:49:01
*
*/
public classTest extends Button {
……
}

```



## 方法注释

```java
public class Test extends Button {
  /**

- 为按钮添加颜色
- @author Administrator
- @param color
- @return
- @exception  (方法有异常的话加)
- @Time2012-11-20 15:02:29
*/
  public voidaddColor(String color){
……
  }
}
```



## 全局变量注释

```java
public final class String
   implements Java.io.Serializable, Comparable<String>,CharSequence
{
   /** The value is used for characterstorage. */
   private final char value[];
   /** The offset is the first index of thestorage that is used. */
   private final int offset;
……
}
```



## 字段/属性注释

```java
public class EmailBody implements Serializable{
   private String id;
   private String senderName;//发送人姓名
   private String title;//不能超过120个中文字符
   private String content;//邮件正文
   private String attach;//附件，如果有的话
   privateSet<EmailList> EmailList;
……
}
```

