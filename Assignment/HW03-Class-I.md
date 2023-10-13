# **HW3 - Class I**

注意：查找资料，了解Java注释的规定和约定，程序中要有清楚的注释。
参考资料：[Google Java Style Guide](https://google.github.io/styleguide/javaguide.html)

## **001-形状信息**
<details>

<summary>
题目
</summary>

### **题目描述**

编一个显示形状特征的类，至少能显示形状的周长和面积，以此类为基础，求圆、正方形、长方形、菱形的周长和面积。

</details>

<details>

<summary>
代码
</summary>

```java
public class Q1_ShapeInfo {
    public static void main(String[] args) {
        // Test Circle
        Circle circle = new Circle(3.0);
        System.out.println("Circle:");
        circle.displayInfo();

        // Test Square
        Square square = new Square(3.0);
        System.out.println("\nSquare:");
        square.displayInfo();
        
        // Test Rectangle
        Rectangle rectangle = new Rectangle(6.0, 8.0);
        System.out.println("\nRectangle:");
        rectangle.displayInfo();

        // Test Rhombus constructed with diagonals
        Rhombus rhombus = new Rhombus(10.0, 12.0);
        System.out.println("\nRhombus:");
        rhombus.displayInfo();

        // Test Rhombus constructed with side and angle
        Rhombus rhombus2 = new Rhombus(10.0, Math.PI / 3, true);
        System.out.println("\nRhombus:");
        rhombus2.displayInfo();
    }
}

class Shape {
    // Method to calculate area
    public double calculateArea() {
        return 0.0;
    }

    // Method to calculate perimeter
    public double calculatePerimeter() {
        return 0.0;
    }

    // Method to display area and perimeter
    public void displayInfo() {
        System.out.println("Area: " + calculateArea());
        System.out.println("Perimeter: " + calculatePerimeter());
    }
}

class Circle extends Shape {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    @Override
    public double calculateArea() {
        return Math.PI * radius * radius;
    }

    @Override
    public double calculatePerimeter() {
        return 2 * Math.PI * radius;
    }
}

class Square extends Shape {
    private double side;

    public Square(double side) {
        this.side = side;
    }

    @Override
    public double calculateArea() {
        return side * side;
    }

    @Override
    public double calculatePerimeter() {
        return 4 * side;
    }
}

class Rectangle extends Shape {
    private double length;
    private double width;

    public Rectangle(double length, double width) {
        this.length = length;
        this.width = width;
    }

    @Override
    public double calculateArea() {
        return length * width;
    }

    @Override
    public double calculatePerimeter() {
        return 2 * (length + width);
    }
}

class Rhombus extends Shape {
    private double diagonal1;
    private double diagonal2;
    private double side;

    // Two ways to construct a rhombus,
    // either by 2 dignals, or by side length and angle
    public Rhombus(double diagonal1, double diagonal2) {
        this.diagonal1 = diagonal1;
        this.diagonal2 = diagonal2;
        this.side = Math.sqrt(Math.abs(diagonal1 * diagonal1 - diagonal2 * diagonal2)) / 2;
    }

    public Rhombus(double side, double angle, boolean useAngle) {
        if (useAngle){
            this.side = side;
            this.diagonal1 = 2 * side * Math.cos(angle / 2);
            this.diagonal2 = 2 * side * Math.sin(angle / 2);
        } else {
            this.diagonal1 = side;
            this.diagonal2 = angle;
            this.side = Math.sqrt(Math.abs(diagonal1 * diagonal1 - diagonal2 * diagonal2)) / 2;
        }
    }

    @Override
    public double calculateArea() {
        return (diagonal1 * diagonal2) / 2.0;
    }

    @Override
    public double calculatePerimeter() {
        return 4 * side;
    }
}
```

</details>


## **002-学生管理程序**

<details>

<summary>
题目
</summary>

### **题目描述**

编写一个学生管理程序：
- 创建一个学生类（例如Student），具有“姓名”、“年龄”、“性别”、“籍贯”、“系别”、“所在学校”等属性。（考虑到学生可能转系或转学，有些属性可能会发生变化）。
- 创建北京大学的学生类（例如PkuStudent）、清华大学的学生类、师范大学学生类，他们是学生类的子类。能显示三所学校学生的具体信息。
- 创建北京大学信息管理系的学生类（例如ImStudent），它是北京大学的学生类的子类，除了能显示学生的基本信息以外，还能显示该系学生的特征（例如该特征是：“我就不信管不了你”）
- 创建主类，用具体的学生测试上述对象。（例如显示修改学生的相关属性）

</details>

<details>

<summary>
代码
</summary>

```java
public class Q2_StudentManage {
    public static void main(String[] args) {
        // Create an example PkuStudent
        System.out.println("----Test PkuStudent----\n");
        PkuStudent pkuStudent = new PkuStudent("Alice", 20, "Male", "Zhejiang", "Computer Science", "Peking University");
        System.out.println("Display info");
        pkuStudent.displayInfo();
        System.out.println("\nChange department to Information Management and display info");
        pkuStudent.setDepartment("Information Management");
        pkuStudent.displayInfo();

        // Create an example ImStudent
        System.out.println("\n----Test ImStudent----\n");
        ImStudent imStudent = new ImStudent("Bob", 22, "Female", "Beijing", "Information Management", "Peking University");
        System.out.println("Display info");
        imStudent.displayInfo();
        System.out.println("\nSet characteristic and display info");
        imStudent.setCharacteristic("我就不信管不了你");
        imStudent.displayInfo();
    }
}
class Student {
    private String name;
    private int age;
    private String gender;
    private String hometown;
    private String department;
    private String school;

    public Student(String name, int age, String gender, String hometown, String department, String school) {
        this.name = name;
        this.age = age;
        this.gender = gender;
        this.hometown = hometown;
        this.department = department;
        this.school = school;
    }

    public void displayInfo() {
        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
        System.out.println("Gender: " + gender);
        System.out.println("Hometown: " + hometown);
        System.out.println("Department: " + department);
        System.out.println("School: " + school);
    }

    public void setName(String newName) {
        name = newName;
    }

    public void setAge(int newAge) {
        this.age = newAge;
    }

    // Gender and hometown is unchangeable, 
    // so there is no method setGender and setHometown

    public void setDepartment(String newDepartment) {
        this.department = newDepartment;
    }

    public void setSchool(String newSchool) {
        this.school = newSchool;
    }
}

class PkuStudent extends Student {
    public PkuStudent(String name, int age, String gender, String hometown, String department, String school) {
        super(name, age, gender, hometown, department, school);
    }
}

class ThuStudent extends Student {
    public ThuStudent(String name, int age, String gender, String hometown, String department, String school) {
        super(name, age, gender, hometown, department, school);
    }
}

class BnuStudent extends Student {
    public BnuStudent(String name, int age, String gender, String hometown, String department, String school) {
        super(name, age, gender, hometown, department, school);
    }
}

class ImStudent extends PkuStudent {
    private String characteristic = "No characteristic now.";

    // Init without characteristic
    public ImStudent(String name, int age, String gender, String hometown, String department, String school) {
        super(name, age, gender, hometown, department, school);
    }

    public ImStudent(String name, int age, String gender, String hometown, String department, String school, String characteristic) {
        super(name, age, gender, hometown, department, school);
        this.characteristic = characteristic;
    }

    public void displayInfo() {
        super.displayInfo();
        System.out.println("Characteristic: " + characteristic);
    }

    public void setCharacteristic(String newCharacteristic) {
        this.characteristic = newCharacteristic;
    }
}
```

</details>

## **003-设备接口**

<details>

<summary>
    题目
</summary>

### **题目描述**

可以将智能手机看做是多种设备（电话、影音播放设备、相机）的组合，假定有一个智能手机具有电话拨号、影音播放、拍照功能。定义一个人，他可以使用智能手机，也可以分别使用电话、影音播放设备、相机等设备。请用程序模拟。

### **提示信息**

使用接口

</details>

<details>

<summary>
    代码
</summary>

```java
public class Q3_DeviceInterface {
    public static void main(String[] args) {
        Smartphone smartphone = new Smartphone();
        Person person = new Person();

        // Use the smartphone
        person.useSmartphone(smartphone, "123456789", "media-1");
        System.out.println("");
        // Use the telephone
        person.useTelephone(smartphone, "987654321");
        System.out.println("");
        // Use the media player
        person.useMediaPlayer(smartphone, "media-2");
        System.out.println("");
        // Use the camera
        person.useCamera(smartphone);
    }
}

// Define the telephone functionality interface
interface Telephone {
    void dial(String phoneNumber);
}

// Define the media player functionality interface
interface MediaPlayer {
    void play(String media);
}

// Define the camera functionality interface
interface Camera {
    void takePhoto();
}

// Define a smartphone class implementing multiple functionality interfaces
class Smartphone implements Telephone, MediaPlayer, Camera {
    @Override
    public void dial(String phoneNumber) {
        System.out.println("Dialing phone number: " + phoneNumber);
    }

    @Override
    public void play(String media) {
        System.out.println("Playing media: " + media);
    }

    @Override
    public void takePhoto() {
        System.out.println("Taking a photo");
    }
}

// Define a person class that can use a smartphone or individual devices like telephone, media player, or camera
class Person {
    public void useSmartphone(Smartphone smartphone, String phoneNumber, String media) {
        System.out.println("Person uses smartphone");
        smartphone.dial(phoneNumber);
        smartphone.play(media);
        smartphone.takePhoto();
    }

    public void useTelephone(Telephone telephone, String phoneNumber) {
        System.out.println("Person uses telephone");
        telephone.dial(phoneNumber);
    }

    public void useMediaPlayer(MediaPlayer mediaPlayer, String media) {
        System.out.println("Person uses media player");
        mediaPlayer.play(media);
    }

    public void useCamera(Camera camera) {
        System.out.println("Person uses camera");
        camera.takePhoto();
    }
}
```

</details>

## **004-矩阵计算**

<details>

<summary>
题目
</summary>

### **题目描述**

已知一个数值矩阵$A$为$\left[\begin{matrix}
    3 & 0 & 4 & 5 \\
    6 & 2 & 1 & 7 \\
    4 & 1 & 5 & 8
\end{matrix}\right]$，另一个矩阵$B$为$\left[\begin{matrix}
    1 & 4 & 0 & 3 \\
    2 & 5 & 1 & 6 \\
    0 & 7 & 4 & 4 \\
    9 & 3 & 6 & 0
\end{matrix}\right]
$，求出$A$与$B$的乘积矩阵$C[3][4]$并输出出来，其中$C$中的每个元素$C[i][j]=\sum A[i][k]*B[k][j]$。

### **提示信息**

用数组实现

</details>

<details>

<summary>
代码
</summary>

```java
public class Q4_MatrixOperation {
    public static void main(String[] args) {
        int[][] A = {
                {3, 0, 4, 5},
                {6, 2, 1, 7},
                {4, 1, 5, 8},
        };

        int[][] B = {
                {1, 4, 0, 3},
                {2, 5, 1, 6},
                {0, 7, 4, 4},
                {9, 3, 6, 0}
        };

        int[][] C = multiplyMatrices(A, B);

        System.out.println("Matrix C = A * B:");
        printMatrix(C);
    }

    public static int[][] multiplyMatrices(int[][] A, int[][] B) {
        int rowsA = A.length;
        int colsA = A[0].length;
        int colsB = B[0].length;

        int[][] C = new int[rowsA][colsB];

        for (int i = 0; i < rowsA; i++) {
            for (int j = 0; j < colsB; j++) {
                for (int k = 0; k < colsA; k++) {
                    C[i][j] += A[i][k] * B[k][j];
                }
            }
        }

        return C;
    }

    public static void printMatrix(int[][] matrix) {
        for (int i = 0; i < matrix.length; i++) {
            for (int j = 0; j < matrix[0].length; j++) {
                System.out.print(matrix[i][j] + " ");
            }
            System.out.println();
        }
    }
}
```

</details>

## **005-时区转换**

<details>

<summary>
题目
</summary>

### **题目描述**

编写一个时区时间的转换程序，对于北京、伦敦、巴黎、纽约等城市，指定任意一个城市，显示上述城市的当前时间，并显示其他城市比给定城市早或晚几个小时。

</details>

<details>

<summary>
代码
</summary>

```java
import java.time.LocalDateTime;
import java.time.ZoneId;
import java.time.format.DateTimeFormatter;
import java.time.Duration;
import java.util.HashMap;
import java.util.Map;

public class Q5_TimeConvert {
    private static Map<String, String> cityTimezones = new HashMap<>();

    public static void main(String[] args) {
        initCityTimezone();

        String selectedCity = "Beijing"; // Selected city
        
        LocalDateTime currentTime = getCityTime(selectedCity);
        // Display the current time for the selected city

        System.out.println("Current time in " + selectedCity + ": " + 
            currentTime.format(DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss"))
        );

        // Display the time difference for other cities relative to the selected city
        showDiff(selectedCity);
    }

    public static void initCityTimezone() {
        // Initialize the mapping of cities to time zones
        cityTimezones.put("Beijing", "Asia/Shanghai");
        cityTimezones.put("London", "Europe/London");
        cityTimezones.put("Paris", "Europe/Paris");
        cityTimezones.put("New York", "America/New_York");
    }

    public static LocalDateTime getCityTime(String selectedCity) {
        // Get the time zone for the selected city
        String selectedTimezone = cityTimezones.get(selectedCity);
        // Get the current time
        LocalDateTime currentTime = LocalDateTime.now(ZoneId.of(selectedTimezone));
        return currentTime;
    }

    public static void showDiff(String selectedCity) {
        LocalDateTime currentTime = getCityTime(selectedCity);
        for (Map.Entry<String, String> entry : cityTimezones.entrySet()) {
            String city = entry.getKey();

            if (!city.equals(selectedCity)) {
                LocalDateTime cityTime = getCityTime(city);
                Duration timeDiff = Duration.between(currentTime, cityTime);
                
                long hoursDiff = timeDiff.toHours();

                String timeDiffMsg = hoursDiff >= 0 ? "ahead" : "behind";
                hoursDiff = Math.abs(hoursDiff);

                System.out.println(city + " is " + hoursDiff + " hours " + timeDiffMsg + " " + selectedCity + ".");
            }
        }
    }
}
```

</details>