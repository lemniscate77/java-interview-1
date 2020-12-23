# Общие вопросы

### Что такое SOLID?
Это акроним(каждая буква что-то означает), придуманный Робертом Мартином. 
+ **S** - Принцип единственной ответственности (single responsibility principle)
Для каждого класса должно быть определено единственное назначение. Все ресурсы, необходимые для его осуществления, должны быть инкапсулированы в этот класс и подчинены только этой задаче.
+ **O** - Принцип открытости/закрытости (open–closed principle) «программные сущности … должны быть открыты для расширения, но закрыты для модификации».
+ **L** - Принцип подстановки Лисков (Liskov substitution principle)
«объекты в программе должны быть заменяемыми на экземпляры их подтипов без изменения правильности выполнения программы». Производный класс должен быть взаимозаменяем с родительским классом.
+ **I** - Принцип разделения интерфейса (interface segregation principle) «много интерфейсов, специально предназначенных для клиентов, лучше, чем один интерфейс общего назначения»
+ **D** - Принцип инверсии зависимостей (dependency inversion principle) «Зависимость на Абстракциях. Нет зависимости на что-то конкретное»

### Какие есть языки на JVM
+ Kotlin — объектно-ориентированный язык для индустриальной разработки, всё больше набирающий популярность
+ Clojure — функциональный язык, диалект Lisp
+ Groovy — сценарный язык, используется для написания скриптов (для gradle, настройки пайплайнов в Jenkins и пр.)
+ Scala — объектно-ориентированный и функциональный язык
+ Ceylon — объектно-ориентированный язык со строгой статической типизацией
+ JRuby — реализация Ruby
+ Jython — реализация Python
+ Nashorn — реализация JavaScript


### Что такое реактивное программирование
Реактивное программирование Rx состоит из трех ключевых моментов:
+ Наблюдаемые - не что иное, как потоки данных. Наблюдаемый упаковывает данные, которые могут передаваться из одного потока в другой. Они в основном испускают данные периодически или только один раз в своем жизненном цикле на основе конфигураций. Существуют различные операторы, которые могут помочь наблюдателю отправить некоторые конкретные данные на основе определенных событий. 
+ Наблюдатели потребляют поток данных, излучаемый наблюдаемым. Наблюдатели подписываются с помощью метода реактивного программирования subscribeOn () для получения данных, передающих наблюдаемым. Всякий раз, когда наблюдаемый передаст данные, все зарегистрированные наблюдатели получают данные в обратном вызове onNext (). Здесь они могут выполнять различные операции, такие как разбор ответа JSON или обновление пользовательского интерфейса. Если есть ошибка, вызванная наблюдаемым, наблюдатель получит ее в onError ().
+ Планировщики (расписание) - это компонент в Rx, который сообщает наблюдаемым и наблюдателям, по какому потоку они должны работать. Можно использовать метод observOn (), чтобы сообщать наблюдателям, на каком потоке они должны наблюдать. Кроме того, можно использовать schedOn (), чтобы сообщить наблюдаемому, в каком потоке они должны запускаться.

Основными преимуществами Rx являются увеличение использования вычислительных ресурсов на многоядерном и многопроцессорном оборудовании, повышение производительности за счет сокращения точек и повышение производительности за счет сокращения точек сериализации, согласно Закону Амдаля и Универсального закона о масштабируемости Гюнтера. Второе преимущество - высокая производительность для разработчиков, поскольку традиционные парадигмы программирования изо всех сил пытались обеспечить простой и поддерживаемый подход к работе с асинхронными и неблокирующими вычислениями и IO. С этими задачами справляется функциональное реактивное программирование, поскольку оно обычно устраняет необходимость в явной координации между активными компонентами.

Одной из самой популярной библиотекой для реализации реативного программирования на Java является RxJava.


### Паттерн наблюдатель 
Это поведенческий паттерн проектирования, который создаёт механизм подписки, позволяющий одним объектам следить и реагировать на события, происходящие в других объектах.
Представьте, что вы имеете два объекта: **Покупатель** и **Магазин**. В магазин вот-вот должны завезти новый товар, который интересен покупателю.
Покупатель может каждый день ходить в магазин, чтобы проверить наличие товара. Но при этом он будет злиться, без толку тратя своё драгоценное время.
С другой стороны, магазин может разослать спам каждому своему покупателю. Многих это расстроит, так как товар специфический, и не всем он нужен.
Получается конфликт: либо покупатель тратит время на периодические проверки, либо магазин тратит ресурсы на бесполезные оповещения.

