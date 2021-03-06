---
title: Индикация загрузки
description: Прямо из коробки Nuxt.js предоставляет вам компонент для отображения состояния загрузки, который отображается при переходах от одной страницы к другой. Вы можете настроить его, отключить или даже создать ваш собственный компонент.
position: 8
category: features
csb_link: https://codesandbox.io/embed/github/nuxt-academy/guides-examples/tree/master/03_features/08_loading?fontsize=14&hidenavigation=1&theme=dark
questions:
  - question: Что нужно сделать, чтобы индикатор прогресса загрузки Nuxt.js заработал?
    answers:
      - Ничего, он работает из коробки
      - Изменить значения свойства `loading` на `true` в файле `nuxt.config.js`
      - Создать компонент индикатора загрузки
    correctAnswer: Ничего, он работает из коробки
  - question: В каком месте вы можете изменить стили для индикатора прогресса загрузки?
    answers:
      - В компоненте макета
      - В компоненте страницы
      - В файле nuxt.config.js
    correctAnswer: В компоненте макета
  - question: В каком свойстве вы можете прописать стили для индикатора загрузки в файле `nuxt.config.js`?
    answers:
      - progress
      - loading
      - loadingBar
    correctAnswer: loading
  - question: Какое свойство вы должны добавить в файл `nuxt.config.js` для отключения индикатора загрузки?
    answers:
      - 'loadingBar: false'
      - "loading: 'none'"
      - 'loading: false'
    correctAnswer: 'loading: false'
  - question: Можете ли вы отключить индикатор загрузки на нужных вам страницах?
    answers:
      - true
      - false
    correctAnswer: true
  - question: Что вы должны использовать чтобы программно запустить индикатор загрузки?
    answers:
      - $nuxt.loading.start()
      - $nuxt.loading()
      - $loading.start()
    correctAnswer: $nuxt.loading.start()
  - question: Какое свойство вы должны использовать чтобы продолжить показывать индикатор загрузки, когда загрузка занимает больше времени, чем продолжительность выставленная по умолчанию?
    answers:
      - "duration: 'continuous'"
      - "loading: 'continuous'"
      - 'continuous: true'
    correctAnswer: 'continuous: true'
  - question: Какие два метода являются обязательными когда вы создаете ваш собственный компонент для отображения загрузки?
    answers:
      - start() and fail()
      - start() and finish()
      - loading() and finish()
    correctAnswer: start() and finish()
  - question: Как вы сможете подключить компонент `loading.vue` после его создания?
    answers:
      - Импортировать его в макет страницы
      - Добавить его в файле `nuxt.config.js` используя свойство `loading`
      - Добавить кго в файле `nuxt.config.js` используя свойство `plugins`
    correctAnswer: Добавить его в файле `nuxt.config.js` используя свойство `loading`
  - question: Что вам нужно добавить в свойство `loading` для показа крутящегося индикатора загурзки когда Nuxt.js используется в режиме ssr:false?
    answers:
      - 'circle: true'
      - 'spinner: circle'
      - 'name: circle'
    correctAnswer: 'name: circle'
---

Прям из коробки Nuxt.js предоставляет вам компонент для отображения состояния загрузки, который показывается при переходах от одной страницы к другой (между маршрутов?). Вы можете настроить его, отключить или даже создать ваш собственный компонент. 

## Настройка индикатора загрузки

Среди прочих свойств, таких как цвет, размер, длительность или направление индикатора загрузки, вы также можете настроить его исходя из потребностей вашего приложения. Это возможно сделать с помощью свойства `loading` в файле `nuxt.config.js` изменив соответствующие своства.

Например, чтобы сделать индикатор загрузки синего цвета и высотой 5px, вам нужно добавить следующие свойства в файле `nuxt.config.js`:

```js
export default {
  loading: {
    color: 'blue',
    height: '5px'
  }
}
```

Ниже вы можете увидеть список свойств для настройки индикатора загрузки.

| Ключ         | Тип     | По умолчанию   | Описание                                                                                                               |
| -----------  | ------- | -------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| color         | String  | 'black'        | CSS цвет индикатора загрузки                                                                                           |
| failedColor  | String  | 'red'          | CSS цвет индикатора загрузки, когда произошла ошибка при переходе между страницами (например когда данные или запрос вернулись с ошибкой). |
| height       | String  | '2px'          | Высота индикатора загрузки (используется в стиле свойства индикатора).                                                   |
| throttle     | Number  | 200            | Задержка в мс перед отображением индикатора загрузки. Полезно для предотвращения мигания индикатора.|
| duration | Number  | 5000           | Максимальная длительность индикатора загрузки. Nuxt.js предполагает, что страница будет отображена в течении 5 секунд. |
| continuous   | Boolean | false          | Возможность дальнейшего анимирования индикатора загрузки, если загрузка занимает больше времени, чем ее заданная длительность.   |
| css    | Boolean | true           | Указать false для удаления стилей индикатора загрузки по умолчанию (и добавления ваших собственных).                   |
| rtl  | Boolean | false          | Установить направление индикатора загрузки справа налево.                                                            |

## Отключение индикатора загрузки

Если вы не хотите отображать индикатор загрузки при переходах между страницами, просто добавьте `loading: false` в ваш файл `nuxt.config.js`:

```js{}[nuxt.config.js]
export default {
  loading: false
}
```

Свойство `loading` дает возможность отключения индикатора загрузки на нужной вам странице.

```html{}[pages/index.vue]
<template>
  <h1>My page</h1>
</template>

<script>
  export default {
    loading: false
  }
</script>
```

## Программный запуск индикатора загрузки

