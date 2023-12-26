---
layout: post
title: "Python for Game Audio: 8 Real-World Use Cases"
slug: python-for-game-audio-use-cases
date: 2021-09-06
description: In this post, I talk about game audio problems that I solved using Python language.
---

In this post, I talk about some Python scripts I've written throughout my career, describing the problems each of them solves. I won't share any sources for these scripts, both because I'm not allowed to do so and because I believe that the whole point of using Python for game audio is creating custom, tailored solutions for very specific problems. I believe that sharing the scripts themselves won't benefit the readers, but I hope that sharing a mindset along with the thought process will.

## 1. Deploy FMOD Banks

### Problem

When making any changes to the FMOD project and rebuilding the banks, ensuring that the fresh banks end up in a game project can be complicated. This is especially true if the FMOD project resides in a separate source control repository from the main project, and you don't want to hard-code the relative paths between the two projects.

### Solution

Write a script that copies all the banks from the FMOD project's `Build` folder to the bank folder within the main game project and checks the new banks out in a source control system.

### Tech

- [pathlib](https://docs.python.org/3/library/pathlib.html) - for working with file paths;
- [shutil](https://docs.python.org/3/library/shutil.html) - for copying files;
- [P4Python](https://www.perforce.com/manuals/p4python/Content/P4Python/Home-p4python.html) - for Perforce `add` and `edit` commands (checking out the new files).

## 2. FMOD CSV Profiling Summary Generator

### Problem

The built-in profiler in FMOD Studio does not create any profiling reports that are easy to compare to previous profiling sessions or explain to other non-audio folks.

### Solution

Add some FMOD stats to the [UE4 CSV Profiler](https://docs.unrealengine.com/4.26/en-US/TestingAndOptimization/PerformanceAndProfiling/CSVProfiler/), write docs describing the way profiling data should be collected (i.e. "for 10 minutes of gameplay starting at the first level"). Then, write a Python script that draws beautiful XKCD-styled plots based on the collected data, saves them as pictures, and packs everything up in a ZIP archive.

![Example of the CPU profiling results plotted by quantiles](/media/fmod-profiling-summary-generator-example.png)

### Tech

- [pandas](https://pandas.pydata.org/) - to process the data;
- [NumPy](https://numpy.org/) - for miscellaneous tasks while working with pandas;
- [loguru](https://github.com/Delgan/loguru) - for logging;
- [Matplotlib](https://matplotlib.org/) - for plotting;
- [pathlib](https://docs.python.org/3/library/pathlib.html) - for working with file paths;
- [zipfile](https://docs.python.org/3/library/zipfile.html) - to pack a profiling report in a convenient ZIP archive.

## 3. FMOD Perforce Diff Viewer

### Problem

FMOD projects consist of a number of .xml files, named with their [UUID](https://en.wikipedia.org/wiki/Universally_unique_identifier)s. In practice, it means that if you want to see the difference between two revisions of the project in a source control system such as Perforce, you'll see a bunch of meaningless numbers and letters, instead of the actual event/preset/parameter/etc. names.

### Solution

Write a script that:

1. connects to Perforce,
2. asks the user for two revision numbers,
3. goes through the files that have been changed between these two revisions,
4. parses their content,
5. and returns a table with the actual FMOD entity names.

If the file has been deleted, this script would only show that it's been deleted, without showing you the actual FMOD entity name or type. This can be fixed by getting the previous revision of the deleted file from Perforce, but I decided not to do this.

![Example of the FMOD Perforce Diff Viewer output](/media/fmod-perforce-diff-viewer-example.png)

### Tech

- [P4Python](https://www.perforce.com/manuals/p4python/Content/P4Python/Home-p4python.html) - to connect to Perforce;
- [colorama](https://pypi.org/project/colorama/) - for colored output;
- [lxml](https://lxml.de/) - for XML parsing;
- [loguru](https://github.com/Delgan/loguru) - for logging;
- [click](https://click.palletsprojects.com/) - for CLI;
- [pathlib](https://docs.python.org/3/library/pathlib.html) - for working with files.

## 4. Audio File Validator

### Problem

From time to time, audio files with the wrong channel count, sample rate, volume, and other properties make their way into the FMOD project, and it's not always easy to find the bad ones.

### Solution

Write a script that generates a report on each of the audio files in a selected folder, comparing the measured properties to the reference values.

![Example of the Audio File Validator output](/media/audio-file-validator-example.png)

### Tech

- [colorama](https://pypi.org/project/colorama/) - for colored output;
- [puremagic](https://pypi.org/project/puremagic/) - to check MIME types;
- [soundfile](https://pysoundfile.readthedocs.io/en/latest/) - to get the sample rate, bit depth, duration, and channel count;
- [NumPy](https://numpy.org/) - to calculate the peak volume;
- [pathlib](https://docs.python.org/3/library/pathlib.html) - for working with files.

## 5. Google Cloud TTS Tool

### Problem

Sometimes we need to generate text-to-speech placeholders for VO lines. When the number of placeholders is small, and I only need a couple of phrases - writing a custom script that connects to a VO spreadsheet or database seems to be excessive, and using the online tools is not really convenient.

### Solution

Write a small GUI application that allows me to generate single VO lines using Google Cloud TTS, with an option to select a voice model and speed.

![A small tool to test and generate the Google Cloud TTS voices](/media/google-cloud-tts-tool-example.png)

### Tech

- [PySimpleGUI](https://pysimplegui.readthedocs.io/en/latest/) - for GUI;
- [Google Cloud Client Library](https://cloud.google.com/apis/docs/cloud-client-libraries) - for Google Cloud connection;
- [pathlib](https://docs.python.org/3/library/pathlib.html) - for working with files.

## 6. VO Data Table Generator

### Problem

As soon as the VO files are imported into the FMOD Studio, an Audio Table is created, a spreadsheet with the subtitles is ready, everything needs to be imported into the Unreal Engine.

### Solution

Write a Python script that:

1. loads the data from a subtitles spreadsheet,
2. correlates the subtitle data to the actual audio files,
3. checks if everything is right with both audio files and subtitle lines,
4. checks if nothing is missing,
5. analyzes the audio files to get their duration (which is needed for subtitle display time),
6. generates a JSON file that's later to be imported into the Unreal Engine as a Data Table, so both audio files and subtitle lines can be triggered by the same key.

### Tech

- [argparse](https://docs.python.org/3/library/argparse.html) - for CLI;
- [json](https://docs.python.org/3/library/json.html) - to work with JSON;
- [dataclasses](https://docs.python.org/3/library/dataclasses.html) - to create custom classes for VO entries;
- [pathlib](https://docs.python.org/3/library/pathlib.html) - for working with files;
- [NumPy](https://numpy.org/) - for more complex array operations;
- [pandas](https://pandas.pydata.org/) - for working with subtitle and key data;
- [puremagic](https://pypi.org/project/puremagic/) - to check file MIME-types;
- [soundfile](https://pysoundfile.readthedocs.io/en/latest/) - to get the audio file durations;
- [loguru](https://github.com/Delgan/loguru) - for logging;
- [numpyencoder](https://pypi.org/project/numpyencoder/) - to allow dumping NumPy types to JSON.

## 7. Spawn Python

### Problem

While there are some ways to distribute Python scripts to other machines that don't have a Python interpreter installed, sometimes there's a need to have a portable Python installation that could be easily transferred to another person.

### Solution

Write a Python script that downloads the [embeddable Python](https://docs.python.org/3/using/windows.html#windows-embeddable) ZIP archive of the specified version from the [Python website](https://www.python.org), configures it, and installs the [pip package manager](https://pip.pypa.io/en/stable/), creating a fully portable Python installation.

### Tech

[The Python Standard Library](https://docs.python.org/3/library/) - for everything.

## 8. Restore Mono

### Problem

Imagine you need to [process a large number of audio files with an external piece of hardware](https://www.instagram.com/p/B37HHlXoth6/), with some of these files being stereo, and some of them being mono. The processing itself is quite easy to do using Cockos REAPER, but if you don't separate the mono and stereo files and process them differently, you'll end up with all of your mono files being stereo, since the processing setup is stereo.

### Solution

Write a Python script that goes through both processed and unprocessed audio files, and correlates them by their names. If the script sees that the unprocessed file is mono - it converts the corresponding processed file to mono.

### Tech

- [pathlib](https://docs.python.org/3/library/pathlib.html) - for working with files;
- [soundfile](https://pysoundfile.readthedocs.io/en/latest/) - to read and write audio files;
- [NumPy](https://numpy.org/) - to convert files to mono.
