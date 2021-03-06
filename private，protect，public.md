# private，protect，public

## 一、类实例的访问权限

1. public

   * 类的实例可以直接访问public修饰的成员变量和成员函数

   * ```c++
     #include<iostream>
     #include<string>
     using namespace std; 
     class AccessTest
     {
     	public:
     		int pub_mem;
     		int pub_fun(){};
     	protected:
     		int prot_mem;
     		int prot_fun(){};
     	private:
     		int priv_memb;
     		int priv_fun(){};	
     };
     int main()
     {
     	AccessTest at;
     	at.pub_mem;     //OK, 类变量可以访问public成员
     	at.pub_func();  //OK, 访问public成员函数是没有问题的
       return 0;
     }
     ```

2. protect

   * 类的实例无法访问protected成员变量和成员函数，但是可以通过声明友元类进而利用实例进行访问

   * ```C++
     #include <iostream>
     using namespace std;
     class C1
     {
         friend class C2; //声明C2是C1的友元类，故C1中的成员变量和成员函数对C2的成员函数而言都是public，这与C1的成员函数一样
     private:
         int x, y;
     
     protected:
         int m, n;
     
     public:
         int getX() const { return x; };
         C1(int x, int y, int m, int n) : x(x), y(y), m(m), n(n){};
     };
     class C2
     {
     public:
         int getxfromC1(const C1 &c) const { return c.x; };
     };
     int main()
     {
         C1 c(1, 3, 2, 4);
         cout << c.getX() << endl;
         C2 c2;
         cout << c2.getxfromC1(c) << endl;
         return 0;
     }
     ```

3. private

   * 对本类的实例而言，private和protected的作用是相同的，不在赘述

## 二、继承类的访问权限

派生类有三种继承方式

1. public继承

   *  **派生类的成员函数**，可以访问基类的public成员、protected成员，但是无法访问基类的private成员

   * **派生类的实例变量**，可以访问基类的public成员，但是无法访问protected、private成员

   * ```c++
     #include <iostream>
     using namespace std;
     class A
     {
     private:
         int a;
     
     protected:
         int b;
     
     public:
         int c;
         A(int a = 0, int b = 0, int c = 0) : a(a), b(b), c(c){}; //添加默认参数
     };
     class A2 : public A
     {
     private:
     public:
         int f1() { return c; };
         int f2() { return b; };
         A2(int b, int c) : A(b, c)
         {
             b = b;
             c = c;
         }; //构造函数不可以继承，并且A2继承了a，但是不能访问
         //int f3(){return a;};
     };
     int main()
     {
         A2 t(3, 2);
         cout << t.c << endl;
         //cout<<t.b<<endl;实例不可以访问protected成员
         //cout<<t.a<<endl;实例不可以访问private成员
         return 0;
     }
     ```

2. protected继承

   * 派生类的成员函数，可以访问基类的public成员、protected成员，但是无法访问基类的private成员。
   * 派生类的实例变量，无法访问基类的任何成员，因为基类的public成员在派生类中变成了protected

3. private继承

   * 派生类的成员函数，可以访问基类的public成员、protected成员，但是无法访问基类的private成员。
   * 派生类的实例变量，无法访问基类的任何成员，因为基类的所有成员在派生类中变成了private

## 三、总结

1. public、protected、private限制的关系主要体现在两个方面：一是类内部的关系（成员函数可以访问任意的类内部成员），二是类的实例和类成员的关系（要视public、protected、private加以区分）
2. private和protected的区别**体现在对基类的继承类中**，在基类中不体现，private继承和protected继承的区别**体现在对派生类的继承中**，在对基类的继承中不体现
3. 类的成员函数可以访问本类中的任意成员，以及从基类继承后的protected和public成员

