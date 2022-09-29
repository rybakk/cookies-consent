# Vue Cookies Consent
![Size](https://img.shields.io/bundlephobia/minzip/vuejs-cookies-consent)
![Downloads](https://img.shields.io/npm/dt/vuejs-cookies-consent)
![Version](https://img.shields.io/npm/v/vuejs-cookies-consent)

Nice and clean component to display message about cookies in Vue

## 📦 Installation

### NPM

`npm install --save vuejs-cookies-consent`

### Yarn

`yarn add vuejs-cookies-consent`

## 🚀 Usage in Vue Components

```vue
<template>
    <cookies-consent :preferences="preferences" />
</template>
<script>
  export default {
    data() {
        preferences: [
            {
                title: 'Analytics',
                description:
                    'Bla bla serviços que podemos oferecer erviços que podemos oferecer erviços que podemos oferecer erviços que podemos oferecer serviços que podemos oferecer.',
                items: [
                    {
                        label: 'GoogleAnalytics',
                        value: 'ga',
                        isEnable: true,
                    },
                    { label: 'Sentry', value: 'sentry', isEnable: true },
                    { label: 'Mapbox', value: 'mapbox', isEnable: true },
                    {
                        label: 'New Relic',
                        value: 'newRelic',
                        isEnable: true,
                    },
                    { label: 'Dog Food', value: 'dogfood', isEnable: true },
                ],
            },
        ],
    }
  }
</script>
```

## 🚀 Usage throughout the Vue project
Add this content to main.js
```js
import Vue from "vue";
import CookiesConsent from 'vuejs-cookies-consent'
Vue.use(CookiesConsent)
```

And add component to your code:

```vue
<template>
    <cookies-consent :preferences="preferences" />
</template>
```

## 🔧 Props

| Prop                  | Type    | Description                                                 | Example                             |
|-----------------------|---------|-------------------------------------------------------------|-------------------------------------|
| preferences           | Array   | Multiple cookies to choose                                  | `preferences="preferences"`         |
| headerTitle           | String  | Heading title                                               | `header-title="Cookies Consent"`    |
| headerDescription     | String  | Heading description                                         | `header-description="Bla bla bla"`  |
| preferencesLabel      | String  | Label text for preferences button                           | `preferences-label="Preferences"`   |
| accept-all-label      | String  | Label text for accept all button                            | `accept-all-label="Accept all"`     |

## 🔧 Events

| Event         | Description                                              | Example                                 |
|---------------|----------------------------------------------------------|-----------------------------------------|
| on-accept-all-cookies        | Fired after accept all button is clicked  | `@onAcceptAllCookies="someMethod"`      |
| on-save-cookie-preferences   | Fired after save button is clicked        | `@onSaveCookiePreferences="someMethod"` |