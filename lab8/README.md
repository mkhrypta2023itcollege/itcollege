# Лабораторна робота №8

**Тема:** Використання SCSS для створення адаптивних стилів  
**Варіант:** без варіантів (скопійовано сторінку лабораторної роботи №7, варіант 2)  
**Сайт-джерело:** <https://lpnu.ua/>

## 1. Мета роботи

Навчитися використовувати препроцесор Sass/SCSS на прикладі верстки головної
сторінки lpnu.ua. Закріпити навички розробки адаптивної веб-сторінки з
використанням гнучких макетів (Flexbox) та грідів (Grid), а також освоїти
компіляцію SCSS у CSS і роботу з source maps.

## 2. Теоретичні відомості

### 2.1. Що таке Sass і SCSS

Sass — препроцесор CSS, який додає до звичайного CSS програмування-подібні
можливості: змінні, вкладеність, міксини, мапи, цикли, умови, імпорти/модулі.
**SCSS** — один із двох синтаксисів Sass (разом із синтаксисом `.sass`).
Файли SCSS мають розширення `.scss` і майже повністю повторюють синтаксис CSS,
тож звичайний CSS є валідним SCSS. Браузер не розуміє SCSS напряму — його
потрібно скомпілювати у CSS.

### 2.2. Основні можливості SCSS

- **Змінні** (`$primary-color: #0076A8;`) — зберігають кольори, розміри, шрифти.
- **Вкладеність** — стилі дочірніх елементів описуються всередині батьківського
  селектора, що відповідає ієрархії HTML.
- **Міксини** (`@mixin`, `@include`) — повторювані набори стилів із параметрами.
- **Мапи** — асоціативні масиви `ключ: значення`, доступ через `map.get()`.
- **Модульність** (`@use`) — розділення стилів на partial-файли (`_variables.scss`,
  `_mixins.scss`) і підключення їх у головному файлі.
- **Компіляція**: `sass --watch scss:css`; для карт джерел — `sass --source-map scss:css`.

### 2.3. Source maps

Файл `css/styles.css.map` зв'язує скомпільований CSS із вихідним SCSS. У кінці
CSS додається коментар `/*# sourceMappingURL=styles.css.map */`. У DevTools
браузера можна бачити оригінальний SCSS-код і номер рядка, а не лише результат
компіляції, що значно спрощує налагодження.

## 3. Порядок виконання роботи

1. Сторінку лабораторної роботи №7 (варіант 2) скопійовано в папку `lab8`:
   `index.html`, зображення `images/hero.jpg` та 12 зображень новин.
2. Стилі `css/styles.css` перенесено у `lab8/scss/styles.scss`.
3. Створено окремі partial-файли:
   - `scss/_variables.scss` — кольори (`$primary-color`, `$secondary-color`,
     `$text-color` та ін.), розміри шрифтів і мапа `$breakpoints`;
   - `scss/_mixins.scss` — міксин `respond-to($breakpoint)`.
4. У `styles.scss` застосовано змінні замість «магічних» значень і вкладеність
   селекторів (`#hero`, `#block-lpnushortcutstop4`, `.news-grid .views-col` тощо).
5. Медіа-запити переписано через `@include m.respond-to(mobile/tablet/desktop)`.
6. Виконано компіляцію командою `sass --source-map scss:css` — створено
   `css/styles.css` і `css/styles.css.map` без помилок і попереджень.
7. У кореневий `index.html` додано посилання на `lab8/index.html`.
8. Сторінку перевірено у браузері на трьох брейкпоінтах.

### Структура проєкту

```text
lab8/
├── index.html              # сторінка з lab7 (header flex + новини grid)
├── css/
│   ├── styles.css          # скомпільований CSS
│   └── styles.css.map      # карта джерел (source map)
├── scss/
│   ├── _variables.scss     # змінні кольорів, шрифтів і мапа брейкпоінтів
│   ├── _mixins.scss        # міксин respond-to()
│   └── styles.scss         # основний файл з вкладеністю та @include
├── images/                 # hero.jpg + 12 зображень новин
└── README.md               # цей звіт
```

### Команди компіляції

```bash
# одноразова компіляція з картою джерел
sass --source-map scss:css

# автоматичне стеження за змінами
sass --watch --source-map scss:css
```

## 4. Відповіді на питання вихідного контролю

### 4.1. Що таке SCSS і чим він відрізняється від CSS?

