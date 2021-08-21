---
title: "The ~ and ^ symbol in package.json Webpack"
date: 2021-08-21 8:00:00 +0700
categories: [Programming, TIL]
tags: [Webpack]
---
The tilde `~` and caret `^` symbols in package.json Webpack
<!--more-->

## Difference
From this answer: [https://stackoverflow.com/a/22345808/3123549](https://stackoverflow.com/a/22345808/3123549){:target="_blank"}
> -   `~version`  **“Approximately equivalent to version”**, will update you to all future **patch versions**, without incrementing the **minor version**.  `~1.2.3`  will use releases from `1.2.3` to `<1.3.0`.
> -   `^version`  **“Compatible with version”**, will update you to all future **minor/patch versions**, without incrementing the **major version**.  `^2.3.4`  will use releases from `2.3.4` to `<3.0.0`.

## Semantic Versioning (semver)
From the document: [https://semver.org/](https://semver.org/){:target="_blank"}

> Given a version number `MAJOR`.`MINOR`.`PATCH`, for example: `2.0.0`, increment the:
> 1. `MAJOR` version when you make incompatible API changes.
> 2. `MINOR` version when you add functionality in a backwards compatible manner.
> 3. `PATCH` version when you make backwards compatible bug fixes.
>
> Additional labels for pre-release and build metadata are available as extensions to the MAJOR.MINOR.PATCH format.

## Reference
1. [https://stackoverflow.com/a/22345808/3123549](https://stackoverflow.com/a/22345808/3123549){:target="_blank"}
2. Click [https://semver.org/](https://semver.org/){:target="_blank"} if you'd like to deep dive into Semver

___
*“One day, all your hard work will pay off.”*
{: .text-center.text-success}
