#  RM踩坑之旅4

## 使用ref明确传递引用

在 C++ 中，`std::ref` 是一个工具，用于显式地将一个变量作为引用传递给函数或构造对象。它通常在需要显式传递引用而非复制值时使用，尤其是当传递给接受值的函数模板时。

### 何时使用 `std::ref`

1. **模板函数**：某些模板函数会复制传入的参数。如果你想传递引用而避免拷贝，可以使用 `std::ref`。
2. **标准库容器**：某些容器（如 `std::vector`）默认会复制存储的元素。如果你想存储引用，可以使用 `std::ref` 包装变量。

在 C++ 中，`std::ref` 是一个工具，用于显式地将一个变量作为引用传递给函数或构造对象。它通常在需要显式传递引用而非复制值时使用，尤其是当传递给接受值的函数模板时。

### 何时使用 `std::ref`

1. **模板函数**：某些模板函数会复制传入的参数。如果你想传递引用而避免拷贝，可以使用 `std::ref`。
2. **标准库容器**：某些容器（如 `std::vector`）默认会复制存储的元素。如果你想存储引用，可以使用 `std::ref` 包装变量。

------

### 用法示例

#### 1. 在标准算法中使用

```c++
#include <iostream>
#include <vector>
#include <functional> // std::ref
#include <algorithm> // std::for_each

void increment(int& n) {
    ++n;
}

int main() {
    int a = 5, b = 10, c = 15;
    std::vector<std::reference_wrapper<int>> vec = {std::ref(a), std::ref(b), std::ref(c)};

    // 通过 std::ref 包装引用
    std::for_each(vec.begin(), vec.end(), [](int& n) { ++n; });

    std::cout << "a: " << a << ", b: " << b << ", c: " << c << '\n'; // a: 6, b: 11, c: 16
    return 0;
}
```

#### 2. 线程中使用

```c++
#include <iostream>
#include <thread>
#include <functional> // std::ref

void print_and_increment(int& x) {
    std::cout << "Before increment: " << x << '\n';
    ++x;
    std::cout << "After increment: " << x << '\n';
}

int main() {
    int value = 10;

    // std::thread 默认会复制参数，使用 std::ref 显式传递引用
    std::thread t(print_and_increment, std::ref(value));
    t.join();

    std::cout << "Value in main: " << value << '\n'; // Value in main: 11
    return 0;
}
```

#### 3. 使用 `std::bind`

```c++
#include <iostream>
#include <functional> // std::bind, std::ref

void modify(int& x, int increment) {
    x += increment;
}

int main() {
    int value = 42;

    // 使用 std::bind 时，显式传递引用
    auto func = std::bind(modify, std::ref(value), 10);
    func();

    std::cout << "Modified value: " << value << '\n'; // Modified value: 52
    return 0;
}
```

### 注意事项

1. **`std::ref` 和 `std::cref`**：

   - `std::ref` 创建可变引用的包装器。
   - `std::cref` 创建常量引用的包装器。

2. **解引用**： 如果你需要直接访问 `std::ref` 包装的值，可以使用 `.get()`，例如：

   ```c++
   std::reference_wrapper<int> ref = std::ref(value);
   int& actual_ref = ref.get();
   ```

3. **类型推导**： 如果使用 `auto` 推导 `std::ref` 包装的对象，它的类型将是 `std::reference_wrapper<T>` 而非原始类型。

## 凸包

在 OpenCV 的 C++ API 中，凸包（Convex Hull）是一种几何操作，用于从一组点中计算出包含所有点的最小凸多边形。OpenCV 提供了 `cv::convexHull` 函数来实现这一功能。

### 基本概念

凸包是包含点集的最小凸多边形，所有点都在多边形内或边上。它可以用于许多计算机视觉任务，比如物体检测、形状分析等。

------

### 使用 `cv::convexHull`

以下是一个使用凸包的示例代码：

```c++
#include <opencv2/opencv.hpp>
#include <vector>
#include <iostream>

int main() {
    // 创建一个黑色图像
    cv::Mat image = cv::Mat::zeros(500, 500, CV_8UC3);

    // 随机生成点
    std::vector<cv::Point> points = { {100, 150}, {200, 80}, {300, 200}, {250, 300}, {150, 400} };

    // 绘制这些点
    for (const auto& point : points) {
        cv::circle(image, point, 5, cv::Scalar(0, 255, 0), -1);
    }

    // 计算凸包
    std::vector<cv::Point> hull;
    cv::convexHull(points, hull);

    // 绘制凸包
    for (size_t i = 0; i < hull.size(); i++) {
        cv::line(image, hull[i], hull[(i + 1) % hull.size()], cv::Scalar(255, 0, 0), 2);
    }

    // 显示结果
    cv::imshow("Convex Hull", image);
    cv::waitKey(0);

    return 0;
}
```

------

### 函数说明

#### `cv::convexHull`

```c++

void cv::convexHull(InputArray points, OutputArray hull, bool clockwise = false, bool returnPoints = true);
```

1. 参数说明：
   - `points`：输入点集，可以是 `std::vector<cv::Point>` 或 `cv::Mat`。
   - `hull`：输出的凸包点集。
   - `clockwise`（可选）：是否按照顺时针方向排列凸包点。
   - `returnPoints`（可选）：是否返回凸包点坐标。设为 `false` 时，返回的是索引。

------

### 示例扩展：结合轮廓检测

凸包常与轮廓检测结合。以下是一个结合 `cv::findContours` 的例子：

```c++
#include <opencv2/opencv.hpp>
#include <vector>

int main() {
    // 生成一个二值图像
    cv::Mat image = cv::Mat::zeros(500, 500, CV_8UC1);
    cv::rectangle(image, cv::Point(100, 100), cv::Point(400, 400), cv::Scalar(255), -1);

    // 找到轮廓
    std::vector<std::vector<cv::Point>> contours;
    cv::findContours(image, contours, cv::RETR_EXTERNAL, cv::CHAIN_APPROX_SIMPLE);

    // 计算每个轮廓的凸包
    for (const auto& contour : contours) {
        std::vector<cv::Point> hull;
        cv::convexHull(contour, hull);

        // 在原图上绘制凸包
        for (size_t i = 0; i < hull.size(); i++) {
            cv::line(image, hull[i], hull[(i + 1) % hull.size()], cv::Scalar(255), 2);
        }
    }

    // 显示结果
    cv::imshow("Convex Hull", image);
    cv::waitKey(0);

    return 0;
}
```

------

### 相关函数

1. **`cv::isContourConvex`**：判断一个轮廓是否是凸的。
2. **`cv::approxPolyDP`**：多边形逼近，与凸包常结合使用以简化形状。
3. **`cv::boundingRect`**：求最小外接矩形。

### 凸包的面积

使用 `cv::contourArea` 函数，输入凸包的点集合。

### 注意事项

- `cv::contourArea` 默认计算的是点集形成的闭合多边形的面积，因此 `hull` 必须表示一个封闭的凸包。
- 如果输入点集较少（如不足 3 个点），则凸包面积会是零，因为无法形成多边形。
- 

## 使用 **rm -rf ***删除文件时要再三确认文件内容

### **血与泪的教训：**:crying_cat_face:

使用终端操作时勤用着  **ls**  查看当前目录，确定删除内容后在 rm -rf * ,享受便捷的同时也要承受粗心带来的后果

### 死亡回放：

<img src="/home/zjq/A&T/踩坑之旅/picture/rm -rf *.png" alt="rm -rf *" style="zoom: 33%;" />







 