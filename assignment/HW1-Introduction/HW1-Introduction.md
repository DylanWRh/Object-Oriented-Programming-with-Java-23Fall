# **HW1 - Introduction**

## **001-Java特征**
<details>

<summary>
题目
</summary>

### **题目描述**

写一个程序，分行输出JAVA的主要特点（JAVA的特点请自行总结）

### **提示信息**

使用语句：`System.out.println();`
`System`是一个类，继承自根类`Object`
`out`是类`PrintStream`类实例化的一个对象，且是`System`类的静态成员变量
`println()`是类`PrintStream`的成员方法，被对象`out`调用

</details>

<details>

<summary>
代码
</summary>

```java
public class Q1_JavaFeature {
    public static void main(String[] args){
        System.out.println("1. 简单");
        System.out.println("2. 面向对象");
        System.out.println("3. 分布式");
        System.out.println("4. 健壮性");
        System.out.println("5. 结构中立");
        System.out.println("6. 安全性");
        System.out.println("7. 可移植");
        System.out.println("8. 解释性");
        System.out.println("9. 高性能");
        System.out.println("10. 多线程");
        System.out.println("11. 动态性");
    }
}
```

</details>

## **002-猜数游戏**
<details>

<summary>
题目
</summary>

### **题目描述**

利用JAVA写一个猜数游戏，游戏简介参考[介绍文档](猜数游戏.pdf)。

</details>

<details>

<summary>
代码
</summary>

```java

import java.util.Scanner;
import java.util.Random;

public class Q2_HiLoGame {
    public static void main(String[] args){
        Scanner scanner = new Scanner(System.in);
        long seed = getInt(scanner, "Enter a seed number (If less than 0, time will be used as seed):");
        
        // Step 1. Ask the user to input a seed number
        if (seed < 0) {
            // Negative, use the computer time for initialization
            seed = System.currentTimeMillis();
        }
        Random random = new Random(seed);

        // Step 2. Ask whether the user wants to start a game
        String yes_or_no = "";
        int target = 0;
        int max_guess = 6;
        while (true){
            // Read the empty line after the seed
            System.out.println("Do you want to play a Hi-Lo game (Y or N)? ");
            // Game ends with any input other than Y and y
            yes_or_no =  scanner.nextLine();
            if (!(yes_or_no.equals("y") || yes_or_no.equals("Y"))) {
                break;
            }
            // Step 3. Start the game
            // Task 1. Randomly generate a secret number between 1 and 100 inclusive
            target = random.nextInt(100) + 1;
            // Task 2. Repeatedly accept the user’s guess
            int guess = 0, lower_bound = 1, upper_bound = 100;
            int i = 0;
            for (i = 0; i < max_guess; i++){
                guess = getGuess(scanner, lower_bound, upper_bound);
                if (guess == target) {
                    // Success, print the number of tries
                    System.out.format("You guessed it in %d tries.\n", i + 1);
                    break;
                }
                else if (guess > target) {
                    upper_bound = guess - 1;
                    System.out.println("Your guess is HI.");
                }
                else {
                    lower_bound = guess + 1;
                    System.out.println("Your guess is LO.");
                }
            }
            // Fail, print a losing message
            if (i == 6){
                System.out.format("You lost. Secret No. was %d.\n", target);
            }
        }
    }

    private static int getInt(Scanner scanner, String hint) {
        String res = null;
        System.out.println(hint);
        while((res = scanner.nextLine()) != null){
            if (isInt(res)){
                return Integer.parseInt(res);
            } else {
                System.out.println("Invalid Input: Must be integer.");
                System.out.println(hint);
            }
        }
        return 0;
    }

    private static boolean isInt(String str){
        try {
            Integer.parseInt(str);
            return true;
        } catch (NumberFormatException e) {
            return false;
        }
    }

    private static int getGuess(Scanner scanner, int lower_bound, int upper_bound) {
        int guess = lower_bound - 1;
        while (true){
            guess = getInt(scanner, String.format("Next Guess (%d-%d): ", lower_bound, upper_bound));
            // Invalid range input
            if ((guess < lower_bound) || (guess > upper_bound)){
                System.out.format("Invalid Input: Must be between %d and %d.\n", lower_bound, upper_bound);
            } else {
                return guess;
            }
        }
    }
}
```

</details>
