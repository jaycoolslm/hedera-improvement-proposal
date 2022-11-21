---
hip: <HIP number (this is determined by the HIP editor)>
title: <HIP title>
author: Jay Cool
working-group: a list of the technical and business stakeholders' name(s) and/or username(s), or name(s) and email(s).
type: Standards Track
category: Service
needs-council-approval: <Yes | No>
status: Draft
created: <date created on>
discussions-to: <a URL pointing to the official discussion thread>
updated: <comma separated list of dates>
requires: <HIP number(s)>
replaces: <HIP number(s)>
superseded-by: <HIP number(s)>
---

## Abstract

It is difficult to sign TokenCreateTransactions with a threshold / multikey, in particular when using GUIs. This is required in the usecase where a token is required to have multiple admin keys. Using a scheduled transaction to submit the partially signed transaction will allow a way for people to sign the transaction without needing to be present at the instant of the token creation.

## Motivation

Creating an extensive token creating platform.

## Rationale

The rationale fleshes out the specification by describing why particular design decisions were made. It should describe alternate designs that were considered and related work, e.g. how the feature is supported in other languages.

The rationale should provide evidence of consensus within the community and discuss important objections or concerns raised during the discussion.

## User stories

As an organization, I want to create multi admin key tokens with non-technical GUIs.
  
## Specification

The spec and syntax will follow existing documentation on signing transactions and scheduled transactions.

## Backwards Compatibility

All HIPs that introduce backward incompatibilities must include a section describing these incompatibilities and their severity. The HIP must explain how the author proposes to deal with these incompatibilities. HIP submissions without a sufficient backward compatibility treatise may be rejected outright.

## Security Implications


## How to Teach This

This implementation will follow the same procedure as established ScheduleCreateTransaction flows.

## Reference Implementation

const publicKeyList = new KeyList(publicKeys)

const tx = await new TokenCreateTransaction()
    .setTokenName(`Multi Admin Token 2`)
    .setTokenSymbol(`MAT2`)
    .setInitialSupply(1000)
    .setTreasuryAccountId(treasuryAccountId)
    .setAdminKey(publicKeyList) // Key list

const scheduleTx = new ScheduleCreateTransaction()
    .setScheduledTransaction(tx)
    .freezeWith(client)

const firstSig = await scheduleTx.sign(myPrivateKey)

const scheduleRes = await firstSig.execute(client)

## Rejected Ideas


## Open Issues


## References


## Copyright/license

This document is licensed under the Apache License, Version 2.0 -- see [LICENSE](../LICENSE) or (https://www.apache.org/licenses/LICENSE-2.0)
