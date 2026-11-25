# Лабораторна робота №5

**Тема:** CSS. Робота з блочною моделлю. Інструменти веб-розробки браузерів Developer tools  
**Варіант:** 1 (селектор `header#hero_container`)  
**Сайт-джерело:** <https://lpnu.ua/>

## 1. Мета роботи

Навчитися користуватися інструментом веб-розробки Chrome Developer tools.
На прикладі сайту Львівської політехніки дослідити реалізацію селекторів,
блочної моделі, шрифтів та кольорів.

## 2. Теоретичні відомості

### 2.1. Блочна модель CSS (Box Model)

Кожен елемент HTML є прямокутною «коробкою», що складається з:

- **content** — вміст (`width`, `height`);
- **padding** — внутрішні відступи (`padding-top`, `padding-right`, `padding-bottom`, `padding-left`);
- **border** — рамка (`border-width`, `border-style`, `border-color`);
- **margin** — зовнішні відступи (`margin-top`, `margin-right`, `margin-bottom`, `margin-left`).

Розмір елемента залежить від `box-sizing`: у Bootstrap 3 використовується
`border-box`, тому `width` включає padding і border.

### 2.2. Модуль CSS Color

Властивості: `color`, `background-color`, `opacity`; функції `rgb()`, `rgba()`,
`hsl()`, `hsla()`, `hexadecimal` (`#RRGGBB`), `color-mix()`. На сайті lpnu.ua
використано `#0076A8`, `#00A1E4`, `#252775`, `rgb(46,49,146)` та градієнт
`rgba(46,49,146,0) → rgba(46,49,146,1)`.

### 2.3. Модуль CSS Fonts

Властивості: `font-family`, `font-weight`, `font-style`, `font-variant`,
`font-size`, `line-height`, `font-stretch`, `font-feature-settings`, правило
`@font-face`. Сайт підключає Roboto / Roboto Condensed / Roboto Slab через
Google Fonts, а `html { font-size: 62.5% }` робить `1rem = 10px`.

### 2.4. Chrome Developer Tools

Виклик: **F12**, **Ctrl+Shift+I**, контекстне меню → **Inspect**.
Основні панелі: Elements, Console, Sources, Network, Performance, Memory,
Application, Security, Lighthouse (Audits). Для цієї роботи використано
панель **Elements** (дерево DOM, вкладки Styles / Computed, box model).

## 3. Завдання (варіант 1)

1. Відкрито <https://lpnu.ua/> у Chrome, викликано Developer tools (F12).
2. У панелі Elements знайдено елементи `header`. На сторінці їх **5**:
   `#navbar`, `#hero_container`, `#logos_container`, `#featured_container`,
   `#events_container`.
3. Для варіанта 1 обрано селектор **`header#hero_container`**.
4. Розмітку блоку скопійовано (Edit as HTML → Copy outerHTML) у
   `lab5/index.html`; зовнішні посилання зроблено абсолютними, а фонове
   зображення збережено локально в `lab5/images/hero.jpg`.
5. У вкладках Styles і Computed перенесено стилі блочної моделі, шрифтів і
   кольорів блоку `header` та його нащадків у `lab5/css/styles.css`.
6. Стилі відтворюють вигляд оригіналу: hero-зображення з градієнтною тінню,
   заголовок унизу зображення та чотири швидкі посилання під ним.
7. Сторінку додано в меню `index.html` (посилання «Лабораторна робота №5»).

### Структура проєкту

```text
lab5/
├── index.html          # скопійований блок header#hero_container
├── css/styles.css      # перенесені стилі (код подано нижче)
├── images/hero.jpg     # фонове зображення з lpnu.ua
└── README.md           # цей звіт
```

## 4. Відповіді на питання вихідного контролю

### 4.1. Як викликати Developer Tools?

Клавіша **F12**, комбінація **Ctrl+Shift+I** (Windows), контекстне меню
елемента → **Inspect / Перевірити** або меню браузера → More tools →
Developer tools.

### 4.2. Які панелі доступні у Chrome Developer Tools?

Elements, Console, Sources, Network, Performance, Memory, Application,
Security, Lighthouse (Audits), Recorder, Coverage, Rendering та інші.

### 4.3. Які можливості панелі Elements використано?

Перегляд дерева DOM, пошук елемента `header#hero_container`, копіювання
HTML-коду (Copy outerHTML), перегляд застосованих стилів у вкладці **Styles**,
обчислених значень і box model у вкладці **Computed**, аналіз медіазапитів
та перевірка станів `:hover` / `:active` для посилань.

### 4.4. Які типи селекторів використано?

