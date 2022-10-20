# Понимание JVM🌏🌏🌏

## Исходный код 💬💬💬


    public class JvmComprehension {

        public static void main(String[] args) {
            int i = 1;                      // 1
            Object o = new Object();        // 2
            Integer ii = 2;                 // 3
            printAll(o, i, ii);             // 4
            System.out.println("finished"); // 7
        }

        private static void printAll(Object o, int i, Integer ii) {
            Integer uselessVar = 700;                   // 5
            System.out.println(o.toString() + i + ii);  // 6
        }
    }

## Цель задания 💬💬💬
Проанализировать код выше и описать каждую строку с точки зрения происходящего в JVM

## Анализ кода 💬💬💬

Первым делом загружается класс JvmComprehension

        public class JvmComprehension {

В метаспейсе у нас будет храниться информация о загруженном классе JvmComprehension и информация о других системных загруженных классах.

Далее построчно:
1. В стек попадает метод main, открывается его frame
    
        public static void main(String[] args) {

 ![Фото1](https://github.com/PuccaGTS/JVM_Task1/blob/main/pic/1.png?raw=true)  

2. Во frame main попадаем переменная i со значением 1.
            
        public static void main(String[] args) {
            int i = 1;                      // 1
 ![Фото2](pic\2.png) 

3. В хипе происходит создание нового объекта и затем создается переменная "о" в frame main, которая ссылается на новый объект типа Oject.


        public static void main(String[] args) {
                    int i = 1;                      // 1
                    Object o = new Object();        // 2
![Фото3](pic\3.png) 

4. В хипе происходит создание нового объекта и затем создается переменная "ii" в frame main, которая ссылается на новый объект типа Integer со значением 2.


        public static void main(String[] args) {
                    int i = 1;                      // 1
                    Object o = new Object();        // 2
                    Integer ii = 2;                 // 3
![Фото4](pic\4.png) 

5. Далее в стэк памяти попадает метод printAll, вызывается метод с тремя параметрами, два из которых берет из кучи, а примитив берет из фрейма main.

        public static void main(String[] args) {
                    int i = 1;                      // 1
                    Object o = new Object();        // 2
                    Integer ii = 2;                 // 3
                    printAll(o, i, ii);             // 4
![Фото5](pic\5.png) 

6. Дополнительно в хипе происходит создание нового объекта и затем создается переменная "useLessVar" в frame printAll, которая ссылается на новый объект типа Integer со значением 700.

        private static void printAll(Object o, int i, Integer ii) {
                    Integer uselessVar = 700;                   // 5

![Фото6](pic\6.png)

7. Происходить печать переданных параметров, вывод их в консоль, после этого frame printAll будет закрыт. Здесь может прийти Уборщик мусора🧹🗑️🚜 и убрать из хипа объект Integer со значением 700, т.к. ссылок на этот объект больше не существует.

        private static void printAll(Object o, int i, Integer ii) {
                    Integer uselessVar = 700;                   // 5
                    System.out.println(o.toString() + i + ii);  // 6
![Фото7](pic\7.png)

8. Происходит вывод в консоль слова "finished" в frame main, после чего frame main закрывается. Здесь может прийти Уборщик мусора🧹🗑️🚜 и убрать из хипа объект Integer со значением 2 и объект типа Oject, т.к. ссылок на эти объект больше не существует.

    public static void main(String[] args) {
                int i = 1;                      // 1
                Object o = new Object();        // 2
                Integer ii = 2;                 // 3
                printAll(o, i, ii);             // 4
                System.out.println("finished"); // 7
            }
![Фото8](pic\8.png)
