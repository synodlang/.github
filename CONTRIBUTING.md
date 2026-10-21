# Contributing to Synod

Thank you for helping. These rules apply to every repository in the
organization unless a repository says otherwise.

## Language changes

A change to the language starts as a pull request to
[`dsl`](https://github.com/synodlang/dsl). It must:

- update the spec and `spec/decisions.md`;
- keep `spec/decisions.md` strictly consistent: no decision may override
  or be an exception to another, except `use ... as`;
- come with matching pull requests to `examples` and to the tutorial.

If you are unsure, open a language proposal issue first.

## Code and examples

- Write canonical code only. Run `synod fmt` before you commit.
- Every repository other than `dsl` declares the `dsl` version it
  implements (currently v0.2.0). Update that declaration when you move to
  a newer version.
- Keep lines free of trailing spaces, use LF line endings, and end every
  file with a newline. CI checks this.

## Licences

- Code is licensed under Apache-2.0.
- Documentation and examples (`dsl`, `examples`) are licensed under
  CC BY 4.0.

By contributing you agree that your work is released under the licence of
the repository you contribute to.
