# Codama ➤ Renderers ➤ JavaScript Umi

[![npm][npm-image]][npm-url]
[![npm-downloads][npm-downloads-image]][npm-url]

[npm-downloads-image]: https://img.shields.io/npm/dm/@codama/renderers-js-umi.svg?style=flat
[npm-image]: https://img.shields.io/npm/v/@codama/renderers-js-umi.svg?style=flat&label=%40codama%2Frenderers-js-umi
[npm-url]: https://www.npmjs.com/package/@codama/renderers-js-umi

This package generates JavaScript clients from your Codama IDLs. The generated clients are compatible with Metaplex's [Umi framework](https://github.com/metaplex-foundation/umi).

## Installation

```sh
pnpm install @codama/renderers-js-umi
```

## Usage

Add the following script to your Codama configuration file.

```json
{
    "scripts": {
        "js": {
            "from": "@codama/renderers-js-umi",
            "args": ["clients/js/src/generated"]
        }
    }
}
```

An object can be passed as a second argument to further configure the renderer. See the [Options](#options) section below for more details.

## Options

The `renderVisitor` accepts the following options.

| Name                          | Type                                                                                                                    | Default   | Description                                                                                                                                                                                      |
| ----------------------------- | ----------------------------------------------------------------------------------------------------------------------- | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `deleteFolderBeforeRendering` | `boolean`                                                                                                               | `true`    | Whether the base directory should be cleaned before generating new files.                                                                                                                        |
| `formatCode`                  | `boolean`                                                                                                               | `true`    | Whether we should use Prettier to format the generated code.                                                                                                                                     |
| `prettierOptions`             | `PrettierOptions`                                                                                                       | `{}`      | The options to use when formatting the code using Prettier.                                                                                                                                      |
| `throwLevel`                  | `'debug' \| 'trace' \| 'info' \| 'warn' \| 'error'`                                                                     | `'error'` | When validating the Codama IDL, the level at which the validation should throw an error.                                                                                                         |
| `customAccountData`           | `string[]`                                                                                                              | `[]`      | The names of all `AccountNodes` whose data should be manually written in JavaScript.                                                                                                             |
| `customInstructionData`       | `string[]`                                                                                                              | `[]`      | The names of all `InstructionNodes` whose data should be manually written in JavaScript.                                                                                                         |
| `linkOverrides`               | `Record<'accounts' \| 'definedTypes' \| 'instructions' \| 'pdas' \| 'programs' \| 'resolvers', Record<string, string>>` | `{}`      | A object that overrides the import path of link nodes. For instance, `{ definedTypes: { counter: 'hooked' } }` uses the `hooked` folder to import any link node referring to the `counter` type. |
| `dependencyMap`               | `Record<string, string>`                                                                                                | `{}`      | A mapping between import aliases and their actual package name or path in JavaScript.                                                                                                            |
| `internalNodes`               | `string[]`                                                                                                              | `[]`      | The names of all nodes that should be generated but not exported by the `index.ts` files.                                                                                                        |
| `nonScalarEnums`              | `string[]`                                                                                                              | `[]`      | The names of enum variants with no data that should be treated as a data union instead of a native `enum` type. This is only useful if you are referencing an enum value in your Codama IDL.     |
| `renderParentInstructions`    | `boolean`                                                                                                               | `false`   | When using nested instructions, whether the parent instructions should also be rendered. When set to `false` (default), only the instruction leaves are being rendered.                          |
