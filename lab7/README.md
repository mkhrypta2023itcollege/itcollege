# Лабораторна робота №7

**Тема:** Використання CSS Flexbox, Grid Layout, transitions та animations для верстки сторінки новин  
**Варіант:** 2 (селектор `header#hero_container`)  
**Сайт-джерело:** <https://lpnu.ua/>

## 1. Мета роботи

Закріпити навички створення адаптивної верстки веб-сторінок із використанням
flexbox, grid та медіа-запитів. На прикладі головної сторінки lpnu.ua
проаналізувати принципи реалізації адаптивного макету та відтворити фрагмент
сторінки — блок новин.

## 2. Теоретичні відомості

### 2.1. Flexbox Layout

Одновимірний модуль CSS для розташування елементів по осі X або Y.
Контейнер задається через `display: flex`; основні властивості контейнера:
`flex-direction`, `flex-wrap`, `justify-content`, `align-items`, `align-content`.
Елементи контейнера керують своїм розміром через `flex: grow shrink basis`,
`align-self`, `order`.

У роботі Flexbox використано для:

- `header#hero_container` і `.region-hero` — вертикальний напрямок (`flex-direction: column`);
- `#hero .container` — вирівнювання заголовка (`align-items`, `justify-content`);
- `#block-lpnushortcutstop4 .shortcuts-row` — гнучка плітка посилань із `flex-wrap: wrap`;
- `.shortcut-link` — `flex: 0 0 50%` на мобільних і `flex-basis: 25%` від 768px.

### 2.2. CSS Grid Layout

Двовимірна система: контейнер сітки та елементи сітки. Основні властивості:
`display: grid`, `grid-template-columns`, `grid-template-rows`, `gap`,
`grid-column`, `grid-row`, `justify-items`, `align-items`.
Одиниця `fr` розподіляє вільний простір між колонками.

У роботі Grid використано для сітки новин:
`grid-template-columns: 1fr` → `repeat(2, 1fr)` → `repeat(4, 1fr)`.
Обгортки `.row` оригінальної розмітки зроблено `display: contents`, щоб
`.views-col` стали прямими елементами сітки. `align-items: start` зберігає
 природну висоту кожної картки (як у оригіналі на плаваючих блоках).

### 2.3. Медіа-запити

```css
@media (умова) {
  /* стилі */
}
```

Використано три стани: mobile (< 768px), tablet (768–1023px), desktop (≥ 1024px).

### 2.4. Transitions та animations

`transition` плавно змінює `color`, `opacity` і `background-color`
при наведенні. `@keyframes fadeInUp` анімує появу карток новин;
затримка задається через `:nth-child(n)`.

## 3. Завдання (варіант 2)

1. Відкрито <https://lpnu.ua/> у Chrome і викликано Developer tools (F12).
2. У панелі Elements знайдено 5 елементів `header`: `#navbar`,
   `#hero_container`, `#logos_container`, `#featured_container`,
   `#events_container`. Для варіанта 2 обрано **`header#hero_container`**.
3. Розмітку `header#hero_container` скопійовано й перебудовано на Flexbox:
   hero-блок із заголовком і чотири швидкі посилання під ним.
4. З `div.main-container` скопійовано блок «Новини університету»
   (`section#block-views-block-front-page-news-block-3`) із 12 новинами.
   Зображення новин і hero збережено локально в `lab7/images/`.
5. Сітку новин зверстано на CSS Grid із трьома брейкпоінтами.
6. Вигляд новин відтворено за стилями сайту: сіра підкладка `#f6f6f6`,
   тег дати `#757575` із сірою лінією під зображенням, сині жирні заголовки
   `#0076A8` (замість карток із рамкою та тінню).
7. Додано hover-ефекти (`transition`) та анімацію появи карток (`@keyframes`).
8. У `index.html` додано посилання на `lab7/index.html`.

### Структура проєкту

```text
lab7/
├── index.html          # header#hero_container (flex) + main (grid)
├── css/styles.css      # стилі, медіазапити, transitions, animations
├── images/             # hero.jpg та 12 зображень новин
└── README.md           # цей звіт
```

## 4. Відповіді на питання вихідного контролю

### 4.1. Які властивості CSS FlexBox використали в роботі?

`display: flex`, `flex-direction: column`, `flex-wrap: wrap`, `flex: 0 0 50%`,
`flex: 1 1 auto`, `flex-basis: 25%`, `align-items: center/flex-end`,
`justify-content: center`, `min-width: 0` (для grid-елементів).

### 4.2. Яким чином реалізовано сітку новин на https://lpnu.ua? Чим відрізняється від вашої реалізації?

На lpnu.ua використано Bootstrap 3: `.views-view-grid .views-col { float: left }`
із класами `.col-12`, `.col-sm-6`, `.col-md-3`, `.row` із від'ємними margins
`-15px` і padding колонок `15px`. Тобто сітка побудована на плаваючих блоках
і фіксованих ширинах колонок.