SCSS — це синтаксис препроцесора Sass, розширення CSS. На відміну від CSS,
він підтримує змінні, вкладеність селекторів, міксини, мапи, умови, цикли
та модульність (`@use`). SCSS-файли компілюються у звичайний CSS, який і
завантажує браузер. Синтаксис SCSS схожий на CSS (на відміну від старого
синтаксису Sass із `.sass`), тому CSS-код можна просто скопіювати у `.scss`.

### 4.2. Як оголошуються змінні в SCSS? Наведіть приклад з роботи.

Змінні починаються з символу `$`, значення записується через двокрапку:

```scss
$primary-color: #0076A8;
$secondary-color: #00A1E4;
$text-color: #333;
$font-size-teaser: 1.8rem;
```

У роботі вони оголошені у `scss/_variables.scss` і використані, наприклад:

```scss
a {
  color: v.$primary-color;
  &:hover { color: v.$secondary-color; }
}
```

### 4.3. Як використовуються міксини в SCSS? Наведіть приклад з роботи.

Міксин оголошується через `@mixin` і підключається через `@include`. У роботі
міксин `respond-to($breakpoint)` отримує ім'я брейкпоінту, шукає його у мапі
`$breakpoints` і генерує медіа-запит із вмістом `@content`:

```scss
@mixin respond-to($breakpoint) {
  @if map.has-key(v.$breakpoints, $breakpoint) {
    @media (min-width: map.get(v.$breakpoints, $breakpoint)) {
      @content;
    }
  }
}

// використання
.news-grid {
  @include m.respond-to(tablet) {
    grid-template-columns: 1fr 1fr;
  }
}
```

(В інструкції наведено глобальні функції `map-has-key()` / `map-get()`;
у роботі використано сучасний модуль `sass:map`, щоб уникнути попереджень
Dart Sass про застарілі глобальні функції.)

### 4.4. Які брейкпоінти екрану додали на сторінці?

У мапі `$breakpoints` визначено:

- `mobile: 576px` — збільшення hero та швидких посилань; новини в 1 колонку;
- `tablet: 768px` — 2 колонки новин, 4 швидкі посилання в ряд;
- `desktop: 1024px` — 4 колонки новин.

### 4.5. Що таке source map і як його можна створити при компіляції SCSS у CSS?

Source map (`*.css.map`) — це файл метаданих, який зв'язує рядки скомпільованого
CSS із вихідним SCSS. Завдяки йому DevTools показує початковий SCSS-код і
номер рядка. Створюється прапорцем `--source-map`:

```bash
sass --source-map scss:css
```

У компільованому CSS з'являється коментар `/*# sourceMappingURL=styles.css.map */`.
Для продакшену карту зазвичай не генерують, щоб зменшити розмір файлів.

## 5. Код SCSS

### 5.1. `scss/_variables.scss`

```scss
// ==========================================================================
// Змінні лабораторної роботи №8
// Кольори, розміри шрифтів і брейкпоінти винесені окремо для повторного
// використання та легкої зміни теми сайту.
// ==========================================================================

// Кольори
$primary-color: #0076A8;      // основний синій (посилання, заголовки новин)
$secondary-color: #00A1E4;    // акцентний синій (hover)
$text-color: #333;            // основний текст
$white: #fff;
$hero-color: rgb(46, 49, 146);
$hero-dark: #252775;
$teaser-bg: #f6f6f6;          // підкладка картки новини
$label-bg: #757575;           // тег дати та лінія під зображенням
$teaser-text: #444444;

// Розміри шрифтів (1rem = 10px, бо html { font-size: 62.5% })
$font-size-base: 1.6rem;
$font-size-small: 1.3rem;
$font-size-shortcut: 1.5rem;
$font-size-shortcut-lg: 1.8rem;
$font-size-teaser: 1.8rem;
$font-size-heading: 2.8rem;
$font-size-hero: 2.2rem;
$line-height-base: 1.42857143;
$line-height-teaser: 2.1rem;

// Мапа брейкпоінтів для міксину respond-to
$breakpoints: (
  mobile: 576px,
  tablet: 768px,
  desktop: 1024px
);
```

### 5.2. `scss/_mixins.scss`

```scss
// ==========================================================================
// Міксини лабораторної роботи №8
// ==========================================================================

@use 'sass:map';
@use 'variables' as v;

// Медіа-запит за ім'ям брейкпоінту з мапи $breakpoints.
// У прикладі з інструкції використано глобальні map-has-key()/map-get();
// тут застосовано сучасний модуль sass:map (map.has-key()/map.get()).
@mixin respond-to($breakpoint) {
  @if map.has-key(v.$breakpoints, $breakpoint) {
    @media (min-width: map.get(v.$breakpoints, $breakpoint)) {
      @content;
    }
  }
}
```

