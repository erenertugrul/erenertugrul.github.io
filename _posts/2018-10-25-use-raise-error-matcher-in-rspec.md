---
layout: post
title:  "Use `raise_error` matcher in Rspec"
date:   2018-10-25 11:30:09 +0900
comments: true
tags:
- programming
---

Yesterday I came accross a tricky useage of `raise_error` matcher in rspec, first I try to use the one line syntax `is_expected.to`
```rb
it { is_expected.to raise_error(SomeError) }
```

but I got an eror which stops the test before the test is finished.

It is confusing in the first time, because `is_expected.to` is shortcut for `expect(subject)`.

Then I found this <a href="https://github.com/rspec/rspec-expectations/issues/805#issuecomment-112239820">excellent explanation</a> in Github isses.

So `expect(subject)` is not a block, subject is executed instantly, so rspec will stop before evaluating `raise_error` matcher.

In order to make it work, we can make subject itself a block
```rb
subject { -> { raise SomeError } }

it { is_expected.to raise_error(SomeError) }
```

But this syntax is creepy, instead it's better to use
```rb
subject { raise SomeError }

expect { subject }.to raise_error(SomeError)
```