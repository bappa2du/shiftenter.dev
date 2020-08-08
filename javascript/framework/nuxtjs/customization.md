---
description: Basic and advance customisation of Nuxt js
---

# Customization

### Layouts

{% tabs %}
{% tab title="pages/index.vue" %}
```text
<template>
  <div>
    <p>Hi from {{ name }}</p>
    <NuxtLink to="/about">
      Home page
    </NuxtLink>
  </div>
</template>

<script>
export default {
  layout: 'dark',
  asyncData ({ req }) {
    return {
      name: req ? 'server' : 'client'
    }
  }
}
</script>
```
{% endtab %}

{% tab title="layouts/dark.vue" %}
```
<template>
  <div class="dark">
    <Nuxt />
  </div>
</template>

<style>
body {
  overflow: hidden;
}
.dark {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  min-height: 100%;
  background: black;
  color: white;
  padding: 10px;
}
.dark a {
  color: white;
}
</style>
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
If no layout defined then default layout will be use.
{% endhint %}

### Middleware

You can add your middleware \(even multiple\) to a specific layout or page.

{% tabs %}
{% tab title="pages/index.vue" %}
```text
export default {
  middleware: ['auth', 'stats']
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Where auth.js & stats.js are **middleware** directory.
{% endhint %}

### External Script

#### Globally:

Include your resources in `nuxt.config.js` \(here in the head object\):

{% tabs %}
{% tab title="nuxt.config.js" %}
```text
export default {
  head: {
    script: [
      {
        src: 'https://cdnjs.cloudflare.com/ajax/libs/jquery/3.1.1/jquery.min.js'
      }
    ],
    link: [
      {
        rel: 'stylesheet',
        href: 'https://fonts.googleapis.com/css?family=Roboto&display=swap'
      }
    ]
  }
}
```
{% endtab %}
{% endtabs %}

#### Locally:

Include your resources in your `.vue` file inside the `pages/` directory \(here in the head function\):

{% code title="pages/about.vue" %}
```text
<template>
  <h1>About page with jQuery and Roboto font</h1>
</template>

<script>
  export default {
    head() {
      return {
        script: [
          {
            src:
              'https://cdnjs.cloudflare.com/ajax/libs/jquery/3.1.1/jquery.min.js'
          }
        ],
        link: [
          {
            rel: 'stylesheet',
            href: 'https://fonts.googleapis.com/css?family=Roboto&display=swap'
          }
        ]
      }
    }
  }
</script>

<style scoped>
  h1 {
    font-family: Roboto, sans-serif;
  }
</style>
```
{% endcode %}

### Host & Port

{% tabs %}
{% tab title="nuxt.config.js" %}
```text
export default {
  server: {
    port: 8000, // default: 3000
    host: '0.0.0.0' // default: localhost
  }
  // other configs
}
```
{% endtab %}
{% endtabs %}

### Firebase

Install the module via NPM or Yarn.

{% tabs %}
{% tab title="YARN" %}
```text
yarn add @nuxtjs/firebase
```
{% endtab %}

{% tab title="NPM" %}
```
npm i @nuxtjs/firebase
```
{% endtab %}
{% endtabs %}

#### Configure:

{% tabs %}
{% tab title="nuxt.config.js" %}
```text
modules: [
    [
      '@nuxtjs/firebase',
      {
        config: {
          apiKey: '<apiKey>',
          authDomain: '<authDomain>',
          databaseURL: '<databaseURL>',
          projectId: '<projectId>',
          storageBucket: '<storageBucket>',
          messagingSenderId: '<messagingSenderId>',
          appId: '<appId>',
          measurementId: '<measurementId>'
        },
        services: {
          auth: true // Just as example. Can be any other service.
        }
      }
    ]
  ],
```
{% endtab %}
{% endtabs %}

