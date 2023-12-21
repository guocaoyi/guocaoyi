---
layout: post
title: Svelte Cheatsheet
date: 2021-11-30
tags:
  - libs/svelte
  - cheatsheet
---

# Svelte Cheatsheet

```bash
. # Svelte
├── Component Format
├── Template Syntax
│   ├── Tags
│   ├── Attributes and Props
│   ├── Text Expressions
│   ├── Comments
│   ├── Block
│   ├── Element Directives
│   ├── Component Directives
│   ├── <slot />
│   └── Special Elements
├── Run Time
│   ├── Lifecycle | Context
│   ├── Store
│   ├── Motion | Transition | Animate
│   ├── Custom Element API
│   └── Client-side | Server-side
└── Compile Time
```

- A Svelte Component for Preview

```tsx
<!-- Steps.svelte -->
<script>
  // logic
  import Step from "./Step.svelte";

  function onProgressDot() {}
  function handleNotify() {}
</script>

<!-- Step.svelte -->
<Step current="1" direction="vert" {onProgressDot} on:notify={handleNotify} />
<img alt="" src="" class="upper" />

<style>
  /* scope */
  .upper {}

  /* global styling */
  :global(body) {
  }
  div :global(strong) {
  }
</style>

<!-- Step.svelte -->
<script>
  import { createEventDispatcher } from "svelte";

  export let current; // props
  export let direction = "hori"; // props with default value

  // reactive declaration, ECMA labeled statement
  $: [statement]
  $: cubecurrent = current ** 4;
  $: {
    const square = () => current ** 2;
    console.info("square:", square());
    console.info("cubecurrent:", cubecurrent);
  }

  const dispatch = createEventDispatcher();
  let onNotify = () => {
    dispatch("notify", ...params);
  };
  let handleClick = () => variable++; // self handler

  export let onProgressDot = () => {};
</script>

<!-- markup | multi markup -->
<span> {current} </span>
<span> {cubecurrent} </span>
<span> {direction} </span>
<button on:click={onNotify} />
<button on:click={handleClick} />
<button on:click={onProgressDot} />
```

## Component Format

- <script/>
- <script context="[module-name]"/>
- <style/>

## Template Syntax

#### Tags

```tsx
<!-- lowercase indicate html element -->
<button /> or <div></div>

<!-- upercase indicate Component -->
<MyComponent bind:value />
```

#### Attributes and Props

```tsx
<button on:click={handleClick} />
<div class="foo"> ... </div>
<input type="checkbox" />
<img src="domain://{url}/index.png" alt="" />
<button disable={!clickable}> ... </button>
```

#### Text Expressions

```tsx
<element> { expression } </element>
<element class="{ expression }"/>
<element style="{ expression }"/>
```

#### Comments

```tsx
<script>
// or /** */
</script>

<!-- -->
<!-- svelte-ignore a11y-** --> // usually for a11y

<style> /* */ </style>
```

#### Block:if\each\await\key\html\debug

- {# if} if block, if control statement, expression return boolean

```tsx
{#if expression} {/if}
{#if expression} {:else} </> {/if}
{#if expression} {:else if expression} </> {:else} </> {/if}
```

- {# each} each block, just like for-loop

```tsx
{#each values as value} </> {/each}
{#each values as value, index} </> {/each}
{#each values as value (key)} </> {/each}
{#each values as value, index(key)} </> {/each}
{#each values as value} </> {:else} </> {/each}
{#each values as { ...spread } } </> {/each}
```

- {# await} await block, expression return promise

```tsx
{#await expression} </> {/await}
{#await expression} </> {:then res} </> {/await}
{#await expression} </> {:then res} </> {:catch err} </> {/await}
{#await expression then res} </> {/await}
{#await expression catch err} </> {/await}
```

- {# key} key block, destroy & recreate node, when value changed

```tsx
{#key expression} </> {/key}
```

- {@html} innerHtml

```tsx
<element>{@html str}</element>
<element>{@html expression}</element>
```

- {@debug}

```tsx
{@debug}  // debugger;
{@debug vri1, vri2, ....} // variable
```

#### Element Directives

- on:eventname

```html
<element on:event="{handler}"
  ><element />
  <element on:event|modifiers="{handler}"></element>

  // stopPropagation\preventDefault\passive\nonpassive\capture // once\self</element
>
```

- bind:property

```tsx
<!-- property:value\checked\selected -->
<element bind:property={variable}></element>

<!-- shorthand -->
<element bind:variable></element>

<pre contenteditable="true" bind:innerHTML={}></pre>
<video bind:[currentTime|paused|duration|...]/>
```

- bind:this 类似于 React#Refs 转发

```tsx
<script>
	let refs;
	onMount(()=> refs.focus());
</script>
<element bind:this={refs} ></element>
```

- bind:group

```tsx
<radio bind:group={group} />
```

- class:name

```tsx
<element class:[name]={variable} />
<element class:[name] />
<element class={expression} /> // expression => string|bool

<!-- multi class -->
<element class="name" class:[name2] class:[name3] />
```

#### Component Directives

- on:[handler]

```tsx
<Component on:[handler] />
```

- bind:variable

```tsx
<Component bind:[variable] />
```

- bind:this

```tsx
<Component bind:this />
```

#### <slot />

```tsx
<slot /> <!-- name=default -->
<slot name="slot1" />
<element slot="slot1" />
<slot name="no-defined">slot no defined will show</slot>

{ $$slots.[name] }

<slot let:name={value} />
<slot prop={variable} />
```

#### Special Elements

```tsx
<!-- render self,aways for recursive,Tree | Menu -->
<svelte.self />

<!-- render a component dynamically -->
<svelte.compoent this={component} />

<svelte.window />
<svelte.head />
<svelte.body />
<svelte.options />
```

## Run Time

#### Lifecycle | Context

```tsx
import {
  onMount,
  onDestroy,
  beforeUpdate,
  afterUpdate,
  tick,
  setContext,
  getContext,
  hasContext,
} from 'svelte'
```

#### Store

```tsx
import { writable, readable, derived } from 'svelte/store'
import { get } from 'svelte/store'
```

#### Motion | Transition | Animate

- `use:`
- `in:|out:`
- `animate:`
- `transition:`

#### Custom Element API

#### Client-side | Server-side

## Compile Time
