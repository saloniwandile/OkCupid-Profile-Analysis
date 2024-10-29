# OkCupid Profiles Analysis
[![Python](https://img.shields.io/badge/Python-3.8-blue.svg)](https://www.python.org/)
[![MongoDB](https://img.shields.io/badge/MongoDB-CloudServer-green.svg)](https://www.mongodb.com/)
[![Python Libraries](https://img.shields.io/badge/Python%20Libraries-Various-red.svg)](https://pypi.org/)
[![NLP](https://img.shields.io/badge/NLP-Various-blue.svg)](https://www.nltk.org/)
[![Data Collection](https://img.shields.io/badge/Data%20Collection-Various-orange.svg)](https://beautiful-soup-4.readthedocs.io/en/latest/)
[![Data Analysis](https://img.shields.io/badge/Data%20Analysis-Various-purple.svg)](https://pandas.pydata.org/)
[![Linux](https://img.shields.io/badge/Linux-Various-black.svg)](https://www.linux.org/)

## Overview

The OkCupid Profiles Analysis project focuses on analyzing user profiles on OkCupid to uncover patterns in matching preferences and profile popularity. This analysis was conducted by a team of three, with a key emphasis on attributes such as age, height, and body type. Additionally, the project explored factors affecting profile popularity, including income and lifestyle choices. The insights derived from this analysis aim to enhance understanding of online dating dynamics and user behaviors.

### Key Features
- **Comprehensive Profile Analysis**: Investigates key attributes like age, height, and body type to identify trends and preferences among users.
- **Popularity Factors**: Analyzes how income and lifestyle choices influence profile popularity and matching preferences.
- **Behavioral Insights**: Provides valuable insights into user behaviors and preferences on the OkCupid platform.
- **Collaborative Effort**: Developed collaboratively with a team, contributing to a more robust and diverse analysis.

### Technologies Used
- **Python**: Utilized for data analysis, scripting, and implementing machine learning models.
- **MongoDB**: Employed for handling large volumes of unstructured data from OkCupid profiles.
- **NLP Libraries**: Applied Natural Language Processing techniques for text analysis and pattern recognition.
- **Data Collection Tools**: Utilized libraries for scraping and collecting data from OkCupid profiles.
- **Data Analysis Libraries**: Leveraged Python libraries for data manipulation, visualization, and analysis.

### Goals
- **Uncover Patterns**: Identify and analyze patterns in user profiles to understand matching preferences and profile popularity.
- **Enhance Understanding**: Improve comprehension of online dating dynamics through detailed examination of user attributes and behaviors.
- **Provide Insights**: Deliver actionable insights into factors affecting profile attractiveness and user preferences on the OkCupid platform.
- **Team Collaboration**: Showcase the effectiveness of teamwork in conducting a comprehensive analysis and deriving valuable conclusions.

## Step - 1 : Getting Started

1. **Installation**: Ensure you have Python and the necessary libraries installed. The following libraries are crucial for the project:

   - `numpy`: For numerical operations.
   - `pandas`: For data manipulation and analysis.
   - `matplotlib`: For creating static, animated, and interactive visualizations.
   - `seaborn`: For statistical data visualization.
   - `wordcloud`: For generating word clouds.
   - `pymongo`: For working with MongoDB.
   - `re`: For regular expressions in Python.

   To install these libraries, you can use the following commands:

   ```bash
   pip install numpy
   pip install pandas
   pip install matplotlib
   pip install seaborn
   pip install wordcloud
   pip install pymongo

## Step - 2 : Dataset Information

The dataset used in this project is sourced from Kaggle and contains detailed profiles from OkCupid users. This dataset provides valuable insights into user attributes and preferences on the platform.

### I. Dataset Details

- **Source**: The dataset can be downloaded from Kaggle at the following link: [OkCupid Profiles Dataset](https://www.kaggle.com/datasets/andrewmvd/okcupid-profiles).
- **Description**: The dataset comprises 60,000 records with structured information including:
  - **Attributes**: Age, sex, orientation, etc.
  - **Text Data**: Open-ended descriptions provided by users, etc.

The dataset contains both structured and unstructured data, making it ideal for analyzing user behavior and matching preferences.

#### How to Access

You can either:
1. **Download from Kaggle**: Visit the provided link and download the dataset directly from Kaggle.
2. **Use Provided Dataset**: Alternatively, the dataset has been uploaded and is available within the project directory. Please refer to the dataset file included in the project for immediate use.

Ensure you place the dataset in the appropriate directory of your project to facilitate smooth data processing and analysis.

### II. NoSQL Database and Dataset

We utilized a MongoDB database to analyze the OKCupid dataset. The dataset contained information regarding dating profiles of users, with unstructured columns (e.g., `essay0` to `essay9`) where users explained their habits, dating preferences, work, daily routines, and more.

#### MongoDB Setup

To analyze the data, we deployed the OKCupid dataset to our MongoDB cloud server. Our analysis leverages MongoDB's NoSQL querying capabilities, using aggregation pipelines to extract and process insights.

#### Steps to Deploy and Connect to MongoDB

1. **Deploy the Dataset to MongoDB**:
   - Ensure you have a MongoDB Atlas account.
   - Create a new cluster if you don’t have one.
   - Import the OKCupid dataset into your MongoDB Atlas cluster. You can use MongoDB's `mongoimport` tool or the Atlas Data Import feature.

2. **Update Your Connection Details**:
   - You need to configure your MongoDB connection string with your credentials. Use the following template to connect to your MongoDB Atlas cluster:
   - For Example for the Analysis 1 - Matching Preferences Exploration update the below section of the code for the for the file which is present (typically `<Your Path to Project>\OkCupid Profiles Analysis\Code and Analysis\Analysis 1 - Matching Preferences Exploration\Matching Preferences Exploration.ipynb`) file, follow these steps:


    ```python
    from pymongo import MongoClient
    from pymongo.errors import ServerSelectionTimeoutError

    try:
        mongo_client = MongoClient("mongodb+srv://<user>:<password>@okcupid.njnu4m5.mongodb.net/OKCupid?retryWrites=true&w=majority")
        print("Connected to MongoDB Atlas")
    except ServerSelectionTimeoutError as e:
        print(f"Error connecting to MongoDB Atlas: {e}")
    except Exception as e:
        print(f"An error occurred: {e}")
    ```

   - Replace `<user>` and `<password>` with your MongoDB Atlas credentials.

3. **Update the Code with Your MongoDB Details**:
   - Before running any analysis scripts, ensure that your code is updated with the correct database name, collection (table) name, and credentials. This is essential for querying the database and retrieving data for analysis.

By following these steps, you will set up your MongoDB environment for the other analysis files as well and be ready to run the analysis as described in this project. Ensure that the dataset and the MongoDB connection are correctly configured to facilitate smooth data processing and accurate results.

## Step - 3 : Code and Analysis

### Analysis 1: Matching Preferences Exploration

#### 1.1 Patterns and Trends in Matching Preferences: Age, Height, and Body Type

This analysis investigates patterns in user matching preferences based on attributes like age, height, and body type on OkCupid. We explored both structured and unstructured data to identify trends and preferences.

**Key Steps:**
1. **Data Filtering**: Utilized MongoDB aggregation to filter profiles based on age, body type, and essay presence.
2. **Data Projection**: Projected necessary fields and combined essay text for analysis.
3. **Categorization**: Added age groups and grouped data by age and body type.
4. **Aggregation**: Calculated average height and grouped essays for further processing.
5. **Visualization**: Generated visualizations to depict average height by age group and body type.

**Results:**
- **Average Height by Age Group and Body Type**: Found that "fit" body type is more common among younger users (19-35), while "average" and "a little extra" types are more evenly spread across age groups 36-45.
- **Insights**: This suggests potential trends in user preferences that could inform OkCupid's recommendation algorithms to improve user experience.

#### 1.2 Essay Content Analysis across Age Groups

Building on the physical attributes analysis, we examined the language used in users' essays to understand how age influences textual self-presentation.

**Key Steps:**
1. **Data Filtering**: Extracted and processed essay data for different age groups.
2. **Text Processing**: Split essays into words and filtered out common terms.
3. **Visualization**: Created bar charts to display frequently used words by age group.

**Results:**
- **Linguistic Patterns**: Found distinct variations in essay content across age groups. For example, users aged 36-45 frequently used words related to career, hobbies, and family, reflecting a focus on personal interests and values.
- **Implications**: The analysis indicates that older users may have a broader range of preferences and values compared to younger users who showed a stronger preference for "fit" body types.

**Example MongoDB Pipelines:**

  ###### Define the aggregation pipeline for matching preferences 
    matching_pipeline = [
        # Filter and process documents
        # ...
    ]

  ###### Execute the aggregation pipeline
      matching_results = list(mongo_database.OKCupid.aggregate(matching_pipeline, allowDiskUse=True))

###### Define the aggregation pipeline for essay content analysis
      essay_pipeline = [
      # Filter and process documents
      # ...
    ]

###### Execute the aggregation pipeline
      essay_results = list(mongo_database.OKCupid.aggregate(essay_pipeline, allowDiskUse=True))

### Analysis 2: Profile Popularity Analysis

#### Overview

In the "Profile Popularity Analysis," we delve into the factors affecting user attractiveness on the OkCupid platform. This analysis explores how structured attributes (e.g., income, lifestyle choices) and unstructured attributes (e.g., essay content) influence a user's popularity. We use MongoDB pipelines to segment data and identify patterns related to income, smoking, drinking preferences, and gender.

#### Analysis Components

#### 2.1 Decoding Popularity: Income, Lifestyle Choices Insights

1. **Income and Smoking Preferences**
   - **Objective**: Understand the relationship between average income and smoking habits, categorized by gender.
   - **Findings**: Non-smokers tend to have a higher average income compared to smokers.

2. **Income and Drinking Preferences**
   - **Objective**: Examine the connection between average income and drinking habits, segmented by gender.
   - **Findings**: Social or rare drinkers generally exhibit a higher average income than frequent drinkers.

#### 2.2 Extending Decoding Popularity by Unraveling Preferences

1. **Smoking and Drinking Preferences by Gender**
   - **Objective**: Investigate the relationship between smoking and drinking habits across genders and correlate with income levels.
   - **Findings**: Gender-specific income differences within smoking and drinking categories highlight nuanced preferences.

2. **Word Cloud Analysis of Essay Content**
   - **Objective**: Generate word clouds for male and female users based on essay content to visualize common themes and interests.
   - **Findings**:
     - **Male Users**: Focus on social activities or career aspirations.
     - **Female Users**: Emphasize relationships, openness, work-life balance, and personal values.

#### MongoDB Pipeline Implementation

The MongoDB aggregation pipeline used for this analysis consists of several stages:

1. **Filtering**: Match documents with necessary structured attributes and essay fields.
2. **Projection**: Select relevant fields for deeper analysis and concatenate essay fields.
3. **Income Categorization**: Classify income into groups for comparative analysis.
4. **Grouping and Aggregation**:
   - Group by smoking and drinking preferences, calculate average income, and count users.
   - Compute percentage distribution of user groups.
5. **Word Cloud Generation**: Aggregate essay content to visualize common terms and themes for male and female users.

#### Sample Pipeline Code
      popularity_pipeline = [
      # Match documents with required fields
      {
          '$match': {
              '$and': [
                  {'income': {'$exists': True, '$type': 'number', '$gte': 0}},
                  {'diet': {'$exists': True, '$ne': None, '$ne': '', '$ne': 'null'}},
                  {'drinks': {'$exists': True, '$ne': None, '$ne': '', '$ne': 'null'}},
                  {'smokes': {'$exists': True, '$ne': None, '$ne': '', '$ne': 'null'}},
                  {'sex': {'$exists': True, '$ne': None, '$ne': '', '$ne': 'null'}},
                  {'$or': [
                      {'essay0': {'$exists': True, '$ne': None, '$ne': '', '$ne': 'null'}},
                      # Continue for other essay fields
                  ]}
              ]
          }
      },
      # Project necessary fields
      {
          '$project': {
              'income': 1,
              'diet': 1,
              'drinks': 1,
              'smokes': 1,
              'sex': 1,
              # Combine essay fields
          }
      },
      # Add income group
      {
          '$addFields': {
              'income_group': {
                  '$switch': {
                      'branches': [
                          # Income range categorization
                      ],
                      'default': "Unknown"
                  }
              },
              'sex': {
                  '$cond': [{'$eq': ['$sex', 'f']}, 'Female', {'$cond': [{'$eq': ['$sex', 'm']}, 'Male', 'Female']}]
              }
          }
      },
      # Group by smoking, drinking preferences
      # Calculate total count and project final structure
      # Execute aggregation
  ]

### Analysis 3: Understanding User Characteristics

#### Overview

This analysis focuses on deriving insights about user characteristics based on their essays, specifically `essay5` and `essay7`, in conjunction with their sex and age. The key objectives are:

1. **Identifying Relationship Preferences**: Categorizing users into three relationship preference groups (romantic, casual, mixed) based on their essay content.
2. **Understanding Ideal Weekend Plans**: Analyzing preferences for weekend activities by examining essay content and demographic data.

#### 3.1 Relationship Preferences

#### Approach

- **Data Extraction**: Utilized MongoDB aggregation pipelines to analyze `essay5` and classify users into three relationship preference categories:
  - **Romantic**: Indicated by keywords such as "love," "romantic," "affection," etc.
  - **Casual**: Indicated by keywords like "casual," "fling," "non-committal," etc.
  - **Mixed**: Users with mentions of both romantic and casual themes.

- **Aggregation**:
  - Created separate pipelines to count the number of users in each category, grouped by gender.

#### Results

- **Findings** illustrates that:
  - A higher percentage of users preferred romantic relationships compared to casual ones.
  - Women showed less inclination towards romantic relationships compared to men but were more interested in casual and mixed relationships.
  - Men exhibited a stronger preference for romantic relationships compared to women, though fewer men preferred casual encounters.

#### 3.2 Weekend Activity Preferences

#### Approach

- **Data Extraction**: Analyzed `essay7` to uncover preferences for weekend activities. Categories included:
  - **Family**: Spending time with family or relatives.
  - **Friends**: Socializing with friends.
  - **Dining/Going Out**: Eating out or going out.
  - **Stay-In**: Staying at home, watching TV, cooking.
  - **Work**: Engaging in work-related tasks.

- **Aggregation**:
  - Used MongoDB pipelines to group data by age and gender, then visualized the preferences.

#### Results

- **Findings** shows that:
  - Women generally prefer spending Friday nights with family or friends, while men are more inclined to work or stay in.
  - Younger users (18-24) of both genders prefer family time. In the 25-34 age group, men start to favor dining out or going out, whereas women continue to prefer family activities.
  - Users in the 35-50 age group of both genders show a preference for dining out or going out.

#### Implementation Details

1. **Data Preparation**: 
   - Filtered documents to ensure valid `sex` and `age` fields, and non-empty essays.

2. **Aggregation Pipelines**:
   - **Relationship Preferences**: Separate pipelines for romantic, casual, and mixed preferences.
   - **Weekend Activities**: Pipelines categorized by activities and age groups.

3. **Visualization**:
   - Used Matplotlib to create bar charts showing the distribution of weekend activity preferences by gender and age group.

### Analysis 4: Analysis of Habits and Relationships

#### Overview

This analysis aims to explore how user habits, as described in their essays (`essay2` and `essay6`), correlate with their relationship statuses. The focus is on understanding preferences related to:
- **Diet**
- **Drinks**
- **Smoking**

The analysis involves filtering and aggregating data based on these habits and examining their relationship with users' statuses. It includes keyword extraction from essays to identify preferences and their potential influence on relationship status.

#### 1. Diet Preferences

#### **Pipeline**:
      diet_pipeline_with_status = [
        {
            '$match': {
                'diet': {'$exists': True, '$ne': None, '$ne': '', '$ne': 'null'}
            }
        },
        {
            '$group': {
                '_id': {'diet': '$diet', 'status': '$status'},
                'count': {'$sum': 1}
            }
        }
    ]

### Observations and Important Insights

#### Observations

- **Dietary Flexibility**: 
  - Singles tend to prefer less restrictive dietary patterns compared to their married counterparts. Specifically, there is a higher proportion of singles who follow diets described as "anything" or "mostly anything" compared to married individuals.

- **Social Drinking**: 
  - A high prevalence of social drinking is observed among single individuals. This trend might be associated with social activities such as frequenting bars or restaurants or enjoying occasional drinks independently of a partner's preferences.

- **Health Focus**: 
  - Despite the trend towards social drinking, there is a notable number of nonsmoking singles. This suggests a potential focus on health among singles, with some choosing to avoid smoking even while engaging in social drinking.

#### Important Insights

- **Dietary Preferences**: Singles' flexibility in dietary preferences might reflect a lifestyle choice that aligns with social and individual habits rather than relationship constraints.

- **Social Behavior**: The correlation between single status and social drinking highlights how relationship status can influence social behaviors and preferences.

- **Health Trends**: The combination of social drinking and nonsmoking among singles indicates a complex relationship between social habits and health consciousness.

These observations offer a deeper understanding of how lifestyle choices related to diet, drinking, and smoking vary with relationship status, providing valuable insights into personal preferences and behaviors.

### Documentation

#### Python and Its Libraries
Documentation for Python programming and its libraries.
[Python Official Documentation](https://docs.python.org/3/)

#### MongoDB Documentation
Official documentation for MongoDB database management and querying.
[MongoDB Documentation](https://www.mongodb.com/docs/)

#### VS Code Documentation
Guides and documentation for Visual Studio Code.
[VS Code Documentation](https://code.visualstudio.com/docs)

#### NLP Libraries Documentation
Information on Natural Language Processing libraries.
[NLTK Documentation](https://www.nltk.org/)
[TextBlob Documentation](https://textblob.readthedocs.io/en/dev/)

#### Jupyter Notebook Documentation
Documentation for Jupyter Notebooks.
[Jupyter Documentation](https://jupyter.org/documentation)

#### Kaggle OKCupid Dataset Documentation
Documentation and details for the OKCupid dataset available on Kaggle.
[Kaggle OKCupid Dataset](https://www.kaggle.com/datasets/andrewmvd/okcupid-profiles)
