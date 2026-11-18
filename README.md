MovieLens Ratings: Data Cleaning & Exploratory Analysis

Cleaning and exploring a deliberately "dirty" version of the MovieLens 100K dataset to understand who rates movies, what they rate highly, and where men and women disagree, as groundwork for a future recommendation system.

Tools: Python · pandas · NumPy · Matplotlib · seaborn · Jupyter

Dataset

Three raw files were merged into one analysis table of 115,214 rows × 15 columns:

File	Rows	Contents
dirty_data.csv	100,000	User–movie ratings with timestamps
dirty_users.csv	1,037	User age, gender, occupation, zip code
dirty_movies.csv	1,766	Title, release date, IMDb URL, genres

Ratings were joined to users on user_id (left join), then to movies on movie id.

Data Quality Issues Found

The pre-cleaning profile turned up several problems:

Missing values: age (11.7%), occupation (11.6%), genres (10.8%), gender (9.5%), rating (2.0%)
Invalid ratings: values ranging from −19 to 25 on what should be a 1–5 scale
Impossible ages: a minimum of −10 and a maximum of 150
Empty column: video release date was 100% null
Duplicate keys: user_id/id and movies_id/movie id held the same information after the merge
Wrong data types: age stored as float, release date stored as text
Multi-value field: genres packed several categories into one string (for example, Crime,Film-Noir,Mystery,Thriller)
Cleaning Steps
Removed or corrected ratings outside the valid 1–5 range
Handled age outliers and converted age to integer
Converted release date to datetime
Dropped the all-null column and the duplicate ID columns
Treated missing demographic and genre values (add your exact method here: dropped, imputed, or "Unknown")
Analysis Questions
Which movies get the most ratings, and how do men and women rate them?
Which movies are rated highest by women, and which by men?
Which movies divide men and women most (largest difference in mean rating)?
Which movies cause the most disagreement overall (highest standard deviation of ratings)?
Key Findings
The audience is skewed: most ratings come from male users, and students are the largest occupation group.
Star Wars (1977) is the most-rated movie in the dataset, with 646 ratings. Drama is the most common genre label.
Averages need a minimum vote count. Many titles at the top of the "highest rated" lists have only a handful of ratings, so their 5.0 averages aren't reliable. Ranking only movies above a ratings threshold gives a truer picture.
The most polarizing titles (for example, The Deadly Cure, Tough and Deadly and Delta of Venus, each with a standard deviation of about 2.8) are niche films with very few ratings.
Next Steps

This EDA defines the problem statements for follow-up work:

Recommendation system: collaborative filtering (user–item or matrix factorization) using rating history plus demographics
Rating prediction: predict a user's rating from age, gender, occupation and genre
User segmentation: cluster users by rating behavior and demographics
Genre trends: genre preferences by age group and occupation, and how they change over release years
Bias checks: test whether ratings differ systematically by gender or occupation
Repository Structure
├── Movies Rating EDA.ipynb   # Full cleaning + EDA notebook
├── LICENSE
└── README.md
How to Run
bash
pip install pandas numpy matplotlib seaborn jupyter
jupyter notebook "Movies Rating EDA.ipynb"

Place the three CSV files in a data/ folder next to the notebook.
