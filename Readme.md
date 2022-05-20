# C++ Второй курс

Начиная с самого начала, программирование строится на взаимодействии программы с оперативной памятью устройства.
Вся RAM делиться на ячейки по 1 байту каждая. Но для удобного использования все эти ячейки, когда до них доходит очередь
быть использованы ми, зачастую группируются для хранения большего объема данных. Так например целое число, если не
вдаваться в подробности, зачастую храниться в блоке из четырех ячеек памяти, то есть занимает 4 байта памяти.
В результате 32-битное целое число, а в 4 байтах именно 32 бита, может достигать значений от -2^31 до (2^31)-1.
Степень 31, а не 32 потому что первый бит отвечает за знак числа, если 0 то +, если 1 то минус, но это не очень важно.

### основные типы данных С++:

- `int` - целое число
- `float` - дробное число
- `double` - дробное число с большим диапазоном допустимых чисел
- `char` - символ, по типу `'f'`, `'a'`, `'1'` и тп.
- `bool` - логический тип данных

### Блок №1

Теперь перейдем непосредственно к тому, как это выглядит на практике. Открой код, который находиться в файле `main.cpp`.
Его там много, но сейчас нас интересует участок окруженный "//1" сверху и снизу.
Сейчас по порядку разберемся что эти каракули на эльфийском значат.

> Сразу стоит оговориться что в конце почти каждой строки, за некоторыми исключениями, следует писать `;`
> Для начала запустите этот файл в любом компиляторе С++ и следите за тем что выводится в консоль
(Некоторые среды разработки, например Visual Studio не позволяют запускать код, в котором есть неинициализированные
> переменные
> по этому в случае если код не запустился, замените строку `int a;` на `int a = 0;` Дальше будет понятно что это
> значит)

Строка `int a;` это непосредственно выделение тех четырех байт под целое число. Мы взяли где-то в памяти 4 байта,
присвоили им имя `а` и теперь можем обращаться к этой памяти как к чему-то единому, называя это целочисленной
переменной.

Дальше идет строка вывода данных в консоль. После `<<` может стоять строка, переменная или результат математического
действия. На этом этапе на экран выведется какое-то невнятное число, что является просто мусором который покоился в этих
байтах до того как мы его потревожили.

Строка `a = 1;` задает нашей переменной значение равное `1`, фактически это значит что в те 4 байта памяти запишется
нечто вот такое: `00000000 00000000 00000000 00000001`. Тут 31 0 и 1 единица в конце, это двоичное представление числа,
что в нашем случае не сильно отличается от десятичного представления.
Это действие, задание переменной начального значения называется **инициализацией**.

На следующей строке мы опять выводим значение переменной, на этот раз оно выглядит приятнее, не правда ли.

> Именно по причине того, что С++ никоим образом не мешает нам использовать неинициализированные переменные, в коде
> постоянно будут встречаться строки по типу `a = 0;`

### Блок №2

Теперь посмотрим на второй блок. Он заметно короче, но делает то же самое. Переменная `b` создается и приобретает
начальное значение в одной строке.

> Также добавлю что в одной области видимости переменные с одинаковыми именами не допускаются.
> На практике, пока что это значит что нам нужно стараться придумывать разные имена для всех новых переменных

### Блок №3

В третьем блоке у нас на первый взгляд происходит какая-то ересь, но нет, это просто прибавление значений переменных, в
нашем случае это все равно что написать `int c = 1 + 1;`

### Блок №4

А четвертый блок выглядит как ночной кошмар математика. Все это на самом деле делает одно и то же, просто прибавляет к
значению переменной `c` `1`. Первый способ это прировнять `c` к этой же `c` только `+ 1`. То же самое что мы делали в
первом блоке, но теперь не просто число, а математическое выражение.
Второй способ называется сложение с присваиванием, это действие прибавляет к изменяемой переменной то число которое
написано в правой части и потом задает получившийся результат этой же переменной.
есть так же `-=`, `*=`, `/=`, думаю достаточно очевидно что они сделают.
Ну и третий способ, два плюса или два минуса под ряд рядом с переменной. Так можно увеличить или уменьшить значение
переменной на единицу. Все три способа одинаково работают и один не является более правильным, а другой менее, просто
где-то удобно так, а где-то по другому.

