# sort()

利用sort()对结构体进行排序，有两种方法来实现：

1. 在结构体中重载''<''运算符

   * ```c++
     struct Test
     {
         int a,b,c;
         bool operator< (const Test& t) const
         {
             if(a!=t.a)
                 return (a<t.a);
             else if(b!=t.b)
                 return (b<t.b);
             else 
                 return (c<t.c);
         }
     }; 
     ```

2. 自定义cmp函数

   * ```c++
     bool cmp(const Test& t1,const Test& t2)
     {
         if(t1.a!=t2.a)
             return (t1.a<t2.a);
         else if(t1.b!=t2.b)
             return (t1.b<t2.b);
         else 
             return (t1.c<t2.c);
     }
     ```