---
layout: post
title: "Python for Game Audio: My Toolkit"
slug: python-for-game-audio-toolkit
date: 2021-02-15
---

In this post, I share the Python toolkit I use to create various tools for game audio implementation.

**DISCLAIMER:** I'm not a professional programmer in any possible way. All the things I'll be talking about are not Python's best practices or universally good pieces of advice. These are simply the tools that I, being a Technical Audio Designer, personally find useful for my job.

## So, Python for Game Audio?

I believe that Python is one of the best programming languages a Technical Audio Designer can learn. Not only because it is easy to learn, has a big community, is well-supported, and has a lot of libraries, but also because it easily interfaces with industry-standard tools, such as:

- Wwise (via [WAAPI Client for Python](https://github.com/audiokinetic/waapi-client-python)),
- Unreal Engine 4 (via [Unreal Python API](https://docs.unrealengine.com/en-US/PythonAPI/index.html)),
- REAPER (via [ReaScript Python API](https://www.reaper.fm/sdk/reascript/reascripthelp.html#p) or [Reapy library](https://github.com/RomeoDespres/reapy)),
- Google Sheets (via [Google Sheets API](https://developers.google.com/sheets/api/quickstart/python)),
- and many more.

I use Python to automate a broad range of tasks, and I can't imagine doing my job without it.

## Development Tools

Here, I'll talk about the tools I use to write Python code.

### Python 3

To program with Python, you'll need [Python](https://www.python.org/).

There are two main versions of Python: Python 2 and Python 3. I strongly recommend using Python 3. [Here's why](https://wiki.python.org/moin/Python2orPython3).

If you're on Windows, I suggest getting Python 3 from its [official website](https://www.python.org/downloads/). If you're on macOS, it's better to use a package manager such as [Homebrew](https://brew.sh/) since it allows you to manage multiple versions of Python easily. On Windows, you may also use [Chocolatey](https://chocolatey.org/) package manager, though I haven't tried it for Python yet.

### PyCharm Community

[PyCharm Community by JetBrains](https://www.jetbrains.com/pycharm/) is an IDE (integrated development environment, which is a fancy way of saying "text editor that can do a lot of stuff"). It's free; it's fast; it's awesome.

There are two versions of PyCharm: Community and Professional. I use the Community and don't ever feel the need to go with the Professional.

There are some folks (usually the ones with extensive programming background) who prefer "simpler" (not really, in my opinion) and more configurable editors such as [Sublime Text](https://www.sublimetext.com/), [Visual Studio Code](https://code.visualstudio.com/), or even [Vim](https://www.vim.org/). However, I believe that PyCharm is simply the best tool to do the job quickly and comfortably, without digging into all the settings too much or learning many weird keyboard shortcuts.

![Real Programmers. Source: XKCD, https://xkcd.com/378/](https://imgs.xkcd.com/comics/real_programmers.png)

### TabNine

[TabNine](https://www.tabnine.com/) is an autocomplete plugin for PyCharm. It uses AI and deep learning to predict what I would write next and suggests that to me automatically.

While there is a perfectly good [autocomplete already built into PyCharm](https://www.jetbrains.com/help/pycharm/auto-completing-code.html), TabNine takes it to another level by providing autofill for whole lines of code, strings, and other code parts that I would usually be writing by hand. It's hard to overestimate how much time it saves. Here is an example:

![A screenshot of the TabNine autocompletion results in PyCharm.](/img/tabnine-autocomplete-python-example.png)

Let me explain what's going on in this picture. I wrote a single line, `first_thing = "String number one"`. When I started to write `seco`, not only did TabNine suggest continuing it as a `second_thing`, but it also guessed that the `second_thing`'s value would be `"String number two"`, and I never mentioned the word "two" anywhere in my code. It understands the underlying semantics of my code, which makes it super-awesome. It also learns from my code (doing it privately on my computer), getting better the more I use it.

## Python Libraries

In this part, I'll talk about Python libraries I use and love the most. Most of them don't work directly with audio, but I still find them incredibly helpful. I'll keep the library descriptions short so that this post won't end up too big.

### Pathlib

[Pathlib](https://docs.python.org/3/library/pathlib.html) is the only library in this list that's a part of The Python Standard Library (which means you already have it if you have Python).

It's a handy library for everything related to paths, files, folders, and filesystem. There are some "older" ways of working with paths in Python, such as `os.path`, though I find Pathlib much more convenient to use in almost all cases.

**Tip:** you can concatenate paths with `/` operator (`combined_path = first_path / second_path`), which I find pretty cool.

### Loguru

[Loguru](https://github.com/Delgan/loguru) is an easy-to-use logging library and a better alternative to using `print()` to debug the code and show valuable info on the screen. Here is how it looks:

![A screenshot of the Loguru output in PyCharm.](/img/loguru-logging-python-example.png)

### NumPy

[NumPy](https://numpy.org/) (Numerical Python) is an enormously powerful library for working with n-dimensional arrays. Why is it relevant? Because when I'm working with audio, the chances are that the audio data I'm working with is represented as an n-dimensional array. While Python supports a lot of kinds of arrays out-of-the-box, NumPy does it much faster, easier, and has a whole lot of additional tools. Also, there are some pretty fast math functions in NumPy that are not only working with NumPy arrays but also with the usual float numbers.

Whenever I need to do some audio analysis or offline DSP processing in Python, I'll probably end up using NumPy or SciPy, either directly or through other higher-level libraries that use them under the hood.

### SciPy

[SciPy](https://scipy.org/) (Scientific Python) is a library with digital filters and other DSP-related things in its [scipy.signal](https://docs.scipy.org/doc/scipy/reference/signal.html) part.

### Matplotlib

[Matplotlib](https://matplotlib.org/stable/index.html) is my go-to library for drawing plots and visualizing data, useful for audio and many other things. The closest alternative is [Plotly](https://plotly.com/python/), but I find it a bit harder to set up.

### SoundFile

[SoundFile](https://github.com/bastibe/PySoundFile) is a library based on [libsndfile](http://www.mega-nerd.com/libsndfile/) (a quite popular C library) and NumPy, which makes reading audio files in Python easy.

### Reapy

[Reapy](https://github.com/RomeoDespres/reapy) is a [ReaScript Python API](https://www.reaper.fm/sdk/reascript/reascripthelp.html#p) wrapper. It makes it possible to write scripts for [REAPER](https://www.reaper.fm/) in Python, using my Python 3 interpreter, not the [one that should be run from the REAPER itself](https://www.reaper.fm/sdk/reascript/reascript.php#reascript_req_py). In other words, I can use a lot more different libraries and write REAPER scripts much more comfortably.

### Puremagic

[Puremagic](https://github.com/cdgriffith/puremagic) is a pure Python library for reading file's [magic numbers](https://en.wikipedia.org/wiki/Magic_number_(programming)). It allows me to check file types more reliably than merely by the file name extensions.

### Requests

[Requests](https://requests.readthedocs.io/en/master/) is one of the most popular Python libraries ever! And I use it for everything related to HTTP requests and getting something from the internet.

### Pandas

[Pandas](https://pandas.pydata.org/) is a data manipulation library that I use for data that's somewhat similar to our usual Excel spreadsheets. When I have something that looks like a table with rows, columns, and different data types - I usually go with Pandas.

### Librosa

[Librosa](https://librosa.org/) is an audio analysis library. It's a bit higher-level than SciPy, thus a bit easier to use.

### Click

[Click](https://click.palletsprojects.com/) is a beautiful library for building CLIs (command-line interfaces). It's easy to use and allows me to create CLI programs without bothering much with the built-in [argparse](https://docs.python.org/3/library/argparse.html).

### P4Python

[P4Python](https://pypi.org/project/p4python/) is a Perforce API library that helps me build workflows that use the Perforce version control system.

### Colorama

[Colorama](https://pypi.org/project/colorama/) is a library that allows me to use colors in my program's output.

### Pyfiglet

[Pyfiglet](https://github.com/pwaller/pyfiglet) is an ASCII art library. I use it to draw beautiful welcome messages for my CLI programs. Like this:

```
    HHHHHHHHH     HHHHHHHHH                                            !!! 
    H:::::::H     H:::::::H                                           !!:!!
    H:::::::H     H:::::::H                                           !:::!
    HH::::::H     H::::::HH                                           !:::!
      H:::::H     H:::::H      eeeeeeeeeeee  yyyyyyy           yyyyyyy!:::!
      H:::::H     H:::::H    ee::::::::::::ee y:::::y         y:::::y !:::!
      H::::::HHHHH::::::H   e::::::eeeee:::::eey:::::y       y:::::y  !:::!
      H:::::::::::::::::H  e::::::e     e:::::e y:::::y     y:::::y   !:::!
      H:::::::::::::::::H  e:::::::eeeee::::::e  y:::::y   y:::::y    !:::!
      H::::::HHHHH::::::H  e:::::::::::::::::e    y:::::y y:::::y     !:::!
      H:::::H     H:::::H  e::::::eeeeeeeeeee      y:::::y:::::y      !!:!!
      H:::::H     H:::::H  e:::::::e                y:::::::::y        !!! 
    HH::::::H     H::::::HHe::::::::e                y:::::::y             
    H:::::::H     H:::::::H e::::::::eeeeeeee         y:::::y          !!! 
    H:::::::H     H:::::::H  ee:::::::::::::e        y:::::y          !!:!!
    HHHHHHHHH     HHHHHHHHH    eeeeeeeeeeeeee       y:::::y            !!! 
                                                   y:::::y                 
                                                  y:::::y                  
                                                 y:::::y                   
                                                y:::::y                    
                                               yyyyyyy                     
```

Hey!
## Really Important Advice

Always use [type hints](https://www.python.org/dev/peps/pep-0484/) in Python.
