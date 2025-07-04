# Исследование кода.

```
public class JvmComprehension { // Загружается класс JvmComprehension через ClassLoader. В метаспейсе создается запись о классе, его методы и поля.

    public static void main(String[] args) { // 0. Вызов метода main. Создается фрейм в стеке для метода main.
        int i = 1;                           // 1. В локальных переменных фрейма main создается переменная i типа int. Значение 1 хранится прямо в стеке.
        Object o = new Object();             // 2. Создается объект Object. В хипе выделяется память под новый объект. Внутри — метаданные объекта и его таблица методов.
                                             //    В локальных переменных main создается ссылка o, которая указывает на этот объект в хипе.
        Integer ii = 2;                      // 3. Создается объект типа Integer. В хипе выделяется память под объект Integer.
                                             //    Это происходит через вызов Integer.valueOf(2).
                                             //    В локальных переменных main создается ссылка ii, указывающая на этот объект.
        printAll(o, i, ii);                  // 4. Вызывается статический метод printAll - в стеке создается новый фрейм для этого метода.
                                             //    В нем сохраняются параметры: ссылки на объекты o, ii, а также значение примитивной переменной i.
        System.out.println("finished");      // 7. Аналогично пункту 6, с разницей в том, что тут методу передается литерал из метаспейса.
    }

    private static void printAll(Object o, int i, Integer ii) {
        Integer uselessVar = 700;                   // 5. Создается новый объект типа Integer. В хипе выделяется память под этот объект.
                                                    //    В локальных переменных фрейма метода сохраняется ссылка на него - переменная uselessVar.
        System.out.println(o.toString() + i + ii);  // 6. Вызывается метод toString() у объекта, на который ссылается переменная o.
                                                    //    Это вызывает обращение к метаданным класса и выполнение метода внутри JVM. Результат — строка.
                                                    //    Далее - операция конкатенации строковых значений - также внутри фрейма метода.
                                                    //    Вызывается статический метод println (с параметрами выше) у объекта System.out.
                                                    //    Это вызывает создание нового фрейма для этого метода в стеке. Метод выводит строку на консоль
    }                                               // После завершения выполнения все локальные переменные внутри фрейма printAll уничтожаются, а сам фрейм удаляется из стека.

} // После завершения методов и исчезновения всех ссылок на объекты, эти объекты без ссылок становятся кандидатами на сборку мусора.
```