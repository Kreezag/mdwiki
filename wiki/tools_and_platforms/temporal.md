# Temporal

[◀ Back](./index.md)


## Documentation

- [Temporal](https://docs.temporal.io/)

- [Setup for typescript](https://learn.temporal.io/getting_started/typescript/dev_environment/)

- [Github typescript example](https://github.com/temporalio/samples-typescript/tree/main)

## Temporal platform Concepts

`Activity` - is a normal function or method that executes a single, well-defined action (either short or long running), 
such as calling another service, transcoding a media file, or sending an email message. 
Activity code can be non-deterministic. We recommend that it be idempotent.

`Workflow` - is a program that coordinates multiple activities and other workflows.
A Workflow Definition in TypeScript is a regular TypeScript function that accepts some input values.

`Worker` - is a process that hosts one or more activity and/or workflow implementations.

`Task Queue` - is a logical grouping of activity and/or workflow tasks.



### Timeouts

---

![Activity Timeouts](https://images.ctfassets.net/0uuz8ydxyd9p/qeHHAfhow01sZ2BXByG8q/bc9913b65ce1cf99a19521a19a78e5bf/122424123-0ab1e300-cfc1-11eb-82c5-cf8856a87242.png)


