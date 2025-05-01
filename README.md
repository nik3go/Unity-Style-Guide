# Руководство по стилю Unity

Эта статья содержит идеи по организации структуры проекта и соглашениям об именовании скриптов и ассетов в Unity.

<a name="toc"></a>
## Оглавление

> 1. [Введение](#introduction)  
> 1. [Структура проекта](#structure)  
> 1. [Скрипты](#scripts)  
> 1. [Соглашения об именовании ассетов](#anc)  
> 1. [Рабочие процессы с ассетами](#asset-workflows)

<a name="introduction"></a>
## 1. Введение

### Разделы

> 1.1 [Стиль](#style)

> 1.2 [Важная терминология](#importantterminology)

<a name="style"></a>
### 1.1 Стиль

#### Если в вашем проекте уже есть руководство по стилю, следует ему придерживаться.
Если вы работаете над проектом или в команде, где уже существует руководство по стилю, его необходимо соблюдать. Любое расхождение между существующим руководством и этим документом должно разрешаться в пользу уже существующего.

Однако, руководства по стилю должны быть живыми документами, и вы должны предлагать изменения как в существующее руководство, так и в это, если считаете, что они принесут пользу всем.

> ##### *Споры о стиле бессмысленны. Должно быть руководство по стилю, и вы должны его соблюдать.*  
> [_Rebecca Murphey_](https://rmurphey.com)

#### Вся структура, ассеты и код в проекте должны выглядеть так, как будто их создал один человек, независимо от количества участников.
Переход от одного проекта к другому не должен требовать переобучения стилю и структуре. Следование руководству по стилю избавляет от лишних догадок и неоднозначностей.

Это также позволяет более продуктивно создавать и поддерживать проект, так как не нужно думать о стиле — просто следуйте инструкциям. Это руководство написано с учетом лучших практик, а значит, его соблюдение поможет свести к минимуму трудноуловимые ошибки.

#### Друзья не позволяют друзьям использовать плохой стиль.
Если вы видите, что кто-то работает без руководства по стилю или вопреки ему — постарайтесь это исправить.

Работая в команде или общаясь в сообществе, гораздо проще помогать и просить помощи, когда все придерживаются единого стиля. Никому не нравится разбираться в чьём-то запутанном коде или работать с ассетами с непонятными именами.

Если вы помогаете кому-то, чей стиль отличается, но при этом последователен и адекватен, вы должны быть в состоянии к нему адаптироваться. Если же они не придерживаются никакого стиля — направьте их сюда.

<a name="importantterminology"></a>
### 1.2 Важная терминология

<a name="terms-prefab"></a>
#### Префабы
Unity использует термин "Prefab" для системы, позволяющей создать, настроить и сохранить объект GameObject со всеми его компонентами, значениями свойств и дочерними объектами в виде повторно используемого ассета.

<a name="terms-level-map"></a>
#### Уровни / Карты / Сцены
Уровни — это то, что некоторые называют картами, а в Unity — сценами. Уровень содержит набор объектов.

<a name="terms-serializable"></a>
#### Сериализуемые
Сериализуемые переменные отображаются в окне Inspector в Unity. Подробнее смотрите документацию Unity по [Serializable](https://docs.unity3d.com/Manual/script-Serialization.html).

<a name="terms-cases"></a>
#### Регистры
Существуют разные способы именования. Вот распространённые стили:

> ##### PascalCase  
> Заглавные буквы в каждом слове, без пробелов, например: `DesertEagle`, `StyleGuide`, `ASeriesOfWords`.  
> 
> ##### camelCase  
> Первая буква строчная, последующие слова с заглавной буквы, например: `desertEagle`, `styleGuide`, `aSeriesOfWords`.  
> 
> ##### lowercase  
> Все буквы строчные, например: `deserteagle`.  
>
> ##### Snake_case  
> Слова могут начинаться с заглавной или строчной буквы, разделяются подчеркиванием, например: `desert_Eagle`, `Style_Guide`, `a_Series_of_Words`.

**[⬆ Вернуться к началу](#table-of-contents)**

<a name="structure"></a>
## 2. Структура проекта
Стиль структуры директорий проекта должен считаться обязательным. Соглашения об именовании ассетов и структура каталогов контента идут рука об руку, и нарушение любого из них вызывает ненужный хаос.

В этом стиле используется структура, полагающаяся больше на возможности фильтрации и поиска в окне Project для работы с ассетами, чтобы находить ассеты определённого типа, а не на общую практику группировки ассетов по типу в папках.

> Используя [соглашение об именовании](#asset-name-modifiers) с префиксами, размещение ассетов в папках по типу, таких как `Meshes`, `Textures` и `Materials`, становится избыточным, так как типы ассетов уже отсортированы по префиксу и могут быть отфильтрованы в обозревателе контента.

> ВАЖНО: Ассеты для разработки (в процессе работы или тестирования, находящиеся в `_Dev`) всегда должны начинаться с символа `_`, чтобы их было легко найти при настройке в инспекторе.
<pre>
Assets
    <a name="#structure-developers">_Dev</a> (используйте `_`, чтобы папка была вверху)
        DeveloperName
            (ассеты в разработке)
    <a name="structure-top-level">ProjectName</a>
        Characters
            Anakin
        FX
            Particles
        Vehicles
            Abilities
                IonCannon
                    (Particle Systems, Textures)
            Weapons
        Gameplay
            Characters
            Equipment
            Input
            Triggers
            Quests
            Scene
            Vehicles
                Abilities
                Air
                    TieFighter
                        (Models, Textures, Materials, Prefabs)
        <a name="#structure-levels">_Levels</a>
            Frontend
            Act1
                Level1
        Lighting
            HDRI
            Lut
            Textures
        MaterialLibrary
            Debug
            Shaders
        Objects
            Architecture (большие объекты, используемые один раз)
                DeathStar
            Props (повторяющиеся объекты для заполнения уровней)
                ObjectSets
                    DeathStar
        Scripts
            AI
            Gameplay
                Triggers
                Quests
                Input
            Tools
        Sound
            Characters
            Vehicles
                TieFighter
                    Abilities
                        Afterburners
            Weapons
        UI
            Art
                Buttons
            Resources
                Fonts
    ExpansionPack (DLC)
    Plugins
    ThirdPartySDK
</pre>

Причины такой структуры изложены в следующих подразделах.

### Разделы

> 2.1 [Названия папок](#structure-folder-names)

> 2.2 [Папки верхнего уровня](#structure-top-level)

> 2.3 [Папки разработчиков](#structure-developers)

> 2.4 [Уровни](#levels)

> 2.5 [Определение ответственности](#structure-ownership)

> 2.6 [`Assets` и `AssetTypes`](#structure-assettypes)

> 2.7 [Большие наборы](#structure-large-sets)

> 2.8 [Библиотека материалов](#structure-material-library)

> 2.9 [Структура сцены](#scene-structure)
<a name="2.1"></a>
<a name="structure-folder-names"><a>
### 2.1 Имена папок
Это общие правила наименования любых папок в структуре контента.

<a name="2.1.1"></a>
#### Всегда используйте [PascalCase](#terms-cases)
PascalCase означает, что имя начинается с заглавной буквы, а вместо пробелов каждое следующее слово также начинается с заглавной буквы. Например: `DesertEagle`, `RocketPistol`, и `ASeriesOfWords`.

<a name="2.1.2"></a>
#### Никогда не используйте пробелы
Подтверждая правило [2.1.1](#2.1.1), никогда не используйте пробелы. Пробелы могут вызывать сбои в работе различных инженерных инструментов и пакетных процессов. В идеале, корневая папка вашего проекта также не должна содержать пробелов и должна располагаться, например, по пути `D:\Project`, а не `C:\Users\My Name\My Documents\Unity Projects`.

<a name="2.1.3"></a>
#### Никогда не используйте символы Unicode и другие специальные символы
Если одного из персонажей вашей игры зовут 'Zoë', имя папки должно быть `Zoe`. Символы Unicode могут быть ещё более проблемными, чем [пробелы](#2.1.2), для инженерных инструментов, и некоторые приложения также не поддерживают символы Unicode в путях.

В дополнение к этому, если в вашем проекте и в имени пользователя компьютера содержатся символы Unicode (например, ваше имя — `Zoë`), любой проект, расположенный в папке `Мои документы`, столкнётся с этой проблемой. Часто достаточно просто переместить проект, например, в `D:\Project`, чтобы устранить эти загадочные ошибки.

Использование других символов вне диапазонов `a-z`, `A-Z` и `0-9`, таких как `@`, `-`, `_`, `,`, `*` и `#`, также может привести к неожиданным и трудно отслеживаемым проблемам на других платформах, в системах контроля версий и в менее надёжных инженерных инструментах.

<a name="structure-no-empty-folders"></a>
#### Никаких пустых папок
Не должно быть никаких пустых папок. Они захламляют обозреватель контента.

Если вы обнаружили в обозревателе контента пустую папку, которую нельзя удалить, выполните следующие действия:
1. Убедитесь, что вы используете систему контроля версий.
1. Перейдите к папке на диске и удалите находящиеся внутри ассеты.
1. Закройте редактор.
1. Убедитесь, что состояние вашей системы контроля версий синхронизировано (например, в Perforce выполните Reconcile Offline Work в каталоге контента).
1. Откройте редактор. Убедитесь, что всё работает как ожидалось. Если нет — откатите изменения, разберитесь в причине сбоя и повторите попытку.
1. Убедитесь, что папка исчезла.
1. Зафиксируйте изменения в системе контроля версий.

<a name="2.2"></a>
<a name="structure-top-level"><a>
### 2.2 Используйте корневую папку для ассетов, специфичных для проекта
Все ассеты проекта должны находиться в папке, названной в честь проекта. Например, если ваш проект называется 'Generic Shooter', _всё_ его содержимое должно находиться в `Assets/GenericShooter`.

> Папка `Developers` не предназначена для ассетов, от которых зависит ваш проект, и, следовательно, не является специфичной для проекта. См. [Папки разработчиков](#2.3) для подробностей.

Существует несколько причин для такого подхода.

<a name="2.2.1"></a>
#### Никаких глобальных ассетов
Часто в руководствах по стилю кода говорится, что не следует загрязнять глобальное пространство имён, и это правило следует той же логике. Когда ассетам разрешено находиться вне папки проекта, становится намного сложнее поддерживать строгую структуру, так как наличие ассетов вне папки поощряет плохую практику неорганизованного хранения.

Каждый ассет должен иметь своё назначение, иначе ему не место в проекте. Если ассет является экспериментальным тестом и не должен использоваться в проекте, он должен быть помещён в папку [`Developer`](#2.3).

<a name="2.2.2"></a>
#### Уменьшение конфликтов при миграции
При работе над несколькими проектами команда часто копирует ассеты из одного проекта в другой, если они оказались полезными для обоих.

Размещая все специфичные для проекта ассеты в корневой папке, вы снижаете вероятность конфликтов при миграции этих ассетов в новый проект.

<a name="2.2.2e1"></a>
##### Пример с мастер-материалом
Допустим, вы создали мастер-материал в одном проекте и хотите использовать его в другом, поэтому вы переносите этот ассет. Если он не находится в корневой папке, его путь может быть, например, `Assets/MaterialLibrary/M_Master`. Если в целевом проекте ещё нет мастер-материала, проблем не возникнет.

По мере развития одного или обоих проектов, их мастер-материалы могут изменяться с учётом особенностей каждого проекта.

Проблема возникает, когда, например, художник для одного из проектов создаёт модульный набор статических мешей, и кто-то хочет использовать его во втором проекте. Если художник использовал экземпляры материалов на основе `Assets/MaterialLibrary/M_Master`, как и было указано, при миграции скорее всего возникнет конфликт с уже перенесённым ранее ассетом `Assets/MaterialLibrary/M_Master`.

Эту проблему трудно предсказать и учесть. Человек, переносящий статические меши, может не быть знаком с разработкой мастер-материала в обоих проектах и даже не знать, что меши используют экземпляры материалов, основанные на мастер-материале. Однако инструмент миграции требует всю цепочку зависимостей и, следовательно, будет вынужден скопировать `Assets/MaterialLibrary/M_Master`, перезаписав существующий ассет.

Если мастер-материалы двух проектов несовместимы _хоть немного_, вы рискуете сломать всю библиотеку материалов проекта, а также любые другие зависимости, которые уже были перенесены, просто потому что ассеты не были размещены в корневой папке. Простая миграция статических мешей превращается в очень трудную задачу.

<a name="2.2.3"></a>
#### Примеры, шаблоны и сторонний контент безопасны
В дополнение к [2.2.2](#2.2.2), если кто-то из команды добавит примерный контент, шаблоны или ассеты, купленные у третьих лиц, можно быть уверенным, что эти ассеты не вызовут конфликтов в проекте, если только имя корневой папки проекта уникально.

Вы не можете доверять стороннему контенту в том, что он будет полностью следовать [правилу корневой папки](#2.2). Существуют ассеты, у которых большая часть содержимого находится в корневой папке, но при этом они могут содержать изменённые примерные ассеты Unity и файлы уровней, загрязняющие глобальную папку `Assets`.

Если вы придерживаетесь правила [2.2](#2.2), худший конфликт, который возможен со сторонним контентом — это если два сторонних ассета имеют одинаковое примерное содержимое. Если все ваши ассеты находятся в специфичной для проекта папке, включая примерный контент, который вы туда переместили, ваш проект никогда не сломается.

#### DLC, подпроекты и патчи легко обслуживать
Если в вашем проекте планируется выпуск DLC или есть несколько связанных подпроектов, которые могут быть перенесены или не включены в сборку, ассеты, относящиеся к этим подпроектам, должны иметь собственную отдельную корневую папку. Это делает создание DLC отдельно от основного контента проекта намного проще. Подпроекты также можно переносить с минимальными усилиями. Если вам нужно изменить материал ассета или добавить какое-либо специфичное поведение через патч, вы можете легко разместить эти изменения в папке патча и работать безопасно, не рискуя повредить основной проект.
<a name="2.3"></a>
<a name="structure-developers"></a>
### 2.3 Используйте папку Developers для локального тестирования

Во время разработки проекта очень часто члены команды создают своего рода «песочницу», в которой могут свободно экспериментировать, не рискуя основным проектом. Поскольку работа может быть в процессе, участники могут захотеть разместить свои ассеты на сервере контроля версий проекта. Не все команды требуют использования папок Developer, но те, кто использует их, часто сталкиваются с распространённой проблемой с ассетами, загруженными в систему контроля версий.

Очень легко случайно использовать ассеты, которые ещё не готовы, что приведёт к проблемам после их удаления. Например, художник может работать над модульным набором статичных мешей и всё ещё корректировать их размеры и привязку к сетке. Если левел-дизайнер увидит эти ассеты в основной папке проекта, он может начать использовать их по всему уровню, не зная, что они подлежат значительным изменениям или удалению. Это приводит к масштабной переделке, которую всей команде приходится устранять.

Если бы эти модульные ассеты были размещены в папке Developer, левел-дизайнер не стал бы их использовать, и проблема бы не возникла.

Когда ассеты будут готовы к использованию, художнику достаточно просто переместить их в соответствующую папку проекта. Это, по сути, «повышает» ассеты от экспериментальных до производственных.

<a name="levels"></a>
### 2.4 Все [сцены](#terms-level-map) должны находиться в папке Levels

Файлы уровней — это особая категория, и в каждом проекте, как правило, есть своя система наименования карт, особенно если используются подуровни или стриминговые уровни. Независимо от системы организации карт в конкретном проекте, все уровни должны находиться в `Assets/ProjectName/Levels`.

Возможность сказать кому-то «открой такую-то карту» без объяснения, где она находится — это экономия времени и повышение удобства. Часто уровни находятся в подпапках `Levels`, таких как `Levels/Campaign1/` или `Levels/Arenas`, но самое главное — чтобы они все находились в `Assets/ProjectName/Levels`.

Это также упрощает процесс сборки для инженеров. Поиск уровней в случайных папках может быть чрезвычайно утомительным. Если все уровни находятся в одном месте, гораздо сложнее случайно забыть включить карту в сборку. Это также упрощает скрипты для построения освещения и процессы QA.

<a name="2.5"></a>
<a name="structure-ownership"></a>
### 2.5 Определяйте владельцев

Если в команде больше одного человека, определяйте владельцев зон, ассетов или функциональности. Некоторые ассеты, такие как сцены или префабы, плохо переносят одновременное редактирование несколькими людьми, что приводит к конфликтам. Назначение одного ответственного за конкретные ассеты (или дающего разрешение на их изменение) помогает избежать этих проблем.

<a name="2.6"></a>
<a name="structure-assettypes"></a>
### 2.6 Не создавайте папки с именами `Assets` или `AssetTypes`

<a name="2.6.1"></a>
#### Создание папки с именем `Assets` избыточно.
Все ассеты и так являются ассетами.

<a name="2.6.2"></a>
#### Создание папок с именами `Meshes`, `Textures` или `Materials` избыточно.
Имена ассетов уже включают тип в себе. Такие папки дают лишь дублирующую информацию, и их легко заменить удобной системой фильтрации Content Browser.

Хотите просмотреть только статичные меши в `Environment/Rocks/`? Просто включите фильтр Static Mesh. Если все ассеты правильно названы, они будут отсортированы по алфавиту вне зависимости от префиксов. Хотите увидеть статичные и скелетные меши? Включите оба фильтра — это исключает необходимость зажимать `Control` и выделять две папки в дереве Content Browser.

> Это также удлиняет путь до ассета без какой-либо пользы. Префикс `SM_` для статичного меша — всего три символа, а `Meshes/` — семь.

Не создавая такие папки, вы также предотвращаете ситуацию, когда кто-то случайно поместит статичный меш или текстуру в папку `Materials`.

<a name="2.7"></a>
<a name="structure-large-sets"></a>
### 2.7 Очень большие наборы ассетов получают собственную структуру папок

Это можно рассматривать как условное исключение из правила [2.6](#2.6).

Некоторые типы ассетов могут содержать огромное количество связанных файлов, где каждый файл выполняет уникальную функцию. Наиболее распространённые примеры — анимации и аудио. Если у вас более 15 подобных ассетов, связанных между собой, их следует хранить вместе.

Например, анимации, используемые несколькими персонажами, следует размещать в `Characters/Common/Animations`, возможно с подпапками вроде `Locomotion` или `Cinematic`.

> Это не относится к ассетам вроде текстур и материалов. Вполне нормально, если в папке `Rocks` много текстур, но обычно эти текстуры связаны только с несколькими конкретными объектами и должны быть соответствующим образом названы. Даже если они являются частью [библиотеки материалов](#2.8).

<a name="2.8"></a>
<a name="structure-material-library"></a>
### 2.8 `MaterialLibrary`

Если ваш проект использует мастер-материалы, многослойные материалы или любые переиспользуемые материалы/текстуры, которые не относятся ни к одной подкатегории ассетов, их следует размещать в `Assets/ProjectName/MaterialLibrary`.

Так у всех «глобальных» материалов будет своё место, и их легко будет найти.

> Это также упрощает реализацию политики «использовать только экземпляры материалов». Если все художники и ассеты должны использовать экземпляры материалов, то единственные обычные материалы, которые должны существовать — это те, что находятся в `MaterialLibrary`. Это легко проверить поиском базовых материалов вне этой папки.

`MaterialLibrary` может содержать не только материалы. Общие утилитные текстуры, функции материалов и другие подобные элементы также следует размещать здесь, в соответствующих папках. Например, универсальные шумовые текстуры — в `MaterialLibrary/Utility`.

Любые тестовые или отладочные материалы следует размещать в `MaterialLibrary/Debug`. Это позволяет легко удалить их перед релизом и сразу видеть, если производственные ассеты используют их — при возникновении ошибок ссылок.

<a name="2.9"></a>
<a name="scene-structure"></a>
## 2.9 Структура сцены

Помимо иерархии проекта, существует также иерархия сцены. Как и раньше, мы предлагаем шаблон, который вы можете адаптировать под свои нужды. Используйте пустые игровые объекты с именами как «папки» сцены.

<pre>
@System
@Debug
@Management
@UI
    Layouts
Cameras
Lights
    Volumes
Particles
Sound
World
    Global
    Room1
        Architecture
        Terrain
        Props
Gameplay
    Actors
    Items
    Triggers
    Quests
_Dynamic
</pre>

- Все пустые объекты должны располагаться в координатах 0,0,0 с поворотом и масштабом по умолчанию.
- Для пустых объектов, служащих только контейнерами для скриптов, используйте префикс “@” – например, `@Cheats`.
- Если вы создаёте объект во время выполнения, размещайте его в `_Dynamic` — не загромождайте корень иерархии, иначе навигация станет неудобной.

**[⬆ Наверх](#table-of-contents)**

<a name="scripts"></a>

## 3. Скрипты

Этот раздел посвящён C#-классам и их структуре. По возможности, правила оформления соответствуют стандартам Microsoft C#.

### Разделы
> 3.1 [Организация класса](#classorganization)  
> 3.2 [Компиляция](#compiling)  
> 3.3 [Переменные](#variables)  
> 3.4 [Функции](#functions)

<a name="classorganization"></a>
### 3.1 Организация класса

Файл исходного кода должен содержать только один публичный тип, хотя допускается наличие нескольких внутренних классов.

Имя файла должно совпадать с именем публичного класса, находящегося в этом файле.

Пространства имён следует организовывать по чётко определённой структуре.

Члены класса следует упорядочивать по алфавиту и группировать в следующие секции:
* Константные поля
* Статические поля
* Поля
* Конструкторы
* Свойства
* События / Делегаты
* Жизненный цикл (Awake, OnEnable, OnDisable, OnDestroy)
* Публичные методы
* Приватные методы
* Вложенные типы

Внутри каждой группы члены упорядочиваются по уровню доступа:
* public  
* internal  
* protected  
* private  

```csharp
namespace ProjectName
{
    /// <summary>  
    /// Краткое описание того, что делает класс
    /// </summary>
    public class Account
    {
        #region Fields
        
        [Tooltip("Публичные переменные, задаваемые в инспекторе, должны иметь Tooltip")]
        public static string BankName;
        
        /// <summary>  
        /// Также следует добавлять summary
        /// </summary>
        public static decimal Reserves;

        public string BankName;
        public const string ShippingType = "DropShip";
        
        private float _timeToDie;
        
        #endregion

        #region Properties
        
        public string Number { get; set; }
        public DateTime DateOpened { get; set; }
        public DateTime DateClosed { get; set; }
        public decimal Balance { get; set; }
              
        #endregion
       
        #region LifeCycle
        
        public Awake()
        {
            // ...
        }
        
        #endregion

        #region Public Methods
        
        public AddObjectToBank()
        {
            // ...
        }
        
        #endregion
    }
}
```

#### Шаблоны скриптов
Чтобы сэкономить время, вы можете переопределить шаблон скрипта Unity по умолчанию своим собственным, чтобы автоматически задавались пространство имён, регионы и т. д. Подробнее см. в этой статье [поддержки Unity](https://support.unity3d.com/hc/en-us/articles/210223733-How-to-customize-Unity-script-templates).

<a name="namespace"></a>
#### Пространство имён
Используйте пространство имён, чтобы убедиться, что область видимости ваших классов/перечислений/интерфейсов и т. д. не конфликтует с существующими из других пространств имён или глобального пространства имён. Проект должен, как минимум, использовать имя самого проекта в качестве пространства имён, чтобы избежать конфликтов с любыми импортированными сторонними ассетами.

#### Все публичные функции должны иметь описание

Проще говоря, любая функция с модификатором доступа `public` должна иметь заполненное описание.


```csharp
/// <summary>
/// Выстрел из оружия
/// </summary>
public void Fire()
{
    // Произвести выстрел.
}
```

#### Группы со сворачиванием
Если класс содержит лишь небольшое количество переменных, группы со сворачиванием не требуются.

Если класс содержит умеренное количество переменных (5–10), все [сериализуемые](#serializable) переменные должны быть объединены в нестандартную группу со сворачиванием. Распространённая категория — `Config`.

Для создания групп со сворачиванием в Unity есть два варианта:

* Первый — определить `[Serializable] public Class` внутри основного класса, однако это может повлиять на производительность. Это позволяет использовать одно и то же имя переменной повторно.
* Второй вариант — использовать атрибут Foldout Group, доступный в [Odin Inspector](https://odininspector.com/).

```
[[Serializable](https://docs.unity3d.com/ScriptReference/Serializable.html)]
public struct PlayerStats
	{
        public int MovementSpeed;
    }
    
[FoldoutGroup("Interactable")]
public int MovementSpeed = 1;
```

#### Комментирование
Комментарии следует использовать для описания намерений, общего алгоритма и/или логического потока.
Идеально, если, читая только комментарии, кто-то, кроме автора, сможет понять предполагаемое поведение и общую работу функции.

Хотя нет минимальных требований к количеству комментариев, и некоторые очень простые процедуры действительно могут обойтись без них, желательно, чтобы большинство процедур имели комментарии, отражающие намерения и подход программиста.

##### Стиль комментариев
Размещайте комментарий на отдельной строке, а не в конце строки с кодом.

Начинайте текст комментария с заглавной буквы.

Заканчивайте текст комментария точкой.

Оставляйте один пробел между символами комментария (`//`) и текстом комментария, как показано в следующем примере.

Стиль комментариев с двумя косыми чертами (`//`) следует использовать в большинстве случаев. По возможности размещайте комментарии над кодом, а не сбоку. Вот примеры:

```
    // Пример комментария над переменной.
    private int _myInt = 5;

```

#### Regions
The `#region` directive enables you to collapse and hide sections of code in C# files. The ability to hide code selectively makes your files more manageable and easier to read. 
```
#region "This is the code to be collapsed"
    Private components As System.ComponentModel.Container
#endregion
```

#### Spacing
Do use a single space after a comma between function arguments.

Example: `Console.In.Read(myChar, 0, 1);`
* Do not use a space after the parenthesis and function arguments.
* Do not use spaces between a function name and parenthesis.
* Do not use spaces inside brackets.
<a name="3.1"></a>
<a name="compiling"></a>
### 3.2 Compiling
All scripts should compile with zero warnings and zero errors. You should fix script warnings and errors immediately as they can quickly cascade into very scary unexpected behavior.

Do *not* submit broken scripts to source control. If you must store them on source control, shelve them instead.

### 3.3 Variables
The words `variable` and `property` may be used interchangeably.

#### Variable Naming

##### Nouns
All non-boolean variable names must be clear, unambiguous, and descriptive nouns. 

##### Case
All variables use PascalCase unless marked as [private](#privatevariables) which use camelCase. 

Use PascalCase for abbreviations of 4 characters or more (3 chars are both uppercase).

##### Considered Context
All variable names must not be redundant with their context as all variable references in the class will always have context.

###### Considered Context Examples:
Consider a Class called `PlayerCharacter`.

**Bad**

* `PlayerScore`
* `PlayerKills`
* `MyTargetPlayer`
* `MyCharacterName`
* `CharacterSkills`
* `ChosenCharacterSkin`

All of these variables are named redundantly. It is implied that the variable is representative of the `PlayerCharacter` it belongs to because it is `PlayerCharacter` that is defining these variables.

**Good**

* `Score`
* `Kills`
* `TargetPlayer`
* `Name`
* `Skills`
* `Skin`

#### Variable Access Level
In C#, variables have a concept of access level. Public means any code outside the class can access the variable. Protected means only the class and any child classes can access this variable internally. Private means only this class and no child classes can access this variable.
Variables should only be made public if necessary.

Prefer to use the attribute `[SerializeField]` instead of making a variable public.

##### Local Variables
Local variables should use camelCase.

###### Implicitly Typed Local Variables
Use implicit typing for local variables when the type of the variable is obvious from the right side of the assignment, or when the precise type is not important.
```
var var1 = "This is clearly a string.";
var var2 = 27;
var var3 = Convert.ToInt32(Console.ReadLine());
// Also used in for loops
for (var i = 0; i < bountyHunterFleets.Length; ++i) {};
```

Do not use var when the type is not apparent from the right side of the assignment.
Example
```
int var4 = ExampleClass.ResultSoFar();
```

<a name="privatevariables"></a>
##### Private Variables
Private variables should have a prefix with a underscore `_myVariable` and use camelCase.

Unless it is known that a variable should only be accessed within the class it is defined and never a child class, do not mark variables as private. Until variables are able to be marked `protected`, reserve private for when you absolutely know you want to restrict child class usage.

##### Do _Not_ use Hungarian notation
Do _not_ use Hungarian notation or any other type identification in identifiers
```
// Correct
int counter;
string name;
 
// Avoid
int iCounter;
string strName;
```

#### Variables accessible in the Editor

##### Tooltips 
All [Serializable](#serializable) variables should have a description in their `[Tooltip]` fields that explains how changing this value affects the behavior of the script.

##### Variable Slider And Value Ranges
All [Serializable](#serializable) variables should make use of slider and value ranges if there is ever a value that a variable should _not_ be set to.

Example: A script that generates fence posts might have an editable variable named `PostsCount` and a value of -1 would not make any sense. Use the range fields `[Range(min, max)]` to mark 0 as a minimum.

If an editable variable is used in a Construction Script, it should have a reasonable Slider Range defined so that someone can not accidentally assign it a large value that could crash the editor.

A Value Range only needs to be defined if the bounds of a value are known. While a Slider Range prevents accidental large number inputs, an undefined Value Range allows a user to specify a value outside the Slider Range that may be considered 'dangerous' but still valid.

#### Variable Types

##### Booleans

###### Boolean Prefix
All booleans should be named in PascalCase but prefixed with a verb.

Example: Use `isDead` and `hasItem`, **not** `Dead` and `Item`.

###### Boolean Names
All booleans should be named as descriptive adjectives when possible if representing general information.

Try to not use verbs such as `isRunning`. Verbs tend to lead to complex states.

###### Boolean Complex States
Do not use booleans to represent complex and/or dependent states. This makes state adding and removing complex and no longer easily readable. Use an enumeration instead.

Example: When defining a weapon, do **not** use `isReloading` and `isEquipping` if a weapon can't be both reloading and equipping. Define an enumeration named `WeaponState` and use a variable with this type named `WeaponState` instead. This makes it far easier to add new states to weapons.

##### Enums
Enums use PascalCase and use singular names for enums and their values. Exception: bit field enums should be plural. Enums can be placed outside the class space to provide global access.

Example: 
```
public enum WeaponType
{
    Knife,
    Gun
}

// Enum can have multiple values
[Flags]
public enum Dockings
{
	None = 0,
	Top = 1,
}

public WeaponType Weapon
```

##### Arrays
Arrays follow the same naming rules as above, but should be named as a plural noun.

Example: Use `Targets`, `Hats`, and `EnemyPlayers`, not `TargetList`, `HatArray`, `EnemyPlayerArray`.

##### Interfaces
Interfaces are led with a capital `I` then followed with PascalCase.

Example: ```public interface ICanEat { }```

<a name="functions"></a>
### 3.4 Functions, Events, and Event Dispatchers
This section describes how you should author functions, events, and event dispatchers. Everything that applies to functions also applies to events, unless otherwise noted.

#### Function Naming
The naming of functions, events, and event dispatchers is critically important. Based on the name alone, certain assumptions can be made about functions. For example:

* Is it a pure function?
* Is it fetching state information?
* Is it a handler?
* What is its purpose?

These questions and more can all be answered when functions are named appropriately.

<a name="function-verbrule"></a>
#### All Functions Should Be Verbs
All functions and events perform some form of action, whether its getting info, calculating data, or causing something to explode. Therefore, all functions should start with verbs. They should be worded in the present tense whenever possible. They should also have some context as to what they are doing.

Good examples:

* `Fire` - Good example if in a Character / Weapon class, as it has context. Bad if in a Barrel / Grass / any ambiguous class.
* `Jump` - Good example if in a Character class, otherwise, needs context.
* `Explode`
* `ReceiveMessage`
* `SortPlayerArray`
* `GetArmOffset`
* `GetCoordinates`
* `UpdateTransforms`
* `EnableBigHeadMode`
* `IsEnemy` - ["Is" is a verb.](http://writingexplained.org/is-is-a-verb)

Bad examples:

* `Dead` - Is Dead? Will deaden?
* `Rock`
* `ProcessData` - Ambiguous, these words mean nothing.
* `PlayerState` - Nouns are ambiguous.
* `Color` - Verb with no context, or ambiguous noun.

#### Functions Returning Bool Should Ask Questions
When writing a function that does not change the state of or modify any object and is purely for getting information, state, or computing a yes/no value, it should ask a question. This should also follow [the verb rule](#function-verbrule).

This is extremely important as if a question is not asked, it may be assumed that the function performs an action and is returning whether that action succeeded.

Good examples:

* `IsDead`
* `IsOnFire`
* `IsAlive`
* `IsSpeaking`
* `IsHavingAnExistentialCrisis`
* `IsVisible`
* `HasWeapon` - ["Has" is a verb.](http://grammar.yourdictionary.com/parts-of-speech/verbs/Helping-Verbs.html)
* `WasCharging` - ["Was" is past-tense of "be".](http://grammar.yourdictionary.com/parts-of-speech/verbs/Helping-Verbs.html) Use "was" when referring to 'previous frame' or 'previous state'.
* `CanReload` - ["Can" is a verb.](http://grammar.yourdictionary.com/parts-of-speech/verbs/Helping-Verbs.html)

Bad examples:

* `Fire` - Is on fire? Will fire? Do fire?
* `OnFire` - Can be confused with event dispatcher for firing.
* `Dead` - Is dead? Will deaden?
* `Visibility` - Is visible? Set visibility? A description of flying conditions?

#### Event Handlers and Dispatchers Should Start With `On`
Any function that handles an event or dispatches an event should start with `On` and continue to follow [the verb rule](#function-verbrule).

Good examples:

* `OnDeath` - Common collocation in games
* `OnPickup`
* `OnReceiveMessage`
* `OnMessageRecieved`
* `OnTargetChanged`
* `OnClick`
* `OnLeave`

Bad examples:

* `OnData`
* `OnTarget`

**[⬆ Back to Top](#table-of-contents)**
<a name="anc"></a>
<a name="4"></a>

## 4. Asset Naming Conventions
Naming conventions should be treated as law. A project that conforms to a naming convention is able to have its assets managed, searched, parsed, and maintained with incredible ease.

Most things are prefixed with the prefix generally being an acronym of the asset type followed by an underscore.

**Assets use [PascalCase](#cases)**

<a name="base-asset-name"></a>
<a name="4.1"></a>
### 4.1 Base Asset Name - `Prefix_BaseAssetName_Variant_Suffix`
All assets should have a _Base Asset Name_. A Base Asset Name represents a logical grouping of related assets. Any asset that is part of this logical group 
should follow the the standard of  `Prefix_BaseAssetName_Variant_Suffix`.

Keeping the pattern `Prefix_BaseAssetName_Variant_Suffix` in mind and using common sense is generally enough to warrant good asset names. Here are some detailed rules regarding each element.

`Prefix` and `Suffix` are to be determined by the asset type through the following [Asset Name Modifier](#asset-name-modifiers) tables.

`BaseAssetName` should be determined by short and easily recognizable name related to the context of this group of assets. For example, if you had a character named Bob, all of Bob's assets would have the `BaseAssetName` of `Bob`.

For unique and specific variations of assets, `Variant` is either a short and easily recognizable name that represents logical grouping of assets that are a subset of an asset's base name. For example, if Bob had multiple skins these skins should still use `Bob` as the `BaseAssetName` but include a recognizable `Variant`. An 'Evil' skin would be referred to as `Bob_Evil` and a 'Retro' skin would be referred to as `Bob_Retro`.

For unique but generic variations of assets, `Variant` is a two digit number starting at `01`. For example, if you have an environment artist generating nondescript rocks, they would be named `Rock_01`, `Rock_02`, `Rock_03`, etc. Except for rare exceptions, you should never require a three digit variant number. If you have more than 100 assets, you should consider organizing them with different base names or using multiple variant names.

Depending on how your asset variants are made, you can chain together variant names. For example, if you are creating flooring assets for an Arch Viz project you should use the base name `Flooring` with chained variants such as `Flooring_Marble_01`, `Flooring_Maple_01`, `Flooring_Tile_Squares_01`.

<a name="1.1-examples"></a>
#### Examples

##### Character

| Asset Type               | Asset Name   |
| ------------------------ | ------------ |
| Skeletal Mesh            | SK_Bob       |
| Material                 | M_Bob        |
| Texture (Diffuse/Albedo) | T_Bob_D      |
| Texture (Normal)         | T_Bob_N      |
| Texture (Evil Diffuse)   | T_Bob_Evil_D |

##### Prop

| Asset Type               | Asset Name   |
| ------------------------ | ------------ |
| Static Mesh (01)         | SM_Rock_01   |
| Static Mesh (02)         | SM_Rock_02   |
| Static Mesh (03)         | SM_Rock_03   |
| Material                 | M_Rock       |
| Material Instance (Snow) | MI_Rock_Snow |

<a name="asset-name-modifiers"></a>
### 4.2 Asset Name Modifiers

When naming an asset use these tables to determine the prefix and suffix to use with an asset's [Base Asset Name](#base-asset-name).

#### Sections

> 4.2.1 [Most Common](#anc-common)

> 4.2.2 [Animations](#anc-animations)

> 4.2.3 [Artificial Intelligence](#anc-ai)

> 4.2.4 [Prefabs](#anc-prefab)

> 4.2.5 [Materials](#anc-materials)

> 4.2.6 [Textures](#anc-textures)

> 4.2.7 [Miscellaneous](#anc-misc)

> 4.2.8 [Physics](#anc-physics)

> 4.2.9 [Audio](#anc-audio)

> 4.2.10 [User Interface](#anc-ui)

> 4.2.11 [Effects](#anc-effects)

<a name="anc-common"></a>
#### Most Common

| Asset Type              | Prefix     | Suffix     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Level / Scene           |  *          |            | [Should be in a folder called Levels.](#levels) e.g. `Levels/A4_C17_Parking_Garage.unity` |
| Level (Persistent)      |            | _P         |                                  |
| Level (Audio)           |            | _Audio     |                                  |
| Level (Lighting)        |            | _Lighting  |                                  |
| Level (Geometry)        |            | _Geo       |                                  |
| Level (Gameplay)        |            | _Gameplay  |                                  |
| Prefab                  |        |            |                                  |
| Probe (Reflection)      | RP_        |            |                                  |
| Probe (Light)           | LP_        |            |                                  |
| Volume                  | V_         |            |                                  |
| Trigger Area            |            | _Trigger   |                                  |
| Material                | M_         |            |                                  |
| Static Mesh             | SM_       |            |                                  |
| Skeletal Mesh           | SK_       |            |                                  |
| Texture                 | T_         | _?         | See [Textures](#anc-textures)    |
| Visual Effects          | VFX_       |            |                                  |
| Particle System         | PS_       |            |                                  |
| Light                   | L_         |            |                                  |
| Camera (Cinemachine)    | CM_         |            | Virtual Camera                   |

<a name="anc-models"></a>

#### 4.2.1a 3D Models (FBX Files)

PascalCase

| Asset Type    | Prefix | Suffix | Notes |
| ------------- | ------ | ------ | ----- |
| Characters    | CH_    |        |       |
| Vehicles      | VH_    |        |       |
| Weapons       | WP_    |        |       |
| Static Mesh   | SM_    |        |       |
| Skeletal Mesh | SK_    |        |       |
| Skeleton      | SKEL_  |        |       |
| Rig           | RIG_   |        |       |

#### 4.2.1b 3d Models (3ds Max)

All meshes in 3ds Max are lowercase to differentiate them from their FBX export.

| Asset Type    | Prefix | Suffix      | Notes                                   |
| ------------- | ------ | ----------- | --------------------------------------- |
| Mesh          |        | _mesh_lod0* | Only use LOD suffix if model uses LOD's |
| Mesh Collider |        | _collider   |                                         |

<a name="anc-animations"></a>

#### 4.2.2 Animations 
| Asset Type           | Prefix | Suffix | Notes |
| -------------------- | ------ | ------ | ----- |
| Animation Clip       | A_     |        |       |
| Animation Controller | AC_    |        |       |
| Avatar Mask          | AM_    |        |       |
| Morph Target         | MT_    |        |       |

<a name="anc-ai"></a>
#### 4.2.3 Artificial Intelligence

| Asset Type              | Prefix     | Suffix     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| AI / NPC                | AI_        |  _NPC          |   *Npc could be pawn of CH_ !AI_                          |
| Behavior Tree           | BT_      |            |                                  |
| Blackboard              | BB_       |            |                                  |
| Decorator               | BTDecorator_ |          |                                  |
| Service                 | BTService_ |            |                                  |
| Task                    | BTTask_  |            |                                  |
| Environment Query       | EQS_     |            |                                  |
| EnvQueryContext         | EQS_     | Context    |                                  |

<a name="anc-prefab"></a>
#### 4.2.4 Prefabs

| Asset Type              | Prefix     | Suffix     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Prefab         |        |            |                                  |
| Prefab Instance         | I       |            |                                  |
| Scriptable Object       |     |        | Assigned "Blueprint" label in Editor |

<a name="anc-materials"></a>

#### 4.2.5 Materials
| Asset Type        | Prefix | Suffix | Notes |
| ----------------- | ------ | ------ | ----- |
| Material          | M_     |        |       |
| Material Instance | MI_    |        |       |
| Physical Material | PM_    |        |       |
| Material Shader Graph | MSG_    |        |       |

<a name="anc-textures"></a>

#### 4.2.6 Textures
| Asset Type              | Prefix     | Suffix     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Texture                 | T_         |            |                                  |
| Texture (Base Color)    | T_         | _BC         | Diffuse / Albedo     	       |
| Texture (Metallic / Smoothness)| T_  | _MS        |                                  |
| Texture (Normal)        | T_         | _N         |                                  |
| Texture (Alpha)         | T_         | _A         |                                  |
| Texture (Height)          | T_         | _H         |                                  |
| Texture (Ambient Occlusion) | T_     | _AO      |                                  |
| Texture (Emissive)      | T_         | _E         |                                  |
| Texture (Mask)          | T_         | _M         |                                  |
| Texture (Packed)        | T_         | _*         | See notes below about [packing](#anc-textures-packing). |
| Texture Cube            | TC_       |            |                                  |
| Media Texture           | MT_       |            |                                  |
| Render Target           | RT_       |            |                                  |
| Cube Render Target      | RTC_     |            |                                  |
| Texture Light Profile   | TLP_     |            |                                  |

<a name="anc-textures-packing"></a>

#### 4.2.6.1 Texture Packing
It is common practice to pack multiple layers of texture data into one texture. An example of this is packing Emissive, Roughness, Ambient Occlusion together as the Red, Green, and Blue channels of a texture respectively. To determine the suffix, simply stack the given suffix letters from above together, e.g. `_ERO`.

> It is generally acceptable to include an Alpha/Opacity layer in your Diffuse/Albedo's alpha channel and as this is common practice, adding `A` to the `_D` suffix is optional.

Packing 4 channels of data into a texture (RGBA) is not recommended except for an Alpha/Opacity mask in the Diffuse/Albedo's alpha channel as a texture with an alpha channel incurs more overhead than one without.
<a name="anc-misc"></a>

#### 4.2.7 Miscellaneous

| Asset Type                      | Prefix | Suffix | Notes |
| ------------------------------- | ------ | ------ | ----- |
| Universal Render Pipeline Asset | URP_   |        |       |
| HD Render Pipeline Asset        | HDRP_  |        |       |
| Post Process Volume Profile     | PP_    |        |       |
| User Interface                  | UI_    |        |       |

<a name="anc-physics"></a>
#### 4.2.8 Physics

| Asset Type        | Prefix | Suffix | Notes |
| ----------------- | ------ | ------ | ----- |
| Physical Material | PM_    |        |       |

<a name="anc-audio"></a>

#### 4.2.9 Audio

| Asset Type     | Prefix | Suffix | Notes                                                        |
| -------------- | ------ | ------ | ------------------------------------------------------------ |
| Audio Clip     | A_     |        |                                                              |
| Audio Mixer    | MIX_   |        |                                                              |
| Dialogue Voice | DV_    |        |                                                              |
| Audio Class    |        |        | No prefix/suffix. Should be put in a folder called AudioClasses |

<a name="anc-ui"></a>
#### 4.2.10 User Interface
| Asset Type       | Prefix | Suffix | Notes |
| ---------------- | ------ | ------ | ----- |
| Font             | Font_  |        |       |
| Texture (Sprite) | T_     | _GUI   |       |

<a name="anc-effects"></a>
#### 4.2.11 Effects
| Asset Type      | Prefix | Suffix | Notes |
| --------------- | ------ | ------ | ----- |
| Particle System | PS_    |        |       |
**[⬆ Back to Top](#table-of-contents)**

<a name="asset-workflows"></a>

## 5. Asset Workflows

This section describes best practices for creating and importing assets usable in Unity.

<a name="toc"></a>
### Sections

> 5.1 [Unity Asset Import Settings](#unityimport)
>
> 5.2 [3ds Max](#3dsmax)
>
> 5.3 [Textures](#textures)
>
> 5.4 [Audio](#audio)

<a name="unityimport"></a>

### 5.1 Unity Asset Import Settings

Unity's [AssetPostprocessor](https://docs.unity3d.com/ScriptReference/AssetPostprocessor.html) lets you hook into the import pipeline and run scripts prior to or after importing assets. This allows you to enforce import settings when assets are first imported into the project. For example textures that end with `_N` can be marked as a Normal Map on import.

Example guide for Import Settings:

https://github.com/justinwasilenko/Unity-AssetPostProcessor

<a name="3dsmax"></a>
### 5.2 3ds Max

Unity guide on importing from 3ds Max:

https://docs.unity3d.com/2017.4/Documentation/Manual/HOWTO-ImportObjectMax.html

Unity tutorial on the FBX Exporter Package for FBX roundtrip:

https://learn.unity.com/project/3ds-max-to-unity-pipeline

#### Setting up 3ds Max

Unity uses 1 unit = 1 meter. Setup 3ds Max to use Meters by going to ```Customize/Units Setup/System Unit Setup``` and set to 1 Unit = 1 Meter. Using the correct scale is very important for correct Physics / GI / and VR interaction.

Animation frame rate in 3ds Max should be set to 30fps. The ```Time Configuration``` dialog box has 3ds Max's FPS settings

##### Working with Small Objects

* Set ```Customize > Customize User Interface > Mouse Wheel Zoom Increment``` to 0.1m to stop over zooming

* Turn on Viewport Clipping and set the slider on the side of the viewport to be able to zoom in on small meshes. (https://knowledge.autodesk.com/support/3ds-max/learn-explore/caas/sfdcarticles/sfdcarticles/Viewport-Clipping.html)

#### Modeling in 3ds Max

* Follow the [asset naming convention](#anc-models)
* Avoid super long thin triangles (Speeds up tile based renderers & helps with proper GI baking)
* Use Area and Angle Weighted Mesh Normals (Unity Import Setting or Create in 3ds Max)

#### Exporting from 3ds Max into Unity

##### Export Settings:

- Triangulate On
- Tangents and Binormals Off
- Smoothing Groups On
- Preserve edge orientation On
- Units - Automatic Off / Scene Units converted to Meters
- Axis Conversion Z-up

Models created in 3ds Max use a different coordinate system then Unity. Models need to have their pivot point rotated +90 degrees on the X axis to import into Unity correctly.

To do this quickly, open the MaxScript editor, paste this code and select and drag this code on to a Toolbar in 3ds Max to create a button that will run this script. It applies a Xform modifier to rotate the pivot before exporting.

```
fn RotateCreationPivot obj rot =
(
select obj
modPanel.addModToSelection (XForm ()) ui:on
obj.modifiers[#XForm].gizmo.rotation += rot as quat
rotate obj (inverse rot as quat)
)
RotateCreationPivot $ (eulerToQuat(eulerAngles 90 0 0))
```


Script to rotate all objects in 3ds Max scene for export

```
(
    mapped fn ProcessObjectsForUnity node =
    (
        resetxform node
        tm = rotatexmatrix 90
        tm.row4 = node.pos
        node.transform = tm
        node.objectoffsetrot = eulerangles -90 0 0
    )
    
    ProcessObjectsForUnity geometry
)
```

* Batch Exporter for 3ds Max (http://www.strichnet.com/improving-the-fbx-workflow-between-3ds-max-and-unity3d/)

##### Exporting CAT Animation to FBX

Bind normal bones to the CAT rig for use in skinning and exporting

###### Bind Pose

Set Motion Panel/Layer Manager/"Setup/Animation Mode" Toggle to ```Red```
Select only the bones and the mesh you wish to export
Export naming: ModelName.FBX

###### Animation

Set Motion Panel/Layer Manager/"Setup/Animation Mode" to ```Green```
Select ONLY the bones required in your hierarchy (These should match the exact same bones used for Bind Pose), don't include the mesh.
Export naming: ModelName@AnimationName.FBX
The @ symbol is a special Unity naming convention allowing the animation to be bound to the Human.fbx in the Unity editor

#### Importing from 3ds Max into Unity

If importing only animation or bones from a FBX: 

* Set ```Preserve Hierarchy Model``` import option to ```True```
* Set ```Rig > Avatar Definition``` to ```Copy From Other Avatar```

MaxListener Window, set width and height of selected bones, maybe objects too?
$.width = 0.01
$.height = 0.01

**[⬆ Back to Top](#table-of-contents)**

<a name="textures"></a>
### 5.3 Textures

* Textures follow the [naming convention](#anc-textures) found above. 
* They are a power of two (For example, 512 x 512 or 256 x 1024).
* Use Texture Atlases wherever possible.
* 3D software should point to the Unity project textures for consistency when you save or export.
* It is better to resize the texture in Photoshop then to use Unity’s compression options when the in game texture resolution is already known. This reduces the file size and import time of the texture into Unity.
* When working with a high-resolution source PSD outside your Unity project use the same name for both the high-resolution and the imported Unity file. This allows quick iteration when swapping between the 2 textures.

More information for importing textures can be found here: [https://docs.unity3d.com/Manual/ImportingTextures.html](https://docs.unity3d.com/Manual/ImportingTextures.html)

Textures requiring the use of a Alpha channel should follow this guide: [https://docs.unity3d.com/Manual/HOWTO-alphamaps.html](https://docs.unity3d.com/Manual/HOWTO-alphamaps.html)

##### Texture File Format

All textures should be of the .PSD format. No layers should be included and only one Alpha channel in the imported file.

**[⬆ Back to Top](#table-of-contents)**

<a name="audio"></a>
### 5.4 Audio

Only import uncompressed audio files in to Unity using WAV or AIFF formats.

Great guide on [Unity Audio Import Optimization](https://www.gamedeveloper.com/audio/unity-audio-import-optimisation---getting-more-bam-for-your-ram)

**[⬆ Back to Top](#table-of-contents)**



#### Article References:
https://unity3d.com/learn/tutorials/topics/tips/large-project-organisation
https://github.com/Allar/ue4-style-guide
http://www.arreverie.com/blogs/unity3d-best-practices-folder-structure-source-control/
