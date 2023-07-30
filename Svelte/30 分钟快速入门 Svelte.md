---
title: 30 分钟快速入门 Svelte
tags: 
categories:
date: 2023-07-30 01:12:55
hidden: true
---

# 30 分钟快速上手 Svelte

---

## 什么是 Svelte

- Svelte 是一个现代的 JavaScript 框架，用于构建用户界面
- 与传统框架不同，Svelte 在构建时将代码转换为高效的原生 JavaScript 代码
- Svelte 不需要运行时库，因此生成的代码体积更小，加载更快

---

## Svelte 的特点

- 响应式：Svelte 使用响应式语法来处理数据的变化
- 组件化：Svelte 支持组件化开发，使代码更易于维护和重用
- 编译时转换：Svelte 在构建时将代码转换为高效的 JavaScript 代码
- 零运行时：Svelte 不需要运行时库，生成的代码体积更小，加载更快

---

## 安装 Svelte

1. 使用 npm 安装 Svelte：

```bash
npx degit sveltejs/template svelte-app
cd svelte-app
npm install
```

2. 运行开发服务器：

```bash
npm run dev
```

3. 在浏览器中打开 `http://localhost:5000` 查看应用

---

## 创建一个 Svelte 组件

1. 在 `src` 目录下创建一个新的 `.svelte` 文件，例如 `HelloWorld.svelte`

2. 编写组件代码：

```html
<script>
  let name = 'World';
</script>

<h1>Hello {name}!</h1>

<style>
  h1 {
    color: blue;
  }
</style>
```

3. 在其他组件中引用该组件：

```html
<script>
  import HelloWorld from './HelloWorld.svelte';
</script>

<HelloWorld />
```

---

## Svelte 的响应式语法

- 使用 `let` 关键字声明响应式变量
- 使用 `{}` 将变量插入到模板中
- 使用 `on:click` 等事件绑定语法处理用户交互
- 使用 `if` 和 `each` 来控制条件渲染和列表渲染

```html
<script>
  let count = 0;
</script>

<button on:click={() => count += 1}>Click me</button>

<p>{count} clicks</p>

{#if count > 10}
  <p>Too many clicks!</p>
{:else if count < 0}
  <p>Too few clicks!</p>
{/if}
```

---

## 组件之间的通信

- 使用 `props` 属性将数据从父组件传递给子组件
- 使用 `context` 上下文将数据在组件树中传递
- 使用 `dispatch` 和 `on:` 语法进行自定义事件的触发和监听

```html
<!-- Parent.svelte -->
<script>
  import Child from './Child.svelte';
  let message = 'Hello from parent';
</script>

<Child {message} />

<!-- Child.svelte -->
<script>
  export let message;
</script>

<p>{message}</p>
```

---

## 生命周期钩子

- Svelte 提供了一些生命周期钩子函数，用于在组件的不同阶段执行特定的操作
- `onMount` 在组件挂载到 DOM 后执行
- `beforeUpdate` 在组件更新前执行
- `afterUpdate` 在组件更新后执行
- `onDestroy` 在组件销毁前执行

```html
<script>
  import { onMount, beforeUpdate, afterUpdate, onDestroy } from 'svelte';

  onMount(() => {
    console.log('Component mounted');
  });

  beforeUpdate(() => {
    console.log('Component about to update');
  });

  afterUpdate(() => {
    console.log('Component updated');
  });

  onDestroy(() => {
    console.log('Component destroyed');
  });
</script>
```

---
## 案例编写

### AI-Translate
---

## 总结

- Svelte 是一个现代的 JavaScript 框架，用于构建用户界面
- Svelte 使用编译时转换将代码转换为高效的 JavaScript 代码
- Svelte 的响应式语法使数据变化更易于处理
- Svelte 不需要运行时