Решение:
Давайте называть **Издателями** те объекты, которые содержат важное или интересное для других состояние. Остальные объекты, которые хотят отслеживать изменения этого состояния, назовём **Подписчиками**.

Паттерн Наблюдатель предлагает хранить внутри объекта издателя список ссылок на объекты подписчиков, причём издатель не должен вести список подписки самостоятельно. Он предоставит методы, с помощью которых подписчики могли бы добавлять или убирать себя из списка.

Когда в издателе будет происходить важное событие, он будет проходиться по списку подписчиков и оповещать их об этом, вызывая определённый метод объектов-подписчиков.
Издателю безразлично, какой класс будет иметь тот или иной подписчик, так как все они должны следовать общему интерфейсу и иметь единый метод оповещения.


### Для чего нужна библиотека Lombok
Библиотека Lombok сокращает количество написанного кода, улучшая читаемость. 
Пример кода:
```
public class Person {

    private String name;
    private int age;
    private Cat cat;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public Cat getCat() {
        return cat;
    }

    public void setCat(Cat cat) {
        this.cat = cat;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Person person = (Person) o;
        return age == person.age &&
                Objects.equals(name, person.name) &&
                Objects.equals(cat, person.cat);
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, age, cat);
    }

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", cat=" + cat +
                '}';
    }
}
ublic class Person {

    private String name;
    private int age;
    private Cat cat;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public Cat getCat() {
        return cat;
    }

    public void setCat(Cat cat) {
        this.cat = cat;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Person person = (Person) o;
        return age == person.age &&
                Objects.equals(name, person.name) &&
                Objects.equals(cat, person.cat);
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, age, cat);
    }

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", cat=" + cat +
                '}';
    }
}
```

То же самое с ломбок:
```
@Data
public class Person {
    String name;
    int age;
    Cat cat;
}
```
Lombok генерирует код  на этапе компиляции. Сама библиотека lombok отсутствует в рантайме. Ее использование не увеличивает размер программы.
В ломбок есть следующие аннотации:
+ Builder - вешается на класс, реализует патерн строитель для объекта
+ NoArgsConstructor - добавляет конструктор без аргументов
+ AllArgsConstructor - добавляет конструктор со всеми параметрами
+ EqualsAndHashCode - добавляет реализации методов equals и hashCode
+ Getter - добавляет геттеры для всех параметров класса
+ Setter - добавляет сеттеры для всех параметров класса
И другие


### Что такое TDD
TDD - Test Driven Development, это методология разработки ПО, которая основывается на повторении коротких циклов разработки: изначально пишется тест, покрывающий желаемое изменение, затем пишется программный код, который реализует желаемое поведение системы и позволит пройти написанный тест. Затем проводится рефакторинг написанного кода с постоянной проверкой прохождения тестов.

TDD считается одной из форм правильного метода построения приложения. Философия разработки на основе тестов заключается в том, что ваши тесты являются спецификацией того, как ваша программа должна вести себя. Если вы рассматриваете свой набор тестов как обязательную часть процесса сборки, если ваши тесты не проходят, программа не собирается, потому что она неверна. Конечно, ограничение заключается в том, что правильность вашей программы определена только как полнота ваших тестов. Тем не менее, исследования показали, что разработка, основанная на тестировании, может привести к снижению ошибок на 40-80% в производстве.


### Что такое BDD
Из-за некоторого методологического сходства TDD (Test Driven Development) и BDD (Behaviour Driven Development) часто путают даже профессионалы. В чем же отличие? Концепции обоих подходов похожи, сначала идут тесты и только потом начинается разработка, но предназначение у них совершенно разное. TDD — это больше о программировании и тестировании на уровне технической реализации продукта, когда тесты создают сами разработчики. BDD предполагает описание тестировщиком или аналитиком пользовательских сценариев на естественном языке — если можно так выразиться, на языке бизнеса.

