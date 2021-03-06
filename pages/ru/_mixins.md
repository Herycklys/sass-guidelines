
# Примеси (Миксины)

Примеси – одна из самых важных частей из всего языка Sass. Они являются ключом к повторному использованю и DRY компонентам. Они позволяют авторам определить стили, которые будут повторно использоваться по всей таблице стилей, без надобности к использованию таких неосмысленных классов, как `.float-left`.

Они могут содержать полный набор правил CSS и в значительной степени всё, что разрешено в любом месте документа Sass. Они могут даже принимать аргументы, прямо как функции. Излишне говорить, что их возможности безграничны.

Но я чувствую, что должен вас предупредить о злоупотреблении силой примесей. Опять же, ключевое слово здесь – это *простота*. Это очень заманчиво – строить чрезвычайно мощные примеси с огромным количеством логики. Это называется техническим усложением и большинство разработчиков страдает от этого. Не усложняйте код, и, прежде всего, сохраняйте его простым. Если примесь становится больше, чем 20 строк или около того, то она должна быть разбита на более мелкие части или полностью пересмотрена.

## Основы

Как было сказано, примеси чрезвычайно полезны, и вы должны их использовать. Правило гласит, что если вам случится встретить набор свойств CSS, которые всегда появляются вместе по какой-либо причине (то есть не случайно), то вы можете поместить их в примесь. [Хак Micro-clearfix от Николаса Галлагера](http://nicolasgallagher.com/micro-clearfix-hack/) заслуживает быть помещенным в примесь (без аргументов), например.

{% include snippets/mixins/01/index.html %}

Еще один обоснованный пример: примесь для определения размера элемента, одновременно определяющий и `ширину`, и `высоту`. Код станет не только легче набирать, но и легче читать.

{% include snippets/mixins/02/index.html %}

Для более сложных примеров примесей, взгляните на [эту примесь для генерации CSS треугольников](http://www.sitepoint.com/sass-mixin-css-triangles/), [эту примесь для создания длинных теней](http://www.sitepoint.com/ultimate-long-shadow-sass-mixin/) или [эту примесь для полифилла CSS градиентов для старых браузеров](http://www.sitepoint.com/building-linear-gradient-mixin-sass/).

## Безаргументные примеси

Иногда примеси нужны только чтобы избежать повторения одной и той же группы свойств снова и снова, здесь не нужны никакие параметры, имеются достаточные значения по умолчанию, поэтому нам необязательно передавать аргументы.

В таких случаях, можно безопасно опустить скобки при их вызове. Ключевое слово `@include` (или знак `+` в синтаксисе на отступах) уже действует как индикатор что это вызов примеси; нет необходимости в скобках в данном случае.

{% include snippets/mixins/08/index.html %}

## Список аргументов

Когда имеете дело с неизвестным количеством аргументов в примеси, используйте `arglist`, а не список. Думайте об `arglist` как о восьмом скрытом недокументированном типе данных Sass, неявность которого позволяет использовать произвольное количество аргументов в примеси или функции, подписи которых содержат `...`.

{% include snippets/mixins/03/index.html %}

Теперь, когда вы делаете примесь, которая принимает несколько аргументов (3 или более), подумайте дважды, прежде чем создавать один список – может быть, будет легче передавать их по одному.

Sass очень умён в работе с примесями и объявлениями функций, так что вы можете передавать список или карту в качестве списка аргументов для функции или примеси, и это считается как рядом аргументов.

{% include snippets/mixins/04/index.html %}

Для получения дополнительной информации о том, лучше ли использовать несколько аргументов, список или список аргументов, [SitePoint имеет приятную статью по этой теме](http://www.sitepoint.com/sass-multiple-arguments-lists-or-arglist/).

## Примеси и вендорные префиксы

Написание пользовательских примесей для обработки префиксов для неподдерживаемых или частично поддерживаемых свойств CSS может быть очень заманчивым. Но мы не будем это делать. Для начала, если вы можете использовать [Autoprefixer](https://github.com/postcss/autoprefixer), используйте Autoprefixer. Это сделает код Sass вашего проекта всегда соотвествующим последним обновлениям и сделает работу это лучше, чем ваш код для подстановки префиксов.

К сожалению, Autoprefixer не всегда подходит. Если вы используете [Bourbon](http://bourbon.io/) или [Compass](http://compass-style.org/), вы уже наверника знаете, что они поставляют коллекцию примесей для обработки вендорных префиксов. Используйте их.

Если вы не можете использовать ни Autoprefixer, ни Bourbon и Compass, то тогда вы должны использовать вашу собственную примесь для подстановки префиска свойствам CSS. Но, пожалуйста, не делайте по примеси на каждое свойство, вручную выводя каждый вендор.

{% include snippets/mixins/05/index.html %}

Делайте это по-умному.

{% include snippets/mixins/06/index.html %}

Использование этой примеси будет очень простым:

{% include snippets/mixins/07/index.html %}

Пожалуйста, помните о том, что это плохое решение. Например, это не поможет справиться со сложными плейсхолдерами, такими как те, которые нужны для Flexbox. Поэтому использование Autoprefixer будет куда лучшим вариантом.
