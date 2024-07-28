# Original Movies vs Sequels: Who wins?
## The data, notebooks, and process notes for project two
## What I aimed to accomplish:
I first started this project with a completely different ending in mind. I had scrapped movie ratings from [Rotten Tomatoes](https://www.rottentomatoes.com/) and I used an API to get ratings from [The Movie Database](https://www.themoviedb.org/). I was planning to compare the ratings of the movies across each platform. However, after I had already gotten all my data I thought of an idea! <u> why don't I see which are the highest rated franchises? what about the lowest? also, are original movies rated higher than franchises? </u> So, I decided to only use my IMDb data that I found [here](https://developer.imdb.com/non-commercial-datasets/). Specifically, I downloaded the <b> title.basics.tsv.gz </b> and <b>title.ratings.tsv.gz</b>. The data from the franchises are from [Film Site](https://www.filmsite.org/series-boxoffice.html) and a <i>loooot</i> of manual work, where I put the franchise on some movies one by one, either because the dataset from IMDb had title differences than the Franchise's one, or because the Franchises data only had specific franchises and didn't include others.
## My findings:
* The highest rated franchise is the Lord of the Rings, and the lowest rated franchise is Transformers.
* Original Movies Get Better Ratings than their Sequels.
* Out of the 62 franchises, the 41 had an original movie as the one with the highest rating. Only 21 franchises (34%) had a sequel movie as the one with the highest rating.
## Data collection process:
As mentioned, IMDb data was found [here](https://developer.imdb.com/non-commercial-datasets/). Specifically, I downloaded the <b> title.basics.tsv.gz </b> and <b>title.ratings.tsv.gz</b>. The data from the franchises are from [Film Site](https://www.filmsite.org/series-boxoffice.html). I did the analysis in 3 notebooks: One is called "imdb" for imdb analysis, one is called "franchises2" for franchise analysis, and the "movie" notebook" is the one where I combines the data and went forward onto the analysis.
## Data analysis process:
IMDB:
- I did not have to do much in this notebook, since the data was pretty good. I just uploaded the two datasets I got, merged them on "tconst" that was a coding for the movies, kept only the movies, sorted them by number of votes, kept only the first 500 rows, and sorted by rating. Lastly, I saved as "imdb.csv"

Franchises 2:
- Here things are more complicated because the table that I was trying to scrape from the website had a film column, that in each row had many many films. I saw that each film was in a <br> tag , so i tried to only take what's inside the br tags. Then, I create a new date column where I take the year out of the end of the film title using ReGex and I insert it in the new column. Then, I get rid of the year in the title.
- But, some films' titles where like: Ip Man 3 (2015/16) Meaning that the seperation didn't happen, and these movies had NaN values in the date column. I saved my data as excel and went onto manually deleting the date from the remaining movies and then fulfilling the date column. <i>Thanfully, in this part the manual work was easy and fast</i>. Then, I save it as "franchisesForMerging.csv"

Movies:
- In this notebook I called the imdb.csv and the franchisesForMerging.csv. I tried to merge the datasets on the film and date column. Now this is where it gets rough.. The franchises dataset and the imdb dataset had some of the same films. But, some films had small (or even big) title differences. Plus, some other films that are part of a franchise where not included in the franchise dataset, because they weren'tincluded in the website I scraped. Thus, quite a lot of manual work happened here, to make sure that each movie is assigned to the correct franchise. the command I used a lot was ex."df.loc[df['Film'] == 'Monsters University', 'Franchise'] = 'Monsters, Inc.'". Plus, some movies had been assigned to more than one franchise. I had to make sure to create a duplicate row, so that I could get rid of them in the next step.
- After making sure that each movie has been assigned to the correct franchise, I only kept the franchises that have 2 or more movies in the dataset. I was left with 62 franchises total.
- Then I created the "sortedFranchisesRatings.csv" where the franchises are sorted by their average ratings for all movies.
- I found total average of the franchises ratings (7.5). The calculation of the median agrees with the result.
- I created a datasets that had a franchise column and two columns: one for the movies that are rated above 7.5 (the average of ratings) and one for those below. (called aboveAndBelow.csv)
- I created a dataset called "itsTrue" where it has a column that says "true" if the original movie is the highest rated movie in the franchise and "false" if its the sequel.
- Found the average of the total of original and sequel movies, to see, is the average of the original better than the sequels (<i> spoiler: yes </i>?

<i> Note: The original movies refer to the first movie ever released from the franchise, while the sequels are all subsequent movies released after the original, regardless of whether their storylines occur before or after the original. Superheroes were assigned to the franchise that corresponds to their specific universe. </i>

In the files I uploaded, you can also find the datasets I created for Visualizations.
- <b> aboveAndBelow.csv </b> : has the franchise column, the average rating column, one column for the movies that the rating is higher that 7.5 (the total average)a dn one for those below.
- <b> franchisesForMerging.csv </b>: is the dataset used in the movie notebook to merge with imdb. Has franchise names, movies, date that we care about.
- <b> imdb.csv </b> : is the dataset used in the movie notebook to merge with franchises. has movies, date, ratings, number of votes
- <b> isTrue.csv </b> : it has a column that says "true" if the original movie is the highest rated movie in the franchise and "false" if its the sequel, and the franchises.
- <b> sortedFranchisesRatings.csv </b> : it has the franchises columns and the average rating for each franchise,

## Where did I grow the most / What did I want to do but couldn't:
The manual work was a little disappointing, and it took quite a long time for me to accept that this would be the way that the movies would be <b>correctly</b> assigned to the <b>correct</b> dataset. I tried the "fuzzywuzzy" library I saw online, to see If I could merge on the film column without the need to have <i>exactly</i> the same name titles. I couldn't make it work. Then, I saw there are libraries such as "jellyfish", that could be better, and tools like Open refine. 

However, it was a fun project, where I struggled a lot and had a chance to practise scraping a table with many lines in a row, merge two datasets that are different, and visualization. I definetely grew on the scraping part, and visualization.

I definitely got the chance to practise my skills, data and visualization wise. I made three vizualizations on flourish. This was also a good chance for me to use an other one of [Soma's templates](https://jsoma.github.io/page-templates/), where I used the scrolly-images one.

## Website
You can fink the url for my website [here](https://ioannapetsiou.github.io/movies/)
