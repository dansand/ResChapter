#Numpy


## Introduction

Python is a _simple general-purpose programming language_. As such, Python is not tied to a specific task or discipline, but is widely used for processing and analyising text, numbers, images, building websites and applications, and increasingly in machine learning and data science. 

Python was created by Guido van Rossum in 1990, its namesake being Monty Python's Flying Circus. It is now developed by a large team of volunteers and is freely available from the Python Software Foundation. That's right, Python is free! More than that, Python has a strong ties to the open source movement. This means there is a culture of sharing and support within the Python 'ecosystem'.

Python, Matlab, or R (or Java, C++, ...)? There are a lot of programming languages, and many tasks - such as the one demonstrated in this chapter - can be completed equally well in all of them. So how to decide? In our group, some researchers chose Python because it was stronger in discipline-specific Libraries than any of it's competetors (for instance Neuroscience, Geophysics). However, for those of us had also dabled in other languages first (e.g. Matlab, R), and found that there was litte 'wasted' effort in switching. Many core concepts extend across all languages, not to mention the more ephemeral skill of 'thinking like a programmer'.

Finally, the introduction should end with a contents page listing how the rest of the chapter will flow.


### Learning Objectives:

In this chapter we're going to look a Python library called Numpy (numeric Python). A library is group of tools (code) designed to assist a common purpose, yet somehow outside the `core` capabilities of the Langauge. Numpy provides the ability to work with structured groups of numbers (arrays). Depending on the situation, these could represent individual measurements, vectors, time series, tables, grids, matrices, etc.

Using Numpy we're going to tackle a simple data science problem, yet one that has some profound implications. If you are new to Python and Numpy, our main suggestion is to __try to understand and keep the data science problem in mind__. Hopefully, if you have a good handle on the problem itself, the utility and efficiency of Python / Numpy will be apparent.


While you won't finish this chapter a fully-fledged Python programmer, we hope that you will get a sense of the 'flavour' of how Python works. Don't get too concerned about understanding _every_ piece of code that's written, but instead try to focus on how the programming approach to the __data science problem__ differs from a workflow you might develop using a spreadsheet or application (for instance Excel or SPSS).

Necessarily, we will introduce some extraneous concepts and terms, that we don't have time to fully-develop or explore . We will provide links ot material to help you master these subjects later on.

By the end of this chapter you will learn:

1. How to import, wrangle, and query structured, numeric data, using Python/Numpy.
2. The 'flavour' of using Python/Numpy for a data science workflow.


### glossary

* Library (e.g Numpy)
* Jupyter notebook
* Variable
* Function
* Boolean
* Elemeni
* index
* slice
* Method


### A data science problem

Our example looks at a real (data) science problem. In fact, we are going to to endeavour to _falsify_ a hypothesis.
We'll try to show that there _are_ predictable patterns in day-to-day stockmarket data, a discovery which would contradict the _efficient market hypothesis_. 

There are a number of statistical analyses relavent to this problem. Our workflow will simply answer __what is the overall frequency with which one days's market value _change_ follows the previous day's _change___.


_Remember, this is one example out of a vast number of problems that we could have chosen. Don't be lured into thinking that Python is a financial / economics tool. The data analysis here is totally general, and very similar problems (i.e. analysis on structured, numeric data) will appear in multiple disciplines._

First we're going need to meet Numpy, and learn the basics of accessing, and querying structured, numeric data.

### Running Python

