# Bias on Wikipedia
## DATA 512 A2 Bias in Data
The goal of this assignment is to explore 'bias' in terms of article coverage and article quality regarding political figures on Wikipedia for many countries.

Data I used for this assignment is a combination of Wikipedia articles data and country population data. And for Wikipedia articles, I used a machine learning algorithm 'ORES' to evaluate the quality of each article.  ORES reads article revision id as an input and it will output a quality score for each article.  

There are 6 score categories here:  
FA - Featured article  
GA - Good article   
B - B-class article     
C - C-class article   
Start - Start-class article   
Stub - Stub-class article   

And a csv file will be saved after calculating score for each article and combining with population dataset as wikipedia_article_population.csv. And it has following attributes:   

| Column         | 
| ------------------|
| country          | 
| article_name |
| revision_id.    | 
| article_quality |
| population      |

For analysis, I calculated the proportion of articles per capita (number of articles regarding politicians divided by the population) and high-quality articles (number of high-quality articles divided by the total articles regarding politicians) for each country. An article is 'high-quality' when 'ORES' evaluates it in the 'FA (Featured Article)' or 'GA (Good Article)' category.  

There will be four visualizations generated for this assignment:   
10 countries with the highest proportion of politician articles per capita.   
10 countries with the lowest proportion of politician articles per capita.   
10 countries with the highest proportion of high-quality politician articles of all politician articles.   
10 countries with the lowest proportion of high-quality politician articles of all politician articles.   

And a short reflection on this assignment in the end.         

To reproduce the result of the project, you will need to clone this repository into your computer.

## Organization of the  project

The project has the following structure:  
   * data-512-a2
     * |- README.md  
     * |- LICENSE  
     * |- ProgrammingStep  
        * |- hcds-a2-bias.ipynb 
        * |- Visualization
          * |- 10 countries with highest proportion of politicians articles per capita.png
          * |- 10 countries with lowest proportion of politicians articles per capita.png
          * |- 10 countries with highest proportion of high-quality articles of all articles.png
          * |- 10 countries with lowest proportion of high-quality articles of all articles.png
     * |- Final Data 
        * |- wikipedia_article_population.csv

In the following sections I will examine these elements one by one. First, let's consider the core of the project which is the hcds-a2-bias.ipynb in hcds-512-a2/ProgrammingStep folder. 

## ProgrammingStep
### hcds-a2-bias.ipynb   
In this Jupiter notebook, detailed steps are documented and presented to 
1) read data for Wikipedia articles dataset and population dataset.   
2) predict quality score for each article using ORES.   
3) combine Wikipedia articles dataset and population dataset.      
4) calculate the proportion of articles per capita and high-quality ("FA" or "GA") articles for each country.
5) create visulizations

#### How to use the Jupyter Notebook
After the Jupyter Notebook is downloaded, run through the notebook.
The module will then output:     
1) 1 final data file in CSV format.     
3) 4 .png images of the visualizations.     

### Visualization
4 .png images of the visualization will be saved after executing hcds-a2-bias.ipynb . The visualization will show    
10 countries with the highest proportion of politician articles per capita.   
10 countries with the lowest proportion of politician articles per capita.   
10 countries with the highest proportion of high-quality politician articles of all politician articles.   
10 countries with the lowest proportion of high-quality politician articles of all politician articles.   

## Data
The Wikipedia article dataset is from Figshare. https://figshare.com/articles/Untitled_Item/5513449. The Wikipedia article dataset can be downloaded as 'page_data.csv' and used in latter analysis.The dataset has 47198 rows and 3 variables: country, page and last_edit. 'country' is the country where the politician is from. 'page' is the article title. And 'last_edit' is the edit ID of the last user who edits the page.  

License of the source data:         
Data is generated under CC-BY-SA 4.0 license.        
Wikimedia Foundation terms of use:    
https://wikimediafoundation.org/wiki/Terms_of_Use/en   

The population data is from Population Research Bureau website.http://www.prb.org/DataFinder/Topic/Rankings.aspx?ind=14. The population dataset can be downloaded as 'Population Mid-2015.csv' and used in latter analysis. The dataset has 21 rows (210 countries in total) and 5 variables: Location,  Location Type, TimeFrame, DataType and Data.
'Location' is the country name. 'Location Type' is always 'Country'.' TimeFrame' is 'Mid-2015'. Data Type is 'Number'. And 'Data' is the country population. We will extract only country name sand population variables for analysis.   

License of the source data:  
Population Reserach Bureau copyright

And for Wikipedia articles, I used a machine learning algorithm 'ORES' (Objective revision Evaluation service) to evaluate the quality of each article. ORES reads article revision id as an input and it will output a quality score  and probabilities the the article's predicted quality for each article.  I extracted only the predicted quality score for analysis. 

There are 6 score categories here:  
FA - Featured article  
GA - Good article   
B - B-class article     
C - C-class article   
Start - Start-class article   
Stub - Stub-class article   
Documentation on what each score category means can be found at https://en.wikipedia.org/wiki/Wikipedia:WikiProject_assessment#Grades  

ORES relevant API documentation:  
https://www.mediawiki.org/wiki/ORES     
ORES API endpoints:      
https://ores.wikimedia.org/v3/#!/scoring/get_v3_scores_context_revid_model    


### Final Data  
After generating a new column of ORES prediction score for each article, inner join the Wikipedia article dataset and population dataset together by country name (remove rows with null values). The data frame has following columns:   

| Column         | 
| ------------------|
| country          | 
| article_name |
| revision_id.    | 
| article_quality |
| population      |

A final data file will be saved as wikipedia_article_population.csv.  

## Important Notes
1) ORES API documentation: https://ores.wikimedia.org/v3/#!/scoring/get_v3_scores_context_revid_model  
2) After taking rev_id for each article into ORES API, it will return a prediction value and a prediction probability for the score. We use only prediction value in this assignment.   
3) The countries in Wikipedia article dataset and population dataset are different. We only keep the common countries for analysis.  
4) For unavailable revision ID, an error will be generated and no quality score can be predicted from ORES. I skipped those rows for analysis.