Индикатор загрузки может быть запущен в вашем компоненте программно, путем вызова метода `this.$nuxt.$loading.start()` для запуска индкатора загрузки, и метода `this.$nuxt.$loading.finish()` для его окончания.

В процессе монтирования вашего компонента страницы, свойство `$loading` может стать доступно не сразу. Если вы хотите запустить индикатор загрузки в методе `mounted`, то вам нужно сделать обертку над методом `$loading` вызвав его внутри `this.$nextTick` как показано в примере ниже.

```js
export default {
  mounted() {
    this.$nextTick(() => {
      this.$nuxt.$loading.start()
      setTimeout(() => this.$nuxt.$loading.finish(), 500)
    })
  }
}
```

## Internals (?) индикатора загрузки

К сожалению, компонент индикатора загрузки не может знать заранее, сколько времени займет загрузка новой страницы. Поэтому невозможно точно анимировать индикатор прогресса до 100% времени загрузки.

Компонент индикатора загрузки Nuxt частично решает эту проблему, позволяя установить `длительность` загрузки, это свойство должно быть установлено для оценки того, сколько времени займет процесс загрузки. Если вы не используете ваш собственный компонент загрузки, то индикатор прогресса всегда будет двигаться от 0% до 100% за заданное время "длительности" загрузки (независимо от фактического прогресса). Если загрузка превысит время "длительности" загрузки, то индиактор прогресса загрузки будет оставаться в положении 100% до тех пор, пока загрузка не закончится.

Вы можете изменить поведение по умолчанию поставив свойство `continuous` в `true`, тогда после достижения 100%, индикатор прогресса загрузки снова начнет уменьшаться до 0% за время "длительности". Если загрузка еще не закончена после достижения 0%, индикатор снова начнет расти с 0% до 100%, и это будет повторяться до тех пор, пока загрузка не завершится.

```js
export default {
  loading: {
    continuous: true
  }
}
```

_Пример работы индикатора загрузки:_

![https://nuxtjs.org/api-continuous-loading.gif](https://nuxtjs.org/api-continuous-loading.gif)

## Использование индивидуального комопонента

Вы можете создать свой собственный компонент, и Nuxt.js будет вызывать его вместо компонента прогресса загрузки по умолчанию. Для этого вам нужно указать путь до вашего компонента в свойстве `loading`. После этого Nuxt.js будет вызывать ваш компонент вместо компонента по умолчанию.

Ваш компонент должен содержать методы, которые представлены в этой таблице:

| Метод         | Обязательность | Описание                                                                                              |
| ------------- | -------------- | ----------------------------------------------------------------------------------------------------- |
| start()       | обязателен     | Вызывается при переходе на страницу, и здесь ваш компонент показывается на странице.                  |
| finish()      | обязателен     | Вызывается когда переход на страницу завершен (и данные загружены), и здесь ваш компонент скрывается. |
| fail(error)   | не обязателен  | Вызывается когда страница не может быть загружена (например при ошибке загрузки данных).              |
| increase(num) | не обязателен  | Вызывается во время загрузки страницы, num - это число, значение которого должно быть меньше чем 100. |

Пример создания вашего собственного комопонента, который находится в папке `components/LoadingBar.vue`:

```html{}[components/LoadingBar.vue]
<template>
  <div v-if="loading" class="loading-page">
    <p>Loading...</p>
  </div>
</template>

<script>
  export default {
    data: () => ({
      loading: false
    }),
    methods: {
      start() {
        this.loading = true
      },
      finish() {
        this.loading = false
      }
    }
  }
</script>

<style scoped>
  .loading-page {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(255, 255, 255, 0.8);
    text-align: center;
    padding-top: 200px;
    font-size: 30px;
    font-family: sans-serif;
  }
</style>
```

После того, как вы создали свой компонент, вам нужно указать путь до него в файле `nuxt.config.js`, чтобы Nuxt.js знал откуда его можно запустить:

```js{}[nuxt.config.js]
export default {
  loading: '~/components/LoadingBar.vue'
}
```

## Свойства индикатора загрузки

Когда Nuxt.js запущен в режиме SPA, данные не сразу прийдут со стороны сервера когда вы перейдете на страницу. Поэтому вместо того, чтобы показывать пустую страницу когда идет загрузка данных, Nuxt.js дает вам анимированый индикатор загрузки, который вы можете настроить изменив цвет индикатора или его фон, а также выбрать встроенный индикатор на выбор.

```js{}[nuxt.config.js]
export default {
  loadingIndicator: {
    name: 'circle',
    color: '#3B8070',
    background: 'white'
  }
}
```

## Встроенные индикаторы

Эти индиакторы импортированы из библиотеки [SpinKit](http://tobiasahlin.com/spinkit). Вы можете посмотреть варианты индикаторов на демо-странице перейдя на нее по ссылке. Для использования одного из них, вам надо добавить название индикатора в свойство `name`. Нет необходимости импортировать или устанавливать что-либо. Это список встроенных индикаторов которые мы можете использовать в своих проектах:

- circle
- cube-grid
- fading-circle
- folding-cube
- chasing-dots
- nuxt
- pulse
- rectangle-bounce
- rotating-plane
- three-bounce
- wandering-cubes

Встроенные индикаторы поддерживают свойства `color` и `background`.

## Индикаторы пользователя

Если вам нужно подключить самодельный индикатор, свойство `name` должно содержать путь к его HTML шаблону. Все параметры также передаются в этот шаблон.

Nuxt.js индикаторы также доступны для использования. Для вдохновения вы можете посмотреть этот [исходный код](https://github.com/nuxt/nuxt.js/tree/dev/packages/vue-app/template/views/loading)

<quiz :questions="questions"></quiz>
