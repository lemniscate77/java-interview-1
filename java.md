# Java Core

### Отличия SoftReference от WeakReference

Главное отличие SoftReference от WeakReference в том как сборщик с ними будет работать. Он может удалить объект в любой момент если на него указывают только weak ссылки, с другой стороны объекты с soft ссылкой будут собраны только когда JVM очень нужна память. Благодаря таким особенностям ссылочных классов каждый из них имеет свое применение. SoftReference можно использовать для реализации кэшей и когда JVM понадобится память она освободит ее за счет удаления таких объектов. А WeakReference отлично подойдут для хранения метаданных, например для хранения ссылки на ClassLoader. Если нет классов для загрузки то нет смысла хранить ссылку на ClassLoader, слабая ссылка делает ClassLoader доступным для удаления как только мы назначим ее вместо крепкой ссылки (Strong reference).

### Как написать immutable класс
Чтоб написать immutable неизменяемый класс, нужно следовать простым пунктам:
+ Сделать класс финальным
+ Сделать все поля приватными и создать только геттеры к ним. Сеттеры, разумеется, не нужно
+ Сделать все mutable поля final, чтобы установить значение можно было только один раз
+ Инициализировать все поля через конструктор, выполняя глубокое копирование (то есть, копируя и сам объект, и его переменные, и переменные переменных, и так далее)
клонировать объекты mutable переменных в геттерах, чтобы возвращать только копии значений, а не ссылки на актуальные объекты
Пример:
```
/**
* Пример по созданию immutable объекта.
*/

public final class FinalClassExample {

   private final int age;

   private final String name;

   private final HashMap<String, String> addresses;

   public int getAge() {
       return age;
   }


   public String getName() {
       return name;
   }

   
/**
    * Клонируем объект перед тем, как вернуть его.
    */

   public HashMap<String, String> getAddresses() {
       return (HashMap<String, String>) addresses.clone();
   }

   
/**
    * В конструкторе выполняем глубокое копирование для mutable объектов.
    */

   public FinalClassExample(int age, String name, HashMap<String, String> addresses) {
       System.out.println("Выполняем глубокое копирование в конструкторе");
       this.age = age;
       this.name = name;
       HashMap<String, String> temporaryMap = new HashMap<>();
       String key;
       Iterator<String> iterator = addresses.keySet().iterator();
       while (iterator.hasNext()) {
           key = iterator.next();
           temporaryMap.put(key, addresses.get(key));
       }
       this.addresses = temporaryMap;
   }
}
```

### Что такое пул строк
Пул String относится к набору строк, которые хранятся в динамической памяти. В этом случае всякий раз, когда создается новый объект, пул строк сначала проверяет, присутствует ли объект в пуле или нет. Если он присутствует, то такая же ссылка возвращается в переменную, иначе новый объект будет создан в пуле строк, и будет возвращена соответствующая ссылка.

### IO и NIO
Основное отличие между двумя подходами к организации ввода/вывода в том, что Java IO является потокоориентированным, а Java NIO – буфер-ориентированным. Потокоориентированный ввод/вывод подразумевает чтение/запись из потока/в поток одного или нескольких байт в единицу времени поочередно. Данная информация нигде не кэшируются. Таким образом, невозможно произвольно двигаться по потоку данных вперед или назад. Если вы хотите произвести подобные манипуляции, вам придется сначала кэшировать данные в буфере.

Подход, на котором основан Java NIO немного отличается. Данные считываются в буфер для последующей обработки. Вы можете двигаться по буферу вперед и назад. Это дает немного больше гибкости при обработке данных. В то же время, вам необходимо проверять содержит ли буфер необходимый для корректной обработки объем данных. Также необходимо следить, чтобы при чтении данных в буфер вы не уничтожили ещё не обработанные данные, находящиеся в буфере.

Потоки ввода/вывода (streams) в Java IO являются блокирующими. Это значит, что когда в потоке выполнения (tread) вызывается read() или write() метод любого класса из пакета java.io.*, происходит блокировка до тех пор, пока данные не будут считаны или записаны. Поток выполнения в данный момент не может делать ничего другого.

Неблокирующий режим Java NIO позволяет запрашивать считанные данные из канала (channel) и получать только то, что доступно на данный момент, или вообще ничего, если доступных данных пока нет. Вместо того, чтобы оставаться заблокированным пока данные не станут доступными для считывания, поток выполнения может заняться чем-то другим.
Селекторы в Java NIO позволяют одному потоку выполнения мониторить несколько каналов ввода. Вы можете зарегистрировать несколько каналов с селектором, а потом использовать один поток выполнения для обслуживания каналов, имеющих доступные для обработки данные, или для выбора каналов, готовых для записи.