BDD — behaviour-driven development — это разработка, основанная на описании поведения. Определенный человек(или люди) пишет описания вида "я как пользователь хочу когда нажали кнопку пуск тогда показывалось меню как на картинке" (там есть специально выделенные ключевые слова). Программисты давно написали специальные тулы, которые подобные описания переводят в тесты (иногда совсем прозрачно для программиста). А дальше классическая разработка с тестами.

В чем преимущество BDD?
+ Тесты читаемые для не программистов
+ Их легко изменять. Они часто пишутся почти на чистом английском
+ Их может писать product owner или другие заинтересованные лица
+ Результаты выполнения тестов более "человечные"
+ Тесты не зависят от целевого языка программирования. Миграция на другой язык сильно упрощается

### Что такое DDD
Предметно-ориентированное проектирование не является какой-либо конкретной технологией или методологией. DDD — это набор правил, которые позволяют принимать правильные проектные решения. Данный подход позволяет значительно ускорить процесс проектирования программного обеспечения в незнакомой предметной области.

Предметно-ориентированное проектирование (реже проблемно-ориентированное, англ. Domain-driven design, DDD) — это набор принципов и схем, направленных на создание оптимальных систем объектов. Процесс разработки сводится к созданию программных абстракций, которые называются моделями предметных областей. В эти модели входит бизнес-логика, устанавливающая связь между реальными условиями области применения продукта и кодом.

Подход DDD особо полезен в ситуациях, когда разработчик не является специалистом в области разрабатываемого продукта. К примеру: программист не может знать все области, в которых требуется создать ПО, но с помощью правильного представления структуры, посредством предметно-ориентированного подхода, может без труда спроектировать приложение, основываясь на ключевых моментах и знаниях рабочей области.


### Что такое FDD
FDD — Эта методология (кратко именуемая FDD) была разработана Джеффом Де Люка (Jeff De Luca) и признанным гуру в области объектно-ориентированных технологий Питером Коадом (Peter Coad). FDD представляет собой попытку объединить наиболее признанные в индустрии разработки программного обеспечения методики, принимающие за основу важную для заказчика функциональность (свойства) разрабатываемого программного обеспечения. Основной целью данной методологии является разработка реального, работающего программного обеспечения систематически, в поставленные сроки.


Как и остальные адаптивные методологии, она делает основной упор на коротких итерациях, каждая из которых служит для проработки определенной части функциональности системы. Согласно FDD, одна итерация длится две недели. FDD насчитывает пять процессов. Первые три из них относятся к началу проекта:
+ разработка общей модели;
+ составление списка требуемых свойств системы;
+ планирование работы над каждым свойством;
+ проектирование каждого свойства;
+ конструирование каждого свойства.

### Что такое CI/CD
Непрерывная интеграция — это методология разработки и набор практик, при которых в код вносятся небольшие изменения с частыми коммитами. И поскольку большинство современных приложений разрабатываются с использованием различных платформ и инструментов, то появляется необходимость в механизме интеграции и тестировании вносимых изменений.

С технической точки зрения, цель CI — обеспечить последовательный и автоматизированный способ сборки, упаковки и тестирования приложений. При налаженном процессе непрерывной интеграции разработчики с большей вероятностью будут делать частые коммиты, что, в свою очередь, будет способствовать улучшению коммуникации и повышению качества программного обеспечения.

Непрерывная поставка начинается там, где заканчивается непрерывная интеграция. Она автоматизирует развертывание приложений в различные окружения: большинство разработчиков работают как с продакшн-окружением, так и со средами разработки и тестирования.

Инструменты CI/CD помогают настраивать специфические параметры окружения, которые конфигурируются при развертывании. А также CI/CD-автоматизация выполняет необходимые запросы к веб-серверам, базам данных и другим сервисам, которые могут нуждаться в перезапуске или выполнении каких-то дополнительных действий при развертывании приложения.

Непрерывная интеграция и непрерывная поставка нуждаются в непрерывном тестировании, поскольку конечная цель — разработка качественных приложений. Непрерывное тестирование часто реализуется в виде набора различных автоматизированных тестов (регрессионных, производительности и других), которые выполняются в CI/CD-конвейере.

Зрелая практика CI/CD позволяет реализовать непрерывное развертывание: при успешном прохождении кода через CI/CD-конвейер, сборки автоматически развертываются в продакшн-окружении. Команды, практикующие непрерывную поставку, могут позволить себе ежедневное или даже ежечасное развертывание. Хотя здесь стоит отметить, что непрерывная поставка подходит не для всех бизнес-приложений.


