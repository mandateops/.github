# MandateOps

**When systems fail, money must still add up.**

MandateOps Audit is a pre-release test for payout backends. It runs your own backend against a test provider, injects the failures that cause double or lost payouts, and checks that every payout still adds up. No real money moves.

## How it fits together

| Piece               | What it is                                                                                                                                                    | Where                                                                                                         |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| `@mandateops/audit` | The TypeScript test library. A test declares the payout it expects, injects a provider failure, calls your service and gets back a record of what money left. | [npm](https://www.npmjs.com/package/@mandateops/audit)                                                        |
| `@mandateops/cli`   | The `mandateops` CLI. It runs your service and the test provider in containers, applies the faults, captures every provider effect and decides the result.    | npm                                                                                                           |
| Hosted runs         | The same tests on MandateOps servers, with run history in your workspace.                                                                                     | [app.getmandateops.com](https://app.getmandateops.com)                                                        |
| Playground          | Payout bugs replayed step by step: where the money and the records stop agreeing, and how to fix it. Hand-written, with no engine code.                       | [play.getmandateops.com](https://play.getmandateops.com) ([source](https://github.com/mandateops/playground)) |

## What a test covers

- A provider commits a payout but its reply is lost, and your backend retries.
- Payouts race for the same shared balance.
- Your service crashes after the provider has moved the money.
- Duplicate or late provider notifications.

Each run produces a record of the amounts and calls involved. `mandateops recheck` re-derives the verdict from that record, so anyone holding it can check the result without trusting us. It does not rerun your backend.

## Get started

```bash
npm install --save-dev @mandateops/audit @mandateops/cli
npx mandateops version
```

Then follow the [getting started guide](https://getmandateops.com/getting-started.md).

## Open and closed

The `@mandateops/audit` package is Apache-2.0 licensed. The [playground](https://github.com/mandateops/playground) is MIT licensed. The `mandateops` CLI and the hosted platform are proprietary.

## Contact

- Questions: hello@getmandateops.com
- Security: see [SECURITY.md](../SECURITY.md) and [getmandateops.com/security](https://getmandateops.com/security)