### Блок №5

В пятом блоке попробуем создать новую переменную `d` и задать ей значение равное половине от `c`. Для этого поделим `c`
на `2`. На выходе мы ожидаем получить `2.5`, поскольку `5 / 2 = 2.5` Но компилятор уже спешит нас обламать и выводит в
консоль ровно 2. Вернемся к битам и байтам. Наше число `5`, если обрезать левые 24 нолика, выглядит вот так: `00000101`
а
число `2` выглядит так: `00000010`

Вспомним о типах данных. Мы все время использовали целое число, соответственно если мы попытаемся присвоить
целочисленной переменной дробное число, то компьютеру ничего не останется кроме как записать в переменную целую часть
числа, а дробную просто отбросить.

### Блок №6

Применив несколько уже упомянутых действий над переменными `c` и `d` мы получим ответ `3`, который полностью
соответствует нашим представлениям о делении числа `6` на `2`

### Блок №7

Теперь давай в седьмом примере попробуем получить дробное число. Для этого воспользуемся типом `float` при создании
переменной `e`. Но вот при делении `6` на `2`, мы опять получили целое число.
На этот раз поделим e на 2 еще раз с помощью оператора деления с присваиванием. Ура, дробное число получено, можешь
отметить этот день в своем календаре)))

### Блок №8

В восьмом примере я покажу разные способы установки значений для дробных чисел. Все выглядит вполне логично, за
исключением последнего варианта. В нем мы просто не указывали дробную часть,
но указали что это число дробное, тут это не особо полезно, но в дальнейшем мы еще будем это использовать.

> Теперь поиграемся немного с выводом данных в консоль. Думаю от твоего внимания не ускользнуло `<< endl` в конце
> каждого
> вывода. Это просто означает окончание строки и переход на новую.
> То же самое будет если написать `<< "\n"`.

### Блок №9

В девятом примере я вывожу в консоль все переменные которые мы успели создать, но теперь немного красивее. Мы выводим
строку в которой пишем название переменной и знак равно,
дальше выводим значение этой самой переменной, а в конце добавляем перенос на новую строку.

```
cout << "что-то что нужно вывести, переменная или просто текст";
cout << "опять что-то выводим " << "но на этот раз двумя частями, и таких частей может быть сколько угодно, главное разделять их знаками <<";
```

> "" означают что текст который в них написан будет восприниматься как строка, и если ты вставишь куда-то две верхние
> строки, то ты увидишь что текст вывелся без изменений.
> Но есть ты забудешь поставить кавычки, то программа просто не запуститься.

### Блок №10

И так, мы уже знаем как создавать и работать с числовыми переменными. Но на этом много не напрограммируешь, необходимо
как-то получать и обрабатывать данные из вне.
В модуле `iostream`, который мы подключали в самом верху, есть функция `cin`, которая принимает данные и записывает их в
переменную.

Давай посмотрим на десятый блок. Мы создали переменную `f`, но не задали ей никакого значения, потому что на следующей
строке мы ожидаем что пользователь введет его сам.
Как видишь значение у переменной `f` ровно такое, какое было введено.

### Блок №11

Нам осталось разобраться с последней недостающей деталькой, логическим типом данных.
Давай разбираться. Я создал переменную `h` с новым типом данных, логическим. Он занимает всего 1 байт и может быть равен
либо `0`, либо `1`, `0` это `ложь`, `1` это `правда`.
Идем дальше, строка `h = 1 == 1;` Что здесь происходит? Мы сравниваем `1` и `1`, равна ли единица единице. Разумеется
что
ответ правда, по этому на выходе мы получим значение `true`.

> Вот сейчас очень важно, `=` это приравнивание, с помощью этого оператора мы задаем значение, а `==` это сравнивание,
> мы
> сравниваем два значения.

Есть так же:

- `!` - отрицание
- `!=`- не равно
- `<` - меньше
- `>` - больше
- `<=` - меньше или равно
- `>=` - больше или равно

