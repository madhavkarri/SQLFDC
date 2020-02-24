# Data Scientist Role Play Using SQL
# Profiling and Analyzing the Yelp Dataset

Using SQL to answer specific questions for an organization and make inferences based on the findings. Dataset was from Yelp, which provides a platform for users to provide reviews and rate their interactions with a variety of organizations – businesses, restaurants, health clubs, hospitals, local governmental offices, charitable organizations, etc. Yelp has made a portion of this data available for personal, educational, and academic purposes.

[//]: # (Image References)

[image1]: ./Writeup_IV/ERYDS.png "ERYDS"

#
Yelp Data Set

https://www.yelp.com/dataset/challenge

#
Entity relationship diagram for the Yelp Data Set
![][image1]

#

Part 1: Yelp Dataset Profiling and Understanding

#
1. Data Profiling: Finding total number of records for each of the tables

```
--SQL Code
Select *
From "table_name"

```
Output
```

i. Attribute table = 10000
ii. Business table = 10000
iii. Category table = 10000
iv. Checkin table = 10000
v. elite_years table = 10000
vi. friend table = 10000
vii. hours table = 10000
viii. photo table = 10000
ix. review table = 10000
x. tip table = 10000
xi. user table = 10000

```

#
2. Find distinct records, either by foreign key or primary key

```
i. Business = 10000
--SQL Code
Select DISTINCT Id
From Business

ii. Hours = 1562
--SQL Code
Select DISTINCT Business_Id
From Hours

iii. Category = 2643
--SQL Code
Select DISTINCT Business_Id
From Category

iv. Attribute = 1115
--SQL Code
Select DISTINCT Business_Id
From Attribute

v. Review = 10000
--SQL Code with id (primary key)
Select DISTINCT Id
From Review

	v. Review = 8090
	--SQL Code with business_id (foreign key)
	Select DISTINCT Business_Id
	From Review

	v. Review = 9581
	--SQL Code with user_id (foreign key)
	Select DISTINCT User_Id
	From Review

vi. Checkin = 493
--SQL Code
Select DISTINCT Business_Id
From CheckIn

vii. Photo = 10000
--SQL Code with id (primary key)
Select DISTINCT Id
From Photo

	vii. Photo = 6493
	--SQL Code with id (foreign key)
	Select DISTINCT Business_Id
	From Photo

viii. Tip = 537
--SQL Code with user_id (foreign key)
Select DISTINCT User_Id
From Tip

	viii. Tip = 3979
	--SQL Code with business_id (foreign key)
	Select DISTINCT Business_Id
	From Tip

ix. User = 10000
--SQL Code with id (primary key)
Select DISTINCT Id
From User

x. Friend = 11
--SQL Code with user_id (foreign key)
Select DISTINCT User_Id
--Select Count(DISTINCT User_Id)
From Friend

xi. Elite_years = 2780
--SQL Code with user_id (foreign key)
Select DISTINCT User_Id
From Elite_Years

```

#
3. Columns with null values in the Users table? Indicate "yes," or "no."
Answer: NO
	
```
	SQL code used to arrive at answer:
	Select
	  id,
	  name,
	  review_count,
	  yelping_since,
	  useful,
	  funny,
	  cool,
	  fans,
	  average_stars,
	  compliment_hot,
	  compliment_more,
	  compliment_profile,
	  compliment_cute,
	  compliment_list,
	  compliment_note,
	  compliment_plain,
	  compliment_cool,
	  compliment_funny,
	  compliment_writer,
	  compliment_photos

	From User
	Where
	  id IS Null OR
	  name IS Null OR
	  review_count IS Null OR
	  yelping_since IS Null OR
	  useful IS Null OR
	  funny IS Null OR
	  cool IS Null OR
	  fans IS Null OR
	  average_stars IS Null OR
	  compliment_hot IS Null OR
	  compliment_more IS Null OR
	  compliment_profile IS Null OR
	  compliment_cute IS Null OR
	  compliment_list IS Null OR
	  compliment_note IS Null OR
	  compliment_plain IS Null OR
	  compliment_cool IS Null OR
	  compliment_funny IS Null OR
	  compliment_writer IS Null OR
	  compliment_photos IS Null

```

#
4. Data aggregation, the smallest (minimum), largest (maximum), and average (mean) value for the following fields:

i. Table: Review, Column: Stars
```	
		min: 1		max: 5		avg: 3.7082
		--SQL Code
		SELECT
		    Min(Stars) as Minimum,
		    Max(Stars) as Maximum,
		    Avg(Stars) as Average
		FROM
		    Review

```

ii. Table: Business, Column: Stars
```	
		min: 1		max: 5		avg: 3.6549
		--SQL Code
		SELECT
		    Min(Stars) as Minimum,
		    Max(Stars) as Maximum,
		    Avg(Stars) as Average
		FROM
		    Business
```

iii. Table: Tip, Column: Likes
```	
		min: 0		max: 2		avg: 0.0144
		--SQL Code
		SELECT
		    Min(Likes) as Minimum,
		    Max(Likes) as Maximum,
		    Avg(Likes) as Average
		FROM
		    Tip
```

iv. Table: Checkin, Column: Count
```	
		min: 1		max: 53		avg: 1.9414
		--SQL Code
		SELECT
		    Min("Count") as Minimum,
		    Max("Count") as Maximum,
		    Avg("Count") as Average
		FROM
		    Checkin
```

v. Table: User, Column: Review_count
```	
		min: 0		max: 2000	avg: 24.2995
		--SQL Code
		SELECT
		    Min(Review_count) as Minimum,
		    Max(Review_count) as Maximum,
		    Avg(Review_count) as Average
		FROM
		    User
```

#
5. List cities with the most reviews in descending order:

	SQL code used to arrive at answer:
	
	Select
	  City,
	  -- total review counts
	  Sum(Review_Count) As TRCs
	From
	  Business
	Group By
	  City
	Order By
	  TRCs Desc

	
	Copy and Paste the Result Below:
		
	+-----------------+-------+
	| city            |  TRCs |
	+-----------------+-------+
	| Las Vegas       | 82854 |
	| Phoenix         | 34503 |
	| Toronto         | 24113 |
	| Scottsdale      | 20614 |
	| Charlotte       | 12523 |
	| Henderson       | 10871 |
	| Tempe           | 10504 |
	| Pittsburgh      |  9798 |
	| Montréal        |  9448 |
	| Chandler        |  8112 |
	| Mesa            |  6875 |
	| Gilbert         |  6380 |
	| Cleveland       |  5593 |
	| Madison         |  5265 |
	| Glendale        |  4406 |
	| Mississauga     |  3814 |
	| Edinburgh       |  2792 |
	| Peoria          |  2624 |
	| North Las Vegas |  2438 |
	| Markham         |  2352 |
	| Champaign       |  2029 |
	| Stuttgart       |  1849 |
	| Surprise        |  1520 |
	| Lakewood        |  1465 |
	| Goodyear        |  1155 |
	+-----------------+-------+
	(Output limit exceeded, 25 of 362 total rows shown)

#
6. Find the distribution of star ratings to the business in the following cities:

SQL code

-- to test appropriate output, use 'Las Vegas' as City


-- this code to verify total ratings in a city 
-- Order By Asc (ascending shows) to show count from 1-star to 5-star for a specific city
-- for Las Vegas there are a total of 23 1-star ratings
-- /*
Select
  Business.Id,
  Business.City,
  Review.Stars
  --Count(Review.Stars) As SC
From 
  Business
Inner Join Review
  On Business.Id = Review.Business_Id
Where
  Business.City = 'Las Vegas'
Order By
  Review.Stars Asc
-- */

-- this code for star rating distribution
--/*
Select
  Review.Stars,
  Count(Review.Stars) As StarCount
From 
  Review
Inner Join Business
  On Review.Business_Id = Business.Id
Where
  Business.City = 'Las Vegas'
Group By
  Review.Stars


i. Avon

SQL code used to arrive at answer:

Select
  Review.Stars,
  Count(Review.Stars) As StarCount
From 
  Review
Inner Join Business
  On Review.Business_Id = Business.Id
Where
  Business.City = 'Avon'
Group By
  Review.Stars

Copy and Paste the Resulting Table Below (2 columns – star rating and count):
+-------+-----------+
| stars | StarCount |
+-------+-----------+
+-------+-----------+
(Zero rows)


ii. Beachwood

SQL code used to arrive at answer:
Select
  Review.Stars,
  Count(Review.Stars) As StarCount
From 
  Review
Inner Join Business
  On Review.Business_Id = Business.Id
Where
  Business.City = 'Beachwood'
Group By
  Review.Stars


Copy and Paste the Resulting Table Below (2 columns – star rating and count):
+-------+-----------+
| stars | StarCount |
+-------+-----------+
|     3 |         1 |
+-------+-----------+

#
7. Find the top 3 users based on their total number of reviews:
		
	SQL code used to arrive at answer:
	Select
	  Name,
	  Review_Count
	From
	  User
	Order By
	  Review_Count Desc
	Limit 3
		
	Copy and Paste the Result Below:
	+--------+--------------+
	| name   | review_count |
	+--------+--------------+
	| Gerald |         2000 |
	| Sara   |         1629 |
	| Yuri   |         1339 |
	+--------+--------------+	

#
8. Does posing more reviews correlate with more fans?
	
	NO
	More reviews does not necessarily mean more fabs

	Please explain your findings and interpretation of the results:

	A quick analysis of number of reviews and number of fans shows that 
	user Amy with maximum number of fans (503) has a review count of 609, less than user Gerald who has a review count of 2000

	+--------+--------------+------+----------------+
	| name   | review_count | fans |            RFR |
	+--------+--------------+------+----------------+
	| Amy    |          609 |  503 | 0.825944170772 |
	| Mimi   |          968 |  497 | 0.513429752066 |
	| Harald |         1153 |  311 | 0.269731136167 |
	+--------+--------------+------+----------------+

	SQL code used to arrive at answer:
	Select
	  Name,
	  Review_Count,
	  Fans,
	  -- ratio of fans to number of reviews (Number of fans per review)
	  Fans*1.0/Review_Count as RFR
	From
	  User
	Order By
	  Fans Desc
	
	A further analysis of fans per review count shows that
	user Rebecca has the maximum number of fans per review basis

	+---------+--------------+------+------+
	| name    | review_count | fans |  RFR |
	+---------+--------------+------+------+
	| rebecca |            6 |   69 | 11.5 |
	| Susan   |            6 |   63 | 10.5 |
	| Nelson  |            7 |   70 | 10.0 |
	+---------+--------------+------+------+

	SQL code used to arrive at answer:
	Select
	  Name,
	  Review_Count,
	  Fans,
	  -- ratio of fans to number of reviews (number of fans per review)
	  Fans*1.0/Review_Count as RFR
	From
	  User
	Order By
	  RFR Desc
	Limit 3

#
9. Are there more reviews with the word "love" or with the word "hate" in them?

	Answer: with word 'love'

	+------------+
	| Count_Love |
	+------------+
	|       1780 |
	+------------+

	+------------+
	| Count_Hate |
	+------------+
	|        232 |
	+------------+
	
	SQL code used to arrive at answer:
	--/* to count text entries
	Select
	  Id,
	  "Text"
	From  
	  Review

	--/* to count text entries with Love
	Select
	  Count("Text") As Count_Love
	From  
	  Review
	Where
	  "Text" Like '%love%'
	--*/

	--/* to count text entries with Hate
	Select
	  Count("Hate") As Count_Hate
	From  
	  Review
	Where
	  "Text" Like '%hate%'

#
10. Find the top 10 users with the most fans:

	SQL code used to arrive at answer:
	Select
		  Name,
		  Review_Count,
		  Fans,
		  -- ratio of fans to number of reviews (number of fans per review)
		  Fans*1.0/Review_Count as RFR
	From
	  User
	Order By
	  Fans Desc
	Limit 10	
	
	Copy and Paste the Result Below:
	+-----------+--------------+------+----------------+
	| name      | review_count | fans |            RFR |
	+-----------+--------------+------+----------------+
	| Amy       |          609 |  503 | 0.825944170772 |
	| Mimi      |          968 |  497 | 0.513429752066 |
	| Harald    |         1153 |  311 | 0.269731136167 |
	| Gerald    |         2000 |  253 |         0.1265 |
	| Christine |          930 |  173 | 0.186021505376 |
	| Lisa      |          813 |  159 |  0.19557195572 |
	| Cat       |          377 |  133 | 0.352785145889 |
	| William   |         1215 |  126 | 0.103703703704 |
	| Fran      |          862 |  124 | 0.143851508121 |
	| Lissa     |          834 |  120 | 0.143884892086 |
	+-----------+--------------+------+----------------+
	
#
11. Is there a strong relationship (or correlation) between having a high number of fans and being listed as "useful" or "funny?" Out of the top 10 users with the highest number of fans, what percent are also listed as “useful” or “funny”?

Key:
0% - 25% - Low relationship
26% - 75% - Medium relationship
76% - 100% - Strong relationship

THERE EXISTS MEDIUM RELATIONSHIP (76%-100%)
	
	SQL code used to arrive at answer:
	Select
	  Id,
	  Fans,
	  Useful,
	  Funny,
	  -- fans per Useful review as percent
	  100.0*Fans/Useful As FPU,
	  -- fans per Funny review as percent
	  100.0*Fans/Funny As FPF  
	From  
	  User
	Order By Fans Desc
	Limit 10

	
	Copy and Paste the Result Below:
	+------------------------+------+--------+--------+----------------+----------------+
	| id                     | fans | useful |  funny |            FPU |            FPF |
	+------------------------+------+--------+--------+----------------+----------------+
	| -9I98YbNQnLdAmcYfb324Q |  503 |   3226 |   2554 |  15.5920644761 |   19.694596711 |
	| -8EnCioUmDygAbsYZmTeRQ |  497 |    257 |    138 |  193.385214008 |  360.144927536 |
	| --2vR0DIsmQ6WfcSzKWigw |  311 | 122921 | 122419 | 0.253008029547 | 0.254045532148 |
	| -G7Zkl1wIWBBmD0KRy_sCw |  253 |  17524 |   2324 |  1.44373430724 |  10.8864027539 |
	| -0IiMAZI2SsQ7VmyzJjokQ |  173 |   4834 |   6646 |  3.57881671494 |   2.6030695155 |
	| -g3XIcCb2b-BD0QBCcq2Sw |  159 |     48 |     13 |         331.25 |  1223.07692308 |
	| -9bbDysuiWeo2VShFJJtcw |  133 |   1062 |    672 |  12.5235404896 |  19.7916666667 |
	| -FZBTkAZEXoP7CYvRV2ZwQ |  126 |   9363 |   9361 |  1.34572252483 |  1.34601004166 |
	| -9da1xk7zgnnfO1uTVYGkA |  124 |   9851 |   7606 |   1.2587554563 |  1.63029187484 |
	| -lh59ko3dxChBSZ9U7LfUw |  120 |    455 |    150 |  26.3736263736 |           80.0 |
	+------------------------+------+--------+--------+----------------+----------------+
	
	
	Please explain your findings and interpretation of the results:

	Answer/Justification for this question was attempted based on the post by Mentor (Ayush Singh) with reference to question 11:
	https://www.coursera.org/learn/sql-for-data-science/discussions/all/threads/xkgEEGHqEeiEphLB3FeC3g

	- A metric was established to determine percent number of Fans per either useful (FPU) or Funny (FPF) review.
	- Correlation/Relationship was established based on the top 10 users based on number of Fans.
	- A cursory look at columns FPU and FPF reveals that, by eliminating top users 2, 6, 7, and 10 a relationshiop can be established
	  between Fans and being listed as useful or funny.
    - Since 4 records have been eliminated out of 10 (60%), the relationship has been established as Medium (26% - 75% - Medium relationship)

#
Part 2: Inferences and Analysis

1. Pick one city and category of your choice and group the businesses in that city or category by their overall star rating. Compare the businesses with 2-3 stars to the businesses with 4-5 stars and answer the following questions. Include your code.

Selected City: Las Vegas
Selected Category: Restaurants

Column Truncated Output

+---------------------+-------+-----------------------+--------------+--------------+---------------------------------+-------------+
| name                | stars | hours                 | review_count | neighborhood | address                         | postal_code |
+---------------------+-------+-----------------------+--------------+--------------+---------------------------------+-------------+
| Wingstop            |   3.0 | Monday|11:00-0:00     |          123 |              | 5045 W Tropicana Ave            | 89103       |
| Wingstop            |   3.0 | Tuesday|11:00-0:00    |          123 |              | 5045 W Tropicana Ave            | 89103       |
| Wingstop            |   3.0 | Friday|11:00-0:00     |          123 |              | 5045 W Tropicana Ave            | 89103       |
| Wingstop            |   3.0 | Wednesday|11:00-0:00  |          123 |              | 5045 W Tropicana Ave            | 89103       |
| Wingstop            |   3.0 | Thursday|11:00-0:00   |          123 |              | 5045 W Tropicana Ave            | 89103       |
| Wingstop            |   3.0 | Sunday|11:00-0:00     |          123 |              | 5045 W Tropicana Ave            | 89103       |
| Wingstop            |   3.0 | Saturday|11:00-0:00   |          123 |              | 5045 W Tropicana Ave            | 89103       |
| Jacques Cafe        |   4.0 | Monday|11:00-20:00    |          168 | Summerlin    | 1910 Village Center Cir, Unit 1 | 89134       |
| Jacques Cafe        |   4.0 | Tuesday|11:00-20:00   |          168 | Summerlin    | 1910 Village Center Cir, Unit 1 | 89134       |
| Jacques Cafe        |   4.0 | Friday|11:00-20:00    |          168 | Summerlin    | 1910 Village Center Cir, Unit 1 | 89134       |
| Jacques Cafe        |   4.0 | Wednesday|11:00-20:00 |          168 | Summerlin    | 1910 Village Center Cir, Unit 1 | 89134       |
| Jacques Cafe        |   4.0 | Thursday|11:00-20:00  |          168 | Summerlin    | 1910 Village Center Cir, Unit 1 | 89134       |
| Jacques Cafe        |   4.0 | Sunday|8:00-14:00     |          168 | Summerlin    | 1910 Village Center Cir, Unit 1 | 89134       |
| Jacques Cafe        |   4.0 | Saturday|11:00-20:00  |          168 | Summerlin    | 1910 Village Center Cir, Unit 1 | 89134       |
| Big Wong Restaurant |   4.0 | Monday|10:00-23:00    |          768 | Chinatown    | 5040 Spring Mountain Rd         | 89146       |
| Big Wong Restaurant |   4.0 | Tuesday|10:00-23:00   |          768 | Chinatown    | 5040 Spring Mountain Rd         | 89146       |
| Big Wong Restaurant |   4.0 | Friday|10:00-23:00    |          768 | Chinatown    | 5040 Spring Mountain Rd         | 89146       |
| Big Wong Restaurant |   4.0 | Wednesday|10:00-23:00 |          768 | Chinatown    | 5040 Spring Mountain Rd         | 89146       |
| Big Wong Restaurant |   4.0 | Thursday|10:00-23:00  |          768 | Chinatown    | 5040 Spring Mountain Rd         | 89146       |
| Big Wong Restaurant |   4.0 | Sunday|10:00-23:00    |          768 | Chinatown    | 5040 Spring Mountain Rd         | 89146       |
| Big Wong Restaurant |   4.0 | Saturday|10:00-23:00  |          768 | Chinatown    | 5040 Spring Mountain Rd         | 89146       |
+---------------------+-------+-----------------------+--------------+--------------+---------------------------------+-------------+

i. Do the two groups you chose to analyze have a different distribution of hours?

YES 
Restaurants with 2-3 stars are open from 11:00-0:00
Restaurants with 4-5 stars are open from either 11:00-20:00 or 10:00-23:00

ii. Do the two groups you chose to analyze have a different number of reviews?

YES
Group with 4-5 stars have a higher number of reviews (168 and 768) relative to 2-3 stars
         
         
iii. Are you able to infer anything from the location data provided between these two groups? Explain.
Restaurants grouping based on star rating had no correlation to their geographical location.
Restaurants Wingstop (2-3 Star Group) and Big Wong (4-5 Star Group) are closer to each other compared to Jacques Cafe and Big Wong (4-5 Star Group)
The geographical vicinity validation was performed by postal_code in google maps. Further more, geographical vicinity can also be validated by latitude and longitude data.

SQL code used for analysis:

Select
  Business.Id,
  Business.Name,
  Business.City,
  Category.Category,
  Stars,  
  Hours.Hours,
  Business.Review_Count,
  Business.Neighborhood,
  Business.Address,
  Business.Postal_Code,
  Business.Latitude,
  Business.Longitude
From
  Business
Inner Join Category On Business.Id = Category.Business_Id
Inner Join Hours On Business.Id = Hours.Business_Id
Where (Business.City = 'Las Vegas' AND Category.Category = 'Restaurants')
Order By Business.Stars

#
2. Group business based on the ones that are open and the ones that are closed. What differences can you find between the ones that are still open and the ones that are closed? List at least two differences and the SQL code you used to arrive at your answer.

Output:
+---------+---------------+-------------------+
| is_open |    Avg(Stars) | Avg(Review_Count) |
+---------+---------------+-------------------+
|       0 | 3.52039473684 |     23.1980263158 |
|       1 | 3.67900943396 |     31.7570754717 |
+---------+---------------+-------------------+

i. Difference 1: Average Star rating of all open businesses > Average Star rating of all closed businesses
         
         
ii. Difference 2: Average Review_Count of all open businesses > Average Review_Count of all closed businesses
         

SQL code used for analysis:
Select
 Is_Open,
 Avg(Stars),
 Avg(Review_Count)
From
  Business
Group By Is_Open
	
#
3. For this last part of your analysis, you are going to choose the type of analysis you want to conduct on the Yelp dataset and are going to prepare the data for analysis.

Ideas for analysis include: Parsing out keywords and business attributes for sentiment analysis, clustering businesses to find commonalities or anomalies between them, predicting the overall star rating for a business, predicting the number of fans a user will have, and so on. These are just a few examples to get you started, so feel free to be creative and come up with your own problem you want to solve. Provide answers, in-line, to all of the following:
	
i. Indicate the type of analysis you chose to do: 

Find best "Business/Businesses" in "USA" that sells "Pizza" with highest "Star" rating or with "Star" rating in descending order
         
         
ii. Write 1-2 brief paragraphs on the type of data you will need for your analysis and why you chose that data:

As the data does not have a table associated with listing of Menu for each business, 
take advantage of semantics or keywords from "table: review and column: text." 
This can be an idea to generate popular Menu for each business using semantics.

Data Generation Method: 
Find best "Business/Businesses" in "United States" that sells "Pizza" with highest "Star" rating or with "Star" rating in descending order
For the case of businesses with identical "Star" rating, use "Review_Count" to sort businesses with equal "Star" rating

Required tables and fields necessary to generate this data
Business:
	Id
	Name
	City
	State
	Latitude  (To select all businesses within contiguous United States)
	Longitude (To select all businesses within contiguous United States)
	Stars	  (To sort the best Business/Businesses in descending order)
	Review_Count (For the case of Businesses with identical "Star" rating)
Review:
	Business_Id
	Text	  (To find the word "pizza")

The latitude and longitude limits were established using the following links
As only 4 points are being considered to establish latitude and longitude coordinates, 
this resulted in a rectangle and few cities form the southern most Canada are listed

a) https://en.wikipedia.org/wiki/List_of_extreme_points_of_the_United_States
b) https://tools.wmflabs.org/geohack/geohack.php?pagename=Lubec,_Maine&params=44_51_38_N_66_59_5_W_type:city
c) https://tools.wmflabs.org/geohack/geohack.php?pagename=List_of_extreme_points_of_the_United_States&params=49_00_08.6_N_122_15_40_W_region:US_type:landmark&title=Sumas%2C+WA
d) https://tools.wmflabs.org/geohack/geohack.php?pagename=Ballast_Key&params=24_31_26_N_81_57_51_W_region:US-FL_type:isle

Final rough latitude and longitude limits used in SQL Code
(49,-66.5) NorthernMost-EasternMost
(49,-122.5)NorthMost-WesternMost
(24.5,-66.5)SouthernMost-EasternMost
(24.5,-122.5)SouthMost-WesternMost

Additional Comments: This analysis can be further improvised by using sentiment analysis associated with the word "Pizza". 
Currently accuracy of the SQL query: "Star" rating is not necessarily associated with "Pizza" being the best menu item of the business,
although most of the results indicate that's the case.
                  
iii. Output of your finished dataset:

Truncated Output without columns Business_Id and Review."Text"

+---------------------------------+------------+-------+----------+-----------+-------+--------------+
| name                            | city       | state | latitude | longitude | stars | review_count |
+---------------------------------+------------+-------+----------+-----------+-------+--------------+
| Spinato's Pizza                 | Tempe      | AZ    |  33.4276 |    -111.9 |   4.5 |          507 |
| Salvatore's Tomato Pies         | Madison    | WI    |  43.0849 |  -89.3759 |   4.5 |          149 |
| Yogurtland                      | Las Vegas  | NV    |  36.1157 |    -115.3 |   4.5 |          116 |
| The Juice Standard              | Henderson  | NV    |   36.018 |  -115.101 |   4.5 |           88 |
| MOD Pizza                       | Tempe      | AZ    |  33.3493 |  -111.901 |   4.5 |           77 |
| Frankstown Wood Fired Pizza     | Pittsburgh | PA    |  40.4822 |  -79.8219 |   4.5 |           19 |
| Angelo's Pizza                  | Lakewood   | OH    |   41.477 |  -81.7883 |   4.0 |          377 |
| Intermezzo Pizzeria and Cafe    | Charlotte  | NC    |  35.2222 |  -80.8217 |   4.0 |          231 |
| Clockwork Pizza                 | Tempe      | AZ    |    33.35 |   -111.93 |   4.0 |          199 |
| Pizza Taglio                    | Pittsburgh | PA    |  40.4603 |   -79.925 |   4.0 |           93 |
| Nick & Ben's Pizza Company      | Surprise   | AZ    |  33.6113 |   -112.36 |   4.0 |           79 |
| Upper Crust Pizza               | Las Vegas  | NV    |  36.1929 |  -115.306 |   4.0 |           56 |
| Po' Boys Restaurant             | Urbana     | IL    |  40.1177 |  -88.2059 |   4.0 |           54 |
| The Buffet                      | Las Vegas  | NV    |  36.1269 |  -115.166 |   3.5 |         3873 |
| Target                          | Las Vegas  | NV    |  36.1142 |  -115.312 |   3.5 |           89 |
| Timpone's                       | Urbana     | IL    |  40.1064 |  -88.2237 |   3.5 |           85 |
| Barro's Pizza                   | Ahwatukee  | AZ    |  33.3181 |  -111.984 |   3.5 |           69 |
| Barro's Pizza                   | Mesa       | AZ    |  33.3659 |  -111.859 |   3.5 |           41 |
| Il Sogno Ristorante             | Toronto    | ON    |  43.7006 |  -79.3969 |   3.5 |           31 |
| Tower Pizzeria                  | Las Vegas  | NV    |  36.1477 |  -115.156 |   3.5 |           21 |
| The Outer Layer                 | Toronto    | ON    |  43.6659 |  -79.4083 |   3.5 |           19 |
| Cinquecento Trattoria           | Toronto    | ON    |  43.6401 |  -79.4212 |   3.5 |           13 |
| Mellow Mushroom                 | Phoenix    | AZ    |   33.318 |  -111.976 |   3.0 |          244 |
| Takara Bune Japanese Restaurant | North York | ON    |   43.776 |  -79.3253 |   3.0 |           33 |
| Rainforest Café                 | Las Vegas  | NV    |  36.1087 |  -115.172 |   2.5 |          444 |
+---------------------------------+------------+-------+----------+-----------+-------+--------------+
(Output limit exceeded, 25 of 26 total rows shown)

         
iv. Provide the SQL code you used to create your final dataset:

Select
  Business.Id,
	Business.Name,
	Business.City,
	Business.State,
	Business.Latitude,
	Business.Longitude,
	Business.Stars,
	Business.Review_Count,
	Review."Text"
From Business
Inner Join Review On Business.Id = Review.Business_Id
Where (Review."Text" Like '%Pizza%' AND 
       Business.Latitude > 24.5 AND Business.Latitude < 49 AND
       Business.Longitude > -122.5 AND Business.Longitude < -66.5
       )
Order By 
  Business.Stars Desc,
  Business.Review_Count Desc

