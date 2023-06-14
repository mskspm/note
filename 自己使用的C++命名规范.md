*2023.04.26* *摘抄自CSDN*

[TOC]

---

# 自己使用的C++命名规范

最重要的一致性规则是命名管理. 命名的风格能让我们在不需要去查找类型声明的条件下快速地了解某个名字代表的含义: 类型, 变量, 函数, 常量, 宏, 等等, 甚至. 我们大脑中的模式匹配引擎非常依赖这些命名规则.

命名规则具有一定随意性, 但相比按个人喜好命名, 一致性更重要, 所以无论你认为它们是否重要, 规则总归是规则.

# 1 基本原则

## 1.1包含字符

- a~z
- A~Z
- 0~9
- -
- _

![202306141602674](https://cdn.jsdelivr.net/gh/mskspm/image/img/202306141637830.png)

## 1.2 命名规则

函数命名, 变量命名, 文件命名要有描述性; 少用缩写.

尽可能使用描述性的命名, 别心疼空间, 毕竟相比之下让代码易于新读者理解更重要. 不要用只有项目开发者能理解的缩写, 也不要通过砍掉几个字母来缩写单词.

### 规范命名

```bash
int price_count_reader;    // 无缩写
int num_errors;            // "num" 是一个常见的写法
int num_dns_connections;   // 人人都知道 "DNS" 是什么
```

### 不规范命名

```bash
int n;                     // 毫无意义.
int nerr;                  // 含糊不清的缩写.
int n_comp_conns;          // 含糊不清的缩写.
int wgc_connections;       // 只有贵团队知道是什么意思.
int pc_reader;             // "pc" 有太多可能的解释了.
int cstmr_id;              // 删减了若干字母.
```

注意, 一些特定的广为人知的缩写是允许的, 例如用 `i` 表示迭代变量和用 `T` 表示模板参数.

模板参数的命名应当遵循对应的分类: 类型模板参数应当遵循 类型命名 的规则, 而非类型模板应当遵循 变量命名 的规则.

## 1.3 命名方法

### *匈牙利命名法*

匈牙利命名法是早期的规范，由微软的一个匈牙利人发明的，是 IDE 还十分智障的年代的产物。那个年代，当代码量很多的时候，想要确定一个变量的类型是很麻烦的，不像现在 IDE 都会给提示，所以才产生了这样一个命名规范，估计现在已经没啥人用了吧……一个十分系统却又琐碎的命名规范。

该命名规范，要求前缀字母用变量类型的缩写，其余部分用变量的英文或英文的缩写，单词第一个字母大写。

e.g.

```cpp
int iMyAge;        #  "i": int
char cMyName[10];  #  "c": char
float fManHeight;  #  "f": float
```

其他前缀类型还有：

```text
a      数组（Array）
b      布尔值（Boolean）
by     字节（Byte）
c      有符号字符（Char）
cb     无符号字符（Char Byte，并没有神马人用的）
cr     颜色参考值（Color Ref）
cx,cy  坐标差（长度 Short Int）
dw     双字（Double Word）
fn     函数（Function）
h      Handle（句柄）
i      整形（Int）
l      长整型（Long Int）
lp     长指针（Long Pointer）
m_     类成员（Class Member）
n      短整型（Short Int）
np     近程指针（Near Pointer）
p      指针（Pointer）
s      字符串（String）
sz     以 Null 做结尾的字符串型（String with Zero End）
w      字（Word）
```

还有其他更多的前缀是根据微软自己的 MFC/句柄/控件/结构等东西定义的，就不过多描述了。

### *驼峰式命名法*

驼峰式命名法，又叫小驼峰式命名法（所以自然就存在大驼峰命名法啦……)。

该命名规范，要求第一个单词首字母小写，后面其他单词首字母大写，简单粗暴易学易用。

```text
int myAge;
char myName[10];
float manHeight;
```

### *帕斯卡命名法*

帕斯卡命名法，又叫***大驼峰式命名法***。

与小驼峰式命名法的最大区别在于，每个单词的第一个字母都要大写。

```text
int MyAge;
char MyName[10];
float ManHeight;
```

### *下划线命名法*

下划线命名法并不如大小驼峰式命名法那么备受推崇，但是也是浓墨重彩的一笔。尤其在宏定义和常量中使用比较多，通过下划线来分割全部都是大写的单词。

该命名规范，也是很简单，要求单词与单词之间通过下划线连接即可。

```text
int my_age;
char my_name[10];
float man_height;
```

