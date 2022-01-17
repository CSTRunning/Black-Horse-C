# C++核心编程
*20220116 李阳*
### 1 内存分区模型
* 代码区：存放函数体的二进制代码，os进行管理。cpp->编译->exe。代码区：共享和只读。
* 全局区：全局变量，静态变量static，常量（字符常量，const修饰的全局变量），const修饰的局部变量不属于全局区
* 栈区：编译器自动分配释放，函数参数，局部变量等
* 堆区：程序员管理和释放，若程序员不释放，程序结束时由os回收，new关键字进行开辟


# C++引用
*20220117 李阳*

    #include<iostream>
    using namespace std;

    int* func() {
        int* p = new int(10);//返回堆区的内存的地址编号
        return p;
    }
    int main() {
        int* p = func();
        cout << "堆区的地址编号" << p<<endl;
        system("pause");
        return 0;
    }
### 88.new运算符
堆区的开辟new和释放delete

    #include<iostream>
    using namespace std;

    int* func() {
        //在堆区创建整型数据,new返回该类型数据的指针
        int * p=new int(10);
        return p;
    }
    void test01() {
        int* p = func();
        cout << *p << endl;
        delete p;
    }

    void test02() {
        int* arr = new int[10];//10代表数组10个元素
        for (int i = 0; i < 10; i++)
        {
            arr[i] = i + 100;
        }
        for (int i = 0; i < 10; i++)
        {
            cout << arr[i] << endl;
        }
        delete[] arr;
    }
    int main() {
        test01();
        test02();
        system("pause");
        return 0;
    }

### 89引用
作用：给变量起别名
语法： 数据类型 &别名=原名

    void func89() {
        int a = 10;
        int& b = a;
        cout << "a=" << a << endl;
        cout << "b=" << b << endl;
        b = 100;
        cout << "a=" << a << endl;
        cout << "b=" << b << endl;
    }
### 90引用注意事项
引用必须初始化，初始化之后就不可以改变

    void func90() {
        //必须初始化，一旦初始化就不能更改
        int a = 10;
        int& b = a;//错误：int &b;   错误：int c=20;b=c;
        cout << "a=" << a << endl;
        cout << "b=" << b << endl;
    }
### 91引用做函数参数
函数传参时，可以利用引用的技术让形参修饰形参，简化指针修饰实参

    cout << "91*********" << endl;
        int a = 10;
        int b = 20;
        //地址传递
        mySwap9101(&a,&b);
        cout << "a=" << a << endl;
        cout << "b=" << b << endl;
        //引用传递
        mySwap9102(a, b);
        cout << "a=" << a << endl;
        cout << "b=" << b << endl;

    void mySwap9101(int * a,int * b) {
        int temp = *a;
        *a = *b;
        *b = temp;
    }
    void mySwap9102(int &a, int &b) {
        int temp = a;
        a = b;
        b = temp;
    }    
原因：引用就是别名，对别名的操作，也就是对实参的操作
### 92引用做函数返回值
不要返回局部变量引用，函数调用作为左值

    cout << "92*********" << endl;
        //引用做函数返回值
        int& ref = test9201();
        cout << "ref="<<ref << endl;//第一次是对的，因为编译器做了保存
        cout << "ref=" << ref << endl;//第二次结果错误，因为a的内存已经释放

        int& ref2 = test9202();
        cout << "ref2=" << ref2 << endl;
        cout << "ref2=" << ref2 << endl;
        test9202() = 1000;
        cout << "ref2=" << ref2 << endl;
        cout << "ref2=" << ref2 << endl;

    int& test9201() {
        int a = 10;//局部变量在栈区
        return a;//相当于返回函数别名

    }

    int& test9202() {
        static int a = 10;//静态变量存放在全局区，数据在程序结束后释放
        return a;

    }
### 93引用的本质
引用的本质在C++内部实现就是一个指针常量

    cout << "92引用的本质" << endl;
        int& ref4 = a;//自动转换:int* const ref=&a;
        //指针常量：指针指向不可以改动，指针指向的值是可以改动的
        ref4 = 10;//内部发现ref是引用，自动转换*ref=20;
        cout << "a=" << a << endl;
        cout << "ref4=" << ref4 << endl;
        func93(a);
        cout << "a=" << a << endl;
    void func93(int& ref) {
        ref = 100;
    }