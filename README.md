# frameless

A wrapped and published fork of the excellent [frameless](https://github.com/typelevel/frameless) library

## Why?

Across the last 4 years there have been PRs that have lagged in release, often also against the OSS Spark releases.  Whilst this is a completely understandable and acceptable part of the process it can hamper development and release of software using frameless, [Quality](https://github.com/sparkutils/quality) for example, made more complicated still by differences in runtimes such as Databricks.  3.5 Spark support took 5 months to release, given the amount of change it's also not too surprising.

The major shift proposed by [#800](https://github.com/typelevel/frameless/pull/800) amps up the level of change and, although it may ease such changes in the future, introduces another unproven depenedency in [shim](https://github.com/sparkutils/shim).  It's beyond reasonable to expect this change requires even more care to release in frameless proper.

In order to test in a corporate setting the software needs to be full blown release on maven central, building local snapshots is not always straight forward, worst still if you need to depend on it.

com.sparkutils.frameless aims to fill that void.

## What com.sparkutils.frameless is not

It's not frameless, it just behaves the same, use the same packages and stays fairly up to date with frameless proper.  Check release logs for confirmations of functionality.

## How does com.sparkutils.frameless relate to the rest of com.sparkutils?

com.sparkutils.frameless builds upon typelevel frameless targetting OSS Spark and uses [shim](https://github.com/sparkutils/shim) to run on a wider variety of runtimes without a major release, [Quality](https://github.com/sparkutils/quality) as of [0.1.3](https://github.com/sparkutils/quality/milestone/8) uses com.sparkutils.frameless as a provided scope artefact.  [testless](https://github.com/sparkutils/testless) provides a shaded test pack against com.sparkutils.frameless (and possibly frameless proper in the future if 800 is merged) to test against various runtimes (primarily Databricks).

## How?

1. Git submodules - the actual source code will be taken from a specific commit of the https://github.com/chris-twiner/frameless/ fork.  Code will be kept in sync on demand
2. Maven - SBT builds are not straightforward to achieve in some corporate environments, keeping sbt pluguins updated and available can be almost a full time role.  As such the build moves to maven with build helper to access the correct source locations.

## Why should I use this?

You need some of the features in the build which are not yet (or possibly won't ever be) included in the official release.  If this isn't the case use the official library.

## Will com.sparkutils.frameless continue to exist if 800 is merged and released?

The repo won't go away, nor will the occasional need.  However it's strongly recommended to use the official library wherever possible.

## What if I find a bug?

If the bug is one that is also found in frameless proper, raise an issue there.  If the issue is one of OSS version changes, look at [testsless' tested combos](https://github.com/sparkutils/testless?tab=readme-ov-file#tested-combos) to see if/when your combination has been tested and re-test the nearest combo (it's possible, for example, that a perfectly running test suite on a Databricks runtime suddenly stops working due to backported fixes or improvements) - it may be that a new, more specific, shim version is required for that runtime rather than anything in either frameless proper or com.sparkutils.frameless (in which case raise an issue on shim).

If the bug is in functionality effected by the use of any com.sparkutils.frameless specific functionality then raise it here.

## Versions

com.sparkutils.frameless starts off from the 0.16 release of frameless proper and, as of 05 April 24) adds [#800 - shim usage](https://github.com/typelevel/frameless/pull/800),  [#805 - correct Seq/Set encoding](https://github.com/typelevel/frameless/pull/805) and  [#806 - correct eval implementation for UDF](https://github.com/typelevel/frameless/pull/806).

more to come...