# 2 命名细节

## 2.1 文件命名

文件名要全部小写, 可以包含下划线 `_` 或连字符`-`, 依照项目的约定,且尽量保证文件名明确. 

可接受的文件命名示例:

```bash
my_useful_class.cc
my-useful-class.cc
myusefulclass.cc
myusefulclass_test.cc // _unittest 和 _regtest 已弃用.
```

> 引自C++ Primer Plus第五版中文版 P8
>
> C++实现源代码的扩展名
> UNIX ： C、cc、cxx、c
> GNU C++ ：C、cc、cxx、cpp、c++
> Borland C++ ： Cpp
> Microsoft Visual C++ ： cpp、cxx、cc Android系统源码中以cc为后缀
> 参考了C++ Primer Plus第五版中文版 P8

不要使用已经存在于 /usr/include 下的文件名 (即编译器搜索系统头文件的路径), 如 db.h.

通常应尽量让文件名更加明确. http_server_logs.h 就比 logs.h 要好. 定义类时文件名一般成对出现, 如 foo_bar.h 和 foo_bar.cc, 对应于类 FooBar.

内联函数必须放在 .h 文件中. 如果内联函数比较短, 就直接放在 .h 中.

## 3. 类型命名

类型名称的每个单词首字母均大写, 不包含下划线: MyExcitingClass, MyExcitingEnum.

所有类型命名 —— 类, 结构体, 类型定义 (typedef), 枚举, 类型模板参数 —— 均使用相同约定, 即以大写字母开始, 每个单词首字母均大写, 不包含下划线. 例如:

```bash
// 类和结构体
class UrlTable { ...
class UrlTableTester { ...
struct UrlTableProperties { ...

// 类型定义
typedef hash_map<UrlTableProperties *, string> PropertiesMap;

// using 别名
using PropertiesMap = hash_map<UrlTableProperties *, string>;

// 枚举
enum UrlTableErrors { ...
```

## **4. 变量命名**

变量 (括函数参数) 和数据成员名一律小写, 单词之间用下划线连接. 类的成员变量以下划线结尾, 但结构体的就不用, 如: a_local_variable, a_struct_data_member, a_class_data_member_.

普通变量命名
举例:

```bash
string table_name;  // 好 - 用下划线.
string tablename;   // 好 - 全小写.
string tableName;  // 差 - 混合大小写
```

**类数据成员**
不管是静态的还是非静态的, 类数据成员都可以和普通变量一样, 但要接下划线.

```bash
class TableInfo {
  ...
 private:
  string table_name_;  // 好 - 后加下划线.
  string tablename_;   // 好.
  static Pool<TableInfo>* pool_;  // 好.
};
1234567
```

**结构体变量**
不管是静态的还是非静态的, 结构体数据成员都可以和普通变量一样, 不用像类那样接下划线:

```bash
struct UrlTableProperties {
  string name;
  int num_entries;
  static Pool<UrlTableProperties>* pool;
};
12345
```

## 5. 常量命名

声明为 constexpr 或 const 的变量, 或在程序运行期间其值始终保持不变的, 命名时以 “k” 开头, 大小写混合. 例如:

```bash
const int kDaysInAWeek = 7;
```

所有具有静态存储类型的变量 (例如静态变量或全局变量, 参见 存储类型) 都应当以此方式命名. 对于其他存储类型的变量, 如自动变量等, 这条规则是可选的. 如果不采用这条规则, 就按照一般的变量命名规则.

## 6. 函数命名

常规函数使用大小写混合, 取值和设值函数则要求与变量名匹配:

```bash
MyExcitingFunction() 
MyExcitingMethod() 
my_exciting_member_variable()
set_my_exciting_member_variable()
```

一般来说,函数名的每个单词首字母大写 (即 “驼峰变量名” 或 “帕斯卡变量名”), 没有下划线. 对于首字母缩写的单词, 更倾向于将它们视作一个单词进行首字母大写 (例如, 写作 `StartRpc()` 而非 `StartRPC()`).

```bash
AddTableEntry()
DeleteUrl()
OpenFileOrDie()
123
```

(同样的命名规则同时适用于类作用域与命名空间作用域的常量, 因为它们是作为 API 的一部分暴露对外的, 因此应当让它们看起来像是一个函数, 因为在这时, 它们实际上是一个对象而非函数的这一事实对外不过是一个无关紧要的实现细节.)

