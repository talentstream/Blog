---
title: Use variant to pass factory parameter
date: 2024-01-23 10:48:14
tags:
---

### Factory Pattern

```c++
class Creator{
public:
    virtual std::unique_ptr<Product> create(ProductId id) {
    if (ProductId::MINE == id) return std::make_unique<ConcreteProductMINE>();
    if (ProductId::YOURS == id) return std::make_unique<ConcreteProductYOURS>();
    return nullptr;  
};
```

 	

以上代码是Wiki提供的一段工厂模式的代码，简单来说，工厂模式就是用于一个创建对象的接口，用于创建不同的物品。

```kotlin
object ShapesFactory {
    /**
     * @param T type of shape sub-class.
     * @param radius required to construct [Circle] instance.
     * @param width required to construct [Rectangle] instance.
     * @param height required to construct [Rectangle] instance.
     */
    fun <T: Shape> getShape(shape: Class<T>, radius: Int, width: Int, height: Int): Shape {
        if (shape.isAssignableFrom(Circle::class.java)) {
            return Circle(radius)
        } else if (shape.isAssignableFrom(Rectangle::class.java)) {
            return Rectangle(width, height)
        } else {
            throw IllegalStateException("Cannot create shape instance for ${shape.simpleName}")
        }
    }
}
```

但是，如果想要每个物品有不同的初始参数设置，如果想要传递参数的话，就会比较麻烦，如果放出相同的接口，则会浪费一些参数。同时，每次新添加需要创建的product就会需要大幅度修改接口。

在[这篇参考文章](https://medium.com/@mohammad.amarneh2015/kotlin-trick-for-passing-arguments-to-factory-methods-1c6f6bb67eac)中，我看到了作者使用 kotlin 的 sealed class 对数据进行封装。隐藏了接口数据的复杂性。使得代码更加可读，易于拓展，同时限制参数类型。

```kotlin
sealed class ShapeFactoryParam {
    data class CircleParam(val radius: Int) : ShapeFactoryParam()
    data class RectangleParam(val width: Int, val height: Int): ShapeFactoryParam()
}
object ShapesFactory {
    fun getShape(param: ShapeFactoryParam): Shape {
        return when (param) {
            is ShapeFactoryParam.CircleParam -> Circle(param.radius)
            is ShapeFactoryParam.RectangleParam -> Rectangle(param.width, param.height)
        }
    }
}
```

### Pass Parameter in C++

在c++中，没有像kotlin 里 sealed class 这么好用的东西。

于是在一番寻找后，找到了 **variant** 这个东西，variant 是一种更通用的union，而且更加type-safe。

同时，有很多方便的标准库函数，也不用自己造轮子了。

在cppreference中，有关于std::visit 添加lambda以及处理不同的类型。

在传递参数时，个人喜欢将param也传递过去，这样子将拆解param全部隐藏到对应的构造函数中。当然，也可以直接就在工厂函数中拆解param。



```c++
struct CircleParam{
  int radius;  
};
struct RectangleParam{
  int width;
  int height;
};

using ShapeParam = std::variant<CircleParam,RectangleParam>;

class Circle{
public:
	Circle(const CircleParam& param)
    	: mRadius{param.radius} {}
private:
    int mRadius;
};

class ShapeFactoy{
public:
	static std::unique_ptr<Shape> GetShape(const ShapeParam& params)
    {
        return std::visit([](auto&& arg))
        {
            using T = std::decay_t<decltype(arg)>;
            if constexpr (std::is_same<T,CircleParam>) {
                return std::make_unique<Circle>(arg);
            }
            else if constexpr(std::is_same<T,RectangleParam>){
                return std::make_unique<Rectangle>(arg);
            }
            else {
                static_assert(always_false_v<T>, "non-exhaustive visitor!");
            }
        },params);
    }
};
```



### Reference

- [Kotlin Trick for passing arguments to Factory Methods](https://medium.com/@mohammad.amarneh2015/kotlin-trick-for-passing-arguments-to-factory-methods-1c6f6bb67eac)

- [c++ variant](https://en.cppreference.com/w/cpp/header/variant)

- [Factory method patten](https://en.wikipedia.org/wiki/Factory_method_pattern)
