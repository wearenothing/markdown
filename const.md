# const

## 一、const 修饰普通类型

```c++
cosnt int a=7;
int b=a;//right
a=8;//wrong!
```

## 二、const修饰指针类型

1. const 位于‘*’左侧，表明指针指向的内容不可以修改
   1. cosnt int* a;
   
   2. int const* a;
   
   3. ```c++
      #include <iostream>
      using namespace std;
      
      int main()
      {
          int a=3;
          int b=4;
          const int* c=&a;
          //*c=3;//不能修改c的内容
          c=&b;//可以修改c指向的对象
          return 0;
      }
      ```
2. const位于‘*’右侧，表明指针本身不可以修改
   
   1. int* const a;
   
   2. ```c++
      #include <iostream>
      using namespace std;
      
      int main()
      {
          int a=3;
          int b=4;
          int* const c=&a;
          *c=3;//能修改c的内容
          //c=&b;//不可以修改c指向的对象
          return 0;
      }
      ```
3. 既有const位于‘*’左侧，也有位于右侧，表明都不可以修改
   
   1. const int* const a;
   
   2. ```c++
      #include <iostream>
      using namespace std;
      
      int main()
      {
          int a=3;
          int b=4;
          const int* const c=&a;
          //*c=3;//不能修改c的内容
          //c=&b;//不可以修改c指向的对象
          return 0;
      }
      ```

## 三、const修饰函数参数或函数返回值

1. **const 修饰函数参数**，一般用于自定义类型的参数传递。因为自定义自类型的参数传递，需要临时对象复制参数，对于临时对象的构造，需要调用构造函数，比较浪费时间，因此我们采取 const 外加引用传递的方法。

   1. ```c++
      #include<iostream>
      using namespace std;
      class Test
      {
      public:
          Test(){}
          Test(int _m):_cm(_m){}
          int get_cm()const
          {
             return _cm;
          }
      private:
          int _cm;
      };
      void Cmf(const Test& _tt)
      {
          cout<<_tt.get_cm();
      }
      int main(void)
      {
          Test t(8);
          Cmf(t);
          system("pause");
          return 0;
      }
      ```

2. **const 修饰自定义类型的作为返回值**，此时返回的值不能作为左值使用，既不能被赋值，也不能被修改

## 四、const修饰类成员函数

const 修饰类成员函数，其目的是防止成员函数修改被调用对象的值

```c++
#include<iostream> 
using namespace std;
class Test
{
public:
    Test(){}
    Test(int _m):_cm(_m){}
    int get_cm()const
    {
       return _cm;
    }
private:
    int _cm;
};
 
void Cmf(const Test& _tt)
{
    cout<<_tt.get_cm();
}
int main(void)
{
    Test t(8);
    Cmf(t);
    system("pause");
    return 0;
}
```



