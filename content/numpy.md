#Numpy

## Introduction


Python is a general purpose programming language, designed to be easy to understand,  allowing beginners to focus on learning programming concepts. As a generic programming language it has no single role, but it is commonly used for processing text, numbers, images, scientific data, building websites and applications, and visualisation.



## Learning Objectives:


In this chpter we're going to look a Python tool (Library) called Numpy (numeric Python). With Numpy we're going to attack a simple data science problem, yet one that has some profound implications.

While you won't finish this chapter a fully-fledged Python programmer, we hope that you will get the 'flavour' of how Python works. Necessarily, we will introduce some extraneous concepts and terms, that we don't have time to fully-develop or explore . We will provide links ot material to help you master these subjects later on.

Our main suggestion is to __try to understand and keep the data science problem in mind__. Hopefully, if you have a good handle on the problem itself, the utility of Python / Numoy will be self evident. If not, demand your money back.

By the end of this chapter you will learn:

1. Why structured, numeric data is cool and totally relevant
2. How to handle, access, and query structured, numeric data, using Python
3. The 'flavour' of using Numpy for a data science problem.

Finally, the introduction should end with a contents page listing how the rest of the chapter will flow.

## Background

Python was first created by Guido von Rossum in 1990 and was named after Monty Python's Flying Circus. It has since been developed by a large team of volunteers and is freely available from the Python Software Foundation.

That's right, Python is free. More than that, Python has a strong ties to the open source movement. This means there is a culture of sharing, cooperation and support.

Python, Matlab, or R (or Java, C++, ...)? There are a lot of programming languages, and many tasks can be completed equally well in all of them. So how to decide? In our group, some grad students chose Python because it was stronger in discipline-specific Libraries than any of it's competetors (for instance Neuroscience, Geophysics).

Some of us had also dabled in other languages first (e.g. Matlab, R), and found that there was litte 'wasted' effort in switching. Many core concepts, extend across all languages, not to mention the more ephemeral skill of 'thinking like a programmer'.

A few further considerations that recommend Python:

* Strong web presence (stack overflow)
* Conference and meetups (Scipy, PyData, Py Con)
* Jupyter


## Context


This section provides the reader some broader context of the tool. Here you’ll define any of the terms you’ll be using in the rest of the chapter. Think of this as the extended glossary. Use language which is clear and to the point. The readers will refer back here if they’re confused with the terminology.

Definitions of terms/glossary

Library (e.g Numpy)
Variable
Boolean
Element
index
slice
Path
MyBinder


## A data science example

Our example looks at a real (data) scientific problem. In fact, we are going to to endeavour to _falsify_ a hypothesis.
We'll try to show that there are predictable patterns in day-to-day stockmarket data, which would contradict the _efficient market hypothesis_. Specifically, __we're going to look at whether today's market value _change_ follows yesterday's _change_, at a rate greater than expected if it were random__.

_Remember, this is one example out of a Universe of problems that we could have chosen. Don't be lured into thinking that Python is a financial / economics tool. The data analysis here is totally general, and very similar problems will appear in multiple disciplines._

First we're going need to meet Numpy, and learn the basics of  access, and query structured, numeric data.


## Numpy

What do we mean by structured, numeric data? Numpy arrays deal with blocks of numbers, they have dimensions, and shapes.
The shapes are always 'rectangular', meaning the blocks of numbers look like sequences (1d), rectangles (2d), or hyperectangles (nd). In this tutorial we'll deal only with 1d Numpy arrays, which are just a sequence of numbers stretching along their single axis.  

We are going to hit the ground running and import some numerical data. In this case, we have a csv (comma separated variable) file containing historical price and volume data from the Nasdaq Stock Exchange (to be precise, the Nasdaq Composite index). This tutorial assumes the data is located in the followinf _relative path_: `data/nasdaq.csv`.

We assume that you are running this code from the notebooks directory of this book. The easiest (although not Necessarily the most robust) way of running the code is to Launch a notebook using the mybinder service.

[![Binder](http://mybinder.org/badge.svg)](http://mybinder.org:/repo/dansand/reschapter/archive/master.zip)

```python
numpy.loadtxt('../data/nasdaq.csv')
```


```
array([ 5249.899902,  5227.209961,  5213.220215, ...,   100.760002,
         100.839996,   100.      ])
```


We can also assign an numpy array to a variable using the same syntax.  Let's re-run `numpy.loadtxt` and save its result:

```python
data = numpy.loadtxt('../data/nasdaq.csv')
```

If we want to get a single number from the array,
we must provide an _index_ in square bracket:

```python
data[0]
```
```
5249.8999020000001
```

```python
print('first value in data:', data[0])
```

```
('first value in data:', 5249.8999020000001)
```


we can select whole sections as well. This is called a _slice_ For example, we can select the first ten days, we could do:

```python
data[0:10]
```
```
array([ 5249.899902,  5227.209961,  5213.220215,  5222.990234,
        5232.330078,  5218.919922,  5212.200195,  5217.689941,
        5260.080078,  5244.600098])
```


A couple of introductions to variables can be found here.



The expression `numpy.loadtxt` is a _function call]_ that asks Python to run the function `loadtxt` that belongs to the `numpy` library.

### Comparison with an Excel workflow

At this stage, it might be useful to consider how you would complete this task using spreadsheets, or another non-Programming language tool.

## Challenge(s)

Part 1: the demonstration/teaching of the learning objective
Part 2: the challenge(s) that embeds the learning objectives - this is the activity you give to your groups

## Plenary (Let's call this something else)

Summarise the main learning objectives/ key points covered in your chapter. These are different from the Learning Objectives where you assume no knowledge. Here you can assume knowledge gained after reading your chapter.

You have learned (how has this chapter provided the reader value):
a)
b)
c)

Where to next? Give the reader some guide to find more information or how to build on this knowledge. Attach a ‘resource pack’ (YouTube links), contact details and so on.

Bibliography to end.
*** APA referencing

## notes

Numpy vs np

The efficient markets hypothesis (EMH), popularly known as the Random Walk Theory,
is the proposition that current stock prices fully reflect available information about the
value of the firm, and there is no way to earn excess profits, (more than the market over
all), by using this information.

## Bibliography
