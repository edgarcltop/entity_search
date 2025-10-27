# Entity Search

`entity-ts-types` lets you define language-agnostic `message` types in `entity` format, then infers TypeScript types from them with no additional codegen.
> Proof of concept

## How it Works

In short, aggressive use of TypeScript'sAnnotated example from the source:

```ts
// Pass the proto string you want to infer `message` names from as a generic parameter
type MessageNames<Entity extends string> =
  // Infer `message` parts using template literal type
  WrapWithNewlines<Proto> extends `${string}${Whitespace}message${Whitespace}${infer MessageName}${OptionalWhitespace}{${string}}${infer Rest}`
    ? // Recursively infer remaining message names
      [MessageName, ...MessageNames<Rest>]
    : [];
```