### Java 8-11, новые методы в Map
+ Java 8: compute
+ Java 8: computeIfAbsent
+ Java 8: computeIfPresent
+ Java 8: forEach
+ Java 8: putIfAbsent
+ Java 11: factory-методы of()


### Try-with-resources
try-with-resources — краткая замена стандартному try..catch..finally. Закрывает ресурс после выхода из секции try-with-resources. Ресурс должен имплементить интерфейс AutoCloseable.

«Ресурс» в данном контексте — это класс, представляющий cобой соединение/cокет/файл/поток. В данном примере нам не нужно следить за тем, чтобы вызвать ::close у переменной is
```
try (InputStream is = new FileInputStream("/path/to/file.txt")) {
	// some code
}
```

### Отличие checked от unchecked exception
+ Checked exceptions (проверяемые исключения). В JDK представлены классом Exception. Исключения, которые нельзя проигнорировать, их обязательно нужно обрабатывать, либо специфицировать в сигнатуре метода, для обработки выше. Как правило, считаются дурным тоном, т.к код со мн-вом конструкций try..catch плохо читабелен, к тому же добавление новых пробрасываемых исключений в сигнатуре метода может сломать контракт вызова у пользователей данного метода.
+ Unchecked exceptions (непроверяемые исключения). В JDK это класс RuntimeException. Можно игнорировать, не требуют обработки через try..catch, или указания в сигнатуре через throws. Минус такого подхода — у вызывающей стороны нет никакого понимания, как обрабатывать ситуацию, когда под капотом «рванет»
+ Error — ошибки, кидаемые JVM в результате нехватки памяти (OutOfMemoryError), переполнения стэка (StackOverflowError) и.т.д


### Отличие map от flatMap в Stream API
map и flatMap применяются к объекту типа Stream<T> и возвращают Stream<R>. Отличие в том, что map на каждый объект создаёт один другой, когда flatMap может создать 0 или больше. 
	
	
### Промежуточные и терминальные операции в Stream API
Промежуточные операции являются ленивыми и не начнут выполняться до тех пор, пока это не понадобится. Если не вызвать терминальную операцию, промежуточные не будут выполняться вообще. Каждая промежуточная операция возвращает поток, благодаря чему можно составлять цепочки операций. К промежуточным операция относятся:
+ filter
+ skip
+ distinct
+ map

Пример терминальных операций:
+ findFirst
+ collect
+ count
+ allMatch
+ min
+ reduce


### Жизненный цикл сервлетов
+ Сервлет загружен
+ Сервлет создан
+ Сервлет инициализирован
+ Обслужить запрос
+ Сервлет уничтожен

### Использование оператора instanceof
Оператор instanceof позволяет проверить принадлежность объекта к определенному классу/родителю. Выражение возвращает true, если объект является экземпляром класса или его потомком. В следующем примере демонстрируется использование оператора instanceof в различных условиях:
```
String str = "Hello";
int    i   = 0;
String gstr;

if (str instanceof java.lang.String) {
    // сообщение будет выведено в консоль, 
    // т.к. выражение будет true
    System.out.println("str is String");
}

if (i instanceof Integer) {
    // сообщение будет выведено в консоль, 
    // т.к. i будет упакована в Integer
    System.out.println("i is Integer");
}

if (gstr instanceof java.lang.String) {
    // gstr не инициализирована и поэтому проверка 
    // вернет false для null
    System.out.println("gstr is a String");
}
```

### Как создать аннотацию
Аннотация задается описанием соответствующего интерфейса.
Например так:
```
import java.lang.annotation.*;
@Target(value=ElementType.FIELD)
@Retention(value= RetentionPolicy.RUNTIME)
public @interface Name {
     String name();
     String type() default  “string”;
}
```
Как видно из примера выше, аннотация определяется описанием с ключевым словом interface и может включать в себя несколько полей, которые можно задать как обязательными, так и не обязательными. В последнем случае подставляется default значение поля.
Также из примера видно, что саму аннотацию можно пометить несколькими аннотациями.
Разберемся для начала, чем можно пометить собственную аннотацию, и зачем.

