# Добавляем React на сайт

### Используйте React в том объёме, в котором вам хочется.

Для внедрения React не надо ничего переписывать. Его можно использовать как для маленькой кнопки, так и для целого приложения.

## Добавляем React за одну минуту

### Шаг 1: Добавляем DOM-контейнер в HTML

Создать пустой тег <div> и дать ему уникальный **id**. Это позволит впоследствии найти тег из JavaScript-кода и отобразить React-компоненты внутри него.

#### Совет

«Контейнер» <div> можно поместить где угодно внутри тега <body>. Вы можете создать любое количество независимых DOM-контейнеров на одной странице. Эти контейнеры принято оставлять пустыми, так как React в любом случае заменяет всё их содержимое.


### Шаг 2: Добавляем script-теги

Теперь нужно добавить три тега <script> перед закрывающим тегом </body>

```
    <!-- ... остальной HTML ... -->

    <!-- Загрузим React. -->
    <!-- Примечание: при деплое на продакшен замените «development.js» на «production.min.js». -->
    <script src="https://unpkg.com/react@17/umd/react.development.js" crossorigin></script>
    <script src="https://unpkg.com/react-dom@17/umd/react-dom.development.js" crossorigin></script>

    <!-- Загрузим наш React-компонент. -->
    <script src="like_button.js"></script>

  </body>
```

Первые два тега загружают React. Третий тег загружает код вашего собственного компонента.

### Шаг 3: Создаем React-компонент

Создайте файл с именем like_button.js рядом с вашим HTML-файлом.

Возьмите этот <a href="https://gist.github.com/gaearon/0b180827c190fe4fd98b4c7f570ea4a8/raw/b9157ce933c79a4559d2aa9ff3372668cce48de7/LikeButton.js">
стартовый код</a> и вставьте его в созданный ранее файл.

Добавьте ещё 2 строки в конец файла like_button.js, после стартового кода:

```
  const domContainer = document.querySelector('#like_button_container');
  ReactDOM.render(e(LikeButton), domContainer);
```

Эти две строки кода ищут элемент <div>, который мы добавили на первом шаге, а затем отображают React-компонент с кнопкой «Нравится» внутри него.

Готово!

### Повторное использование компонентов

Пример с переиспользованием: https://gist.github.com/gaearon/faa67b76a6c47adbab04f739cba7ceda

### Минификация JavaScript для продакшена

Несжатый JavaScript значительно замедляет страницу для ваших пользователей, поэтому для продакшена необходимо минифицировать JavaScript.

Если вы уже минифицируете свои скрипты, то не забудьте подготовить к продакшену сам React. Для этого поменяйте окончания ссылок на React на production.min.js:

```
  <script src="https://unpkg.com/react@17/umd/react.production.min.js" crossorigin></script>
  <script src="https://unpkg.com/react-dom@17/umd/react-dom.production.min.js" crossorigin></script>
```

### Используем React с JSX

без JSX: 

```
  return e(
    'button', // тег
    { onClick: () => this.setState({ liked: true }) }, // атрибуты
    'Нравится' // children
  );
```

c JSX:

```
// Отобразить <button> с текстом «Нравится»
  return (
    <button onClick={() => this.setState({ liked: true })}>
      Нравится
    </button>
  );
```

## Быстрый старт с JSX

Чтобы попробовать JSX, нужно добавить такой скрипт на страницу:

```
<script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
```

Теперь синтаксис JSX доступен внутри каждого script-тега, у которого есть атрибут type="text/babel".

## Добавляем JSX в проект

1. npm init -y
2. npm install babel-cli@6 babel-preset-react-app@3

### Запускаем препроцессор JSX

Создайте директорию **src** и наберите в терминале следующее:

```
npx babel --watch src --out-dir . --presets react-app/prod
```

#### Примечание 
npx - инструмент для запуска пакетов появившийся в npm версии 5.2+