У моїй реалізації застосовано сучасний **CSS Grid**: `display: grid`,
`grid-template-columns` із `fr`, `gap: 24px`, а `.row` має `display: contents`.
Переваги: немає floats і від'ємних відступів, проміжки задаються явно.
Візуальне оформлення карток (сіра підкладка, тег дати, сині заголовки,
зменшення прозорості зображення при наведенні) скопійовано з оригінального
сайту; додатково додано анімацію появи, якої у оригіналі немає.

### 4.3. Які брейкпоінти екрану додали на сторінці?

- **Mobile** — до 767px: 1 колонка новин, 2 швидкі посилання в ряд;
- **Tablet** — 768–1023px: 2 колонки новин, 4 посилання в ряд (`@media (min-width: 768px)`);
- **Desktop** — 1024px і більше: 4 колонки новин (`@media (min-width: 1024px)`).

### 4.4. Які властивості CSS модуля Grid Layout використали в роботі?

`display: grid`, `grid-template-columns: 1fr / repeat(2, 1fr) / repeat(4, 1fr)`,
`gap`, `align-items: start`, `display: contents` для проміжних `.row`,
`min-width: 0` для елементів сітки.

## 5. Код файлу `lab7/css/styles.css`

`css
/* ==========================================================================
   Лабораторна робота №7 — варіант 2
   Flexbox (header#hero_container) + CSS Grid (Новини університету)
   transitions, animations та адаптивність: 768px / 1024px

   Вигляд блоку новин відтворено за стилями сайту lpnu.ua:
   сіра підкладка #f6f6f6, сірий тег дати #757575, сині заголовки #0076A8.
   ========================================================================== */

*,
*::before,
*::after {
  box-sizing: border-box;
}

html {
  font-size: 62.5%; /* 1rem = 10px */
  -webkit-text-size-adjust: 100%;
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
  color: #0076A8;
  text-decoration: none;
  transition: color 0.3s ease-out;
}

a:hover,
a:focus {
  color: #00A1E4;
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

/* ==========================================================================
   1. header#hero_container — FLEXBOX
   ========================================================================== */
#hero_container {
  display: flex;
  flex-direction: column;
}

.region-hero {
  display: flex;
  flex-direction: column;
}

#hero {
  position: relative;
  display: flex;
  width: 100%;
  min-height: 200px;
  background-color: rgb(46, 49, 146);
  background-position: center top !important;
  background-size: cover !important;
  overflow: hidden;
}

.shadow {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  min-height: 120px;
  background: linear-gradient(to bottom, rgba(46, 49, 146, 0), rgba(46, 49, 146, 1));
  pointer-events: none;
}

#hero .container {
  position: absolute;
  right: 0;
  bottom: 0;
  left: 0;
  display: flex;
  align-items: flex-end;
  justify-content: center;
  margin: auto;
}

#hero h2 {
  max-width: 900px;
  margin: 0 0 24px;
  text-align: center;
  font-size: 22px;
}

#hero a {
  display: inline-block;
  color: #fff;
  transition: color 0.4s ease-out, text-shadow 0.4s ease-out;
}

#hero a:hover,
#hero a:focus {
  color: #00A1E4;
  text-shadow: 0 2px 12px rgba(0, 0, 0, 0.35);
}

#block-lpnushortcutstop4 {
  display: flex;
  flex-direction: column;
  background: rgb(46, 49, 146);
}

#block-lpnushortcutstop4::before {
  display: block;
  width: 100%;
  height: 2px;
  content: "";
  background-image: linear-gradient(to right, #2E3192 0%, #fff 50%, #2E3192 100%);
}

#block-lpnushortcutstop4 .field {
  flex: 1 1 auto;
}

.shortcuts-row {
  display: flex;
  flex-wrap: wrap;
}

.shortcut-link {
  display: flex;
  flex: 0 0 50%;
  color: #fff;
}

.shortcut-link > div {
  display: flex;
  flex: 1 1 auto;
  align-items: center;
  justify-content: center;
  min-height: 104px;
  padding: 12px 15px;
  transition: background-color 0.3s ease;
}

.shortcut-link h2 {
  display: flex;
  align-items: center;
  gap: 5px;
  margin: 0;
  text-align: center;
  font-size: 15px;
}

.shortcut-link h2 i {
  color: #00A1E4;
}

.shortcut-1,
.shortcut-4 {
  background: #252775;
}

.shortcut-link:hover > div {
  background: #00A1E4;
}

.shortcut-link:hover h2,
.shortcut-link:hover h2 i {
  color: #fff;
}

/* ==========================================================================
   2. main — ГРІД НОВИН (стиль як на lpnu.ua)
   ========================================================================== */
.main-container {
  max-width: 940px;
  padding: 0 15px 60px;
  margin: 0 auto;
}

.view-header h2 {
  margin: 30px 0;
  text-align: center;
  font-family: "Roboto Condensed", "Roboto", sans-serif;
  font-size: 28px;
  font-weight: 400;
}

.view-header h2 a {
  color: #0076A8;
  border-bottom: 2px solid #0076A8;
  transition: color 2s ease-out, border-color 2s ease-out;
}

.view-header h2 a:hover,
.view-header h2 a:active {
  color: #00A1E4;
  border-bottom-color: #00A1E4;
}

/* Mobile: 1 колонка */
.news-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 24px;
  align-items: start;
}

/* Початкова розмітка lpnu.ua має row-обгортки — робимо їх «прозорими» для grid */
.news-grid .row {
  display: contents;
}

.news-grid .views-col {
  min-width: 0;
  animation: fadeInUp 0.5s ease both;
}

.news-grid .views-col > div,
.news-grid .views-col > div > span {
  display: block;
}

/* Сіра підкладка картки новини, як на сайті */
.news-grid .views-col > div {
  background: #f6f6f6;
}

.news-grid .views-col a {
  display: block;
  color: #0076A8;
}

.news_teaser {
  color: #444444;
}

/* Зображення з сірою лінією внизу; дата перекриває його край */
.news-grid .news_teaser img {
  position: relative;
  z-index: 1;
  display: block;
  width: 100%;
  height: auto;
  margin-bottom: -12px;
  border-bottom: 2px solid #757575;
  opacity: 1;
  transition: opacity 2s ease-out;
}

.news-grid .news_teaser span {
  position: relative;
  z-index: 2;
  display: inline-block;
  margin-left: 15px;
  padding: 5px 7px;
  color: #fff;
  font-size: 13px;
  letter-spacing: 1px;
  text-transform: uppercase;
  background: #757575;
}

.news-grid h3 {
  margin: 15px 0 30px;
  padding: 0 15px 15px;
  color: #0076A8;
  font-size: 18px;
  font-weight: bold;
  line-height: 21px;
  transition: color 0.3s ease-out;
}

/* Hover: зображення стає напівпрозорим, як на оригіналі */
.news-grid a:hover img,
.news-grid a:focus img {
  opacity: 0.65;
}

.news-grid a:hover h3,
.news-grid a:focus h3 {
  color: #00A1E4;
}

/* Анімація появи карток із затримкою */
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

.news-grid .views-col:nth-child(2) { animation-delay: 0.05s; }
.news-grid .views-col:nth-child(3) { animation-delay: 0.10s; }
.news-grid .views-col:nth-child(4) { animation-delay: 0.15s; }
.news-grid .views-col:nth-child(5) { animation-delay: 0.20s; }
.news-grid .views-col:nth-child(6) { animation-delay: 0.25s; }
.news-grid .views-col:nth-child(7) { animation-delay: 0.30s; }
.news-grid .views-col:nth-child(8) { animation-delay: 0.35s; }
.news-grid .views-col:nth-child(9) { animation-delay: 0.40s; }
.news-grid .views-col:nth-child(10) { animation-delay: 0.45s; }
.news-grid .views-col:nth-child(11) { animation-delay: 0.50s; }
.news-grid .views-col:nth-child(12) { animation-delay: 0.55s; }

/* ==========================================================================
   3. Медіа-запити (3 брейкпоінти)
   ========================================================================== */

/* Tablet: 768px – 1023px → 2 колонки новин, 4 швидкі посилання в ряд */
@media (min-width: 768px) {
  body {
    padding-top: 55px; /* компенсація відсутнього navbar lpnu.ua */
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

  .shortcut-link h2 {
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

  .news-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

/* Desktop: 1024px і більше → 4 колонки новин */
@media (min-width: 1024px) {
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
    font-size: 18px;
  }

  .news-grid {
    grid-template-columns: repeat(4, 1fr);
  }
}

`

## 6. Висновок

У роботі досліджено адаптивну верстку сайту Львівської політехніки за
допомогою Chrome DevTools. Для варіанта 2 відтворено `header#hero_container`
на Flexbox та блок «Новини університету» на CSS Grid із виглядом, максимально
наближеним до оригінального сайту. Додано три брейкпоінти, hover-переходи й
анімацію появи карток. Отримано навички комбінування одновимірного (Flexbox)
і двовимірного (Grid) розташування в одній сторінці.

Git-команди (гілка `lab7`, merge, push) не виконувалися: проєкт не є
git-репозиторієм, робота залишена у папці проєкту.

## Перелік посилань

1. <https://developer.mozilla.org/en-US/docs/Web/CSS>
2. <https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Flexbox>
3. <https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Grids>
4. <https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Media_queries>
5. <https://developer.chrome.com/docs/devtools>
6. <https://lpnu.ua/>
