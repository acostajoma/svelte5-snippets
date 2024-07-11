# Svelte Snippets Extension for VSCode

A collection of useful snippets for Svelte development, including support for JavaScript, TypeScript, and Svelte templates.

## Installation

1. Open **Visual Studio Code**.
2. Go to the **Extensions** view by clicking the square icon in the sidebar or pressing `Ctrl+Shift+X`.
3. Search for `svelte5snippets`.
4. Click **Install**.

## Snippets

### JavaScript and TypeScript Snippets

#### Svelte State Rune

**Prefix**: `svstate`

```javascript
let state = $state(, .frozen)(initialValue);
```

Creates a state variable with optional `.frozen` modifier.

#### Get a Snapshot of Svelte State

**Prefix**: `svstatesnapshot`

```javascript
$state.snapshot(stateName);
```

Creates a snapshot of a Svelte state variable.

#### Compare the Svelte State Value Using .is

**Prefix**: `svstateis`

```javascript
$state.is(stateName, value);
```

Checks if a state and a second value are the same.

#### Svelte Derived Rune

**Prefix**: `svderived`

```javascript
let derivedState = $derived(initialValue);
```

Uses the Svelte derived rune.

#### Svelte Derived Rune with .by Modifier

**Prefix**: `svderivedby`

```javascript
let derivedState = $derived.by(() => {
  expression;
  return derivedStateValue;
});
```

Uses the Svelte derived rune with `.by` modifier.

#### Svelte Effect Rune

**Prefix**: `sveffect`

```javascript
$effect(, .pre, .root)(() => {
    expression
});
```

Creates an effect rune with optional `.pre` and `.root` modifiers.

#### Svelte Effect Tracking Rune

**Prefix**: `sveffecttracking`

```javascript
$effect.tracking();
```

Indicates if the code is running inside a tracking context, such as an effect or template.

#### Svelte Bindable Rune

**Prefix**: `svbindable`

```javascript
$bindable(fallback);
```

Declares a prop as bindable.

#### Svelte Inspect Rune

**Prefix**: `svinspect`

```javascript
/**
 * Will console.log when `variable1,` or `variable2` change.
 * Note this only works during development
 * More notes on https://svelte-5-preview.vercel.app/docs/runes#$inspect
 */
$inspect(variable1, variable2);
```

Creates an inspect rune.

#### Svelte Host Rune

**Prefix**: `svhost`

```javascript
/**
 * Retrieves the this reference of the custom element that contains this component.
 * Only available inside custom element components, and only on the client-side.
 */
$host();
```

Gets the `this` reference to the custom component.

#### Svelte Snippet

**Prefix**: `svsnippet`

```javascript
import type { Snippet } from 'svelte';

{#snippet name(params)}
    body
{/snippet}

{@render name(params)}
```

Creates a Svelte snippet.

#### Svelte Untrack

**Prefix**: `svuntrack`

```javascript
import { untrack } from "svelte";

// To prevent something from being treated as an $effect/$derived dependency, use untrack
untrack(() => constantToUntrack);
```

Prevents something from being treated as an $effect/$derived dependency using `untrack`.

#### Import and Use Svelte on Event

**Prefix**: `svonevent`

```javascript
import { on } from "svelte/events";

const off = on(element, "event", () => {
  expression;
});

// later, if we need to remove the event listener:
off();
```

Imports and uses the `on` event handler from Svelte with an example event listener.

#### Structure for Svelte Store

**Prefix**: `svstore`

```javascript
export function createStoreName(initialValue) {
  let storeName = $state(initialValue);
  return {
    get storeName() {
      return storeName;
    },
    set storeName(value) {
      storeName = value;
    },
  };
}
```

Creates a general store function with state management.

### Svelte Page (JavaScript)

**Prefix**: `svpage`

```javascript
/** @type {import('./$types').Load} */
export const load = async ({ params }) => {
  return {
    // your code here
  };
};

/** @type {import('./$types').Actions} */
export const actions = {
  default: async ({ params }) => {
    // your code here
  },
};
```

Creates the server load action and imports its type.

### Svelte Actions (JavaScript)

**Prefix**: `svactions`

```javascript
/** @type {import('./$types').Actions} */
export const actions = {
  default: async ({ params }) => {
    // your code here
  },
};
// Method is only available in +page.server files
```

Creates the server action and imports its type only on +page.server files, adding a comment if the method is only available on server pages.

### Svelte Request Event (JavaScript)

**Prefix**: `svrequest`

