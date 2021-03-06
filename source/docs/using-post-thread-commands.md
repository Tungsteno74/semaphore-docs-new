---
layout: post
title: Using after job commands
category: Customizing your build
---

You can easily define commands for Semaphore to execute after build commands on
each job, regardless of whether the build commands passed or failed.

To do this, simply set a command to "after job" in your project's [Build
Settings](/docs/customizing-build-commands.html):

<img src="/docs/assets/img/post-thread-commands/settings.png" class="img-bordered-padding img-responsive">

This is useful when you need to, for example, upload assets to S3 or tail the test.log.

During these commands an [environment
variable](/docs/available-environment-variables.html) `SEMAPHORE_THREAD_RESULT`
is available. It can hold the value of either "passed" or "failed".

## Debugging

"After job" commands are useful when you need to, for example, upload assets to
S3 or tail the test.log.

You can have your test suite run just one problematic spec file, where you would
temporarily add some verbose speculative puts statements (in a separate branch).

In addition to that, tailing the last 1000 lines of log/test.log as after job
command may reveal a backtrace of an error which causes the whole blank body
thing to happen.

Example build command:

```bash
bundle exec rspec spec/models/problematic_spec.rb
```

Example after job command:

```bash
tail -n 1000 log/test.log
```