### Инструменты CI/CD
+ Jenkins — открытое серверное приложение, которое позволяет разработчикам быстрее строить, автоматизировать и тестировать любой проект
+ Buddy — веб-инструмент для непрерывной интеграции и доставки с дружественным интерфейсом
+ TeamCity — инструмент непрерывной интеграции, разработанный JetBrains и выпущенный в 2006 году. Работает в среде Java, используется для создания и развертывания различных проектов. TeamCity поддерживает интеграцию со многими облачными платформами
+ Bamboo — еще один инструмент CI/CD, разработанный Atlassian. Написан на Java, поддерживает другие языки и технологии, например, CodeDeply, Ducker, Maven, Git, SVN, Mercurial, Ant, AWS, Amazon
+ GitLab CI — законченная платформа управления кодом с несколькими мини-инструментами, каждый из которых выполняет свой набор функций для полного SDLC. Обеспечивает анализ представлений кода, управление ошибками и CI/CD в едином веб-хранилище


### Утечка памяти
Все программы в рамках популярных ОС представляют собой определенным образом структурированный набор данных и инструкций. ОС знает, как работать с этими наборами данных и инструкций, и делает это в некотором заведенном порядке. В рамках ОС для этого есть объект - процесс, который подгрузит приготовленные разработчиком инструкции и данные, будет определенным образом выделять под них время процессора, порождать другие объекты ядра ОС, которые тоже что-то делают.

Сами инструкции так же могут взаимодействовать с разными сущностями операционной системы, файловой системой, порождать потоки, с периферией, выводить что-то на экран, взаимодействовать при работе с оперативной памятью. Все эти ресурсы, или многие из них - разделяемые. Например, вывод на экран, т.к. экран один. Или работа с памятью, т.к. ее конечное количество. И все это делается через API ОС напрямую, или через какие-то обертки над этим API ОС.
И раз память можно выделять, ее следует и освобождать, т.е. уведомлять ОС, что этот участок памяти "свободен", и может быть отдан любому другому процессу под его нужды. Контроль за тем, нужна ли программе еще та или иная память остается на усмотрение программы, ОС этим, естественно, не управляет.

И раз управление выделенной на куче памятью находится на стороне программы, программа может быть построена так, что иногда будет уведомлять ОС о том, чтобы выделить ей какую-то память, но не уведомлять об освобождении.
В цикле это приводит к тому, что со временем объем используемой программой памяти начинает бесконечно расти.

В Java контролем за освобождением памяти занимается Garbage Collector(сборщик мусора)


### Утечки памяти в Java
+ Строковые операции - наиболее частая ситуация, когда возникают утечки памяти в Java-приложениях.
Для понимания. из-за чего происходят проблемы при работе со строками, вспомним, что в Java при выполеннии таких операций, как вызов метода substring() у строки, возвращается экземпляр String лишь и изменёнными значениями переменных length и offset — длины и смещения char-последовательности. При этом, если мы получаем строку длиной 5000 символов и хотим лишь получить её префикс, используя метод substring(), то 5000 символов будут продолжать храниться в памяти.
Для систем, которые получают и обрабатывают множество сообщений, это может быть серьёзной проблемой.
Для того, чтобы избежать данную проблему, можно использовать два варианта:

```
String prefix = new String(longString.substring(0,5)); //первый вариант
String prefix = longString.substring(0,5).intern(); //второй вариант
```

+ Классы ObjectInputStream и ObjectOutputStream хранят ссылки на все объекты, с которыми они работали, чтобы передавать их вместо копий. Это вызывает утечку памяти при непрерывнои использовании (к примеру, при сетевом взаимодействии).
Для решения этой проблемы необходимо периодически вызывать метод reset()

+ Часто ситуация с утечкой памяти возникает при использовании паттерна Observer (Наблюдатель). Как известно, Observer хранит список своих слушателей, которые подписаны на оповещения об определенных действиях. При этом, если мы больше не используем некий класс, который является подписчиком этого наблюдателя, то GC не сможет “собрать” его, поскольку ссылка на него хранится в самом экземпляре Observer

