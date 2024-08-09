# STL

## string

### 构造函数初始化

```c++
string str1;
string srt2("abcd");
string str3(str2)
string str4(str3,2)//这个2表示从位置2开始复制，包括2
string str5(5,'a')//5表示将a这个字符复制5次
```

### 运算符重载

```c++
string str6 = str5;
str6 = str2;
str6 = "abcdef";
```

### 赋值成员函数

```c++
str6.assign(str5);
str6.assign("kjkjk");
str6.assign("123455",2,4);//4表示从2位置开始加4个字符
str6.assign(6,'a');

```

### 加号重载

```c++
str3 += str6;
//拼接成员函数
str3.append("mmmmmm",3);//3表示拼接前三个字符
```

### 成员访问

```c++
str3[1] = 'p';
str3.at(1) = '0';//at会报越界异常，上面的不会
```

### 查找

```c++
str3.find("aaa");//会返回第一次找到这个字符的下标
str3.find("aaa",6);//6表示从第六个位置开始找
//如果没找到会返回一个npos
cout << (str3.find("aaa",6) == str3.npos)//此时输出会为1
//npos 是一个static修饰的静态常量，所以可以用string::作用域符访问
cout << (str3.find("aaa",6) == string::npos)
```

### 替换

```c++
str3.replace(1,3,"ioioi",2);//1表示从位置1开始，删除3个元素，2表示从"ioioi"从拿前两个元素
```

### 比较

```c++
cout << str3 < str2 << endl;//比较会根据字典排序，现比较第一个字符的大小，
string str3 = "abcd";
    string str2 = "Abcd";
    cout << (int)'a' << endl;
    cout << (int)'A' << endl; 
    cout << (str3 < str2) << endl;
//输出
97
65
0//说明'a'是大于'A'的，也就是看ASCI
```

### 子串

```c++
str3.substr(1,5)//1表示位置，5代表从1开始截取5个长度
```

### 插入

```c++
str3.insert(1,"byd")//会在原来的1位置插入字符,原来1号位置字符会移到后面
```

### 删除

```c++
str3.erase(2)//从位置2元素开始删除，包括位置2
```



## 迭代器和reverse算法

### begin和end

```c++
std::string str = "abcd";
std::begin(str);//begin返回一个起始迭代器，也就是起始指针,迭代器的本质是指针
cout << *str.begin() << endl//*解引用获得str首地址的值
std::end(str)//返回str末尾指针，也就是d后面的/0
//迭代器遍历元素
auto s = std::begin(str);
auto e = std::end(str);
while(s != e){
cout << *s << endl
s++;}
//reverse
std::reverse(std::begin(str),std::end(str))//左闭右开
```



## for遍历

```c++
1.基本遍历
int arr[] {1,2,3,4,5};
for(int i = 0;i<arr.size();i++){
cout << arr[i] << " " }//此时i表示数组中的下标
2.foreach
for(int x : arr){
cout << x << " "}//x要定义为跟arr相同的类型，每一遍循环都会对应arr中的一个元素，有点类似于每一遍都是int x = arr[i];
//如果要修改值怎么办
for(int &x : arr){
cin >> x;}
```

## pair

