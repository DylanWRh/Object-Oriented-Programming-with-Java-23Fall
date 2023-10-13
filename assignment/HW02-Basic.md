# **HW1 - Introduction**

注意：查找资料，了解Java注释的规定和约定，程序中要有清楚的注释。
参考资料：[Google Java Style Guide](https://google.github.io/styleguide/javaguide.html)

## **001-字符判断**
<details>

<summary>
题目
</summary>

### **题目描述**

给定一个字符类型的数据，判断它是字母还是数字，如果是字母，继续判断是大写字母或小写字母。将结果输出到控制台上。

### **提示信息**

提示：使用`Character`类的方法

</details>

<details>

<summary>
代码
</summary>

```java
import java.util.Scanner;

public class Q1_CharacterJudge {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Please enter a character:");
        char ch = scanner.next().charAt(0); // Get the character to be judged (the first character of input)
        CharacterJudger judger = new CharacterJudger(); // Define a new judger
        String result = judger.judge(ch); // Make judgement and get the result
        output(ch, result); // Output the result
    }
    
    public static void output(char ch, String result){
        System.out.format("The character '%c' is %s", ch, result);
    }
}

class CharacterJudger {
    /**
     * Judges whether a given character is letter or digit
     * @param ch the character to be judged
     * @return a string showing judging result
     */
    public String judge(char ch){
        String result = "";
        if (Character.isUpperCase(ch)) result = "an uppercase letter";
        else if (Character.isLowerCase(ch)) result = "a lowercase letter";
        else if (Character.isDigit(ch)) result = "a digit";
        else result = "neither a letter nor a digit";
        return result;
    }
}
```

</details>

## **002-素数判断**
<details>

<summary>
题目
</summary>

### **题目描述**

判断 101-200 之间有多少个素数，并输出所有素数。

### **提示信息**

素数又称质数，有无限个。一个大于1的自然数，除了1和它本身外，不能被其他自然数整除，换句话说就是该数除了1和它本身以外不再有其他的因数

</details>

<details>

<summary>
代码
</summary>

```java
public class Q2_PrimeJudge {
    public static void main(String[] args) {
        int start = 101, end = 200;
        output(start, end);
    }
    
    public static void output(int start, int end){
        int counter = 0; // Count the number of primes in [start, end]
        int[] primes = new int[end - start + 1]; // Record all primes in [start, end]
        PrimerJudger judger = new PrimerJudger();
        for (int i = start; i <= end; i++){
            if (judger.judge(i)){
                primes[counter++] = i; // When meets a prime, add it to the array
            }
        }
        System.out.format("There are %d primes between %d and %d.\n", counter, start, end);
        for (int i = 0; i < counter; i++){ // Output all primes
            System.out.print(primes[i] + ", ");
        }
    }
}

class PrimerJudger {
    /**
     * Judges whether a given number is prime
     * @param num the number to be judged
     * @return true of the number is prime
     */
    public boolean judge(int num){
        if (num <= 1) return false; // Special case
        for (int i = 2; i <= num / 2; i++){
            if (num % i == 0) return false;
        }
        return true;
    }
}
```

</details>

## **003-奖金计算**
<details>

<summary>
题目
</summary>

### **题目描述**

企业发放的奖金根据利润提成。利润`I`低于或等于10万元时，奖金可提10%；利润高于10万元，低于20万元时，低于10万元的部分按10%提成，高于10万元的部分，可提成7.5%；20万到40万之间时，高于20万元的部分，可提成5%；40万到60万之间时高于40万元的部分，可提成3%；60万到100万之间时，高于60万元的部分，可提成1.5%，高于100万元时，超过100万元的部分按1%提成，给定当月利润`I`，求应发放奖金总数？

### **提示信息**

用户通过控制台输入利润数额，程序输出奖金数额

</details>

<details>

<summary>
代码
</summary>

```java
import java.util.Scanner;

public class Q3_BonusCalc {
    public static void main(String args[]) {
        System.out.println("Please enter the value of profit (>= 0, unit: 10k yuan)");
        Scanner scanner = new Scanner(System.in);
        float profit = scanner.nextFloat(); // Get profile value
        BonusCalcer calcer = new BonusCalcer();
        float bonus = calcer.calc(profit); // Get bonus value
        output(profit, bonus); // Output the bonus value
    }
    public static void output(float profit, float bonus) {
        System.out.format("The profit is %.0f yuan, and the bonus is %.0f yuan", profit * 10000f, bonus * 10000f);
    }
}

class BonusCalcer {
    /**
     * Calculate bonus based on profit
     * @param profit a float number indicating profit
     * @return a float indicating the bonus
     */
    public float calc(float profit) {
        float[] profitPreCalc = new float[6];
        profitPreCalc[0] = 0f;
        profitPreCalc[1] = 0.1f * 10;
        profitPreCalc[2] = profitPreCalc[1] + 0.075f * 10;
        profitPreCalc[3] = profitPreCalc[2] + 0.05f * 20;
        profitPreCalc[4] = profitPreCalc[3] + 0.03f * 20;
        profitPreCalc[5] = profitPreCalc[4] + 0.015f * 40;
        if (profit <= 10)  return profitPreCalc[0] +   0.1f * profit;
        if (profit <= 20)  return profitPreCalc[1] + 0.075f * (profit - 10);
        if (profit <= 40)  return profitPreCalc[2] +  0.05f * (profit - 20);
        if (profit <= 60)  return profitPreCalc[3] +  0.03f * (profit - 40);
        if (profit <= 100) return profitPreCalc[4] + 0.015f * (profit - 60);
        return profitPreCalc[5] + 0.01f * (profit - 100);
    }
}
```

</details>

## **004-整数排序**
<details>

<summary>
题目
</summary>

### **题目描述**

给定三个整数`x`,`y`,`z`，请把这三个数由小到大输出

</details>

<details>

<summary>
代码
</summary>

```java
import java.util.Scanner;

public class Q4_IntSort {
    public static void main(String args[]) {
        System.out.println("Please enter 3 integers:");
        Scanner scanner = new Scanner(System.in);
        int x = scanner.nextInt();
        int y = scanner.nextInt();
        int z = scanner.nextInt();
        IntSorter sorter = new IntSorter(); // Create a new sorter
        sorter.setNumber(x, y, z); // Put x, y, z into the sorter
        sorter.sortInt();
        output(sorter.arrayInt);
    }
    public static void output(int[] arrayInt) {
        for (int i: arrayInt){ // use advanced for-loop to output numbers
            System.out.print(i + " ");
        } 
    }
}

class IntSorter {
    public int[] arrayInt = new int[3];
    public void setNumber(int x, int y, int z){
        arrayInt[0] = x;
        arrayInt[1] = y;
        arrayInt[2] = z;
    }
    public void sortInt(){
        // Do 3-element bubbling sort
        if (arrayInt[0] > arrayInt[1]) swap(0, 1);
        if (arrayInt[1] > arrayInt[2]) swap(1, 2);
        if (arrayInt[0] > arrayInt[1]) swap(0, 1);
    }
    /**
     * swap arrayInt[i] and arrayInt[j]
     * @param i first array index, 0 <= i <= 2
     * @param j second array index, 0 <= j <= 2
     */
    private void swap(int i, int j){
        int temp = arrayInt[i];
        arrayInt[i] = arrayInt[j];
        arrayInt[j] = temp;
    }
}
```

</details>

## **005-打印菱形**
<details>

<summary>
题目
</summary>

### **题目描述**

打印出如下图案（菱形）
```
   *
  ***
 *****
*******
 *****
  ***
   *
```

### **提示信息**

不能直接复制该图形通过`System.out.println`进行输出，需要通过循环等其他方式输出。

</details>

<details>

<summary>
代码
</summary>

```java
public class Q5_DiamondPrint {
    public static void main(String args[]) {
        output(7);
    }
    private static void output(int nLine) {
        int nLineHalf = nLine / 2;
        int lineLength = 2 * nLineHalf + 1;
        for (int i = 0; i <= nLineHalf; i++) {
            // Calculate numbers of stars and spaces for each line
            int numStar = 2 * i + 1;
            int numSpace = (lineLength - numStar) / 2;
            outputOneLine(numSpace, numStar);
        }
        for (int i = 0; i < nLineHalf; i++){
            // Calculate numbers of stars and spaces for each line
            int numSpace = i + 1;
            int numStar = lineLength - 2 * numSpace;
            outputOneLine(numSpace, numStar);
        }
    }
    /**
     * output one line based on given number of stars and number of spaces
     * @param numSpace number of spaces
     * @param numStar number of stars
     */
    private static void outputOneLine(int numSpace, int numStar){
        String resSpace = repeatString(" ", numSpace);
        String resStar = repeatString("*", numStar);
        String res = resSpace + resStar + resSpace;
        System.out.println(res);
    }
    /**
     * repeat a string for n times and return
     * @param str the string to be repeated
     * @param n the number to repeat
     * @return the repeated string
     */
    private static String repeatString(String str, int n){
        return new String(new char[n]).replace("\0", str);
    }
}
```

</details>

## **006-基本运算**
<details>

<summary>
题目
</summary>

### **题目描述**

设`x=2.5`，`a=7`，`y=4.7`，计算表达式`x+a%3*(int)(x+y)%2/4`的值，并在程序注释中说明为什么会得出这样的值。

</details>

<details>

<summary>
代码
</summary>

```java
public class Q6_ValueCalc {
    /*
     * The output is 2.5
     * Explanation:
     *   x + a % 3 * (int)(x + y) % 2 /4 
     * = x + (Some Integer) % 2 / 4
     * = x + (0 or 1) / 4
     * = x
     * So the result is x = 2.5
     */
    public static void main(String args[]) {
        float x = 2.5f, y = 4.7f;
        int a = 7;
        System.out.println(x + a % 3 * (int)(x + y) % 2 / 4);
    }
}
```

</details>

## **007-九九乘法表**
<details>

<summary>
题目
</summary>

### **题目描述**

编写打印九九乘法表的程序

</details>

<details>

<summary>
代码
</summary>

```java
public class Q7_MultiplicationTable {
    public static void main(String args[]) {
        printTable(9);
    }
    public static void printTable(int n){
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= i; j++){
                System.out.print(j+"*"+i+"="+(j*i)+"\t");
            }
            System.out.println();
        }
    }
}
```

</details>

## **008-小球弹跳**
<details>

<summary>
题目
</summary>

### **题目描述**

一球从100米高度自由落下，每次落地后反跳回原高度的一半；再落下，求它在第10次落地时，共经过多少米？第10次反弹多高？

</details>

<details>

<summary>
代码
</summary>

```java
public class Q8_BallBounce {
    static double totDistance = 0;
    static double finalHeight = 0;
    public static void main(String args[]) {
        updateData(100.0, 10);
        outputData(10);
    }
    /**
     * Update totDistance and curHeight, given number of bounces
     * @param n number of bounces
     */
    private static void updateData(double initHeight, int n) {
        double curHeight = initHeight;
        for (int i = 0; i < n; i++){
            if (i == 0) totDistance += curHeight;
            else totDistance += 2 * curHeight;
            curHeight = getNextHeight(curHeight);
        }
        finalHeight = curHeight;
    }
    private static double getNextHeight(double prevHeight) {
        return prevHeight / 2;
    }
    private static void outputData(int n){
        System.out.format("After %d bounces, total distance is %.8fm\n", n, totDistance);
        System.out.format("After %d bounces, the ball can reach %.8fm high", n, finalHeight);
    }
}
```

</details>

## **009-日期计算**
<details>

<summary>
题目
</summary>

### **题目描述**

输入某年某月某日，判断这一天是这一年的第几天

### **提示信息**

闰年的判断，可根据以下三点进行判断。
- 普通年能被4整除且不能被100整除的为闰年。(如2004年就是闰年,1900年不是闰年)
- 世纪年能被400整除的是闰年。(如2000年是闰年，1900年不是闰年)
- 对于数值很大的年份,这年如果能整除3200,并且能整除172800则是闰年。如172800年是闰年，86400年不是闰年(因为虽然能整除3200，但不能整除172800)


</details>

<details>

<summary>
代码
</summary>

```java
import java.util.Scanner;

public class Q9_DateCalc {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Enter the year: ");
        int year = scanner.nextInt();
        System.out.print("Enter the month: ");
        int month = scanner.nextInt();
        System.out.print("Enter the day: ");
        int day = scanner.nextInt();
        DateCalculator dateCalculator = new DateCalculator();
        if (dateCalculator.isValidDate(year, month, day)){
            int dayOfYear = dateCalculator.getDayOfYear(year, month, day);
            output(dayOfYear);
        }
        else output(-1); // Use -1 to mark invalid date input
    }
    private static void output(int dayOfYear){
        if (dayOfYear < 0) {
            System.out.println("Invalid date input.");
            return;
        }
        String suffix = "th";
        if (dayOfYear % 10 == 1 && dayOfYear % 100 != 11) {
            suffix = "st";
        } else if (dayOfYear % 10 == 2 && dayOfYear % 100 != 12) {
            suffix = "nd";
        } else if (dayOfYear % 10 == 3 && dayOfYear % 100 != 13) {
            suffix = "rd";
        }
        System.out.println("This day is the " + dayOfYear + suffix + " day of the year.");
    }
}

class DateCalculator {
    final int[] daysInMonth = {0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};

    public int getDayOfYear(int year, int month, int day) {
        int dayOfYear = day;
        for (int i = 1; i < month; i++) {
            dayOfYear += daysInMonth[i];
        }
        if (isLeapYear(year) && month > 2) {
            dayOfYear++;
        }
        return dayOfYear;
    }
    /**
     * Check if year is leap
     * @param year
     * @return true if year is leap
     */
    private boolean isLeapYear(int year) {
        // Leap year if it's divisible by 4 but not by 100
        // or if it's a century year divisible by 400
        if (year < 3200) return ((year % 4 == 0 && year % 100 != 0) || (year % 400 == 0));
        // Very large year is if it's divisible by 3200 and also by 172800
        return (year % 3200 == 0 && year % 172800 == 0);
    }
    /**
     * Check if date is valid
     */
    public boolean isValidDate(int year, int month, int day) {
        if (year < 1 || month < 1 || month > 12 || day < 1 || day > 31) {
            return false;
        }

        int maxDays = daysInMonth[month];
        if (month == 2 && isLeapYear(year)) {
            maxDays = 29; // February has 29 days in a leap year
        }

        return (day <= maxDays);
    }
}

```

</details>

## **010-求式子的值**
<details>

<summary>
题目
</summary>

### **题目描述**

已知$S=1-\dfrac{1}{2}+\dfrac{1}{3}-\dfrac{1}{4}+\cdots+\dfrac{(-1)^{n-1}}{n}$，利用循环编程求解n=100时的S值。

### **提示信息**

用两种及以上循环语句分别实现

</details>

<details>

<summary>
代码
</summary>

```java
public class Q10_SeriesSum {
    public static void main(String[] args) {
        int n = 100;
        // Create a SeriesCalculator instance
        SeriesSumCalculator seriesCalculator = new SeriesSumCalculator();
        // Use a for loop
        double sumForLoop = seriesCalculator.calculateSumForLoop(n);
        System.out.println("The value of S for n = " + n + " using a for loop: " + sumForLoop);
        // Use a while loop
        double sumWhileLoop = seriesCalculator.calculateSumWhileLoop(n);
        System.out.println("The value of S for n = " + n + " using a while loop: " + sumWhileLoop);
    }
}

class SeriesSumCalculator {
    /**
     * Calculate the series sum up to a given number using a for loop.
     * @param n The number of terms in the series.
     * @return The sum of the series.
     */
    public double calculateSumForLoop(int n) {
        double sum = 0;
        for (int i = 1; i <= n; i++) {
            double term = ((i % 2 == 0) ? -1.0 : 1.0) / i;
            sum += term;
        }
        return sum;
    }
    /**
     * Calculate the series sum up to a given number using a while loop.
     * @param n The number of terms in the series.
     * @return The sum of the series.
     */
    public double calculateSumWhileLoop(int n) {
        double sum = 0;
        int i = 1;
        while (i <= n) {
            double term = ((i % 2 == 0) ? -1.0 : 1.0) / i;
            sum += term;
            i++;
        }
        return sum;
    }
}
```

</details>