+ Singleton - как только экземпляр-синглтон был инициализирован, он остаётся в памяти на всё время жизни приложения. Как следствие, данный экземпляр не сможет быть собран сборщиком. Данный паттерн стоит применять лишь тогда, когда это обосновано реальными требованию к постоянному хранению в памяти.


### Сложность быстрой сортировки
Ещё эту сортировку называют сортировка Хоара - в честь человека, придумавшего этот алгоритм. Лучшее и среднее время этого алгоритма - O(n*logN) т.е. предел до которого можно улучшать сортировку. Но есть и худший случай, когда данные уже отсортированы, тогда время становился O(n^2) - худший случай, который не превосходит метод пузырька. Имено по этой причине в большинстве библиотечных алгоритмов используется сортировка слиянием, как самый надёжный, выдающий всегда O(n*logN).

### Что такое Big O

Сложность алгоритмов обычно оценивают по времени выполнения или по используемой памяти. В обоих случаях сложность зависит от размеров входных данных: массив из 100 элементов будет обработан быстрее, чем аналогичный из 1000. При этом точное время мало кого интересует: оно зависит от процессора, типа данных, языка программирования и множества других параметров. Важна лишь асимптотическая сложность, т. е. сложность при стремлении размера входных данных к бесконечности.

Допустим, некоторому алгоритму нужно выполнить 4n3 + 7n условных операций, чтобы обработать n элементов входных данных. При увеличении n на итоговое время работы будет значительно больше влиять возведение n в куб, чем умножение его на 4 или же прибавление 7n. Тогда говорят, что временная сложность этого алгоритма равна О(n3), т. е. зависит от размера входных данных кубически.

Использование заглавной буквы О (или так называемая О-нотация) пришло из математики, где её применяют для сравнения асимптотического поведения функций. Формально O(f(n)) означает, что время работы алгоритма (или объём занимаемой памяти) растёт в зависимости от объёма входных данных не быстрее, чем некоторая константа, умноженная на f(n).


### Какие бывают виды тестирования
+ Блочное (модульное, unit testing) тестирование наиболее понятное для программиста. Фактически это тестирование методов какого-то класса программы в изоляции от остальной программы.

Не всякий класс легко покрыть unit тестами. При проектировании нужно учитывать возможность тестируемости и зависимости класса делать явными. Чтобы гарантировать тестируемость можно применять TDD методологию, которая предписывает сначала писать тест, а потом код реализации тестируемого метода. Тогда архитектура получается тестируемой. Распутывание зависимостей можно осуществить с помощью Dependency Injection. Тогда каждой зависимости явно сопоставляется интерфейс и явно определяется как инжектируется зависимость — в конструктор, в свойство или в метод.
+ Интеграционное тестирование - наиболее сложное для понимания. Есть определение — это тестирование взаимодействия нескольких классов, выполняющих вместе какую-то работу. Однако как по такому определению тестировать не понятно. Можно, конечно, отталкиваться от других видов тестирования. Но это чревато.

Если к нему подходить как к unit-тестированию, у которого в тестах зависимости не заменяются mock-объектами, то получаем проблемы. Для хорошего покрытия нужно написать много тестов, так как количество возможных сочетаний взаимодействующих компонент — это полиномиальная зависимость. Кроме того, unit-тесты тестируют как именно осуществляется взаимодействие (см. тестирование методом белого ящика). Из-за этого после рефакторинга, когда какое-то взаимодействие оказалось выделенным в новый класс, тесты рушатся. Нужно применять менее инвазивный метод.
+ Системное тестирование - это тестирование программы в целом. Для небольших проектов это, как правило, ручное тестирование — запустил, пощелкал, убедился, что (не) работает. Можно автоматизировать. К автоматизации есть два подхода.

Первый подход — это использовать вариацию MVC паттерна — Passive View и формализовать взаимодействие пользователя с GUI в коде. Тогда системное тестирование сводится к тестированию Presenter классов, а также логики переходов между View. Но тут есть нюанс. Если тестировать Presenter классы в контексте системного тестирования, то необходимо как можно меньше зависимостей подменять mock объектами. И тут появляется проблема инициализации и приведения программы в нужное для начала тестирования состояние.

Второй подход — использовать специальные инструменты для записи действий пользователя. То есть в итоге запускается сама программа, но щелканье по кнопкам осуществляется автоматически. 


