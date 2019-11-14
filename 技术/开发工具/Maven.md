> Maven是一个异常强大的构建工具，能够帮我们自动化构建过程：清理->编译->测试->生成报告->打包->编译；

# Maven说明

## Maven安装目录结构

* bin：包含mvn运行的脚本；
*  boot：只有一个plexus-classworlds的jar文件，它是一个类加载器框架，maven使用它加载自己的类库；
* conf：包含一个非常重要的文件：settings.xml；
* lib：包含了所有Maven运行时需要的Java类库；
* LICENSE.txt：记录了Maven使用的软件许可证；
* NOTICE.txt：记录了Maven包含的第三方软件；
* README.txt：包含了Maven的简要介绍；



## settings.xml

全局范围：$M2_HOME/conf/settings.xml

用户范围、便于Maven升级：~/.m2/settings.xml



## 项目的主代码和测试代码

1、主代码会被打包到最终的构建中，应该放到src/main/java目录下；
Java类的包名应该是：com.公司名.项目名.包名；

2、测试代码：只在运行测试时用到，不会被打包。应放到src/test/java目录下；



## 项目构建的文件名规则
规则：artifactId-version[-classifier].packaging

案列：nexus-indesxer-2.0.0.javadoc.jar;



## 依赖范围

<!-- 依赖范围，test表示该依赖只对测试有效，不声明依赖范围，默认值为compile-->
<scope>test</scope>
依赖范围是用来控制依赖与classpath（编译、测试、运行）的关系

**Maven有以下几种依赖范围:**

| 范围     | 说明                                                         |
| -------- | ------------------------------------------------------------ |
| compile  | 默认，编译、测试和运行三种环境变量都有效                     |
| test     | 仅对测试环境变量有效                                         |
| provided | 对于编译和测试有效，在运行时无效                             |
| runtime  | 对于测试和运行时有效，编译时无效                             |
| system   | 此依赖不是通过 Maven 仓库解析的，而且往往与本机系统绑定，可能造成构建的不可移植 |
| import   | 不会对三种环境产生实际影响                                   |



## 重复引入依赖时，依赖调解的原则：

第一原则：路径最近者优先（传递性靠前的）；

第二原则：第一声明者优先（先声明的）；

# Maven命令

| 命令                          | 说明                                 | 示例 |
| ----------------------------- | ------------------------------------ | ---- |
| clean                         | 清理输出目录target/                  |      |
| compile                       | 编译项目主代码                       |      |
| install                       | 将项目输出的jar安装到了Maven本地仓库 |      |
| mvn dependency:list           | 查看当前项目已解析依赖               |      |
| mvn dependency:tree           | 查看当前项目的依赖树                 |      |
| mvn dependency:ananlyze       | 分析依赖树                           |      |
| Used  undeclared dependencies | 项目中有使用，但是没有声明的依赖     |      |
| Unused declared dependencies  | 项目中未使用，但显示声明的依赖       |      |

