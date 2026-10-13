# Biome 2.5.15 panics: `path is expected to be under the root`

`web/biome.json` enables git ignore. Biome uses that directory as the ignore root, then panics when it checks a path outside `web/`.

## Reproduce

From `web/`:

```sh
npx @biomejs/biome@2.5.15 lint ../backend/file.ts
```

2.5.15 exits with `path is expected to be under the root`.

The same binary accepts a file inside the config directory:

```sh
npx @biomejs/biome@2.5.15 lint file.ts
```

2.5.14 reports `Checked 1 file` for `../backend/file.ts`.

## Layout

- `web/biome.json` enables `vcs` with `clientKind: "git"` and `useIgnoreFile: true`. `vcs.root` is unset.
- `web/file.ts` is inside the config directory.
- `backend/file.ts` is outside it.
