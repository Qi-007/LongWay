# RM踩坑之旅2

## 类的

创建一个类，类的末尾要加 ；

```c++
class person
{
  int m_age;  
};
```



## 类不能写入main函数中



## 类的命名不能使用C++中的关键字

**关键字举例如下：**

控制语句关键字	

if	条件语句，用于根据条件表达式的结果执行代码块。
else	与if配合使用，用于条件为假时执行代码块。
switch	用于根据一个变量的值执行不同的代码块。
case	在switch语句中用于匹配变量的值。
default	在switch语句中用于处理所有未匹配的情况。
for	循环语句，用于执行代码块多次，通常用于已知次数的循环。
while	循环语句，用于根据条件表达式重复执行代码块。
do	与while配合使用，先执行代码块，再检查条件表达式。
break	终止循环或switch语句，并跳出语句块。
continue	跳过当前循环迭代，继续下一次迭代。
goto	无条件跳转到标记位置，不推荐使用，因为会使代码难以维护。
return	用于从函数中返回值，并终止函数执行。

### 数据类型关键字

int	整数类型。
float	单精度浮点数类型。
double	双精度浮点数类型。
char	字符类型。
void	无类型，常用于函数无返回值。
bool	布尔类型，表示真或假。
short	短整数类型，通常为16位。
long	长整数类型，通常为32位或更长。
signed	有符号类型修饰符。
unsigned	无符号类型修饰符。
wchar_t	宽字符类型，通常用于Unicode字符。
### 存储类型关键字	

auto	自动类型推断，C++11 引入。
register	建议将变量存储在寄存器中，实际使用由编译器决定。
static	指定变量在其作用域内保持其值和生命周期。
extern	声明变量或函数在另一个文件中定义。
mutable	允许常量成员在const成员函数中被修改。
thread_local	声明线程局部存储变量，每个线程有其独立实例。

### 类和对象相关关键字

class	定义类。
struct	定义结构体，默认访问权限为公有。
union	定义共用体。
this	指针，指向调用对象自身。
public	访问权限，公有成员。
private	访问权限，私有成员。
protected	访问权限，受保护成员。
virtual	声明虚函数，支持多态。
friend	声明友元，允许非成员函数访问私有和保护成员。
explicit	显式构造函数，防止隐式转换。
new	动态分配内存。
delete	释放动态分配的内存。
operator	重载运算符。
sizeof	计算对象或类型的字节大小。
typename	声明类型名称，特别是在模板中使用。

### 异常处理关键字	

try	用于捕获异常。
catch	用于处理异常。
throw	用于抛出异常。

### 其他关键字	

namespace	定义命名空间，用于组织代码，避免命名冲突。
using	引入命名空间或类型别名。
inline	建议编译器内联函数，减少函数调用开销。
const	声明常量或常量成员函数。
volatile	指示变量可能会被程序外因素修改，防止编译器优化。
enum	定义枚举类型。
typedef	为现有类型定义新的名称。
template	定义模板，用于泛型编程。
constexpr	用于在编译时计算常量表达式。
nullptr	空指针常量，取代旧的NULL。
dynamic_cast	用于安全地将基类指针转换为派生类指针。
static_cast	用于执行显式转换。
reinterpret_cast	用于重新解释类型的比特模式。
const_cast	用于移除const或volatile属性。
typeid	用于在运行时获取对象的类型信息。
export	用于模板导出，C++20之前被弃用，现已被删除。
import	用于模块导入，C++20引入。
————————————————

                            版权声明：本文为博主原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接和本声明。

原文链接：https://blog.csdn.net/TENET123/article/details/140612521



## 堆区开辟的数据需要程序员手动释放



 如果属性有在堆区开辟的数据 ，一定要自己提供拷贝构造函数 ，防止浅拷贝带来的问题.



## 类初始化列表

**注意冒号**

```c++ 
class Person{
public:
Person （int a, int b, int c） : m_A (a), m_B (b), m_C (c)
{
    
}
};
```



