#### 统计男生数量的优雅实现
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
