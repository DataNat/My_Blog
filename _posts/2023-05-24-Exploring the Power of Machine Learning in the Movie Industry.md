---
layout: post
title: 'Exploring the Power of Machine Learning in the Movie Industry'
tags: [Startups, JavaScript]
featured_image_thumbnail:
featured_image: assets/images/posts/2019/movie_cover.png
featured: true
hidden: true
---


## Introduction

In recent years, online streaming has gained tremendous popularity, with streaming companies venturing into the production business to create captivating movies and shows. In this competitive industry, understanding audience preferences and predicting movie popularity is crucial. Data science plays an integral role in providing valuable insights to gain viewer interest.

In this blog, we will discuss the process of predicting movie popularity and discover how our personalized recommendation system enhances the users' experience.

### Exploring Movie Popularity

'Popularity' is a measure of the level of interest and engagement among IMDB users for a movie. It measures on a scale of 1 to 1000. By analyzing user ratings, reviews, views, and overall buzz, we gain valuable insights into audience preferences and trends.

#### Popularity Distribution

```python
# Creating a violin plot of popularity
fig = px.violin(tmdb_5000_mov, y='popularity', 
                box=True, title='Distribution of Popularity')
fig.update_layout(yaxis_title='Popularity')
fig.show()
pio.write_image(fig, 'violin_plot_popularity.png')


 <img src="/assets/images/posts/2019/popularity.png" alt="popularity">

### Release Dates

Movies released in June, July, and December tend to gain the highest levels of interest, with an average popularity score ranging from 28 to 30. On the other hand, movies released in January, February, and September have a lower average popularity score that ranges from 12 to 18.

```python
# Creating the bar plot with plotly
fig = px.bar(monthly_avg_popularity, x="release_date_month",
             y="popularity",
             labels={"release_date_month": "Release Month",
                     "popularity": "Average Popularity"},
             template="plotly_white",
             color="popularity",
             color_continuous_scale="Blues")

# Setting labels for the x-axis tick
fig.update_layout(
    xaxis=dict(
        tickmode="array",
        tickvals=list(range(1, 13)),
        ticktext=['Jan', 'Feb', 'Mar', 'Apr', 'May',
                  'Jun', 'Jul', 'Aug', 'Sep', 'Oct',
                  'Nov', 'Dec']
    )
)

# Setting labels for the title & axis
fig.update_layout(
    title="Average Movie Popularity by Release Month",
    xaxis_title="Release Month",
    yaxis_title="Average Popularity",
    font=dict(size=18)
)

# Showing the plot
fig.show()

 <img src="/assets/images/posts/2019/month.png" alt="Month">

### Genres

Certain genres stand out for their popularity among viewers. Adventure, Animation, Science Fiction, Fantasy, and Action movies captivated audiences more than other genres, with average popularity scores ranging from 32 to 39.

In comparison, Comedy and Drama movies have an average popularity score of 18. Mystery, Thriller, War, and Crime movies fall in between, with an average score of 24, showing a moderate level of popularity.

```python
# Creating a bar plot
fig = go.Figure(data=go.Bar(
    x=group_genres['genres'],
    y=group_genres['popularity'],
    marker_color='green'
))

# Updating title and axis
fig.update_layout(
    title='Popularity of Genres',
    xaxis_title='Genres',
    yaxis_title='Popularity',
    height=600,
    width=1000
)

# Showing the plot
fig.show()

 <img src="/assets/images/posts/2019/genres.png" alt="Genres">

## Predicting Movie Popularity

Using machine learning, we have developed a regression model that accurately predicts movie popularity. We started with a baseline model, OLS, and improved its performance by selecting certain features, resulting in a minimized root mean squared error (RMSE). Subsequently, we implemented three machine learning models, Random Forest, XGBoost, and AdaBoost, and found that Random Forest outperformed the others in terms of predictive accuracy. Lastly, we implemented a general MLP (Multi-Layer Perceptron) model, which showed fairly good results in capturing complex patterns and relationships within the data.

We decided to further improve the results by implementing hyperparameter tuning techniques. Here are snippets of the code used for hyperparameter tuning of the Random Forest and General MLP models.

### Hypertuning Random Forest

```python
# Setting up parameters
parameters = {
   'n_estimators': [100, 150, 200, 250, 300],
   'max_depth': [1,2,3,4],
}

# Creating the Regressor
rf = RandomForestRegressor(n_jobs=-1)

# Performing randomized search 
grid_search_rf = GridSearchCV(estimator=rf,
                              param_grid=parameters,
                              verbose=1,
                              n_jobs=-1,
                              cv=5)

### Hypertuning General MLP

```python
# Using MLP architecture with Keras model
Kmodel = KerasRegressor(build_fn=mlp)

# Using hyperparameter optimizers options for grid search
optimizers = ['rmsprop', 'adam']
epochs = np.array([50, 100])
batches = np.array([10, 20])
param_grid = dict(optimizer=optimizers, epochs=epochs, batch_size=batches)

# Using grid search cross-validation
grid_search_mlp = GridSearchCV(estimator=Kmodel,
                               param_grid=param_grid,
                               n_jobs=-1,
                               cv=3,
                               verbose=2)

The top-performing models in terms of prediction accuracy were Random Forest (Tuned) with an RMSE of 22 and Random Forest with an RMSE of 23. XGBoost followed with an RMSE of 25, while KerasRegressor achieved an RMSE of 26. The OLS-SelectK model demonstrated reasonable prediction accuracy with an RMSE of 28. AdaBoost and MLP models had higher RMSE values of 33 and 34, respectively.

<img src="/assets/images/posts/2019/movie_results.png" alt="movie_results">

## Conclusion

The machine learning models, particularly with hyperparameter tuning, have shown promising results in predicting movie popularity. Further improvements can be made by fine-tuning the MLP model with a larger dataset to enhance its effectiveness.

This analysis demonstrates how machine learning can extract valuable insights from movie data, driving advancements in the industry and opening doors for future possibilities.

The complete code can be found on our [GitHub repository](https://github.com/DataNat/Movie_Popularity_Predictor-Recommendation-System) for a deeper understanding of the methodology and implementation.
