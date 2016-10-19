---
title: Development Principles
keywords: development, build
tags: [development]
sidebar: designprinciples_sidebar
permalink: designprinciples_development_principles.html
summary: "High-level principles related to the development of the system."
---

1. Software assets to be held on [Github](https://github.com/nhs-digital){:target="_blank"}.
2. Software to be licensed under the [Apache 2 License](http://www.apache.org/licenses/LICENSE-2.0){:target="_blank"}.
3. Code repositories will use the [Gitflow](http://nvie.com/posts/a-successful-git-branching-model/){:target="_blank"} branching model.
	1. Contributors make changes by submitting [Pull Requests](https://help.github.com/articles/using-pull-requests/){:target="_blank"}.
	2. Editors review pull requests for consistency prior to merging into `develop`.
	3. Periodically, editors create a `release` candidate (where appropriate, editors will seek wider review of release candidate assets including clinical review, Connectathon testing etc).
	4. Following successful review, assets are marked as active and published to `master` branch. 
8. Software assets will follow [Semantic Versioning](http://semver.org/){:target="_blank"}.
	1. Major versions will be maintained in parallel for a period of time before deprecation (for at least 12 months).
9. Github [Webhooks](https://developer.github.com/webhooks/){:target="_blank"} will be used to automatically build & publish software assets to a public test instance.
