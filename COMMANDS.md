# Commands

OpenResume is a Next.js app with two parts: a **resume builder** (form on the left, live PDF preview on the right, PDF made in the
browser with `@react-pdf/renderer`) and a **resume parser** (drop a PDF, see the fields it reads, using `pdfjs-dist`).
Everything runs in the browser; there's no database and no server API. Data is kept in the browser's local storage.
Licence: AGPL v3, see `LICENSE`. It needs **Node 18 or newer** and npm (the lockfile is `package-lock.json`).

## Setup

```
npm ci                                # installs from package-lock.json
```

No `.env` is needed.

## Run

```
npm run dev                           # http://localhost:3000 (builder at /resume-builder, parser at /resume-parser)
npm run build && npm start            # production build; another port: npm start -- -p 3100
```

## Check

```
npm test                              # Jest unit tests (jsdom; files named *.test.ts / *.test.tsx)
                                      # app imports like "lib/redux/resumeSlice" work in tests; for code that uses
                                      # structuredClone (lib/deep-merge.ts), start the file with /** @jest-environment node */
npx jest <path>                       # one test file
npm run test:watch                    # watch mode
npm run lint                          # ESLint (next lint)
npx tsc --noEmit                      # types — run after `npm run build` once (it generates next-env.d.ts)
npx prettier --check src              # formatting; to fix: npx prettier --write src
```

Before any change: `npm test` passes 7 tests in 3 files, `npm run lint` passes with 1 warning
(`src/app/lib/redux/hooks.tsx` react-hooks/exhaustive-deps), `npx tsc --noEmit` is clean after a build, and Prettier reports no
issues in `src`.

## Sample PDFs

`public/resume-example/` has example resumes the parser page uses.
