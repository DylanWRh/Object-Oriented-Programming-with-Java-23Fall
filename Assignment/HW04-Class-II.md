# **HW4 - Class II**

注意：查找资料，了解Java注释的规定和约定，程序中要有清楚的注释。
参考资料：[Google Java Style Guide](https://google.github.io/styleguide/javaguide.html)

## **000-有用的`.java`文件**

<details>

<summary>
<code>ArrayProcessor.java</code>
</summary>

在`002-元素排序`、`003-元素交换`中被使用
```java
import java.util.ArrayList;

public class ArrayProcessor <T>{
    private ArrayList<T> arrayList = new ArrayList<>();

    public void addElement(T t) {
        arrayList.add(t);
    }
    
    public void insertElement(int n, T t) {
        arrayList.add(n, t);
    }

    public void sortArray() {
        arrayList.sort(null);
    }

    public void printArray() {
        for (T element: arrayList) {
            System.out.print(element+" ");
        }
        System.out.println("");
    }

    public void swapElement(int m, int n) {
        T tmp1 = arrayList.get(m);
        T tmp2 = arrayList.get(n);
        arrayList.set(m, tmp2);
        arrayList.set(n, tmp1);
    }
}
```

</details>

## **001-矩阵计算**

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

用集合实现

</details>

<details>

<summary>
代码
</summary>

```java
import java.util.ArrayList;

public class Q1_MatrixOperation {
    public static void main(String[] args) {
        // Build Matrix A
        ArrayList<ArrayList<Integer>> A = new ArrayList<>();
        ArrayList<Integer> ALine = new ArrayList<>();
        ALine.add(3); ALine.add(0); ALine.add(4); ALine.add(5); A.add(ALine);
        ALine = new ArrayList<>();
        ALine.add(6); ALine.add(2); ALine.add(1); ALine.add(7); A.add(ALine);
        ALine = new ArrayList<>();
        ALine.add(4); ALine.add(1); ALine.add(5); ALine.add(8); A.add(ALine);

        // Build Matrix B
        ArrayList<ArrayList<Integer>> B = new ArrayList<>();
        ArrayList<Integer> BLine = new ArrayList<>();
        BLine.add(1); BLine.add(4); BLine.add(0); BLine.add(3); B.add(BLine);
        BLine = new ArrayList<>();
        BLine.add(2); BLine.add(5); BLine.add(1); BLine.add(6); B.add(BLine);
        BLine = new ArrayList<>();
        BLine.add(0); BLine.add(7); BLine.add(4); BLine.add(4); B.add(BLine);
        BLine = new ArrayList<>();
        BLine.add(9); BLine.add(3); BLine.add(6); BLine.add(0); B.add(BLine);

        ArrayList<ArrayList<Integer>> C = multiplyMatrices(A, B);

        System.out.println("Matrix C = A * B:");
        printMatrix(C);
    }

    public static ArrayList<ArrayList<Integer>> multiplyMatrices(
        ArrayList<ArrayList<Integer>> A, 
        ArrayList<ArrayList<Integer>> B
    ) {
        int colsA = A.get(0).size();
        int colsB = B.get(0).size();

        ArrayList<ArrayList<Integer>> C = new ArrayList<>();

        for (ArrayList<Integer> rowA: A) {
            ArrayList<Integer> CLine = new ArrayList<>();
            for (int j = 0; j < colsB; j++) {
                int CElement = 0;
                for (int k = 0; k < colsA; k++) {
                    CElement += rowA.get(k) * B.get(k).get(j);
                }
                CLine.add(CElement);
            }
            C.add(CLine);
        }

        return C;
    }

    public static void printMatrix(ArrayList<ArrayList<Integer>> matrix) {
        for (ArrayList<Integer> matrixRow: matrix) {
            for (int matrixElement: matrixRow) {
                System.out.print(matrixElement + " ");
            }
            System.out.println();
        }
    }
}
```

</details>

## 002-元素排序

<details>

<summary>
题目
</summary>

### **题目描述**

给定一个数组，按元素的自然顺序排序并输出，现输入一个元素，要求按照排序规律将它插入数组中，并再次输出结果。

### **提示信息**

用集合实现

</details>

<details>

<summary>
代码
</summary>

```java
import java.util.Scanner;

public class Q2_ArraySortAndInsert {
    public static void main(String[] args) {
        // Create an ArrayProcessor
        ArrayProcessor<Integer> intArrayProcessor = new ArrayProcessor<>();
        ArrayProcessor<Float> floatArrayProcessor = new ArrayProcessor<>();

        // Read int elements from stdin
        Scanner scanner = new Scanner(System.in);
        System.out.println("Input integers separated by space:");
        String input = scanner.nextLine();
        String[] inputIntArray = input.split(" ");
        for (String intStr : inputIntArray) {
            int intNum = Integer.parseInt(intStr);
            intArrayProcessor.addElement(intNum);
        }

        // Read float elements from stdin
        System.out.println("Input floats separated by space:");
        input = scanner.nextLine();
        inputIntArray = input.split(" ");
        for (String floatStr : inputIntArray) {
            float floatNum = Float.parseFloat(floatStr);
            floatArrayProcessor.addElement(floatNum);
        }

        // Print initial arrays
        System.out.println("***Initial integer array***");
        intArrayProcessor.printArray();
        System.out.println("***Initial float array***");
        floatArrayProcessor.printArray();
        
        // Sort and print
        intArrayProcessor.sortArray();
        System.out.println("***Sorteed integer array***");
        intArrayProcessor.printArray();
        floatArrayProcessor.sortArray();
        System.out.println("***Sorteed float array***");
        floatArrayProcessor.printArray();

        // Input elements to insert
        System.out.println("Input an integer to insert:");
        int newIntElement = scanner.nextInt();
        System.out.println("Input a float to insert:");
        float newFloatElement = scanner.nextFloat();

        // Insert, sort and print int array
        intArrayProcessor.addElement(newIntElement);
        intArrayProcessor.sortArray();
        System.out.println("***Integer array after insertion***");
        intArrayProcessor.printArray();

        // Insert, sort and print float array
        floatArrayProcessor.addElement(newFloatElement);
        floatArrayProcessor.sortArray();
        System.out.println("***Float array after insertion***");
        floatArrayProcessor.printArray();
    }   
}
```

</details>

## 003-元素交换

<details>

<summary>
题目
</summary>

### **题目描述**

给定一个数组，用程序实现交换两个指定的元素，并将输出交换前和交换后的元素及其位置，请用程序测试。

### **提示信息**

使用泛型和集合

</details>

<details>

<summary>
代码
</summary>

```java
public class Q3_ArraySwap {
    public static void main(String[] args) {
        // Create ArrayProcessors
        ArrayProcessor<Integer> intArrayProcessor = new ArrayProcessor<>();
        ArrayProcessor<Float> floatArrayProcessor = new ArrayProcessor<>();

        // Initializa arrays
        for (int i=0; i<5; i++) {
            intArrayProcessor.addElement(i);
            floatArrayProcessor.addElement((float)i);
        }

        // Print initial arrays
        System.out.println("Initial integer aray");
        intArrayProcessor.printArray();
        System.out.println("Initial float aray");
        floatArrayProcessor.printArray();

        // Swap items
        System.out.println("Swap numbers at 1 and 2 of integer array");
        intArrayProcessor.swapElement(1, 2);
        System.out.println("Swapped integer aray");
        intArrayProcessor.printArray();

        System.out.println("Swap numbers at 3 and 4 of float array");
        floatArrayProcessor.swapElement(3, 4);
        System.out.println("Swapped float aray");
        floatArrayProcessor.printArray();
    }
}
```

</details>

## 004-反射机制

<details>

<summary>
题目
</summary>

### **题目描述**

设计一个类，用反射机制显示出该类所具有的属性和方法

</details>

<details>

<summary>
代码
</summary>

```java
import java.lang.reflect.Field;
import java.lang.reflect.Method;
import java.lang.reflect.Constructor;

public class Q4_Reflection {
    // Use the class ArrayProcesor<Integer>
    public static void main(String[] args) {
        // Get class information
        Class<MyClass> myClassClass = MyClass.class;

        // Display attributes
        System.out.println("Attributes of MyClass:");
        Field[] fields = myClassClass.getDeclaredFields();
        for (Field field : fields) {
            System.out.println("Field name: " + field.getName() + ", type: " + field.getType());
        }

        // Display methods
        System.out.println("\nMethods of MyClass:");
        Method[] methods = myClassClass.getDeclaredMethods();
        for (Method method : methods) {
            System.out.println("Method name: " + method.getName() + ", return type: " + method.getReturnType());
        }

        // Display construct methods
        System.out.println("\nConstructors of MyClass:");
        Constructor<?>[] constructors = myClassClass.getDeclaredConstructors();
        for (Constructor<?> constructor : constructors) {
            System.out.println("Method name: " + constructor.getName());
        }
    }
}

class MyClass {
    private int privateVar;
    public String publicVar;

    MyClass() {}
    protected MyClass(int var) {}
    private void foo() {}
    public int bar() {return 1;}
}
```

</details>

## 005-英文诗处理器

<details>

<summary>
题目
</summary>

### **题目描述**

设计一个英文诗处理器类，该类需实现如下方法
- 分词
  - 参数为`String`，将输入的参数`String`中`\n`（换行）和标点符号（`,.;!:'`）替换为空格，古代英语转化为现代英语，这里仅替换`thou`和`thee`为`you`。然后根据“空格”对文本进行分割，并返回切割后的数组，分割后的数组是一个类型为`String []`数组
    - 为简单起见，原本包含`thou`的单词也直接将其中的`thou`替换为`you`即可，如`thousand`也转换为`yousand`后进行处理
    - 假如方法的参数为`"Hello\nI'm Kyle!"`，那么返回的结果应为一个包含4个`String`对象的数组`{Hello, I, m, Kyle}`
    - 假如方法的参数为`"I need thee"`，那么返回的结果应为`{I, need, you}`
  - 提示：需用到`String`对象的`replace`和`split`方法
- 词频统计
  - 参数为一个`String[]`单词数组，统计该数组中的词的词频，并返回一个`Map<String, Integer>`类型，其中`key`为单词本身，`value`为词频
    - 假如方法输入字符串`{how, are, you, fine, and, you}`，那么返回的结果应为`{are=1, how=1, you=2, fine=1, and=1}`
  - 提示：在使用`HashMap`时，首先需要使用`contains`方法判断当前`HashMap`是否存在当前需要处理的`key`，若不存在时使用`get`方法取回，返回的对象是`null`。与数组不同，`HashMap`本身的`toString`方法会返回格式化后的`Map`内容，而不是内存引用位置，因此可直接将`HashMap`放与`System.out.print()`中用于调试程序
- 排序
  - 参数为`Map<String, Integer>`，其中`String`为单词，`Integer`为其词频，按照词频降序将该`Map`输出到标准输出，当词频相同时，按照单词字母顺序升序输出
    - 假如方法输入为`{are=1, how=1, you=2, fine=1, and=1}`，应输出`{you=2, and=1, are=1, fine=1, how=1}`
  - 提示：创建一个内部类，用于存储词和词频，实现`Comparable`接口的`compareTo`方法，依次对比词频和单词

### **输入样例**

```
O my Luve's like a red, red rose\nThat's newly sprung in June;\nO my Luve's like the melodie\nThat's sweetly play'd in tune.\n\nAs fair art thou, my bonnie lass,\nSo deep in luve am I:\nAnd I will luve thee still, my dear,\nTill a' the seas gang dry:\n\nTill a' the seas gang dry, my dear,\nAnd the rocks melt wi' the sun:\nI will luve thee still, my dear,\nWhile the sands o' life shall run.\n\nAnd fare thee weel, my only Luve\nAnd fare thee weel, a while!\nAnd I will come again, my Luve,\nTho' it were ten thousand mile.
```

### **输出样例**
```
{my=8, the=6, And=5, you=5, I=4, Luve=4, a=4, s=4, dear=3, in=3, luve=3, will=3, O=2, That=2, Till=2, dry=2, fare=2, gang=2, like=2, red=2, seas=2, still=2, weel=2, As=1, June=1, So=1, Tho=1, While=1, again=1, am=1, art=1, bonnie=1, come=1, d=1, deep=1, fair=1, it=1, lass=1, life=1, melodie=1, melt=1, mile=1, newly=1, o=1, only=1, play=1, rocks=1, rose=1, run=1, sands=1, shall=1, sprung=1, sun=1, sweetly=1, ten=1, tune=1, were=1, while=1, wi=1, yousand=1}
```

</details>

<details>

<summary>
代码
</summary>

```java
import java.util.Arrays;
import java.util.HashMap;
import java.util.Map;
import java.util.List;
import java.util.Collections;
import java.util.AbstractMap;
import java.util.ArrayList;

public class Q5_PoemProcess {
    public static void main(String[] args) {

        test();

        String poem = PoemGenerator.poem;
        PoemProcessor poemProcessor = new PoemProcessor(poem);

        // Split words
        poemProcessor.split();
        // Printer.printArray(poemProcessor.getSplittedPoem());

        // Count word frequency
        poemProcessor.countWordFreq();
        // System.out.println(poemProcessor.wordFreq);

        // Sort
        List<Map.Entry<String, Integer>> sortedWordFreq = poemProcessor.getSortedWordFreq();
        System.out.println(sortedWordFreq);
    }

    public static void test() {
        testSplit();
        testCountWordFreq();
        testgetSortedFreq();
    }

    public static void testSplit() {
        String poem1 = "Hello\nI'm Kyle!";  // (1.b) Testcase 
        String poem2 = "I need thee";       // (1.c) Testcase
        PoemProcessor poemProcessor1 = new PoemProcessor(poem1);
        PoemProcessor poemProcessor2 = new PoemProcessor(poem2);
        String[] poemSplit1 = poemProcessor1.getSplittedPoem();
        String[] poemSplit2 = poemProcessor2.getSplittedPoem();
        String[] trueSplit1 = {"Hello", "I", "m", "Kyle"};
        String[] trueSplit2 = {"I", "need", "you"};

        if (Arrays.equals(poemSplit1, trueSplit1) &&  Arrays.equals(poemSplit2, trueSplit2)) {
            System.out.println("Splitting test passed!");
        } else {
            System.out.println("Splitting test error!");
        }
    }

    public static void testCountWordFreq() {
        String[] words = {"how", "are", "you", "fine", "and", "you"};
        Map<String, Integer> wordFreq = PoemProcessor.countWordFreq(words);
        Map<String, Integer> trueWordFreq = new HashMap<>();
        trueWordFreq.put("how", 1);
        trueWordFreq.put("are", 1);
        trueWordFreq.put("fine", 1);
        trueWordFreq.put("and", 1);
        trueWordFreq.put("you", 2);

        if (trueWordFreq.equals(wordFreq)) {
            System.out.println("CountWordFreq test passed!");
        } else {
            System.out.println("CountWordFreq test error!");
        }
    }

    public static void testgetSortedFreq() {
        Map<String, Integer> wordFreq = new HashMap<>();
        wordFreq.put("how", 1);
        wordFreq.put("are", 1);
        wordFreq.put("fine", 1);
        wordFreq.put("and", 1);
        wordFreq.put("you", 2);
        List<Map.Entry<String, Integer>> sortedWordFreq = PoemProcessor.getSortedWordFreq(wordFreq);

        List<Map.Entry<String, Integer>> trueSortedWordFreq = new ArrayList<>(wordFreq.entrySet());
        trueSortedWordFreq.set(0, new AbstractMap.SimpleEntry<>("you", 2));
        trueSortedWordFreq.set(1, new AbstractMap.SimpleEntry<>("and", 1));
        trueSortedWordFreq.set(2, new AbstractMap.SimpleEntry<>("are", 1));
        trueSortedWordFreq.set(3, new AbstractMap.SimpleEntry<>("fine", 1));
        trueSortedWordFreq.set(4, new AbstractMap.SimpleEntry<>("how", 1));

        if (trueSortedWordFreq.equals(sortedWordFreq)) {
            System.out.println("GSortedFreq test passed!");
        } else {
            System.out.println("GSortedFreq test error!");
        }
    }
}

class PoemProcessor {
    String poem;
    String[] poemSplit = null;
    Map<String, Integer> wordFreq = null;

    public PoemProcessor(String poem) {
        // (1.a) Replace "thou" and "thee" with you
        this.poem = poem;
        this.poem = this.poem.replace("thou", "you");
        this.poem = this.poem.replace("thee", "you");
    }

    public void replace(String target, String replacement) {
        poem = poem.replace(target, replacement);
    }

    public void replace(String[] targets, String replacement) {
        for (String target: targets) {
            this.replace(target, replacement);
        }
    }

    public void split() {
        String[] targets = {"\n", ",", ".", ":", ";", "!", "'"};
        String replacement = " ";
        this.replace(targets, replacement);
        poemSplit = poem.split("[ ]+");
    }

    public String[] getSplittedPoem() {
        if (this.poemSplit == null) {
            this.split();
        }
        return poemSplit;
    }

    // (2) Count frequency of words
    public void countWordFreq() {
        wordFreq = countWordFreq(poemSplit);
    }

    // (2) Count frequency of words
    static public Map<String, Integer> countWordFreq(String[] words) {
        Map<String, Integer> wordFreq = new HashMap<>();
        for (String word: words) {
            wordFreq.put(word, wordFreq.getOrDefault(word, 0) + 1);
        }
        return wordFreq;
    }

    // (3) Sorting
    static public List<Map.Entry<String, Integer>> getSortedWordFreq(Map<String, Integer> wordFreqMap) {
        List<Map.Entry<String, Integer>> sortedWordFreq = new ArrayList<>(wordFreqMap.entrySet());

        // Sort the list based on frequency (descending) and word (ascending)
        Collections.sort(sortedWordFreq, (a, b) -> {
            int freqCompare = b.getValue().compareTo(a.getValue());
            if (freqCompare != 0) {
                return freqCompare; // Sort by frequency in descending order
            }
            return a.getKey().compareTo(b.getKey()); // Sort by word in ascending order
        });

        return sortedWordFreq;
    }

    public List<Map.Entry<String, Integer>> getSortedWordFreq() {
        return getSortedWordFreq(this.wordFreq);
    }
}

class PoemGenerator {
    static public String poem = //
                "O my Luve's like a red, red rose\n" + //
                "That's newly sprung in June;\n" + //
                "O my Luve's like the melodie\n" + //
                "That's sweetly play'd in tune.\n" + //
                "\n" + //
                "As fair art thou, my bonnie lass,\n" + //
                "So deep in luve am I:\n" + //
                "And I will luve thee still, my dear,\n" + //
                "Till a' the seas gang dry:\n" + //
                "\n" + //
                "Till a' the seas gang dry, my dear,\n" + //
                "And the rocks melt wi' the sun:\n" + //
                "I will luve thee still, my dear,\n" + //
                "While the sands o' life shall run.\n" + //
                "\n" + //
                "And fare thee weel, my only Luve\n" + //
                "And fare thee weel, a while!\n" + //
                "And I will come again, my Luve,\n" + //
                "Tho' it were ten thousand mile.";
}

class Printer {
    static public <T> void printArray(T[] arrayT) {
        System.out.print("{");
        for (T arrayElement: arrayT){
            System.out.print(arrayElement + ", ");
        }
        System.out.println("}");
    }
}
```

</details>