- селектори тегів: `header`, `section`, `div`, `h2`, `a`, `i`;
- селектори ідентифікаторів: `#hero_container`, `#hero`,
  `#block-lpnushortcutstop4`, `#block-views-block-front-page-news-block-1`;
- селектори класів: `.region-hero`, `.container`, `.row`, `.col-xs-6`,
  `.col-sm-3`, `.shortcut-1` … `.shortcut-4`, `.shadow`, `.clearfix`;
- селектори нащадків: `#hero h2`, `#hero .container`,
  `#block-lpnushortcutstop4 h2`, `#block-lpnushortcutstop4 .col-xs-6`;
- селектор атрибута: `[class*="col-xs-"]`;
- псевдокласи: `:link`, `:visited`, `:hover`, `:active`;
- псевдоелементи: `::before`, `::after`;
- медіазапити: `min-width: 480px`, `768px`, `992px`, `1200px`, `1600px`.

### 4.5. Які властивості CSS Block Model використано?

`width`, `min-height`, `padding`, `margin` (включно з від'ємними `-15px` у
`.row` та `auto` у `.container`), `border-top`, `box-sizing: border-box`,
`position: relative/absolute`, `float`, `transform: translate(-50%, -50%)`.

### 4.6. Які властивості CSS Fonts використано?

`font-family` (Roboto, Roboto Condensed, Helvetica Neue), `font-size`
(`1.6rem`, `2.2rem` … `5rem`), `font-weight` (400 / 500), `font-style`,
`line-height: 1.42857143`. Розмір кореневого шрифту — `62.5%`.

### 4.7. Які властивості CSS Color використано?

`color` (`#333`, `#fff`, `#0076A8`, `#00A1E4`), `background-color`
(`#fff`, `#252775`, `rgb(46,49,146)`), `background` із зображенням і
градієнтом `rgba(...)`, `transition: color 3s ease-out`.

## 5. Код файлу `lab5/css/styles.css`

