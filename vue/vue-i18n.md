# vue-i18n

Vue I18n is internationalization plugin of Vue.js.

## Compatibility

- Vue.js 3.0.0 +

## Feature

Like with most Vue plugins, the call to use needs to happen before the call to mount.

- Adding the global properties and methods such as `$t`, `$i18n`
- Enabling the `useI18n` composables
- Globally registering the `i18n-t`, `i18n-d`, and `i18n-n` components.

## install

```sh
npm install vue-i18n@10  # v10
npm install vue-i18n@11  # v11
```

## main.js

```js
import { createApp } from "vue";
import { createI18n } from "vue-i18n";
const i18n = createI18n({ i18nOptions });
const app = createApp({ appOptions });
app.use(i18n);
app.mount("#app");
```

## Browser

```html
<script src="https://unpkg.com/vue@3"></script>
<script src="https://unpkg.com/vue-i18n@11" ver="latest"></script>
<script src="https://unpkg.com/vue-i18n@11.0.0/dist/vue-i18n.global.js" ver="specific"></script>
```

```html
<!-- es modules import -->
<script type="module" src="https://unpkg.com/vue@3/dist/vue.esm-browser.js"></script>
<script type="module" src="https://unpkg.com/vue-i18n@11/dist/vue-i18n.esm-browser.js"></script>
```

```html
<script>
const { createApp } = Vue;
const { createI18n, useI18n } = VueI18n;
</script>
```

## Instance

```js
// i18n.js 定义
const i18n = createI18n({
  locale: "zhCn",
  fallbackLocale: "en",
  messages: {
    en: {
      message: {
        hello: "hello world",
      },
    },
    zhCn: {
      message: {
        hello: "你好 世界",
      },
    },
  },
});
```

```html
<!-- i18n.vue 使用 -->
<script>
import { useI18n } from "vue-i18n";
const { t, locale } = useI18n();

const hello = t("message.hello");
locale.value = "zhCn";
</script>

<template>
  <select v-model="$i18n.locale">
    <option v-for="locale in $i18n.availabelLocales" :key="`locale-${locale}`" :value="locale">
      {{ locale }}
    </option>
  </select>
  <h1>{{ $t("message.hello") }}</h1>
</template>
```

## message format syntax

- `hello: '{msg} world'` => `$t('message.hello', {msg: 'hello'})`
- `hello: '{0} world'` => `$t('message.hello', ['hello'])`
