# Movies-ETL: Extract, Transform, and Load

## Purpose
The purpose of this repository is to contain the progress of extracting movie data from three different sources, transforming and cleaning the data, and loading the merged data into a table called "movies" in PostgreSQL. 

## Results

#### Extract
After importing the dependencies, I read in the kaggle metadata and MovieLens ratings CSV files as Pandas DataFrames:

    kaggle_metadata = pd.read_csv(kaggle, low_memory=False)
    ratings = pd.read_csv(movielens)

Next, I read in the Wikipedia data JSON file using the code:

    with open(wiki, mode='r') as file:
            wiki_movies_raw = json.load(file)

#### Transform
I used Pandas with Python in Jupyter Notebook in order to clean and transform the data. I edited the column names, filtered out TV show data, transformed the remaining movie data using regular expressions. Lastly, I consolidated the data.

The `wiki_movies_df` DataFrame from [ETL_clean_wiki_movies.ipynb](https://github.com/stephperillo/Movies-ETL/blob/main/ETL_clean_wiki_movies.ipynb) displays the cleaned data from the Wikipedia JSON file:

![wiki_movies_df.head.png](https://github.com/stephperillo/Movies-ETL/blob/main/Resources/wiki_movies_df.head.png)

The list of columns shows the cleaned up column names:

![wiki_movies_df.columns](https://github.com/stephperillo/Movies-ETL/blob/main/Resources/wiki_movies_df.columns.png)

In the [ETL_clean_kaggle_data.ipynb](https://github.com/stephperillo/Movies-ETL/blob/main/ETL_clean_kaggle_data.ipynb), I cleaned the data from the kaggle CSV. 

![movies_with_ratings_df.png](https://github.com/stephperillo/Movies-ETL/blob/main/Resources/movies_with_ratings_df.head.png)

This image confirms that the `movies_df` DataFrame was created successfully:
![movies_df.head.png](https://github.com/stephperillo/Movies-ETL/blob/main/Resources/movies_df.head.png)

#### Load

In [ETL_create_database.ipynb](https://github.com/stephperillo/Movies-ETL/blob/main/ETL_create_database.ipynb) I added the `movies_df` DataFrame and MovieLens rating CSV data to a SQL database. 

This is the query in the `movies` table to count the rows:

![movies_query.png](https://github.com/stephperillo/Movies-ETL/blob/main/Resources/movies_query.png)

The query for the count of rows in the `ratings` table is shown below:

![ratings_query.png](https://github.com/stephperillo/Movies-ETL/blob/main/Resources/ratings_query.png)

There are 26,024,289 rows in the `ratings` table! I also included code to print the elapsed time it takes to import each row to the database. 

These tools and techniques will very useful in future analyses.
