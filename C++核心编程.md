# C++���ı��
*20220116 ����*
### 1 �ڴ����ģ��
* ����������ź�����Ķ����ƴ��룬os���й���cpp->����->exe���������������ֻ����
* ȫ������ȫ�ֱ�������̬����static���������ַ�������const���ε�ȫ�ֱ�������const���εľֲ�����������ȫ����
* ջ�����������Զ������ͷţ������������ֲ�������
* ����������Ա������ͷţ�������Ա���ͷţ��������ʱ��os���գ�new�ؼ��ֽ��п���


# C++����
*20220117 ����*

    #include<iostream>
    using namespace std;

    int* func() {
        int* p = new int(10);//���ض������ڴ�ĵ�ַ���
        return p;
    }
    int main() {
        int* p = func();
        cout << "�����ĵ�ַ���" << p<<endl;
        system("pause");
        return 0;
    }
### 88.new�����
�����Ŀ���new���ͷ�delete

    #include<iostream>
    using namespace std;

    int* func() {
        //�ڶ���������������,new���ظ��������ݵ�ָ��
        int * p=new int(10);
        return p;
    }
    void test01() {
        int* p = func();
        cout << *p << endl;
        delete p;
    }

    void test02() {
        int* arr = new int[10];//10��������10��Ԫ��
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

### 89����
���ã������������
�﷨�� �������� &����=ԭ��

    void func89() {
        int a = 10;
        int& b = a;
        cout << "a=" << a << endl;
        cout << "b=" << b << endl;
        b = 100;
        cout << "a=" << a << endl;
        cout << "b=" << b << endl;
    }
### 90����ע������
���ñ����ʼ������ʼ��֮��Ͳ����Ըı�

    void func90() {
        //�����ʼ����һ����ʼ���Ͳ��ܸ���
        int a = 10;
        int& b = a;//����int &b;   ����int c=20;b=c;
        cout << "a=" << a << endl;
        cout << "b=" << b << endl;
    }
### 91��������������
��������ʱ�������������õļ������β������βΣ���ָ������ʵ��

    cout << "91*********" << endl;
        int a = 10;
        int b = 20;
        //��ַ����
        mySwap9101(&a,&b);
        cout << "a=" << a << endl;
        cout << "b=" << b << endl;
        //���ô���
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
ԭ�����þ��Ǳ������Ա����Ĳ�����Ҳ���Ƕ�ʵ�εĲ���
### 92��������������ֵ
��Ҫ���ؾֲ��������ã�����������Ϊ��ֵ

    cout << "92*********" << endl;
        //��������������ֵ
        int& ref = test9201();
        cout << "ref="<<ref << endl;//��һ���ǶԵģ���Ϊ���������˱���
        cout << "ref=" << ref << endl;//�ڶ��ν��������Ϊa���ڴ��Ѿ��ͷ�

        int& ref2 = test9202();
        cout << "ref2=" << ref2 << endl;
        cout << "ref2=" << ref2 << endl;
        test9202() = 1000;
        cout << "ref2=" << ref2 << endl;
        cout << "ref2=" << ref2 << endl;

    int& test9201() {
        int a = 10;//�ֲ�������ջ��
        return a;//�൱�ڷ��غ�������

    }

    int& test9202() {
        static int a = 10;//��̬���������ȫ�����������ڳ���������ͷ�
        return a;

    }
### 93���õı���
���õı�����C++�ڲ�ʵ�־���һ��ָ�볣��

    cout << "92���õı���" << endl;
        int& ref4 = a;//�Զ�ת��:int* const ref=&a;
        //ָ�볣����ָ��ָ�򲻿��ԸĶ���ָ��ָ���ֵ�ǿ��ԸĶ���
        ref4 = 10;//�ڲ�����ref�����ã��Զ�ת��*ref=20;
        cout << "a=" << a << endl;
        cout << "ref4=" << ref4 << endl;
        func93(a);
        cout << "a=" << a << endl;
    void func93(int& ref) {
        ref = 100;
    }