`css
/* ==========================================================================
   Лабораторна робота №5, варіант 1
   Стилі скопійовані з головної сторінки https://lpnu.ua/
   для блоку header#hero_container та його нащадків.
   Джерела: Bootstrap 3.4.1, Drupal Bootstrap, тема lpnu.ua
   ========================================================================== */

/* --- База: блочна модель, шрифти й кольори (як у DevTools → Computed) --- */
*,
*::before,
*::after {
  box-sizing: border-box;
}

html {
  font-size: 62.5%; /* 1rem = 10px, як на lpnu.ua */
  -webkit-text-size-adjust: 100%;
  -ms-text-size-adjust: 100%;
}

body {
  margin: 0;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-size: 1.6rem;
  line-height: 1.42857143;
  color: #333;
  background-color: #fff;
}

.fontyourface {
  font-family: "Roboto", "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-style: normal;
  font-weight: normal;
}

a {
  text-decoration: none;
}

a:link,
a:visited {
  color: #0076A8;
  text-decoration: none;
  transition: color 0.5s ease-out;
}

a:hover,
a:active {
  color: #00A1E4;
  text-decoration: none;
  transition: color 0.5s ease-out;
}

h2 {
  font-family: inherit;
  font-weight: 500;
  line-height: 1.1;
  color: inherit;
  margin: 20px 0 10px;
  font-size: 30px;
}

/* --- Сітка Bootstrap 3, яка використана всередині header --- */
.container,
.container-fluid {
  padding-right: 15px;
  padding-left: 15px;
  margin-right: auto;
  margin-left: auto;
}

.container::before,
.container::after,
.container-fluid::before,
.container-fluid::after,
.clearfix::before,
.clearfix::after,
.row::before,
.row::after {
  display: table;
  content: " ";
}

.container::after,
.container-fluid::after,
.clearfix::after,
.row::after {
  clear: both;
}

.row {
  margin-right: -15px;
  margin-left: -15px;
}

[class*="col-xs-"],
[class*="col-sm-"] {
  position: relative;
  min-height: 1px;
  padding-right: 15px;
  padding-left: 15px;
}

.col-xs-6,
.col-sm-3 {
  float: left;
}

.col-xs-6 {
  width: 50%;
}

/* ==========================================================================
   header#hero_container
   ========================================================================== */
#hero_container {
  display: block;
}

#hero {
  position: relative;
  width: 100% !important;
  background-position: center center !important;
  background-size: cover !important;
  min-height: 200px;
  background-color: rgb(46, 49, 146);
}

#hero .container {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  margin: auto;
}

.shadow {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  min-height: 120px;
  background: linear-gradient(to bottom, rgba(46, 49, 146, 0), rgba(46, 49, 146, 1));
}

#hero h2 {
  text-align: center;
  margin: 0 0 24px;
  font-size: 22px;
}

#hero a:link,
#hero a:visited {
  color: #fff;
  text-decoration: none;
  transition: color 3s ease-out;
}

#hero a:hover,
#hero a:active {
  color: #00A1E4;
  text-decoration: none;
  transition: color 3s ease-out;
}

/* ==========================================================================
   Блок швидких посилань #block-lpnushortcutstop4
   ========================================================================== */
#block-lpnushortcutstop4 {
  background: rgb(46, 49, 146);
}

#block-lpnushortcutstop4::before {
  display: block;
  width: 100%;
  height: 2px;
  content: "";
  background-image: linear-gradient(to right, #2E3192 0%, #fff 50%, #2E3192 100%);
}

#block-lpnushortcutstop4 .col-xs-6 {
  position: relative;
  min-height: 104px;
}

#block-lpnushortcutstop4 h2 {
  margin: 0;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
  font-size: 15px;
}

#block-lpnushortcutstop4 h2 svg,
#block-lpnushortcutstop4 h2 i {
  color: #00A1E4;
  margin-right: 0.5rem;
}

.shortcut-1,
.shortcut-4 {
  background: #252775;
}

#block-lpnushortcutstop4 a:link,
#block-lpnushortcutstop4 a:visited {
  color: #fff;
  text-decoration: none;
  transition: color 3s ease-out;
}

#block-lpnushortcutstop4 a:hover,
#block-lpnushortcutstop4 a:active {
  color: #00A1E4;
  text-decoration: none;
  transition: color 3s ease-out;
}

/* ==========================================================================
   Адаптивні стани (медіазапити сайту lpnu.ua)
   ========================================================================== */
@media only screen and (min-width: 480px) {
  #hero {
    min-height: 300px;
  }

  .shadow {
    min-height: 160px;
  }

  #hero h2 {
    margin: 0 0 30px;
    font-size: 34px;
  }

  #block-lpnushortcutstop4 .col-xs-6 {
    min-height: 106px;
  }

  #block-lpnushortcutstop4 h2 {
    font-size: 17px;
  }
}

@media only screen and (min-width: 768px) {
  /* На сайті над hero є navbar висотою 55px — компенсуємо його відсутність */
  body {
    padding-top: 55px;
  }

  .container {
    width: 750px;
  }

  .col-sm-3 {
    width: 25%;
  }

  #hero {
    min-height: 400px;
    margin-top: -55px;
    border-top: 1px solid rgb(46, 49, 146);
  }

  .shadow {
    min-height: 215px;
  }

  #hero h2 {
    font-size: 40px;
    margin: 0 0 30px;
  }

  #block-lpnushortcutstop4 .col-xs-6 {
    min-height: 110px;
  }

  #block-lpnushortcutstop4 h2 {
    font-size: 15px;
  }

  .shortcut-1,
  .shortcut-3 {
    background: none;
  }

  .shortcut-2,
  .shortcut-4 {
    background: #252775;
  }
}

@media only screen and (min-width: 992px) {
  .container {
    width: 970px;
  }

  #hero {
    min-height: 500px;
  }

  .shadow {
    min-height: 270px;
  }

  #hero h2 {
    margin: 0 0 40px;
  }

  #block-lpnushortcutstop4 .col-xs-6 {
    min-height: 124px;
  }

  #block-lpnushortcutstop4 h2 {
    font-size: 18px;
  }
}

@media only screen and (min-width: 1200px) {
  .container {
    width: 1170px;
  }

  #hero {
    min-height: 550px;
  }

  .shadow {
    min-height: 295px;
  }

  #hero h2 {
    font-size: 50px;
    margin: 0 0 50px;
  }

  #block-lpnushortcutstop4 .col-xs-6 {
    min-height: 134px;
  }

  #block-lpnushortcutstop4 h2 {
    font-size: 21px;
  }
}

@media only screen and (min-width: 1600px) {
  #hero {
    min-height: 650px;
  }

  .shadow {
    min-height: 350px;
  }

  #hero h2 {
    margin: 0 0 65px;
  }

  #block-lpnushortcutstop4 .col-xs-6 {
    min-height: 120px;
  }

  #block-lpnushortcutstop4 h2 {
    font-size: 22px;
  }
}

`

## 6. Висновок

У роботі досліджено реалізацію блочної моделі, шрифтів і кольорів на сайті
Львівської політехніки за допомогою Chrome DevTools. Для варіанта 1
відтворено блок `header#hero_container` разом із заголовком новини та блоками
швидких посилань. Отримано навички роботи з панеллю Elements, вкладками
Styles і Computed, перегляду box model і перенесення стилів у власний CSS.

Git-команди (створення вітки `lab5`, merge, push) не виконувалися: проєкт
не є git-репозиторієм, робота залишена у папці проєкту.
