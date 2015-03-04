---
layout: post
title: "Fix composer.lock conflicts easily"
image: uploads/composer-lock-conflicts.png
---

Probably you should be committing the `composer.lock` file in your projects, if not take a look at [these](https://stackoverflow.com/a/12896850) [links](http://ilikekillnerds.com/2014/09/should-you-commit-composer-lock-into-your-git-repository/) [now](https://philsturgeon.uk/php/2014/11/04/composer-its-almost-always-about-the-lock-file/).

And if you're working with someone else on the same project or not, you probably have faced the ugly merge conflict with `composer.lock`.

In my case I can simply do the following to fix the conflict:

1. remove the `composer.lock` file entirely.
2. do `composer update`.
3. commit the newly created `composer.lock`.

And we're done!

*Be careful when using `\*` versions or `dev-master` in the `composer.json` file.*