### Что такое ленивая загрузка
Это приём в программировании, когда некоторая ресурсоёмкая операция (создание объекта, вычисление значения) выполняется непосредственно перед тем, как будет использован её результат. Таким образом, инициализация выполняется «по требованию», а не заблаговременно. Аналогичная идея находит применение в самых разных областях: например, компиляция «на лету».

Пруимущества:
+ Инициализация выполняется только в тех случаях, когда она действительно необходима
+ Ускоряется начальная инициализация

Недостатки:
+ Невозможно явным образом задать порядок инициализации объектов
+ Возникает задержка при первом обращении к объекту, что может оказаться критичным при параллельном выполнении другой ресурсоёмкой операции. Вследствие этого требуется тщательно просчитывать целесообразность использования «ленивой» инициализации в многопоточных программных системах


### Какое из следующих утверждений о потоках неверно
1.) Если метод start() вызывается дважды для одного и того же объекта Thread, во время выполнения генерируется исключение.
2.) Порядок, в котором запускались потоки, может не совпадать с порядком их фактического выполнения.
3.) Если метод run() вызывается напрямую для объекта Thread, во время выполнения генерируется исключение.
4.) Если метод sleep() вызывается для потока, во время выполнения синхронизированного кода, блокировка не снимается.

Правильный ответ: 3. Если метод run() вызывается напрямую для объекта Thread, во время выполнения исключение не генерируется. Однако, код, написанный в методе run() будет выполняться текущим, а не новым потоком. Таким образом, правильный способ запустить поток – это вызов метода start(), который приводит к выполнению метода run() новым потоком.

Вызов метода start() дважды для одного и того же объекта Thread приведёт к генерированию исключения IllegalThreadStateException во время выполнения, следовательно, утверждение 1 верно. Утверждение 2 верно, так как порядок, в котором выполняются потоки, определяется Планировщиком потоков, независимо от того, какой поток запущен первым. Утверждение 4 верно, так как поток не освободит блокировки, которые он держит, когда он переходит в состояние Ожидания.


### Что такое «сериализация»?
**Сериализация (Serialization)** - процесс преобразования структуры данных в линейную последовательность байтов для дальнейшей передачи или сохранения. Сериализованные объекты можно затем восстановить (десериализовать).

В Java, согласно спецификации Java Object Serialization существует два стандартных способа сериализации: стандартная сериализация, через использование интерфейса java.io.Serializable и «расширенная» сериализация - java.io.Externalizable.

Сериализация позволяет в определенных пределах изменять класс. Вот наиболее важные изменения, с которыми спецификация Java Object Serialization может справляться автоматически:
+ добавление в класс новых полей;
+ изменение полей из статических в нестатические;
+ изменение полей из транзитных в нетранзитные.

Обратные изменения (из нестатических полей в статические и из нетранзитных в транзитные) или удаление полей требуют определенной дополнительной обработки в зависимости от того, какая степень обратной совместимости необходима.


### Что такое UML?
**UML** – это унифицированный графический язык моделирования для описания, визуализации, проектирования и документирования объектно-ориентированных систем. UML призван поддерживать процесс моделирования на основе объектно-ориентированного подхода, организовывать взаимосвязь концептуальных и программных понятий, отражать проблемы масштабирования сложных систем.

Важно, что UML переводится как Unified Modeling Language. Главное здесь слово Unified. То есть наши картинки поймём не только мы, но и остальные, знающие UML. Получается, это такой международный язык рисования схем.

Отличительной особенностью UML является то, что словарь этого языка образуют графические элементы. Каждому графическому символу соответствует конкретная семантика, поэтому модель, созданная одним человеком, может однозначно быть понята другим человеком или программным средством, интерпретирующим UML. Отсюда, в частности, следует, что модель системы, представленная на UML, может автоматически быть переведена на объектно-ориентированный язык программирования, то есть, при наличии хорошего инструментального средства визуального моделирования, поддерживающего UML, построив модель, мы получим и заготовку программного кода, соответствующего этой модели.

Плюсы и минусы UML проектирования
Плюсы:
+ трата времени
+ необходимость знания различных диаграмм и их нотаций

Минусы:
+ возможность посмотреть на задачу с разных точек зрения
+ другим программистам легче понять суть задачи и способ ее реализации
+ диаграммы сравнительно просты для чтения после достаточно быстрого ознакомления с их синтаксисом