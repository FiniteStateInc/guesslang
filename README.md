# Guesslang [![Build Status](https://travis-ci.org/yoeo/guesslang.svg?branch=master)](https://travis-ci.org/yoeo/guesslang) [![Documentation Status](https://readthedocs.org/projects/guesslang/badge/?version=latest)](http://guesslang.readthedocs.io/en/latest/?badge=latest)


![Chameledit](docs/_static/images/guesslang-small.png)

Guesslang detects the programming language of a given source code:

```bash
echo '
package main
import "fmt"

func main() {
    fmt.Println("My mascot is a gopher and Google loves me. Who am I?")
}

' | guesslang

# Output: The source code is written in Go
```

Guesslang supports `20 programming languages`:

| Languages   |             |             |             |             |
|-------------|-------------|-------------|-------------|-------------|
| C           | C#          | C++         | CSS         | Erlang      |
| Go          | HTML        | Java        | Javascript  | Markdown    |
| Objective-C | PHP         | Perl        | Python      | Ruby        |
| Rust        | SQL         | Scala       | Shell       | Swift       |

With a guessing **accuracy higher than 90%**.

## Apps powered by Guesslang

#### Chameledit

[Chameledit](https://github.com/yoeo/chameledit) is a simple web-editor
that automatically highlights your code.

![](docs/_static/images/chameledit.gif)

##### Pasta

[Pasta](https://github.com/yoeo/pasta) is a [Slack](https://slack.com) bot
that pretty pastes source code.

[Watch the demo here](https://github.com/yoeo/pasta)

#### GG

[GG](https://github.com/yoeo/gg) is a silly guessing game.

## Documentation

* Guesslang documentation is available at
  https://guesslang.readthedocs.io/en/latest/

* Guesslang language detection explained here
  https://guesslang.readthedocs.io/en/latest/how.html

* Guesslang is based on [Tensorflow](https://github.com/tensorflow/tensorflow)
  machine learning framework

## Installation

* Python 3.6+ is required

* Install the latest stable version:

```bash
pip3 install guesslang
```

* or install Guesslang from source code:

```bash
pip3 install .
```

* Windows specific

To run [Tensorflow](https://github.com/tensorflow/tensorflow)
on Microsoft Windows you need to install Visual C++ runtime libraries,
available on [Microsoft website](https://www.microsoft.com/en-us/download/details.aspx?id=53587)

## Guesslang command line

* Show all available options

```bash
guesslang --help
```

* Detect the programming language of ``/bin/which``:

```bash
guesslang -i /bin/which

# >>> The source code is written in Shell
```

* Detect the programming language of a given text:

```bash
echo '
/** Turn command line arguments to uppercase */
object Main {
  def main(args: Array[String]) {
    val res = for (a <- args) yield a.toUpperCase
    println("Arguments: " + res.toString)
  }
}
' | guesslang

# >>> The source code is written in Scala
```

* Detect the programming languages of a source code that embeds
  an other source code ([sourcecodeception](http://explosm.net/comics/1605/)):

```bash
echo '
from __future__ import print_function


def dump_code(code):
  print(code)


if __name__ == "__main__":
    dump_code("""
        #include<stdio.h>

        int main(int argc, char** argv)
        {
          char* command = argv[0];
          printf("%s - %d args\n", command, --argc);
          return 0;
        }
    """
    )

' | guesslang --all

# >>> The source code is written in Python or C
```

## Guesslang Python package

* Guesslang can be used as a Python package.
  [Package documentation available here](https://guesslang.readthedocs.io/en/latest/guesslang.html)

``` python

from guesslang import Guess


name = Guess().language_name("""
    % Quick sort

    -module (recursion).
    -export ([qsort/1]).

    qsort([]) -> [];
    qsort([Pivot|T]) ->
          qsort([X || X <- T, X < Pivot])
          ++ [Pivot] ++
          qsort([X || X <- T, X >= Pivot]).
""")

print(name)  # >>> Erlang
```

## License and credits

* [Guesslang documentation](https://guesslang.readthedocs.io/en/latest/)

* Guesslang icon created with
  [AndroidAssetStudio](https://github.com/romannurik/AndroidAssetStudio)

* Guesslang — Copyright (c) 2017 Y. SOMDA, [MIT License](LICENSE)

## MODIFICATIONS BY FINITE STATE:

The current upstream version of this repo is broken. It has a hard-pinned dependency on TensorFlow 1.7.0rc1, which is no longer provided by pip. In order to work around this, this fork of the repo updates that requirement to the latest version of TensorFlow 1.x that is still available in pip.  
