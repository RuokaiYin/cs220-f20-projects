# Project 9: Analyzing the Movies

## Clarifications/Corrections

**Find any issues?** Report to us:  
- Tim Ossowski [ossowski@wisc.edu](mailto:ossowski@wisc.edu)
- Changho Shin [cshin23@wisc.edu](mailto:cshin23@wisc.edu)
- Vinay Sahadevappa Banakar [vin@wisc.edu](mailto:vin@cs.wisc.edu)

## Learning Objectives

In this project, you will
- Use matplotlib to plot bar graphs and visualize statistics
- Reinforce your knowledge even further about dictionaries and lists
- Apply the idea of binning by creating dictionaries to group similar movies 
- Begin using custom sorting for lists

## Coding Style Requirements

Remember that coding style matters! **We might deduct points for bad coding style.** Besides the [requirements in p8](https://github.com/msyamkumar/cs220-f20-projects/tree/master/p8), here are a list of other common bad coding habits:

- Do not use meaningless names for variables or functions (e.g. uuu = "my name").
- Do not write the exact same code in multiple places. Instead, wrap this code into a function and call that function whenever the code should be used.
- Do not call unnecessary functions.
- Avoid using slow functions multiple times within a loop.
- Inappropriate use of data structures.
- Avoid calling functions that iterate over the entire dataset within another loop. For example, do not call get_column(colname) within a loop; instead, call the function before the loop and store the result in a variable.

## Introduction

In p8, you created very useful helper functions to help parse the raw movie IMDb dataset. In this project, we will be using the work you
did in p8 to load the movie data and analyze the data even further. **For the questions asking you to plot, our test.py is unable to check whether your plot is correct. As long as you have any output for these questions, you will pass the tests. So make sure compare your plots with the expected pngs ([Q4.png](https://github.com/msyamkumar/cs220-f20-projects/tree/master/p9/Q4.png), [Q5.png](https://github.com/msyamkumar/cs220-f20-projects/tree/master/p9/Q5.png), [Q6.png](https://github.com/msyamkumar/cs220-f20-projects/tree/master/p9/Q6.png), [Q7.png](https://github.com/msyamkumar/cs220-f20-projects/tree/master/p9/Q7.png), [Q8.png](https://github.com/msyamkumar/cs220-f20-projects/tree/master/p9/Q8.png), [Q12.png](https://github.com/msyamkumar/cs220-f20-projects/tree/master/p9/Q12.png)) before submitting your notebook.**

As usual, hand in the `main.ipynb` file (use the `#qN` format).  Start by downloading the following files: [`test.py`](https://github.com/msyamkumar/cs220-f20-projects/tree/master/p9/test.py), [`mapping.csv`](https://github.com/msyamkumar/cs220-f20-projects/tree/master/p9/mapping.csv), and [`movies.csv`](https://github.com/msyamkumar/cs220-f20-projects/tree/master/p9/movies.csv).

In `main.ipynb`, make sure to include a new cell with the following code:

```python
import csv
import copy 
import matplotlib
import pandas

%matplotlib inline # Allows you to render matplotlib graphs in the same notebook

def plot_dict(d, label="Please Label Me!!!"):
    ax = pandas.Series(d).sort_index().plot.bar(color="black", fontsize=16)
    ax.set_ylabel(label, fontsize=16)
```

Finally, copy all the functions you wrote from p8 to `main.ipynb`. As a reminder, the functions you should include are `process_csv`, `get_mapping`, `get_raw_movies`, `get_movies`.

If you are ready, let's get started!

<h2> Analyzing the Movie Data </h2>

For all these questions, we will be looking at the movies in `mapping.csv`. You can load the list of movies using the function
you wrote in the last project (Note you should only have to do this once):

```python
movies = get_movies("movies.csv", "mapping.csv")
```

This will result on a list of movies, which we can loop over and answer interesting questions about. Each entry in the list should be
a dictionary that looks something like this:

```python
{'title': 'The Big Wedding',
 'year': 2013,
 'rating': 5.6,
 'directors': ['Justin Zackham'],
 'actors': ['Robert De Niro'],
 'genres': ['Comedy', 'Drama', 'Romance']}
```

---

The first few questions can be answered using similar methods to earlier projects. They should help familiarize yourself with the data
and understand how to traverse it with loops:

### #q1 Find the average rating for movies with less than 4 actors (length of actor list < 4)?


### #q2 Find the average rating for movies with more than 5 actors (length of actor list > 5) ?


### #q3 What is the average rating of movies which start with the letter 'a' (case insensitive)?

---

For questions 4-8, your answers should be plots. Use the `plot_dict()` function to answer these questions Make sure to label the vertical axis with an informative name for all your graphs!

### #q4 Plot the title vs rating of movies featuring "Tom Cruise".

Comments: The horizontal axis should be names of movies Tom Cruise was in. The vertical axis should be the corresponding rating of these movies. 


### #q5 Plot the title vs rating of movies featuring "Sylvester Stallone".



### #q6 Plot the number of movies played by ["John Wayne", "Glenn Ford", "Danny Glover"].

Comments: The graph should have 3 bars, one for each of these actors. The height of each bar should be the number of movies the actor played in.

### #q7 Plot the number of movies that start with each letter of the alphabet.

Comments: The graph should have 26 bars, one for each letter of the alphabet. The x-axis should be in alphabetical order. The height of each bar should be the number of movies which start with that letter.

Hint: 1) define a dictionary which maps a letter in the alphabet to the number of movies that start with that letter:

```python
letters = "abcdefghijklmnopqrstuvwxyz"
letter_to_num_movies = {}
for letter in letters:
  	letter_to_num_movies[????] = ????
 
# Loop through movies and update letter_to_num_movies
```

2) remember to use `.lower()`.

### #q8: Plot the number of movies there are for each genre.

Comments: The graph should have 1 bar for each unique genre. The height of each bar should be the number of movies that contain that genre in its list of genres.

Hint: A movie might have multiple genres. Make sure you count all of the genres in the list for each movie:

```python
genre_to_num_movies = {}

for movie in movies:
  	for genre in movie['genres']:
    		...

```


### #q9 For each letter of the alphabet (except 'x'), what is the average rating of movies that start with that letter (case insensitive)?

Comments: Your answer should be a dictionary mapping each letter of the alphabet to the average rating of movies that start with that letter. The reason we exclude 'x' is that no movies start with a 'x' in this dataset, making the average undefined.

Hint: Since this question asks for an average, consider having a dictionary mapping a letter in the alphabet to a **list** of ratings of movies which start with that letter. Recall the average of entries in a list `numbers` can be computed with `sum(numbers)/len(numbers)`:

```python
letters = "abcdefghijklmnopqrstuvwyz" # No x this time!
letter_to_num_movies = {}
for letter in letters:
  	letter_to_num_movies[????] = ????
 
# Loop through movies and update letter_to_num_movies

# Go through letter_to_num_movies to find the average for each letter

```

### #q10 What is the average movie rating for each genre?

Comments: Your answer should be a dictionary mapping each genre to a number.


Hint: Consider using the same idea as hint in question 9.

### #q11 How many movies in each genre have a rating of above 4.0? (rating > 4.0)

Comments: Your answer should be a dictionary mapping each genre to a number.


Hint: Use a similar strategy to q8, but only include movies with rating above 4.

### #q12 Plot the number of movies that were released each year in the last decade (2010<= year <=2020)

Comments: Your answer should be a dictionary mapping each year to a number. Note that there are only movies up to the year 2018, so the graph should not have bars for years 2019 and 2020. See [Q12.png](https://github.com/msyamkumar/cs220-f20-projects/tree/master/p9/Q12.png) for reference.


### #q13 Which year (or years) had the highest number of movie releases?

Comments: Your answer should be a list. If there is a tie, the list should contain multiple years in it. Otherwise, the list should only have 1 year in it.

---

For the rest of the questions, custom sorting will be important.

### #q14 Which 5 genres have the least number of movies?

Hint: Create a dictionary which maps genre name to the number of movies in that genre. Also create a list of all unique genres. Define a custom sorting function:

```python
"""
This function returns the number of movies in this genre
"""
def genre_sort(genre_name):
  	return ????
```

Finally, sort the list of all unique genres according to this custom function:

```python
sorted(????, key = genre_sort)
```


### #q15 Which 5 genres have the most number of movies?

Hint: Use your answer from q14.

### #q16 Which 10 actors are featured in the most movies?

### #q17 Which actor has played in the greatest number of movies?

### #q18 How many actors have only acted in only 1 movie?

### #q19 What are the titles of the top 3 rated movies in the dataset?

### #q20 What are the titles of the bottom 19 rated movies in the dataset?

#### 

After you add your name and the name of your partner to the notebook, please remember to **Kernel->Restart and Run All** to check for errors then run the test.py script one more time before submission.  To keep your code concise, please **remove your own testing code that does not influence the correctness of answers.** 

