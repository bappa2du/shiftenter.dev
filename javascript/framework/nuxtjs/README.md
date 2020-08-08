---
description: The Intuitive Vue Framework
---

# NuxtJS

### Installation

{% tabs %}
{% tab title="YARN" %}
```text
yarn create nuxt-app <project-name>
```
{% endtab %}

{% tab title="NPM" %}
```
npm init nuxt-app <project-name>
```
{% endtab %}

{% tab title="NPX" %}
```
npx create-nuxt-app <project-name>
```
{% endtab %}
{% endtabs %}

It will ask you some questions \(name, Nuxt options, UI framework, TypeScript, linter, testing framework, etc.\), when answered, it will install all the dependencies. The next step is to navigate to the project folder and launch it:

{% tabs %}
{% tab title="YARN" %}
```text
cd <project-name>
yarn dev
```
{% endtab %}

{% tab title="NPM" %}
```
cd <project-name>
npm run dev
```
{% endtab %}
{% endtabs %}

The application is now running on [http://localhost:3000](http://localhost:3000/). Well done!

### SEO HTML

{% tabs %}
{% tab title="index.vue" %}
```text
<template>
  <div class="container">
    <h1>Home page 🚀</h1>
    <NuxtLink to="/about">
      About page
    </NuxtLink>
  </div>
</template>

<script>
export default {
  head: {
    title: 'Home page 🚀',
    meta: [
      { hid: 'description', name: 'description', content: 'Home page description' }
    ],
    noscript: [
      { innerHTML: 'Body No Scripts', body: true }
    ],
    script: [
      { src: '/head.js' },
      // Supported since 1.0
      { src: '/body.js', body: true },
      { src: '/defer.js', defer: '' }
    ]
  }
}
</script>

<style>
.container {
  text-align: center;
  margin-top: 150px;
  font-size: 20px;
}
</style>
```
{% endtab %}
{% endtabs %}

### Basic Structure

![Nuxt Js Folder Structure](../../../.gitbook/assets/screenshot-2020-08-08-at-9.32.35-pm.png)



