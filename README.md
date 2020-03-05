# ETL-project
 
ETL Project Report
The two data sources we had used were: https://www.kaggle.com/orgesleka/imdbmovies and https://www.kaggle.com/stefanoleone992/rotten-tomatoes-movies-and-critics datasets#rotten_tomatoes_movies.csv. While both were stored as CSV, there were distinct errors that occured in the extraction process--even for the simple import of the CSV.

Extract:
The IMDB csv file was actually determined to have approximately 500 lines that were unsuable. This was due to being saved as a CSV, with titles actually containing commas. This made the rows space out up to 3 columns farther than others. This had to be avoided by having the import of the csv skip error lines rather than try to import it. This was considered acceptable as it was 500 out of approximatley 14500 lines (3.4% error rate). 

Issues (Transforming):
In order to have these databases be transformed into a single database, there were more issues that needed to be addressed. In order to join on the movie titles, the data has to be adjusted to ensure exact matches. The first concern that came up was the IMDB database listed the year the movie came out in the actual title. This information had to be deleted completely. This still only led to approximately 30 records matching of around 14000 each.

To further connect the data, each movie title from both CSVs were copied into another column, and had all spacing removed. This allowed for around 2900 movies to join together. This, however, led to duplicate data due to reboots of old movies. I norder to combat that, the merge had to be done on both title AND year released. This was initially thought impossible, as when the rotten tomatoes columns were displayed in jupyter notebook, it did not show that data available. However, when manually reviewing, it was actually determined that there was a column for streaming date and theaters date that was not displaying, but callable.

Due to having two separate dates to work with, the data has to be pulled into one columnn, converted to date time, and have the year extracted to join with the IMDB.

After this conversion, around 1400 movies were successfully combined into 1 data file.

-       
Load:
-       We used pandas to load in our database and read in the data from the CSV and imported the information into MongoDB and SQLite

As a challenge for us, we wanted to load the data into both SQLite and MongoDB. We were able to successfully set up the SQLite server with relative ease, and get the information imported from the dataframe through a simple to_sql command.

The MongoDB server caused a little bit more trouble, as the information had to be looped through correctly. Was the information was called into an array, it had to be looped through and input into a dictionary to allow for MongoDB to digest it. After a few test runs, and not able to get MongoDB to correctly create the database, we were able to loop through the data and get it to successfully write.