取值和设值函数的命名与变量一致. 一般来说它们的名称与实际的成员变量对应, 但并不强制要求. 例如 `int count()` 与 `void set_count(int count)`.

## 7. 命名空间命名

命名空间以小写字母命名. 最高级命名空间的名字取决于项目名称. 要注意避免嵌套命名空间的名字之间和常见的顶级命名空间的名字之间发生冲突.

顶级命名空间的名称应当是项目名或者是该命名空间中的代码所属的团队的名字. 命名空间中的代码, 应当存放于和命名空间的名字匹配的文件夹或其子文件夹中.

注意 *不使用缩写作为名称* 的规则同样适用于命名空间. 命名空间中的代码极少需要涉及命名空间的名称, 因此没有必要在命名空间中使用缩写.

要避免嵌套的命名空间与常见的顶级命名空间发生名称冲突. 由于名称查找规则的存在, 命名空间之间的冲突完全有可能导致编译失败. 尤其是, 不要创建嵌套的 `std` 命名空间. 建议使用更独特的项目标识符 (`websearch::index` ，`websearch::index_util`) 而非常见的极易发生冲突的名称 (比如 `websearch::util`).

对于 `internal` 命名空间, 要当心加入到同一 `internal` 命名空间的代码之间发生冲突 (由于内部维护人员通常来自同一团队, 因此常有可能导致冲突). 在这种情况下, 请使用文件名以使得内部名称独一无二 (例如对于 `frobber.h`, 使用 `websearch::index::frobber_internal`).

## 8. 枚举命名

枚举的命名应当和 *常量* 或 *宏* 一致: `kEnumName` 或是 `ENUM_NAME`.

单独的枚举值应该优先采用 常量 的命名方式. 但 宏 方式的命名也可以接受. 枚举名 `UrlTableErrors` (以及 `AlternateUrlTableErrors`) 是类型, 所以要用大小写混合的方式.

```bash
enum UrlTableErrors {
    kOK = 0,
    kErrorOutOfMemory,
    kErrorMalformedInput,
};
enum AlternateUrlTableErrors {
    OK = 0,
    OUT_OF_MEMORY = 1,
    MALFORMED_INPUT = 2,
};
12345678910
```

2009 年 1 月之前, 我们一直建议采用 *宏* 的方式命名枚举值. 由于枚举值和宏之间的命名冲突, 直接导致了很多问题. 由此, 这里改为优先选择常量风格的命名方式. 新代码应该尽可能优先使用常量风格. 但是老代码没必要切换到常量风格, 除非宏风格确实会产生编译期问题.

## 9. 宏命名

你并不打算 使用宏, 对吧? 如果你一定要用, 像这样命名: `MY_MACRO_THAT_SCARES_SMALL_CHILDREN`.

参考 预处理宏; 通常 *不应该* 使用宏. 如果不得不用, 其命名像枚举命名一样全部大写, 使用下划线:

```bash
#define ROUND(x) ...
#define PI_ROUNDED 3.0
12
```

## 10. 命名规则的特例

如果你命名的实体与已有 C/C++ 实体相似, 可参考现有命名策略.

`bigopen()`: 函数名, 参照 open() 的形式

```
uint`: `typedef
```

`bigpos`: `struct` 或 `class`, 参照 `pos` 的形式

`sparse_hash_map`: STL 型实体; 参照 STL 命名约定

`LONGLONG_MAX`: 常量, 如同 INT_MAX

# 速记

## 1 文件命名

文件命名全部小写/每个首字母大写

```
myusefulclass.h
myusefulclass.cpp
MyUsefulClass.cpp
```

## 2 数据类型命名（类名、结构体名、枚举、类型定义typedef等）

以大写字母开头，每个单词字母均大写，不包含下划线。

```c++
class SensorDev;
struct SensorProperties;
enum SensorType;
```

## 3 变量命名

### 3.1普通成员变量

普通成员变量：小写字母及下划线组成

```c++
int car_num;
```

### 2.2 类成员变量

通常在以`m_`开头 或 在结尾处加上`_`。

```c++
int m_car_num;
int car_num_;
```

### 2.3 全局变量

通常以`g_`开头。

```
int g_car_num;
```

### 2.4 常量

通常以`k`开头并混合大小写。

```c++
int kCarNum;
```

## 4 函数命名

函数命名通常以小驼峰法命名，以动词形式，表示函数功能，见名知意。

```
setCarNum();
getCarType();
```

## 5 命名空间

大驼峰命名法。

```c++
namespace ProjectAppService;
```



