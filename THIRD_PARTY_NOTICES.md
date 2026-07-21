# Third-Party Notices

Focused contains third-party material. Except for the material identified
below, the Focused source is licensed under the PolyForm Shield License
1.0.0. The identified material is excluded from the PolyForm Shield license
and remains governed by the license stated in this file.

## shadcn/ui

Focused incorporates and adapts source code from
[shadcn/ui](https://github.com/shadcn-ui/ui/tree/fa4872c8ed948c111884e52ae23a649e83591b71).

The following scopes, including Focused modifications within those scopes,
are licensed under the MIT License reproduced below and are not licensed
under PolyForm Shield:

- `src/lib/utils.ts` — entire file.
- `src/components/ui/button.tsx` — entire file.
- `src/components/ui/checkbox.tsx` — entire file.
- `src/components/ui/input.tsx` — entire file.
- `src/components/ui/label.tsx` — entire file.
- `src/components/ui/select.tsx` — entire file.
- `src/components/ui/switch.tsx` — entire file.
- `src/styles/globals.css` — the opening theme/token section, beginning with
  `@import "tailwindcss";` and ending with the closing brace of
  `@theme inline` (lines 1–64 at source commit
  `57c284ed6e522ea489a348eb6955af613b53d6d8`).

MIT License

Copyright (c) 2023 shadcn
Copyright (c) 2026 Prithvi B (modifications)

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

## Runtime dependencies

Focused uses third-party npm packages listed in `package.json` and locked by
`pnpm-lock.yaml`. Those packages are not relicensed under PolyForm Shield. A
built distribution must retain the copyright notices and license texts
required by the packages whose code it contains.

At source commit `57c284ed6e522ea489a348eb6955af613b53d6d8`, the
frozen production installation contains 53 packages: 50 MIT, one Apache-2.0
(`class-variance-authority@0.7.1`), one ISC
(`lucide-react@0.525.0`), and one 0BSD (`tslib@2.8.1`). No copyleft,
noncommercial, or other source-available dependency license was found. No
dependency in that installation ships a separate `NOTICE` file.

This summary does not replace the complete upstream license texts required
for any packaged or bundled distribution.
