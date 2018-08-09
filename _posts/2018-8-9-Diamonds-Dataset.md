---
layout: post
title: Diamonds Dataset
---

Today I completed a project of mine, which was to predict the transaction value of diamonds given certain properties. Its uploaded on my GitHub profile ([here]()) and on my Kaggle profile ([here]()).

The notebook has some comments and headings to explain what is going on. But you might have to turn to documentation, stackoverflow and google to completely know what's going on in there.  
The dataset is a simple collection of over 50000 diamond transactions which has features like the cut quality, color, depth, table, carat, price etc. and is hosted at Kaggle ([here](https://www.kaggle.com/shivam2503/diamonds)). My goal was to explore the data and try to find the transaction values within an absolute error of 500$.

I used simple feature engineering and data cleaning to prepare my data and then applied regression with Gradient Boosting Trees Regressor and Random Forest Regressor, out of which, the Random Forests gave better results.  
I managed to achieve a mean absolute error of around 315$ for the transaction price of a diamond, and am quite satisfied with my results, though there is still a lot of scop for improvement. But still I've decided to put this project behind me now and move on to bigger datasets.

So stay tuned to know more about my machine learning adventures!