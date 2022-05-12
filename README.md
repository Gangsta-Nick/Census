## Stream API

### Перепись населения

В данной работе были реализованы классы `Sex` и `Education` типа `enum`

1. Класс `sex` содержит информацию о поле человека:

```Java
public enum Sex {
    MAN,
    WOMAN
}
```
2. Класс `Education` содержит типы образования:

```Java
public enum Education {
    ELEMENTARY,
    SECONDARY,
    FURTHER,
    HIGHER
}
```

Так же был создан класс `Person` и содержит в себе информацию о имени, возрасте, поле и образовании человека:

```Java
class Person {
    private String name;
    private String family;
    private Integer age;
    private Sex sex;
    private Education education;

    public Person(String name, String family, int age, Sex sex, Education education) {
        this.name = name;
        this.family = family;
        this.age = age;
        this.sex = sex;
        this.education = education;
    }

    public String getName() {
        return name;
    }

    public String getFamily() {
        return family;
    }

    public Integer getAge() {
        return age;
    }

    public Sex getSex() {
        return sex;
    }

    public Education getEducation() {
        return education;
    }

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", family='" + family + '\'' +
                ", age=" + age +
                ", sex=" + sex +
                ", education=" + education +
                '}';
    }
}
```

Так же из коллекции объектов `Person` были:
1. Найдено количество несовершеннолетних (т.е. люди моложе 18 лет)
2. Получен список фамилий призывников (т.е. мужчины от 18 до 27 лет)
3. Отсортирован по фамилиям список потенциальных работоспособных людей с высшим образованием в выборке (т.е. людей с высшим образованием от 18 до 60 лет для женщин и от 18 до 65 лет для мужчин)

В классе `Main` в функции `main()` созданы коллекции экземпляров класса Person. Для примера будем считать, производится перепись населения города Лондон с населением в 10 миллионов человек. Для генерации исходных данных воспользуемся следующим способом:

```java
List<String> names = Arrays.asList("Jack", "Connor", "Harry", "George", "Samuel", "John");
List<String> families = Arrays.asList("Evans", "Young", "Harris", "Wilson", "Davies", "Adamson", "Brown");
Collection<Person> persons = new ArrayList<>();
for (int i = 0; i < 10_000_000; i++) {
    persons.add(new Person(
                names.get(new Random().nextInt(names.size())),
                families.get(new Random().nextInt(families.size())),
                new Random().nextInt(100),
                Sex.values()[new Random().nextInt(Sex.values().length)],
                Education.values()[new Random().nextInt(Education.values().length)])
    );
}
```
1. Для поиска несовершеннолетних использовался промежуточный метод `filter()` и терминальный метод `count()`.
2. Для получения списка призывников применялось несколько промежуточных методов `filter()`, а также для преобразования данных из `Person` в `String` (так как нужны только фамилии) используйте метод `map()`. Так как требуется получить список `List<String>` терминальным методом будет `collect(Collectors.toList())`.
3. Для получения отсортированного по фамилии списка потенциально работоспособных людей с высшим образованием применялось несколько промежуточных методов `filter()`. Завершение стрима происходит методом `collect()`.
