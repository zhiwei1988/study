### 函数

#### 位置实参

#### 关键字实参

关键字实参让你无需考虑调用中的实参顺序。使用时务必准确地指定函数定义中的形参名。

#### 默认值

为保证 Python 能正确地解读位置实参，使用默认值时，在形参列表中必须先列出没有默认值的形参，再列出有默认值的形参。

#### 传递任意数量的实参

有时候，你预先不知道函数需要接受多少个实参，好在 Python 允许函数从调用语句中收集任意数量的实参。

```python
def make_pizza(*toppings):
    print toppings
```

形参名 *toppings 中的星号让 Python 创建一个名为 toppings 的空元组，并将收到的所有值都封装到这个元组中。

#### 使用任意数量的关键字实参

有时候，需要接受任意数量的实参，但预先不知道传递给函数的会是什么样的信息。这种情况下，可将函数编写成能接受任意数量的键-值对。

```python
def build_profile(first, last, **user_info):
    profile = {}
    profile['first_name'] = first
    profile['last_name'] = last
    for key, value in user_info.items():
        profile[key] = value
    return profile
```

形参 `**user_info` 中的两个星号让 Python 创建一个名为 user_info 的空字典，并将收到的所以名称-值对都封装到这个字典中。

### 类

#### 创建和使用类

类中的函数称为**方法**。

通过实例访问的变量称为**属性**。

#### 继承

一个类继承另一个类时，它将自动获得另一个类的所有属性和方法。

创建子类的实例时，Python 首先需要完成的任务是给父类的所有属性赋值。

##### Python 2.7 中的继承

```python
class Car(object):
    def __init()__(self, make, model, year):
        --snip---

class ElectricCar(Car):
    def __init__(self, make, model, year):
        super(ElectricCar, self).__init__(make, model, year)
        --snip--
```

##### 重写父类的方法

子类中可以定义一个与父类中同名的方法来重写父类中的方法。

### 用户输入和 while 循环

如果你使用的是 Python 2.7，应该使用函数 raw_input() 来提示用户输入。Python 2.7 中也包含 input()，但它将用户输入解读为 Python 代码，并尝试运行它们。

### BUILT-IN METHODS

#### classmethod

[classmethod](https://www.programiz.com/python-programming/methods/built-in/classmethod)

与 classmethod 很像，都是关联到类而不是对象。

* Static method knows nothing about the class and just deals with the parameters
* Class method works with the class since its parameter is always the class itself

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
```

```python
@classmethod
def fromBirthYear(cls, name, birthYear):
    return cls(name, date.today().year - birthYear)

def display(self):
    print(self.name + "'s age is: " + str(self.age))
```

classmethod 的第1个参数必须是 cls

