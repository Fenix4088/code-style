
# Coding Style Guide

> Правила нейминга и оформления программного кода

- [PHP](#PHP)
- [CSS / SASS / SCSS](#link-css)
- [JavaScript](#javascript)


## PHP

```php
<?php
namespace FastFood\Page;

use FastFood\Logic\OrderLogic;
use FastFood\Menu\MenuFactory;
use Drinks\Whiskey; // Mike`s namespace
use Vendor\Food\FoodOrderInterface;

/**
* OrderPage Controller
*
* Приём заказов с сайта
* Отправка писем
*/
class OrderPage extends OrderLogic implements FoodOrderInterface {
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
    public function go() {
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
    private function sampleMethod(string $name, int $size = 0) {
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

###Структура

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



## CSS / SASS / SCSS


## JavaScript



***INSERT***




## License

[![License](http://img.shields.io/:license-mit-blue.svg?style=flat-square)](http://badges.mit-license.org)

- **[MIT license](http://opensource.org/licenses/mit-license.php)**
- Copyright 2020 © <a href="https://www.searates.com" target="_blank">SeaRates</a>.