---
layout: page
title: guile-words - Vocabulary for Scheme and C programs
description: guile-words, vocabulary for Scheme
permalink: /words/
---

*guile-words* is a [Guile](http://www.gnu.org/software/guile/) port of the
[Vocabulary](https://github.com/prodicus/vocabulary) Python library
that displays meanings, synonyms, antonyms and more for a given word.

*guile-words* is primarily provided as a library but it includes
example programs that function as command-line applications to make
use of it. An interesting bonus that comes from using the Guile
programming language is that the library becomes immediately available
in *C* (and *C++*) programs and libraries as well.

The program makes use of several online dictionaries:

- Wordnik
- Glosbe _(not yet implemented)_
- BighugeLabs
- Urbandict

## *Documentation*

* auto-gen TOC
{:toc}

## Requirements

Aside from a correct Guile installation, the library also requires
*[guile-json](https://github.com/aconchillo/guile-json)*

## Installation

Download the [tar file](https://github.com/pasoev/guile-words/releases/download/0.01/guile-words-0.01.tar.gz) or clone a git reository

{% highlight bash %}

git clone https://github.com/pasoev/guile-words.git

{% endhighlight %}

put the *words.scm* (or the compiled *.go*) file in the Guile site
package, typically

    /usr/share/guile/site/

## Usage examples

### The Scheme library
{% highlight scheme %}

(use-modules (words))

(antonym "good")
 => (ant bad evil bad badness evil evilness ill)

(synonym "poor")
 => (syn hapless miserable misfortunate pathetic
 ... piteous pitiable pitiful wretched inadequate short poor people people)

(hyphenation "momentary")
 => [{"seq":0,"text":"mo","type":"stress"},
 ... {"seq":1,"text":"men"},{"seq":2,"text":"ta"},{"seq":3,"text":"ry"}]

{% endhighlight %}

## Reference

### Available functions

- meaning
- synonym
- antonym
- similar
- related
- hyphenation
- pronunciation

### Adding new actions

Every high-level look up command added as a function to the Scheme
library immediately becomes available to the C application.

#### Adding actions to already supported backends

* Add a new action to the action list

  {% highlight scheme %}

  (define actions
   '((#:meaning . "define")
     (#:synonym . "syn")
     (#:antonym . "ant")
     (#:related . "rel")
     (#:similar . "sim")
     (#:usage-examples . "usage-examples")
     (#:hyphenation . "hyphenation")
     (#:pronunciation . "pronunciations")
     (#:define . "definitions"))
     (#:newaction . "newaction" )) ; <== Your new action here

    {% endhighlight %}

* Define a high level function that calls the existing backend service
and pass the newly defined action to it: 

  {% highlight scheme %}

  (define (similar word)
    (parse-bighuge word #:newaction))

  {% endhighlight %}

### The C client program

{% highlight bash %}

app synonym good
=> full estimable honorable respectable beneficial just upright
... expert practiced proficient skillful skilful dear near
depend quality vantage well thoroughly soundly

{% endhighlight %}

## Contributing

The [git repository](https://github.com/pasoev/guile-words.git)
contains the
[TODO.md](https://github.com/pasoev/guile-words/blob/master/TODO.md)
file. Look at [issues](https://github.com/pasoev/guile-words/issues)
page on github as well.

## Copying

Please, see the
[LICENSE](https://github.com/pasoev/guile-words/blob/master/LICENSE)
file.

This library is free software; you can redistribute it and/or
modify it under the terms of the GNU Lesser General Public
License as published by the Free Software Foundation; either
version 3 of the License, or (at your option) any later version.

This library is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
Lesser General Public License for more details.

You should have received a copy of the GNU Lesser General Public
License along with this library; if not, write to the Free Software
Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA
02110-1301 USA




<a href="https://github.com/pasoev/guile-words"><img style="position: absolute; top: 0; right: 0; border: 0;" src="https://camo.githubusercontent.com/365986a132ccd6a44c23a9169022c0b5c890c387/68747470733a2f2f73332e616d617a6f6e6177732e636f6d2f6769746875622f726962626f6e732f666f726b6d655f72696768745f7265645f6161303030302e706e67" alt="Fork me on GitHub" data-canonical-src="https://s3.amazonaws.com/github/ribbons/forkme_right_red_aa0000.png"></a>
