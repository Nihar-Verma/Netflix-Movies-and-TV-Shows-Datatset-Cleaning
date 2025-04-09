# Netflix-Movies-and-TV-Shows-Datatset-Cleaning
By perforing shape operation I found this dataset contains 8807 Netflix titles with 12 columns including content type, title, cast, country, date_added, release_year, rating, duration, listed_in, description.
In this dataset, several columns have missing values with varying percentages:

director: 29.91% missing
country: 9.44% missing
cast: 9.37% missing
date_added: 0.11% missing
rating: 0.05% missing
duration: 0.03% missing
Rather than dropping rows with missing values (which would significantly reduce our dataset), I've chosen to impute these values in ways that maintain analytical integrity:

For director, I've used content-specific imputation:

TV Shows → "Various Directors" (reflecting the common practice of multiple directors for series)
Movies → "Unknown Director"
For country, cast, rating, and description, I've used descriptive placeholders that clearly indicate missing information without introducing bias.

This approach preserves the maximum amount of data for analysis while ensuring transparency about which values were originally missing.

During data exploration, I identified two key format issues that needed correction:

Date formatting problems:

The date_added column contained string dates with inconsistent leading whitespace
By applying str.strip() before conversion and using the proper date format (%B %d, %Y), I successfully converted these strings to proper datetime objects
This enables time-based analysis and proper sorting by date
Misplaced duration values:

I discovered 3 records where duration values (e.g., "90 mins") were incorrectly placed in the rating column
Using regex pattern matching ('\d+ mins'), I identified these misclassified values
For each incorrect record:
If the duration column was empty, I moved the value to its proper place
I then set the rating to "NR" (Not Rated) to maintain data integrity
These corrections ensure that both date-based queries and content rating analyses will produce reliable results, without losing any valuable information from the dataset.

