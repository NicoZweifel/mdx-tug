# mdx-tuc

[![Docs](https://img.shields.io/badge/docs-online-green)](https://mdx-tug.pages.dev/)

Easily bundle and manage typed [`MDX`](https://mdxjs.com/) files.

## Setup

### Installation

```
pnpm i mdx-tub
```

### Examples

- [Next.js](https://mdx-tug.pages.dev/configuration/next)
- [Remix](https://mdx-tug.pages.dev/configuration/remix)

### Bundling

The easiest way to get all bundled documents within a folder is to call the `bundle` function.

> [!Warning] > `bundle`, `MDXService` or any other exports from the `mdx-tug` root entrypoint
> should only be imported in a server or build context.

Options and dependencies can be passed to `bundle` or `MDXService.create`.

> [!Note]
> If you require more control, consider [injecting
> dependencies](https://mdx-tug.pages.dev/customization/DI) and using `MDXService` directly.
>
> For more information check out the [Configuration](https://mdx-tug.pages.dev/configuration) section!

```ts {1,7-10} showLineNumbers
import { bundle } from "mdx-tug";

// ...

return bundle({
  cwd: "/docs",
  fields: {
    title: {
      required: true,
    },
  },
});
```

> [!Tip]
> Automatically generates a `FrontmatterProcessor`, according to the given
> `fields`.

#### Types

To guarantee a correct type inference, specifying the `Frontmatter` type is recommended.

```ts {1-3,7} showLineNumbers
type Frontmatter = {
  title: string;
};

// ...

return bundle<Frontmatter>({
  cwd: "/docs",
  fields: {
    title: {
      required: true,
    },
  },
});
```

> [!Note]
> The given Fields cannot be undefined after the `Frontmatter` has been processed.
>
> If a required field is `undefined`, an `Error` will be thrown.

### `Component`

```tsx {1,12} showLineNumbers
import { Component } from "mdx-tug/client";

// ...

const doc = docs.filter((x) => slug === x.path)[0];

if (!doc) return <div>not found</div>;

return (
  <div>
    <h1>{doc.frontmatter.title}</h1>
    <Component doc={doc} />
  </div>
);
```

> [!Tip]
> Start editing `MDX` documents inside `/docs` or the configured [working
> directory](https://mdx-tug.pages.dev/configuration)

## Notes

- Author mdx files in a `docs` folder or with [any file pattern](https://mdx-tug.pages.dev/configuration#options).
- Support for [`MDX`](https://mdxjs.com/) syntax in descriptions, table of contents, headings and more.
- Full support for custom components and snippets. Import anything in your documents, all files will be bundled in parallel with [`mdx-bundler`](https://github.com/kentcdodds/mdx-bundler) and [`esbuild`](https://esbuild.github.io/).
- [`prettier`](https://prettier.io/) and [`eslint`](https://eslint.org/) configuration for automatic linting and formatting of files, including [`MDX`](https://mdxjs.com/) documents and Code blocks.

## Mentions

- [`vike`](https://vike.dev/) for providing a customizable, versatile web framework.
- [`mdx-bundler`](https://github.com/kentcdodds/mdx-bundler) for providing a blazingly fast [`esbuild`](https://esbuild.github.io/mdx-bundler) based bundler for [`MDX`](https://mdxjs.com/) files.
- [`Contentlayer`](https://contentlayer.dev/) for providing inspiration around the [`MDX`](https://mdxjs.com/) Developer Experience.
- [`feather`](https://feathericons.com/) for providing customizable lightweight svg icons.
