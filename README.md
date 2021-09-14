# bosch_manufacturing_line
University of Michigan: Milestone Project 1

Data Source Kaggle: [Bosch Manufacturing Line](https://www.kaggle.com/c/bosch-production-line-performance/data)

Project Description:
Analyze and predict internal failures of components in a manufacturing assembly line based on various test conditions.
The reason behind taking this project is to help the company produce quality products at lower manufacturing cost while avoiding product recalls later.

Specific questions to explore: This can be divided in to 3 sub-sections “Category, Date and Numeric”:
1.	Category:  What is the relationship between components and each production line? How many components were being assembled per line, what were those components and how frequently? The goal was also to explore how we can connect processing of components with assembly time as well as inspection test conditions (pass/fail).
2.	Datetime and Numeric Response: How to extract summary statistics per line such as mean, standard deviation between response target and assembly time as well as on an average how many test observations contributed to the summary statistics? Since, the dataset was large as well as sparse, this approach was useful but at the expense of processing time. 
3.	Combined analysis: What is the breakdown of lines which are failing test inspections purely based on numeric responses without any merge? Then, how should we merge extracted summary from category/datetime and Numeric analysis, and see has anything changed. Example, do we have fewer number of lines after the merge? If yes, then why and if that is significant then can we do similarity analysis with the rest? 

Data Manipulation Methods:  
•	Approach taken to summarize full dataset: Due to large file size, we had to use a combination of pyspark function and python lists and dictionaries to summarize csv files, then use pandas to further manipulate, merge and make plots. 

•	Processing Steps: After creating spark session, we used a simple function which collected assembly component counts and its usage per production line while avoiding null values. Then, extracted summary statistics as python list or dictionary as seem fit to store results as a csv file for further analysis. 

•	Data Joining Schema: After extracting information from individual tables, in order to connect the 3 csv files, we used production line LSF integer values as foreign keys to establish the relationship. The first merge operation was between category table and the numeric table which helped us gather response variable (pass/fail) per production line. Then, we merged again to see assembly times. However, it was interesting to note that the final merged table had only 22% of the production lines where assembly time and test observations were captured, making us believe that these lines probably acted as a node network for performing critical operations such as assembly of sub-assemblies, which company wanted to keep a watch on.

<img width="400" alt="image" src="https://user-images.githubusercontent.com/39008846/133240009-9599dee3-9456-445b-8e8a-6cb62c9a95d4.png">