### 5.3. `scss/styles.scss`

```scss
// ==========================================================================
// Лабораторна робота №8 — Використання SCSS для створення адаптивних стилів
// Сторінка скопійована з лабораторної роботи №7 (варіант 2):
// header#hero_container — Flexbox, блок «Новини університету» — CSS Grid.
// ==========================================================================

@use 'variables' as v;
@use 'mixins' as m;

*,
*::before,
*::after {
  box-sizing: border-box;
}

html {
  font-size: 62.5%; // 1rem = 10px
  -webkit-text-size-adjust: 100%;
}

body {
  margin: 0;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-size: v.$font-size-base;
  line-height: v.$line-height-base;
  color: v.$text-color;
  background-color: v.$white;
}

.fontyourface {
  font-family: "Roboto", "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-style: normal;
  font-weight: normal;
}

a {
  color: v.$primary-color;
  text-decoration: none;
  transition: color 0.3s ease-out;

  &:hover,
  &:focus {
    color: v.$secondary-color;
  }
}

h2,
h3 {
  font-family: inherit;
  font-weight: 500;
  line-height: 1.1;
  color: inherit;
}

.container,
.container-fluid {
  width: 100%;
  padding-right: 15px;
  padding-left: 15px;
  margin-right: auto;
  margin-left: auto;
}

.clearfix::after {
  display: table;
  clear: both;
  content: "";
}

// --------------------------------------------------------------------------
// 1. header#hero_container — Flexbox (вкладеність за ієрархією HTML)
// --------------------------------------------------------------------------
#hero_container {
  display: flex;
  flex-direction: column;

  .region-hero {
    display: flex;
    flex-direction: column;
  }
}

#hero {
  position: relative;
  display: flex;
  width: 100%;
  min-height: 200px;
  background-color: v.$hero-color;
  background-position: center top !important;
  background-size: cover !important;
  overflow: hidden;

  .shadow {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    min-height: 120px;
    background: linear-gradient(to bottom, rgba(46, 49, 146, 0), rgba(46, 49, 146, 1));
    pointer-events: none;
  }

  .container {
    position: absolute;
    right: 0;
    bottom: 0;
    left: 0;
    display: flex;
    align-items: flex-end;
    justify-content: center;
    margin: auto;
  }

  h2 {
    max-width: 900px;
    margin: 0 0 24px;
    text-align: center;
    font-size: v.$font-size-hero;
  }

  a {
    display: inline-block;
    color: v.$white;
    transition: color 0.4s ease-out, text-shadow 0.4s ease-out;

    &:hover,
    &:focus {
      color: v.$secondary-color;
      text-shadow: 0 2px 12px rgba(0, 0, 0, 0.35);
    }
  }
}

#block-lpnushortcutstop4 {
  display: flex;
  flex-direction: column;
  background: v.$hero-color;

  &::before {
    display: block;
    width: 100%;
    height: 2px;
    content: "";
    background-image: linear-gradient(to right, #2E3192 0%, #fff 50%, #2E3192 100%);
  }

  .field {
    flex: 1 1 auto;
  }

  .shortcuts-row {
    display: flex;
    flex-wrap: wrap;
  }
}

.shortcut-link {
  display: flex;
  flex: 0 0 50%;
  color: v.$white;

  > div {
    display: flex;
    flex: 1 1 auto;
    align-items: center;
    justify-content: center;
    min-height: 104px;
    padding: 12px 15px;
    transition: background-color 0.3s ease;
  }

  h2 {
    display: flex;
    align-items: center;
    gap: 5px;
    margin: 0;
    text-align: center;
    font-size: v.$font-size-shortcut;

    i {
      color: v.$secondary-color;
    }
  }

  &:hover {
    > div {
      background: v.$secondary-color;
    }

    h2,
    h2 i {
      color: v.$white;
    }
  }
}

.shortcut-1,
.shortcut-4 {
  background: v.$hero-dark;
}

// --------------------------------------------------------------------------
// 2. main — сітка новин (Grid, стиль як на lpnu.ua)
// --------------------------------------------------------------------------
.main-container {
  max-width: 940px;
  padding: 0 15px 60px;
  margin: 0 auto;
}

.view-header {
  h2 {
    margin: 30px 0;
    text-align: center;
    font-family: "Roboto Condensed", "Roboto", sans-serif;
    font-size: v.$font-size-heading;
    font-weight: 400;

    a {
      color: v.$primary-color;
      border-bottom: 2px solid v.$primary-color;
      transition: color 2s ease-out, border-color 2s ease-out;

      &:hover,
      &:active {
        color: v.$secondary-color;
        border-bottom-color: v.$secondary-color;
      }
    }
  }
}

.news-grid {
  display: grid;
  grid-template-columns: 1fr; // mobile
  gap: 24px;
  align-items: start;

  // Обгортки Bootstrap 3 не є елементами grid
  .row {
    display: contents;
  }

  .views-col {
    min-width: 0;
    animation: fadeInUp 0.5s ease both;

    > div {
      display: block;
      background: v.$teaser-bg;
    }

    > div > span {
      display: block;
    }

    a {
      display: block;
      color: v.$primary-color;

      &:hover,
      &:focus {
        img {
          opacity: 0.65;
        }

        h3 {
          color: v.$secondary-color;
        }
      }
    }

    .news_teaser {
      color: v.$teaser-text;

      img {
        position: relative;
        z-index: 1;
        display: block;
        width: 100%;
        height: auto;
        margin-bottom: -12px;
        border-bottom: 2px solid v.$label-bg;
        opacity: 1;
        transition: opacity 2s ease-out;
      }

      span {
        position: relative;
        z-index: 2;
        display: inline-block;
        margin-left: 15px;
        padding: 5px 7px;
        color: v.$white;
        font-size: v.$font-size-small;
        letter-spacing: 1px;
        text-transform: uppercase;
        background: v.$label-bg;
      }
    }

    h3 {
      margin: 15px 0 30px;
      padding: 0 15px 15px;
      color: v.$primary-color;
      font-size: v.$font-size-teaser;
      font-weight: bold;
      line-height: v.$line-height-teaser;
      transition: color 0.3s ease-out;
    }
  }
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(18px);
  }

  to {
    opacity: 1;
    transform: translateY(0);
  }
}

// Затримка появи кожної наступної картки (цикл SCSS)
@for $i from 2 through 12 {
  .news-grid .views-col:nth-child(#{$i}) {
    animation-delay: ($i - 1) * 0.05s;
  }
}

// --------------------------------------------------------------------------
// 3. Адаптивність через мапу $breakpoints та міксин respond-to
// --------------------------------------------------------------------------
@include m.respond-to(mobile) {
  #hero {
    min-height: 300px;
  }

  .shadow {
    min-height: 160px;
  }

  #hero h2 {
    font-size: 34px;
  }

  .shortcut-link > div {
    min-height: 106px;
  }
}

@include m.respond-to(tablet) {
  body {
    padding-top: 55px; // компенсація відсутнього navbar lpnu.ua
  }

  .container {
    max-width: 750px;
  }

  #hero {
    min-height: 400px;
  }

  .shadow {
    min-height: 215px;
  }

  #hero h2 {
    font-size: 40px;
  }

  .shortcut-link {
    flex-basis: 25%;
  }

  .shortcut-link > div {
    min-height: 110px;
  }

  .shortcut-1,
  .shortcut-3 {
    background: none;
  }

  .shortcut-2,
  .shortcut-4 {
    background: v.$hero-dark;
  }

  .news-grid {
    grid-template-columns: 1fr 1fr; // tablet: 2 колонки
  }
}

@include m.respond-to(desktop) {
  .container {
    max-width: 970px;
  }

  #hero {
    min-height: 500px;
  }

  .shadow {
    min-height: 270px;
  }

  #hero h2 {
    font-size: 40px;
    margin-bottom: 40px;
  }

  .shortcut-link > div {
    min-height: 124px;
  }

  .shortcut-link h2 {
    font-size: v.$font-size-shortcut-lg;
  }

  .news-grid {
    grid-template-columns: repeat(4, 1fr); // desktop: 4 колонки
  }
}
```

Скомпільований результат — `css/styles.css` разом із `css/styles.css.map`.

## 6. Висновок

У роботі освоєно базові можливості препроцесора SCSS: змінні для кольорів і
шрифтів, вкладеність селекторів за ієрархією HTML, мапу брейкпоінтів і міксин
`respond-to()` для адаптивних медіа-запитів, а також модульну організацію стилів
через `@use`. Сторінку лабораторної роботи №7 успішно переведено на SCSS і
скомпільовано у CSS із source map. Перевірка у браузері підтвердила, що вигляд
сторінки та адаптивні стани (576 / 768 / 1024 px) збережені.

Git-операції (вітка `lab8`, `merge`, `push`) не виконувалися: проєкт не є
git-репозиторієм, робота залишена у папці проєкту.

## Перелік посилань

1. <https://sass-lang.com/>
2. <https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Responsive_Design>
3. <https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Media_queries>
4. <https://developer.chrome.com/docs/devtools>
5. <https://lpnu.ua/>