И так, переходим на третью строку: `h = 1 == 2;` Разумеется что `1` не равна `2`, по этому результат сравнения будет
`false`, что мы и видим на выходе.
Четвертая строка демонстрирует возможность сравнивать переменную с каким то значением или другой переменной.
Поскольку на прошлой строке у нас получилась ложь, то сравнение `false` и `false` вернет, ожидаемо, правду.
Ну и последняя строка, на которой мы берем значение обратное значению переменно `h`. Простыми словами это выглядит как
`не правда`, что по другому является `ложью`, именно ее мы и наблюдаем в консоли.

### Блок №12

Что ж, мы теперь полностью готовы к познанию того, как обрабатывать данные. В двенадцатом блоке мы видим так называемое
условие `if(условие){ действие }`. Дословно это можно перевести так: "Если утверждение в круглых скобках правдиво, то
выполнить действие в фигурных скобках". В нашем случае утверждение в скобках всегда правдиво, поскольку мы туда передаем
заведомо правдивое значение.

### Блок №13

В разделе 13 мы видим вторую часть условия `else{ действие }`, которая дословно обозначает "Иначе, если условие не
выполнилось, то...". В данном случае, поскольку наша переменная `h` все еще равна `false`, то выполниться блок `else`

### Блок №14

Продолжаем познавать все прелести условий. На этот раз у нас добавился блок `else if(условие){ действие }`, который
будет выполнен в случае если первое условие не выполнилось. Дословно это значит "Иначе если первое условие не сработало,
то проверить другое условие". Стоит заметить что таких блоков с дополнительными условиями может быть сколько угодно,
главное соблюдать порядок: `if` -> `else if` -> `else`.

### Блок №15

Условия это конечно превосходно, но вся их сила раскрывается в тандеме с циклами. Всего есть три вида циклов,
что на самом деле лож, так как два из них в своей основе содержат третий. Сейчас станет понятнее.

Разберем фундаментальный вид циклов. Выглядит он так: `while(условие){ действие }`, и дословно значит: "Повторять
действие в фигурных скобках, до тех пор, пока правдиво условие в круглых". Правда вот есть один нюанс, если мы поместим
на место условия `true`, то цикл будет повторяться вечно. В нашем случае цикл будет повторяться до тех пор, пока не
будет введено число 5.

### Блок №16

А что делать если нам нужно четко установить количество повторений цикла? Нужна дополнительная переменная, которая будет
выступать в роли счетчика. В нашем случае мы создали переменную `k`, поставили в цикле условие `k < 5`, а в самом цикле 
на каждом этапе прибавляем к ее значению 1.

### Блок №17

Теперь давай посмотрим на следующий тип циклов. Делает этот цикл ровно то же самое что и предыдущий, за одним исключением,
в написании он компактнее. Разберем все по порядку. В самом начале мы объявляем переменную-счетчик (так же туда можно поместить
уже объявленную переменную: `int l = 0;` -> `k = 0;`. Так же эту часть можно полностью опустить, написав вместо нее `;`).
Дальше мы ставим условие, в нашем случае `l < 5;` (эту часть также можно опустить написав просто `;`, но тогда цикл будет
повторяться бесконечно). Ну и последняя часть, действие которое будет выполнено при переходе на следующий круг цикла. Вместо
`l++` вполне написать `l *= 2`. В зависимости от того, что написано в последней части объявления цикла будет меняться и его
поведение. К слову, это тоже можно пропустить: просто не писать ничего на том месте, тогда нам придется или где-то в другом
месте как-то менять наше переменную `l`, или же цикл будет бесконечным.

>Очень важный момент, переменная `l` не будет доступна нигде за пределами этого цикла. Если нам нужно использовать эту переменную
где-то еще, то стоит объявлять ее за пределами цикла.

### Блок №18

Теперь разберем последний вид циклов. Его используют реже всего, потому что его специфика в том, что тело цикла выполнится хотя бы
один раз, а потом произойдет проверка условия. В случае если условие ложно, цикл не пойдет на второй круг. Попробуем повторить
то что мы писали в предыдущих двух блоках. Как видим, условие не поменялось, вывод тоже, но вот цикл мы использовали другой.
Ниже я продемонстрировал что цикл выполниться хотя бы раз, даже при ложном условии.