+ @Retention позволяет указать жизненный цикл аннотации: будет она присутствовать только в исходном коде, в скомпилированном файле, или она будет также видна и в процессе выполнения. Выбор нужного типа зависит от того, как вы хотите использовать аннотацию, например, генерировать что-то побочное из исходных кодов, или в процессе выполнения стучаться к классу через reflection.
+ @Target указывает, что именно мы можем пометить этой аннотацией, это может быть поле, метод, тип и т.д.
+ @Documentedуказывает, что помеченная таким образом аннотация должна быть добавлена в javadoc поля/метода и т.д.
+ @Inherited помечает аннотацию, которая будет унаследована потомком класса, отмеченного такой аннотацией


### Что такое семафор
Semaphore – это новый тип синхронизатора: семафор со счётчиком, реализующий шаблон синхронизации Семафор. Доступ управляется с помощью счётчика: изначальное значение счётчика задаётся в конструкторе при создании синхронизатора, когда поток заходит в заданный блок кода, то значение счётчика уменьшается на единицу, когда поток его покидает, то увеличивается. Если значение счётчика равно нулю, то текущий поток блокируется, пока кто-нибудь не выйдет из защищаемого блока. Semaphore используется для защиты дорогих ресурсов, которые доступны в ограниченном количестве, например подключение к базе данных в пуле.

### Задача на пост и пре инкремент
Что выведет следующая программа?:

```
public class A{
 
static int a = 1111;
static
{
        a = a-- - --a;
}
    
{
        a = a++ + ++a;
}
 
 public static void main(String[] args)  {
       System.out.println(a);
    }
}
```





Ответ: 2


### Типы вложенных классов в Java
Есть 4 типа таких классов:
+ Статические вложенные классы
+ Внутренние классы
+ Локальные классы
+ Анонимные (безымянные) классы


### Что такое default method в Interface?
Дефолтный метод у интерфейса - относительно новая фишка в Java. Раньше, интерфейсы только определяли методы, которые должен реализовать класс, имплементирующий его. Теперь же у интерфейсов могут быть методы с реализацией, выглядит это так:
```
public interface Car {

   public default void gas() {
       System.out.println("Газ!");
   }

   public default void brake() {
       System.out.println("Тормоз!");
   }
}
```


### Какая разница между абстрактным классом и интерфейсом?
Абстрактный класс:
+ абстрактные классы имеют дефолтный конструктор; он вызывается каждый раз, когда создается предок этого абстрактного класса
+ содержит как абстрактные методы, так и не абстрактные. По большому счету может и не содержать абстрактных методов, но все равно быть абстрактным классом
+ класс, который наследуется от абстрактного, должен реализовать только абстрактные методы
+ абстрактный класс может содержать Instance Variable

Интерфейс:
+ не имеет никакого конструктора и не может быть инициализирован
+ только абстрактные методы должны быть добавлены (не считая default methods)
+ классы, реализующие интерфейс, должны реализовать все методы (не считая default methods)
+ интерфейсы могут содержать только константы
 
 
### Всегда ли добавление в ArrayList имеет сложность O(1)?
Чаще всего это действительно так, но не всегда. Внутри ArrayList находится массив. И когда пустые элементы в этом массиве заканчиваются, реализация ArrayList расширяет его - происходит создание нового массива, большего размера, куда происходит копирование старого, и уже в новый добавляется элемент. Таким образом, иногда вставка в ArrayList может занимать линейное время O(n)

### Всегда ли в Java существовали дженерики
Нет, не всегда. Дженерики появились в Java версии 1.5 (с поддержкой обратной совместимости, т.е. код версии 1.4 продолжил работать на последующих версиях)

### Что такое wildcards
Пример с использованием wildcards:
```
public static void iterateAnimals(Collection<? extends Animal> animals) {

   for(Animal animal: animals) {
       System.out.println(animal.toString());
   }
}
```

Конструкция <? extends Animal> - и есть wildcard. Она означет что метод принимает на вход коллекцию объектов класса Animal либо объектов любого класса-наследника Animal (? extends Animal)

Ещё возможен такой вариант:

```
public static void iterateAnimals(Collection<? super Cat> animals) {

   for(int i = 0; i < animals.size(); i++) {
       System.out.println(animals.get(i).toString());
   }
}
```

Конструкция <? super Cat> говорит компилятору, что метод iterateAnimals() может принимать на вход коллекцию объектов класса Cat либо любого другого класса-предка Cat. 