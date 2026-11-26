### 1. Что нашёл

- **Бесконечная анимация фото (высокая критичность):** у `.about-photo img` крутился бесконечный `about-drift` с изменением `object-position`, из-за чего крупное фото постоянно перерисовывалось в простое.
- **Фоновый таймер галереи (высокая критичность):** `setInterval` в `onMount` работал каждые 4.5 сек без очистки и без проверки `document.hidden`, дёргая Swiper и DOM даже в неактивной вкладке.
- **Тяжёлый `onScroll` (средняя критичность):** на каждый тик скролла выполнялись множественные `querySelectorAll` и `getBoundingClientRect()` без `requestAnimationFrame`.
- **Дубли запросов и утечка подписки (средняя критичность):** `onMount` трижды дёргал `/api/flats.json`, спамил расчётами в консоль и перезаписывал `flats` в цикле; в `onMount` не было отписки от `uiStore.subscribe`

### 2. Что исправил

- Убрал анимацию `about-drift` у `.about-photo img`.
- Добавил в интервал галереи проверку `document.hidden`, а в cleanup `onMount` — `clearInterval`, `clearTimeout` и отписку от `uiStore`.
- Обернул обработку скролла в `requestAnimationFrame`.
- Оставил один запрос `/api/flats.json` в `loadFlats()`, убрал `console.log` в `preparePayments` и лишнее обновление массива в цикле.
- Добавил `loading="lazy"` для картинок ниже первого экрана и для `<iframe>` с видео на YouTube.
- Вынес код по функциям для удобства (`loadFlats()`, `loadNews()` и `initMap()`).
- В `onMount()` добавил IntersectionObserver для секций.

### 3. Как проверил, что стало лучше

- смотрел по поведению ноутбука (нагрев/кулеры, плавность скролла и тд)
- тестировал отображение на различных экранах с помощью браузерных инструментов разработчика

### 4. Что сделал бы дальше

- Перевести анимации в `onScroll` с `top`/`height`/`width` на GPU-свойства (`transform`) и закэшировать DOM-элементы вне обработчика.

# Larch Quay

Landing page for the Larch Quay residential quarter.

## Requirements

- Node 24

## Setup

```
npm install
```

## Commands

- `npm run dev` starts the dev server on http://localhost:5173
- `npm run build` creates a production build in `dist`
- `npm run preview` serves the production build on http://localhost:4173