Our intention is that while reading this chapter, you will be able to simultaneously run and edit the code we discuss. For this purpose we have set up a Jupyer notebook through the _mybinder_ service. Unless other options are available to you, try clicking on this [![Binder](http://mybinder.org/badge.svg)](http://mybinder.org:/repo/dansand/reschapter) link, which should open a Python session in the form of a Jupyter notebook. 

There are a minimal set of instructions within your Jupyer notebook to get you up and running. In devising this lesson, we do assume that there will be some instructors available for trouble-shooting.  

## Numpy

What do we mean by structured, numeric data? Numpy arrays are tables of numbers. The tables of may look like sequences (1-D), grids (2-D), or hyper-grids (n-D). In this tutorial we'll deal only with 1-D Numpy arrays, which are just a sequence of numbers stretching along their single axis.  Think of these data as a time series, with `n` values (which we call the elements of the array). A 1-D and 2-D array are shown below:

__Example of 1-D array__

```
   ┌──────┬──────┬──────┬──────┬──────┐
   │ 0.00 │ 0.25 │ 0.50 │ 0.75 │ 1.00 │
   └──────┴──────┴──────┴──────┴──────┘

```

__Example of 2-D array__

```
   ┌───┬───┬───┐
   │ 4 │ 5 │ 7 │
   ├───┼───┼───┤
   │ 0 │ 2 │ 6 │
   ├───┼───┼───┤
   │ 8 │ 4 │ 0 │
   └───┴───┴───┘
```

At this point you may wonder _is this it?_ Of course, Numpy is not just numbers in grid form. As we we see, it is also a set of syntax and function to very concisely and efficiently, wrangle, query and analyse those stored numbers. 


### importing data

We are going to dive right in and import some quantitative data. In this case, we have a csv (comma separated variable) file containing historical price and volume data from the Nasdaq Stock Exchange (to be precise, the Nasdaq Composite index). This tutorial assumes the data is located in the followinf _relative path_: `../data/nasdaq.csv`.

```python
numpy.loadtxt('../data/nasdaq.csv')
```

```
array([ 5249.899902,  5227.209961,  5213.220215, ...,   100.760002,
         100.839996,   100.      ])
```

The expression `numpy.loadtxt` is a _function call_ that asks Python to run the function `loadtxt` that belongs to the `numpy` library.

When we execucted this code, Python returned a set of numbers to us, enclosed in brackets and preceeded by the word _array_. The numbers are the data from the csv file, representing the __daily closing price for the Nasdaq composite index__ for a certain number of days. For simplicity we won't worry about the specific dates for this excercise. The word array is shown because we the `numpy.loadtxt` function constructs a specific type of object called an array. 

### numpy arrays as variables

We can also assign an numpy array to a variable using the same syntax.  Let's re-run `numpy.loadtxt` and save its result:

```python
data = numpy.loadtxt('../data/nasdaq.csv')
```

The key thing you need to understand is taht when we create a varible (usinf the `=` sign), the object on thr RHS of the `=` is now assigned to the varibale name. The object (in this case an array of numbers) gets stired in memory, and the name we _chose_ for our variable becomes the object that we work with. This might be easier to see in the following piece od code, where we plot the contents of our `data` variable.

A couple of introductions to variables can be found here...


The following lines will produce a simple plot of the the data. The only thing you need to understand here is that there is a pythin function called `plt.plot` that generates plots. To actually use this fucntion we have to hand it an object to plot. In this case it was our varible (our Numpy array) called data. 

```python
%pylab inline
plt.plot(data)
```

![Alt](../figs/nasdaq.png "Nasdaq data (backwards)")


If you're clued into the U.S stockmarket, you'll notice that our data is backwards. This is simply because the data in csv format was ordered by most-recent first. We can easily reverse the data,  but as it will not affect our analysis, we won't bother doing so now. 

The total number of data points (days) can be found by running:

```python
data.shape
```
  
```  
(11496,)
```

We say that the variable we named `data` has an _attribute_ called _shape_. The `.shape` attrubute can be called for any Numpy array; it will return the number of data points (elements) in each dimension. In this case there is 1 dimension, with `11496` elements, each representing a single day.




### maths with arrays

A great feature of numpy arrays is that we can do maths with entire arrays at once. Let's see this by running some code:

```python
data*2
```

```
array([ 10499.799804,  10454.419922,  10426.44043 , ...,    201.520004,
          201.679992,    200.      ])
```

Python returned 2  times each element of the original array, as does:

```python
data + data
```

```
array([ 10499.799804,  10454.419922,  10426.44043 , ...,    201.520004,
          201.679992,    200.      ])
```

And a final check:

```python
data - data
```
```
array([ 0.,  0.,  0., ...,  0.,  0.,  0.])
```

### indexing

If we want to get a single number from the array, we provide the number that represents the position of the element in teh array. This number is known as the _index_, and we refer to this process as _indexing_. When indexing an array, we provide the index in square brackets immediately after the _variable_ that represtents the Numpy array:

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

A more general view of the process of indexing is shown in the following schematic:

```
onetwothree = numpy.arange(3)
onetwothree[0]

   ┏━━━┓───┬───┐   ┏━━━┓
   ┃ 0 ┃ 1 │ 3 │ → ┃ 0 ┃
   ┗━━━┛───┴───┘   ┗━━━┛

```

Okay, if you've got this far well done! We just introduced a whole heap of concepts, at a pace that may have left you somewhat overwhelmed! Let's briefly summarise what we just did:

* imported a python library named Numpy
* used a _fucntion_ from Numpy to load a text file from out computer's filesystem
* used _variable assignment_ to create a Pyth variale that represents (points to) our Numpy array. 
* passed our variable to a different fucntion to create  quick plot.
* learnt how to access a _single_ element of our Numpy array using _indexing_. 

### slicing and dicing

Beyond indexing, we need a way to extract whole sections of data at once. This is called a _slice_. For example, to select the first ten days of our `data` array, we could do:

```python
data[0:10]
```
```
array([ 5249.899902,  5227.209961,  5213.220215,  5222.990234,
        5232.330078,  5218.919922,  5212.200195,  5217.689941,
        5260.080078,  5244.600098])
```

So the slice `[0:10]` means start at elemnent / index 0, and go up to (but not including) elemnent / index 10.

The up to (but not including), is simply a decision the engineers made when writing the library, as was the decision to start counting at 0. Feel free to love / hate these conventions.

A more general view of the process of _slicing_ is shown in the following schematic:

```
onetwothree = numpy.arange(3)
onetwothree[0:2]

   ┏━━━┓━━━┓───┐   ┏━━━┓━━━┓
   ┃ 0 ┃ 1 ┃ 3 │ → ┃ 0 ┃ 1 ┃
   ┗━━━┛━━━┛───┘   ┗━━━┛━━━┛

```


There are a couple of handy shortcuts with slices. First, if you omit of the element indexes on either side of the colon, it defaults, to the start / end of the array. Hence `data[0:10] <=> data[:10]`.

Also, negative indexes visit the elements in reverse order. Given this, which element would we be referring to when we write `data[-1]`? How about using `data[-3]`?


### slicing one array with another

Slicing gets a little fancier when we use one numpy array to slice another. Let's create a simple array with some integer values

```python
indices = np.array([1,44,722])
print(indices)
```

```
array([  1,  44, 722])
```

So let's try slicing our `data` array with our `indices` array:

```python
data[indices]
```

```
array([ 5227.209961,  4862.569824,  3929.570068])
```

While it might not be immediately obvious, our code returned the values of the `data` array, but only those elements correspoding to the indexes provided by the array `indices` (a numpy array we stored in a variable called `indices`)

One way we could check this is by passing both the original and sliced arrays into the Python function `len()` (length):

```python
len(data)
```
```
11496
```

```python
len(data[indices])
```
```
3
```
Hopefully it's clear that this means our original `data` numpy array had 11496 elements, while the sliced array has just 3.

### composing the tricks

So now we know about doing maths and slices. Let's see how these techniques combine. Say we have an arbitrary array called `u` then the meaning of the expression `u[1:] - u[:-1]` is demonstrated in the following figure:

![Alt](../figs/vectorized_diff.png "difference")

The array that results from  `u[1:] - u[:-1]` is the nth + 1 element of u minus the nth element. Necessarily, output array is one element shorter that u (we loose one element of overlap when we offset)


### asking questions / boolean arrays

Now we go up a gear. Frequently, we are going to want to ask quantitative questions about our data. Consider the following expression, and its output:

```python
data > data.mean()
```

```
array([ True,  True,  True, ..., False, False, False], dtype=bool)
```
We know what `data` is. The new parts here are the `>` symbol and the strange `data.mean()` thingo.  You may guess that `>` is similar to the mathematical _greater than_ operator. Well done. The expression `data.mean()` simply returns the mean of the data array. So `data.mean()` simply stands for a number - the mean of the dataset. To test this, try running `data.mean()` by itself.

```
data.mean()
```

```
1336.6577597914056
```

So what about that output, an array of True and ad False values? In plain English, the code `data > data.mean()`,  could be stated as 'is the value(s) of `data` bigger than the mean value of the data'. Numpy interprets this element-by-element, and returns

* `True` if an an element / value is greater than data.mean()
* `False` if an element / value is smaller. An array of "true" and `False` is called a Boolean array.

The kicker is that we can slice the original array, by this Boolean array:

```python
data[data > data.mean()]
```

```
array([ 5249.899902,  5227.209961,  5213.220215, ...,  1349.050049,
        1340.459961,  1346.359985])
```

Now we can check how many values in our dataset are greater than the mean.

```python
len(data[data > data.mean()])
```

```
4789
```

This process may be more clear if we break it apart a bit by creating an intermediary array. 

```python
ba = data > data.mean()

len(data[ba])
```

```
4789
```

Here explicity created an array `ba` to store the boolean values (`True` `False `) rather using them implicity. 


#The final flourish

Before we put together our analysis, remember that our `data` array contains the daily closing price for the Nasdaq Compisite Index. We are interested in the overall frequency with which today's closing price _change_ follows yesterday's.

The following line code combines all the Pyton/Numpy skills we have developed. Runnign this code will return a Numpy array which will have one of two values: `True` if one day's price (`data[1:]`) is greater than the previous day's price `data[:-1]`; otherwise `False`. The array containing these True and False values are assinged to the new array which we have called `follow`.

```python
follow = data[:-1] < data[1:]
```

Think about this for a bit. If the Nasdaq price goes up tow days in a row, the corresponding values in `follow` will be [...,`True`, `True`,...]. If the price went down for any consectuve days, the values would be [...,`False`, `False,...]. 

Finally, we want to assess how often either these consective True or Falsevalues appear. To do that we will run the following code. This uses one new piece of systax: in Python `==` means 'is equal to to'. 

```python
seq = follow[:-1] == follow[1:]
```

To reiterate, `seq` will contaian return `True ` if Yesterday's price _change_ was the same as _today's_ price change, otherwise return `False`. Once again these values are assigned to a new variable, called `seq

## Challenge

Your challenge is to combine the following two Python expressions to answer the question what is the overall frequency with which one day's closing price _change_ follows the previous days'. You simple need to combine the two expressions with one of the Python mathermatical operators ('+', '-', '/'). Good luck. 


```python
seq.sum(), len(data)
```

## Summary

### What just happened?

Summarise the main learning objectives/ key points covered in your chapter. These are different from the Learning Objectives where you assume no knowledge. Here you can assume knowledge gained after reading your chapter.

You have learned (how has this chapter provided the reader value):
a)
b)
c)

### Links

Where to next? Give the reader some guide to find more information or how to build on this knowledge. Attach a ‘resource pack’ (YouTube links), contact details and so on.

### Further analysis

See the github repo for a more rigourous statistical test

### Notes

Numpy vs np

The efficient markets hypothesis (EMH), popularly known as the Random Walk Theory,
is the proposition that current stock prices fully reflect available information about the
value of the firm, and there is no way to earn excess profits, (more than the market over
all), by using this information.

After a bit more Python training, you will understand that in writing `data.mean()` that we have accessed a _Method_ of the object `data`.

Installing Python

### Bibliography
