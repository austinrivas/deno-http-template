OpenFaaS Deno HTTP template
=============================================

An OpenFaaS of-watchdog template written for Deno.

## Installation

```sh
$ faas template pull https://github.com/austinrivas/deno-http-template
$ faas new --list
Languages available as templates:
- deno-http
```

## Create Function

```sh
faas new <name> --lang deno-http
```

## Testing

Deno provides a built in test runner.

```sh
deno test --allow-net
```

This repo also includes vscode debug configurations.
  - Run Tests
  - Debug Current Test File
  - Debug Seleted Test Case

### Linting

Deno also provides a built in code linter.

```sh
deno fmt
```

## Usage

This template provides a thin wrapper around the [Deno Http Server](https://doc.deno.land/https/deno.land/std/http/server.ts) provided by the Deno stdlib. The wrapper implementation closely mirrors the Deno [serve](https://doc.deno.land/https/deno.land/std/http/server.ts#serve) function.

### [Example Handler](https://github.com/austinrivas/deno-http-template/blob/master/template/deno-http/function/handler.ts)
### [Wrapper](https://github.com/austinrivas/deno-http-template/blob/master/template/deno-http/main.ts)

## Example Function

A working example of this function template can be found [here](https://github.com/austinrivas/openfaas_deno_func).

## Extras

This repo also contains a [base image](https://github.com/austinrivas/deno-http-template/blob/master/deno-http-base/Dockerfile) that can be extended as needed by other templates.

The base image is consumed by the deno template itself and the included [okteto image](https://github.com/austinrivas/deno-http-template/blob/master/okteto/Dockerfile) which can be used for remote development on the [Okteto Platform](https://okteto.com/) for remote OpenFaaS development.

A [Test and Enforce Deno Format github action](https://github.com/austinrivas/openfaas_deno_func/blob/master/.github/workflows/test-fmt-deno.yml) is included that will trigger on pull request. This action runs the deno tests and throws an error if `deno fmt` returns changes.
