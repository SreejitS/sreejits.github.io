---
layout: post
title:  "Getting started with Embedded Rust Part 1!"
date:   2020-11-06 11:01:19 +0400
categories: jekyll update
---

The ever so stangnant embedded systems industry which generally trails the the
cutting edge desktop dev environment by apporx 10-20 years is getting better at
debuggin tools and RTOSs now. It could be attributed to the attention that the
big players are giving to IoT. fitbits,alexas,google home are a common
vocabulary among the current tech enthusiasts. Casue of this we are getting
really good rtos like bezos rtos and zephyr rtos. Another interesting aspect is
the development of a modern systems programming language which is a high level
language as the paradigms provided by it are 
modern (array,tupple,vecotrs,oops,pattern matching all are provided) mozilla
foundation called rust which with its zero cost abstractions and strict borrow
checker ensures most of the errors comonly found in c are compile time errors
rather than run time errors, which I do agree is less exciting. I mean the idea
that you can crash a whole system by out of bound array access kinda makes you
feel powerful. 

So in series of posts i would like to guide people sort of familiar with
embedded systems on how to get started with rust and how to write safe programs
that one can use for reliablity.

Starting with the basics lets get the dev env ready and we will blink some
lights.

The board I will be using is a cheap stm32 clone called the black pill based on
stm32f411 which is a much powerful replacement for the popular bluepill based on
stm32f103. You will be needing st-link to connect it to you PC for flashing.

I will be assuming Windows environment. Go head down to rust installation script
[here](https://rustup.rs/)
and follow the instructions to install rust compiler. Yes! Remeber that this is
a high level compiled language unlike Java or Python.

**Why you need this?**
This is the compiler and will be used to convert the code you will write into
symbols that the target will be able to run execute, which in our case is
stm32f4 which is based on arm's cortex m4 arch.
{% highlight ruby %}
$ rustc -V
rustc 1.47.0 (18bf6b4f0 2020-10-07)
{% endhighlight %}

Next, install arm-none-eabi-gdb. Get it from
[here](https://developer.arm.com/open-source/gnu-toolchain/gnu-rm/downloads).Remeber
to tick/select the "Add path to environment variable" option. Then verify that the
tools are in your %PATH%:

**Why you need this?**
This helps us to load the code onto the controller and allows us to step through
the code for debugging. As this also supports remote debugiin when the target is
not with you. You can consider this is a sort of client program.
{% highlight ruby %}
$ arm-none-eabi-gdb -v
GNU gdb (GNU Tools for ARM Embedded Processors) 7.6.0.20140731-cvs
{% endhighlight %}

Now install openocd from
[here](https://github.com/xpack-dev-tools/openocd-xpack/releases).

**Why you need this?**
You can consider this as the server side of the the debugging part which
supports multiple transport layer for debugging, of which we will be using arm-none-eabi-gdb.
{% highlight ruby %}
$ openocd -v
xPack OpenOCD, x86_64 Open On-Chip Debugger 0.10.0+dev (2020-10-13-17:29)
{% endhighlight %}

Now once our env is ready and set, we will use cargo which comes as part of
installing rust which is package manager for rust.
Navigate to a folder of you choice and execute the following command.

cargo install cargo-generate
cargo generate --git https://github.com/rust-embedded/cortex-m-quickstart

This will fetch the code and make a rust project for you.

Places to specify details:
compiler - thumbv7em-none-eabihf
linker - size
cargo.toml file
led pin number in src.


how to compile
how to flash

whats next


You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