> template<typename _T1, typename _T2>
>
>   struct pair
>
>   {
>
>    typedef _T1 first_type;   /// @c first_type is the first bound type
>
>    typedef _T2 second_type;  /// @c second_type is the second bound type
>
>    _T1 first;         /// @c first is a copy of the first object
>
>    _T2 second;         /// @c second is a copy of the second object
>
>    // _GLIBCXX_RESOLVE_LIB_DEFECTS
>
>    // 265.  std::pair::pair() effects overly restrictive
>
>    /** The default constructor creates @c first and @c second using their
>
> ​    \*  respective default constructors.  */
>
> pair是一个模板类，本质是一个结构体，里面只有first和second两个变量

```c++
pair<int,int> p;
p.first = 1.
p.second = 2;
//构造函数
auto p2(p);
auto p2 = p;
//比较
cout << p2 == p << endl;
//按字典序原则，先比较first再比较second
```



## vector

```c++
//构造函数
vector<int> c1;
int n = 10;
vector<int> c2(n);//指定长度
vector<int> c3(c2);//拷贝构造
vector<int> c4(n,144);//表示将n个元素都赋值为144
vector<int> c5 = ({1,2,3,4,5});
vector<int> c6 = (c5.begin(),c5.end());//[begin(),end())

//访问元素
cout << c5[2] << endl;
cout << c5.at(2) << endl;//at的优势会对越界进行检查，[]是不会检查
cout << c5.front();//返回第一个数
cout << c5.back();//返回最后一个数
cout << c5.empty();//查看是否为空，返回bool类型
cout << c5.size() << " " << c5.capacity()//大小是元素个数，容量是能存储元素的个数，容量会大于等于大小
cout << c5 == c6;
cout << *c5.begin();//输出第一个元素的值
cout << *c5.end();//输出最后一个元素后一个元素的值
cout << *c5.rbegin();//表示最后一个元素的值
cout << *c5.rend();//表示第一个元素的前一个元素，比如int类型第一个元素地址为0x104,这时就会指向0x100

//遍历
for(auto it = c5.begin();it != c5.end();it++){
cout << *it << " ";
}

for(int & it : c1){
cout << it << " "};

//赋值
c5.push_back(1);//将1放到数组末尾
c5.pop_back();//将数组末尾元素弹出
c5.erase(c5.begin());//只删除第一个元素
c5.erase(unique(c5.begin(),c5.end()),c5.end());//去重
c5.clear();//清空所有元素，并且c5.size()也变成0
```

## map

```
//构造函数
map<string,int> m1;//内部是一个pair，第一个元素是键，第二个元素是值
m1["aaa"] = 123;
m1.insert("ccc",222);
for(auto x : m1){
cout << x.first << " " << x.second;}

```

### map的应用

```c++
//计算每一个字符出现的次数
string str = "asdakjfioasdlajfioasa";
map<char,int> m;
for(auto ch : str){
++m[ch];}
//排序

```



## set

```c++
//set底层是红黑树，是重复有序的
//template<typename _Key, typename _Compare, typename _Alloc>
    class set;作为内模板类型要用<>尖括号,如果有第二个参数就表示比较类型
//并且比较函数是一个类，不能是函数
set<int> s1;
set<int> s2(s1);
set<int> s3(s1.begin(),s1.end());
int arr[] = {1,2,3,4};

//比较
struct opr{
bool opreator()
(int a, int b){
return a > b;//表示大的在前面}}
set<int,opr> s4(arr,arr+4);

//方法
cout << s4.empty();
cout << s4.count(1);//表示找到元素值为1的个数，只能是1或0
cout << *s4.find(1);//find表示返回迭代器,还需解引用输出

//lower_bound,upper_bound
cout << *s4.lower_bound(4);//返回大于等于元素4的迭代器
cout << *s4.upper_bound(4);//返回大于元素4的迭代器

//遍历
for(auto it = s4.begin();it!=s4.end();it++){
cout << *it << " ";}
s4.insert(1);
s4.insert(2);

```



## sort

```
int arr[] = {0,1,2,3,4};
string str = "sahjafg";
sort(str.begin(),str.end());//默认升序排序
sort(str.begin(),str.end(),less<int>());//升序排序
sort(str.begin(),str.end(),greater<int>());//降序排序
bool cmp(char a,char b){
return a > b;}//大的在前面
sort(str.begin(),str.end(),cmp)//自定义比较规则

```



## *和&运算符的区别

> 在C++中，`*`（星号）和`&`（和号）是两个不同的运算符，它们在不同的上下文中有不同的含义和用途。
>
> 1. `*`（星号）：
>    - 解引用运算符：用于获取指针指向的内存地址中存储的值。例如，如果有一个指向整数的指针 `int* ptr`，那么 `*ptr` 将给出该指针指向的整数的值。
>    - 乘法运算符：用于数学运算，表示乘法。例如，`a * b` 表示 `a` 和 `b` 的乘积。
> 2. `&`（和号）：
>    - 取地址运算符：用于获取变量的内存地址。例如，如果有一个整数变量 `int a`，那么 `&a` 将给出变量 `a` 的内存地址。
>    - 按引用传递：在函数参数中使用，表示传递变量的引用而不是复制变量的值。这可以提高效率，尤其是对于大型数据结构。例如，`void func(int& x)` 表示 `func` 函数接收一个整数的引用。
>
> 在指针和引用的上下文中，`*` 和 `&` 的区别尤为明显：
>
> - 当你有一个指针变量时，`*` 用于解引用，即通过指针获取数据。例如，`int* ptr = &a;` 创建了一个指向整数变量 `a` 的指针，`*ptr` 将给出 `a` 的值。
> - 当你有一个引用变量时，`&` 用于获取引用指向的变量的地址。例如，`int& ref = a;` 创建了一个对整数变量 `a` 的引用，`&ref` 将给出 `a` 的地址，但这不是常用操作，因为引用本身就是变量的别名。
>
> 总结来说，`*` 用于通过指针获取数据，而 `&` 用于获取变量的地址或创建变量的引用。在实际编程中，正确理解和使用这两个运算符对于编写高效和安全的代码至关重要。

