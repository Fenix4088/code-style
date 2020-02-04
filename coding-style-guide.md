
# Coding Style Guide

> Правила нейминга и оформления программного кода

- [PHP](#php)
- [CSS / SASS / SCSS](#css--sass--scss)
- [JavaScript](#javascript)

---

## PHP

```php
<?php
namespace FastFood\Page;

use FastFood\Logic\OrderLogic;
use FastFood\Menu\MenuFactory;
use Drinks\Whiskey; // Mike's namespace
use Vendor\Food\FoodOrderInterface;

/**
* OrderPage Controller
*
* Приём заказов с сайта
* Отправка писем
*/
class OrderPage extends OrderLogic implements FoodOrderInterface 
{
    const TYPE_MAIN = "order-type-main";
    const TYPE_VEGETARIAN = "order-type-vegetarian";
    const TYPE_VEGAN = "order-type-vegan";
    const TYPE_GLUTENFREE = "order-type-glutenfree";

    // Menu list
    private OtherClass $menu;

    // Iterator for counter
    public int $iterator;

    /**
    * Comment about functionality
    *
    * @return void Обязательно описываем, что функция возвращает void
    */
    public function go()
    {
        $this->menu = MenuFactory::create($_GET["type"]);
        $this->sampleMethod($this->menu->getName(), $this->menu->getSize());
        $output = $this->longMethodWithManyArgs(
            $this->getDefaultSize(),
            123,
            "example"
        );
    }

    /**
    * Comment with parameters PHP Doc
    *
    * @param string $name Call method name
    * @param int $size Call method name
    * @return void
    *
    * @throws Exception If element in array is not an integer
    * @throws MessageException Second exception
    */
    private function sampleMethod(string $name, int $size = 0)
    {
        $maxSize = OtherClass::getMaxSize($name);

        $arrInline = ['a1', 'b2', 'c3']; // тут в конце нет запятой

        $arrMultyline = [
            'a1',
            'b2',
            'c3', // тут есть запятая
        ];

        if ($size === 0) {
            $this->menu->fillEmpty(OtherClass::getDefault());
        } elseif ($size > $maxSize) {
            $size = $maxSize;
        } else {
            switch ($size) {
                // family style set
                case OtherClass::SIZE_INDIVIDUAL:
                $this->menu->setStyle("individual");
                break;
                // default style set
                default:
                $this->menu->setStyle(Menu::SIZE_DEFAULT);
                break;
            }
        }

        if (!$theSwitch) {
            return;
        }

        // or this, allow only for inline if
        if (!$theSwitch) return;
    }

    /**
    * Comment with parameters PHP Doc
    *
    * @param int $firstNumber param1 description
    * @param int $secondNumber param2 description
    * @param string $exampleString param3 description
    * @param array $options param4 description
    * @return MenuFactory|bool Как оформлять mixed return, on success MenuFactory, on error - bool false
    *
    * @throws Exception If element in array is not an integer
    */
    public function longMethodWithManyArgs(
        int $firstNumber,
        int $secondNumber = 0,
        string $exampleString = null,
        array $options = []
    ):MenuFactory {
        $duplicate = MenuFactory::create($this->menu->getType());

        // Allow multiline if v.1
        if ($duplicate->getSize() !== 0
        && $duplicate->name === $exampleString) {
            return MenuFactory::createDefault();
        } elseif ($duplicate>getSize() !== 0 && $first > 0) { // and inline if
            return MenuFactory::createDefault();
        }
        return false;
    }
}

```

### Структура

- Добавлять пробел после запятой
- Добавлять пробелы вокруг операторов сравнения и бинарных операторов (&&, ==, ===, || и т.п.) за исключением оператора конкатенации (.)
- Унарные операторы (!, --, ++ и т.п.) располагать впритык к переменной (без отступа)
- Применять точное сравнение в операция сравнения, когда не нужен перебор типов - <a href="https://www.php.net/manual/en/language.operators.comparison.php" target="_blank">`Comparison Operators`</a> - использование identical приоритетно ( ===, !== )
- Добавьте пустую строку перед оператором return, если он не внутри блока (например if)
- Используйте return null; когда надо вернуть null, и return; когда надо вернуть void.
- Используйте фигурные скобки { } для блоков во всех случаях кроме inline if, но даже для них рекомендовано использовать скобки.
- Определяйте один класс на файл, за исключением когда классы не для создания экземпляров извне, которые не относятся к PSR-0 и PSR-4.
- Объявите наследование класса и все реализованные интерфейсы в одной строке с именем класса;
- Объявляйте свойства класса перед методами;
- Сначала объявите открытые методы (public), затем защищенные (protected) и, наконец, закрытые (private). Исключением из этого правила являются конструктор класса и методы setUp () и tearDown () тестов PHPUnit, которые всегда должны быть первыми методами, повышающими читабельность;
- Объявите все аргументы в одной строке с именем метода / функции, независимо от количества аргументов;
- Используйте круглые скобки при создании экземпляров классов независимо от количества аргументов, которые имеет конструктор - new MyClass();
- Строки сообщений об исключениях и ошибках должны быть объединены с использованием sprintf;
- Не используйте пробелы вокруг [квадратных скобок];
- Добавьте оператор use для каждого класса, который не является частью глобального пространства имен;
- Когда теги PHPDoc, такие как @param или @return, включают в себя null и другие типы, всегда помещайте null в конец списка типов.
- Для объявления и описания массивов использовать квадратные скобки [‘a’,’b’], и не использовать array(‘a’,’b’);
- Для всех методов, возвращающих единственный тип данных, мы указывает этот тип данных при определении метода, в том числе и для типа void ( method():string, method():void и т.п. ), в случае возвращения mixed (нескольких типов) значений, эти типы мы описываем в PHP Doc в формате /* @return int|void Comment.
- Не ставить закрывающий тэг “?>” в конце PHP файлов.
- Кодировка для всех файлов «UTF-8 без BOM»

### Соглашение об именах

- Используйте camelCase для переменных PHP, имен функций и методов, аргументов (например, $acceptContentTypes, hasSession());
- Используйте snake_case для параметров конфигурации
- Используйте пространства имен для всех классов PHP и UpperCamelCase для их имен (например, ConsoleLogger);
- Константы должны использовать UPPERCASE_UNDERSCORED
- Добавляйте префикс Abstract для всех абстрактных классов.
- Суффикс интерфейсов - Interface;
- Суффикс для трейтов – Trate;
- Суффикс для исключений – Exception;
- Используйте UpperCamelCase для именования файлов PHP (например, EnvVarProcessor.php) и lower-case с дефисами для именования шаблонов и веб- ресурсов (section-layout.phtml, index.scss);
- В комментариях PHP Doc используйте такие типы данных: bool (вместо boolean или Boolean), int (вместо integer или Integer), float (вместо Real или Double).

### Скобки

- Открывающие скобки { для классов и методов всегда с новой строки, для всех остальных блоков - всегда должны быть в конце той же строки.

- Закрывающие скобки всегда должны быть помещены в начале новой строки (})
- Один уровень отступа должен применяться внутри и только внутри фигурных скобок

```php
class MyClass
{
    Method()
    {
        if (a === b) {
            foreach ($arr as $item) {
            
            }
        }
    }
}
```
### Шаблоны .phtml

- В случаях присваивания переменных и вызовов функций прямо в шаблоне, в частях кода где не используется закрытие php тэга ?>, рекомендовано использовать фигурные скобки { }. Во всех остальных случаях – альтернативный синтаксис или фигурные скобки.
- Запрещается использовать альтернативный синтаксис в «одну строку», когда в одной строке и открытие и закрытие блока.
- Запрещается использовать альтернативный синтаксис вне блоков содержащих чистый html.
- Для вывода текста рекомендовано использовать тэг <?= вместо <?php echo или <? echo.’
- Рекомендовано использовать short tags синтаксис <? ?>, вместо <?php ?>.

> Пример применения блоков и стилей в шаблоне

```php
<div>
    <!-- recommended -->
    <? foreach ($arr as $item) { ?>
        <div><?=$item->title?></div>
    <? } ?>

    <!-- recommended -->
    <? foreach ($arr as $item) {
        $item->iterator++;
        $item->renderPart();
    } ?>

    <!-- good -->
    <? foreach ($arr as $item): ?>
        <div><?=$item->title?></div>
    <? endforeach ?>

    <!-- VERY BAD -->
    <? foreach ($arr as $item):
        $item->iterator++;
        $item->renderPart();
    endforeach ?>
</div>
```
### Документация

- Добавьте блоки PHPDoc для всех классов, методов и функций;
- Сгруппируйте аннотации вместе, чтобы аннотации одного типа сразу следовали друг за другом, а аннотации другого типа разделялись одной пустой строкой;
- Опустите тег @return, если метод ничего не возвращает;
- Аннотации @package и @subpackage не используются;
- Не вставляйте блоки PHPDoc в одну строку, даже если они содержат только один тег;
- Для описания простых функций можно использовать вместо PHP Doc – простой комментарий - //comment.

---

## CSS / SASS / SCSS

> Пример SCSS:

```scss

/**
SCSS
**/

.block { /* Блок */
    font-size: 13px;
    font-style: italic;
    font-weight: bold;

    position: absolute;
    left: 10px;
    top: 10px;
    right: 50%;
    bottom: 30px;

    border: 1px solid red;
    background-color: #fff;

    &_wrapper { /* Элемент */
      padding: 10px;
    }

    &_list { /* Элемент */
        margin-top: 10px;
        & > li {
          margin-left: 10px;
        }
    }

    &_input-form { /* Элемент */
        border-radius: 10px;

        &_blue { /* Модификатор */
          background-color: blue;
        }
    
        &_enabled {
          display: block;
        }
    }
}

```

### Блок

Функционально независимый компонент страницы, который может быть повторно использован.

Название блока характеризует смысл («что это?» — «меню»: menu, «кнопка»: button), а не состояние («какой, как выглядит?» — «красный»: red, «большой»: big).


```html
<!-- Верно. Семантически осмысленный блок `error` -->
<div class="error"></div>
<div class="error-message"></div>
<div class="error-message-block"></div>
<!-- Неверно. Описывается внешний вид -->
<div class="red-text"></div>
```

Блок не должен влиять на свое окружение, т. е. блоку не следует задавать внешнюю геометрию (в виде отступов, границ, влияющих на размеры) и позиционирование.

### Вложенность

- Блоки можно вкладывать друг в друга.
- Допустима любая вложенность блоков.

```html
<!-- Блок 'header' -->
<header class="header">
<!-- Вложенный блок 'logo' -->
<div class="logo"></div>
<!-- Вложенный блок 'search-form' -->
<form class="search-form"></form>
</header>
```

### Элемент

Составная часть блока, которая не может использоваться в отрыве от него.

ОСОБЕННОСТИ:
- Название элемента характеризует смысл («что это?» — «пункт»: item, «текст»: text), а не состояние («какой, как выглядит?» — «красный»: red, «большой»: big).
- Структура полного имени элемента соответствует схеме: имя-блока_имя-элемента. Имя элемента отделяется от имени блока одним подчеркиванием (_).

```html
<!-- Блок 'search-form' -->
<form class="search-form">
<!-- Элемент 'input' блока 'search-form' -->
<input class="search-form_input">
<!-- Элемент 'button' блока 'search-form' -->
<button class="search-form_button">Найти</button>
</form>
```

### Принципы работы с элементами

##### ВЛОЖЕННОСТЬ
Элементы можно вкладывать друг в друга.
Допустима любая вложенность элементов.
Элемент — может быть частью блока или быть частью другого элемента.
##### ПРИНАДЛЕЖНОСТЬ
Элемент — всегда часть блока и не должен использоваться отдельно от него.
##### НЕОБЯЗАТЕЛЬНОСТЬ
Элемент — необязательный компонент блока. Не у всех блоков должны быть элементы.

### Когда создавать блок, когда — элемент?

##### СОЗДАВАЙТЕ БЛОК
Если фрагмент кода может использоваться повторно и не зависит от реализации других компонентов страницы.

##### СОЗДАВАЙТЕ ЭЛЕМЕНТ
Если фрагмент кода не может использоваться самостоятельно, без родительской сущности (блока).

Исключение составляют элементы, реализация которых для упрощения разработки требует разделения на более мелкие части — подэлементы.

### Модификаторы

Cущность, определяющая внешний вид, состояние или поведение блока либо элемента.

##### ОСОБЕННОСТИ:
Название модификатора характеризует внешний вид («какой размер?», «какая тема?» и т. п. — «размер»: size-s, «тема»: theme-islands), состояние («чем отличается от прочих?» —
«отключен»: disabled, «фокусированный»: focused) и поведение («как ведет себя?», «как взаимодействует с пользователем?» — «направление»: directions-left-top).

Имя модификатора отделяется от имени блока или элемента одним подчеркиванием (_).

```html
<!-- Блок 'search-form' -->
<form class="search-form">
<!-- Элемент 'input' блока 'search-form' -->
<input class="search-form_input search-form_input_enabled">
<!-- Элемент 'button' блока 'search-form' -->
<button class="search-form_button_blue">Найти</button>
</form>
```

### Формирование название класса или ID элемента

- Первым указывается имя блока или нескольких блоков
- Вторым указывается имя элемента или элементов
- Последним идёт список модификаторов

> блок_элемент_элемент

circles_wrapper блок_элемент

circles_wrapper_selected блок_элемент_модификатор

circles_input блок_элемент

circles_input_error блок_элемент_модификатор

circles_list блок_элемент

circles_list_item блок_элемент_элемент или блок_блок_элемент

circles_list_item_blue блок_элемент_элемент_модификатор

circles_list_item_blue_bold блок_элемент_элемент_модификатор_модификатор

circles_blue блок_модификатор


### Соглашение об именах

- В CSS названиях разрешается использовать маленькие (прописные) латинские буквы, цифры, - и _.
- Название блока, элемента и модификатора может содержать только латинские буквы, цифры и – (дефис). Пример: block, element-name, modificator-is-bold
- Разделителем между блоками, элементами и модификаторами является _ (нижнее подчеркивание). Пример: block_element_modificator.


---

## JavaScript

> Максимальная разрешенная версия для использования: ECMAScript 2015 (ES6).

> Для продакшена компилируется в es5 используя Babel.

> Разрешенные библиотеки: React, JQuery (deprecated минимизируем использование).

Code Style Guide:
- English - https://github.com/airbnb/javascript
- Русский - https://github.com/leonidlebedev/javascript-airbnb

Code Style Guide для React'a:
- English - https://github.com/airbnb/javascript/tree/master/react
- Русский - https://github.com/leonidlebedev/javascript-airbnb/tree/master/react

---

## License

[![License](http://img.shields.io/:license-mit-blue.svg?style=flat-square)](http://badges.mit-license.org)

- **[MIT license](http://opensource.org/licenses/mit-license.php)**
- Copyright 2020 © <a href="https://www.searates.com" target="_blank">SeaRates</a>.