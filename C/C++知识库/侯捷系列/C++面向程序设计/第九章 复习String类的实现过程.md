# 第九章 复习String类的实现过程

# 9.1 编程示例

class String

{

public:

String(const char* cstr = 0);

String(const String& str);

String& operator=(const String& cstr);

~String();

char* get_c_str() const {return m_data;}

private:

char* m_data;

};

---

# 9.2 ctor和dtor（构造函数和析构函数）

// 构造函数

inline

String::String(const char* cstr = 0)

{

if(cstr)

{

m_data = new char[strlen(cstr)+1];

strcpy(m_data,cstr);

}

else // 未指定初值

{

m_data = new char[1];

- m_data = '\0';

}

}

// 析构函数

inline

String::~String()

{

delete[] m_data;

}

---

# 9.3 copy ctor(拷贝构造函数)

// 拷贝构造函数

inline

String::String(const String& str)

{

m_data = new char[strlen(str.m_data)+1];

strcpy(m_data,str.m_data);

}

---

# 9.4 copy assignment operator(拷贝赋值函数)

// 拷贝赋值函数

inline

String& String::operator=(const String& str)

{

if(this == &str)

{

return *this;

}

delete[] m_data;

m_data = new char[strlen(str.m_data)+1];

strcpy(m_data,str.m_data);

return *this;

}

---

# 9.5 &区别

1. String& 出现在类型的后面表示 **引用**
2. &str 出现在值的前面表示取地址，得到的是一个指针