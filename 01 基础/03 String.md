# 概览
注意：String属于引用类型，不属于基本数据类型。

String被声明为final类型，所以不可被继承。
内部使用char数组存储数据，该数组被声明为final，所以char数组初始化之后不能再引用
其他数组，并且String内部没有提供改变char数组的方法，因此可以保证String不可变。

```
public final class String
implements java.io.Serializable, Comparable<String>, CharSequence {
    @Stable
    private final byte[] value;
```

# 不可变的好处
* String不可变性天生具备线程安全性，可以在多个线程中安全使用。
