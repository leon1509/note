#### Stream - 去除偶数(filter应用) | https://www.liaoxuefeng.com/wiki/1252599548343744/1322402956967969
````
    public static void main(String[] args) {
        IntStream.of(1, 2, 3, 4, 5, 6, 7, 8, 9)
                .filter(n -> n % 2 != 0)
                .forEach(System.out::println);
    }
````

#### Stream - 平方计算 & 字符操作（去空格、变大写）
````
    public static void main(String[] args) {
        Stream<Integer> m1 = mapSequence();
        m1.forEach(System.out::println);

        changeString();
    }

    // 对x计算它的平方
    protected static Stream<Integer> mapSequence() {
        Stream<Integer> s = Stream.of(1, 2, 3, 4, 5);
        Stream<Integer> s2 = s.map(n -> n * n);
        return s2;
    }

    // 利用map()，不但能完成数学计算，对于字符串操作，以及任何Java对象都是非常有用的
    protected static void changeString() {
        List.of("  Apple ", " pear ", " ORANGE", " BaNaNa ")
                .stream()
                .map(String::trim) // 去空格
                .map(String::toUpperCase) // 变大写
                .forEach(System.out::println); // 打印
    }
````

#### Stream - 统计男生数量的优雅实现
````
Stream
Java 8 API添加了一个新的抽象称为流Stream，可以让你以一种声明的方式处理数据。使得代码调用起来更加优雅～ 直接来看代码：

public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student("张三", "男"));
        students.add(new Student("李四", "男"));
        students.add(new Student("小红", "女"));
        students.add(new Student("小花", "女"));
        students.add(new Student("小红", "女"));
        
        -------------------- before  --------------------
        //统计男生个数
        //传统的 for each 循环遍历
        long boyCount = 0;
        for (Student student : students) {
            if (student.isBoy()) {
                boyCount++;
            }
        }
 
        System.out.println("男生个数 = " + boyCount);
 
        -------------------- after (建议)  --------------------
 
        //统计男生个数
        //stream 流遍历
        long count = students.stream()
                .filter(Student::isBoy) // 等同于.filter(student -> student.isBoy())
                .count();
                
        System.out.println("男生个数 = " + boyCount);
}
相比与 传统的 For 循环，更推荐大家使用 stream 遍历。 stream 流的链式调用，还有许多骚操作，如 sorted, map, collect等操作符，可以省去不必要if-else，count等判断逻辑。
````

#### Stream - 从一组给定的LocalDate中过滤掉工作日，以便得到休息日
````
public class Main {
    public static void main(String[] args) {
        Stream.generate(new LocalDateSupplier())
                .limit(31)
                .filter(ldt -> ldt.getDayOfWeek() == DayOfWeek.SATURDAY || ldt.getDayOfWeek() == DayOfWeek.SUNDAY)
                .forEach(System.out::println);
    }
}

class LocalDateSupplier implements Supplier<LocalDate> {
    LocalDate start = LocalDate.of(2020, 1, 1);
    int n = -1;
    public LocalDate get() {
        n++;
        return start.plusDays(n);
    }
}
````

#### 数组排序
````
    public static void main(String[] args) {
        String[] array = new String[] { "Strawberry", "Apple", "Orange", "Banana", "Lemon", "Leaf", "Peach" };
        /*
        Arrays.sort(array, (s1, s2) -> {
            return s1.compareTo(s2);
        });
        */
        // 更简便的写法
        Arrays.sort(array, (s1, s2) -> s1.compareTo(s2));
        System.out.println(String.join(", ", array));
    }
````
