# `inline-mdx.macro`

[![Babel Macro](https://img.shields.io/badge/babel--macro-%F0%9F%8E%A3-f5da55.svg?style=flat-square)](https://github.com/kentcdodds/babel-plugin-macros)

[![npm version](https://img.shields.io/badge/npm-0.2.4-brightgreen.svg)](https://github.com/hamlim/inline-mdx.macro)

A babel-macro for converting mdx into an inline component.

```js
import { inline } from 'inline-mdx.macro'
import { MDXTag } from '@mdx-js/tag'

const SomeMDXComponent = inline`

## This is some MDX source

<SomeComponent />

~~strikethrough~~
`
```

generates...

```js
const SomeMDXComponent = ({ components }) => (
  <MDXTag name="wrapper" components={components}>
    <MDXTag name="h2" components={components}>{`This is some MDX source`}</MDXTag>{' '}
    <SomeComponent />{' '}
    <MDXTag name="p" components={components}>
      <MDXTag
        name="del"
        components={components}
        parentName="p"
      >{`strikethrough`}</MDXTag>
    </MDXTag>
  </MDXTag>
)
```

### You can also use `import` inline as well

```js
import React from 'react'
import { inline, imports } from 'inline-mdx.macro'
imports()

const SomeMDXComponent = inline`

## This is some MDX source

<SomeComponent />

import Foo from './foo';
import Another from './another';

~~strikethrough~~
`
```

generates ...

```jsx
import React from 'react'
import { MDXTag } from '@mdx-js/tag'
import Foo from './foo'
import Another from './another'

const SomeMDXComponent = ({ components }) => (
  <MDXTag name="wrapper" components={components}>
    <MDXTag
      name="h2"
      components={components}
    >{`This is some MDX source`}</MDXTag>
    <SomeComponent />
    <MDXTag name="p" components={components}>
      <MDXTag
        name="del"
        components={components}
        parentName="p"
      >{`strikethrough`}</MDXTag>
    </MDXTag>
  </MDXTag>
)
```

### TODO

_readme driven development 😆_

- [x] plugin that works for the default case
- [x] hoist imports somehow?