```javascript
/** @type {import('./$types').RequestHandler} */
export const GET = async ({ params }) => {
  return new Response();
};
// Method is only available in +server files
```

Creates the server action and imports its type.

### Svelte Props (JavaScript)

**Prefix**: `svprops`

```javascript
/**
 * @typedef {Object} Props
 * @property {typedef} param
 */

/** @type {Props} */
let { param } = $props();
```

Creates a props snippet.

### Svelte if Block

**Prefix**: `svif`

```svelte
{#if condition}
    // your code here
{/if}
```

Creates an if block in Svelte.

### Svelte if-else Block

**Prefix**: `svifelse`

```svelte
{#if condition}
    // your code here
{:else}
    // your else code here
{/if}
```

Creates an if-else block in Svelte.

### Svelte if-elseif-else Block

**Prefix**: `svifelseif`

```svelte
{#if condition1}
    // code if condition1 is true
{:else if condition2}
    // code if condition2 is true
{:else}
    // code if neither condition1 nor condition2 is true
{/if}
```

Creates an if-else if-else block in Svelte.

### Svelte @html Block

**Prefix**: `svhtml`

```svelte
{@html htmlContent}
```

Uses the `@html` directive in Svelte.

### Svelte @debug Block

**Prefix**: `svdebug`

```svelte
{@debug variables}
```

Uses the `@debug` directive in Svelte.

### Svelte @const Block

**Prefix**: `svconst`

```svelte
{@const variableName = value}
```

Uses the `@const` directive in Svelte.

### Svelte #key Block

**Prefix**: `svkey`

```svelte
{#key key}
    // your code here
{/key}
```

Creates a `#key` block in Svelte.

### Svelte #await Block

**Prefix**: `svawait`

```svelte
{#await promise}
    // waiting state
{:then value}
    // resolved state
{:catch error}
    // error state
{/await}
```

Creates an `#await` block in Svelte.

### Svelte #each Block

**Prefix**: `sveach`

```svelte
{#each items as item (key)}
    // your code here
{/each}
```

Creates an `#each` block in Svelte.

### Svelte Page for TypeScript

**Prefix**: `svpagets`

```typescript
import type { ${TM_FILENAME_BASE/^([a-z])|([lps])|[^a-zA-Z]/${1:/capitalize}${2:/upcase}/g}Load${TM_FILENAME_BASE/^(?!\\+page\\.server$).*|(.*)/${1:+, Actions}/} } from './\\$types';

export const load: ${TM_FILENAME_BASE/^([a-z])|([lps])|[^a-zA-Z]/${1:/capitalize}${2:/upcase}/g}Load = async ({ params }) => {
    return {
        // your code here
    };
};

${TM_FILENAME_BASE/^(?!\\+page\\.server$).*|(.*)/${1:+export const actions = {
    default: async ({  }) => {
        // your code here
    }
};}/}
```

Creates the server load action and imports its type for TypeScript.

### Svelte Actions for TypeScript

**Prefix**: `svactionsts`

```typescript
${TM_FILENAME_BASE/^(?!\\+page\\.server$).*|(.*)/${1:+import type { Actions } from './$types';
export const actions = {
    default: async ({  }) => {
        // your code here
    }
};}${1:?
:// Method is only available in +page.server files}/}
```

Creates the server action and imports its type only on +page.server files for TypeScript, adding a comment if the method is only available on server pages.

### Svelte Request Event for TypeScript

**Prefix**: `sv

requestts`

```typescript
${TM_FILENAME_BASE/^(?!\\+server$).*|(.*)/${1:+import type { RequestHandler } from './$types';
export const GET: RequestHandler = async ({  }) => {
    return new Response();
};}${1:?
:// Method is only available in +server files}/}
```

Creates the server action and imports its type for TypeScript.

### Svelte Props for TypeScript

**Prefix**: `svpropsts`

```typescript
type Props = {
  param: typedef;
};

let { param }: Props = $props();
```

Creates a props snippet for TypeScript.

### Create the Structure of a TS Svelte Page

**Prefix**: `svpagets`

```svelte
<script lang='ts'>
    import { type PageData } from './$types';
    import type { Snippet } from 'svelte';

    type Props = {
        data: PageData,
        children: Snippet,
        newProp: typeDef
    }

    let {
        children,
        data,
        newProp
    }: Props = $props();
</script>
```

Create the structure of a TypeScript Svelte page.

## Contributing

Feel free to fork this repository, make improvements, and send a pull request. All contributions are welcome!

## License

This extension is licensed under the MIT License.

```

```
