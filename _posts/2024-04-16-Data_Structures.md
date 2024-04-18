---
comments: true
layout: post
title: Data Structures Writeup Blog
description: Explanation and Preparation for CPT Collegeboard
type: plans
courses: {'compsci': {week: 28} }
---

# Python Model and SQlite Database

**Sqlite Database (items/points column relevant for my feature)**

- From VSCode using SQLite3 Editor, show your unique collection/table in database, display rows and columns in the table of the SQLite database.

![SQldatabase](https://files.catbox.moe/4dghqg.png)

*Important columns for my feature are the points and items column.*

**Database Initialization Code** 

- From VSCode model, show your unique code that was created to initialize table and create test data.

![BakingClass](https://files.catbox.moe/1amyo2.png)

*Defined a baking class that allows to create, read, update, and delete records in the table (changes in Points/Items when baking).*

![InitBakings](https://files.catbox.moe/70ly2a.png)

*Baking API initializes the database and populates the 'bakings' table with test data.*

![Data1](https://files.catbox.moe/qyvocb.png)

*Recipes for baked items defined in a dictionary*

![Data2](https://files.catbox.moe/ekc1rp.png)

*List of baked goods that corelate with recipe defined above*

![Data3](https://files.catbox.moe/8x0dxh.png)

*Instance to update items and points columns after new item is created*

**Lists and Dictionaries**

- Python API code and use of List and Dictionaries.

*As shown above, ingredients (stored in dictionary) and bakedgoods (stored in list) present in api code (bakings.py model file).*

- In VSCode using Debugger, show a list as extracted from database as Python objects.

- In VSCode use Debugger and list, show two distinct example examples of dictionaries, show Keys/Values using debugger.

**APIs and JSON**

- Python API code and use of Postman to request and respond with JSON.

- In VSCode, show Python API code definition for request and response using GET, POST, UPDATE methods. Discuss algorithmic condition used to direct request to appropriate Python method based on request method.

- In VSCode, show algorithmic conditions used to validate data on a POST condition.

![algo](https://files.catbox.moe/9obqr4.png)

*The BakingAPI class defines a Flask API endpoint with CRUD operations for managing baking recipes. The _CRUD inner class handles POST and GET requests. The POST method extracts recipe data from the request body, attempts to create a new recipe object, and returns its details if successful. If not, it returns an error message. The GET method retrieves all existing recipes from the database and returns them as a JSON response.*

- In Postman, show URL request and Body requirements for GET, POST, and UPDATE methods.

![postman](https://files.catbox.moe/98e00h.png)

![postman2](https://files.catbox.moe/lh8hlu.png)

*Get requests successfully show defined recipes and user data registered in api*

- In Postman, show the JSON response data for 200 success conditions on GET, POST, and UPDATE methods.

![200](https://files.catbox.moe/rgc3ky.png)

*User successfully authenticated*

- In Postman, show the JSON response for error for 400 when missing body on a POST request.

![400](https://files.catbox.moe/y87pc2.png)

*Missing user password therefore user can't be authenticated into account and play under FlayFusion*

- In Postman, show the JSON response for error for 403 when providing an unknown user ID to a UPDATE request.

![403](https://files.catbox.moe/ldwd2e.png)

*Unauthorized user forbidden to access information or perform update request*

**Frontend**

- JavaScript API fetch code and formatting code to display JSON.

![fetch](https://files.catbox.moe/antw64.png)

*Converts the response body to JSON format. Then, it initializes variables currentItems and currentPoints, iterates over each row of the JSON data, and updates these variables based on the row's uid. It also updates the lenIngredients variable based on the length of currentItems. Finally, it updates the localStorage with the parsed ownedItems array.*

- In Chrome inspect, show response of JSON objects from fetch of GET, POST, and UPDATE methods.

![jsonobjects](https://files.catbox.moe/giz5a0.png)

*Uses get request to update item/points, post request used for user specific actions* 

- In the Chrome browser, show a demo (GET) of obtaining an Array of JSON objects that are formatted into the browsers screen.

![demo](https://files.catbox.moe/jr6s8e.png)

*Drag and drop feature registers ingredient items in a list, baking sends this JSON data which is then outputted as a string when new item is created*

- In JavaScript code, describe fetch and method that obtained the Array of JSON objects.

![jsondump](https://files.catbox.moe/uhdq19.png)

*Fetches JSON data from a specified URL using the Fetch API. After retrieving the data, it iterates over each row, checks if the uid matches the one stored in localStorage, extracts the items and points, and updates the currentItems, currentPoints, and lenIngredients variables accordingly.*

- In JavaScript code, show code that performs iteration and formatting of data into HTML.

![iteration](https://files.catbox.moe/antw64.png)

*Iterates through each row in the data array, if there is a match between and recipe and item, it retrieves the items and points from that row. New item is appended* 

- In the Chrome browser, show a demo (POST or UPDATE) gathering and sending input and receiving a response that show update. Repeat this demo showing both success and failure.

![BakingClass](https://files.catbox.moe/1amyo2.png)

- In JavaScript code, show and describe code that handles success. Describe how code shows success to the user in the Chrome Browser screen.

![success](https://files.catbox.moe/8r42td.png)

*Success handled by converting JSON data into strings in which a loop determines wether a valid recipe is being made based on the list and dictionary above.*

- In JavaScript code, show and describe code that handles failure. Describe how the code shows failure to the user in the Chrome Browser screen.

![failure](https://files.catbox.moe/x71h35.png)

*Failure outputted to console.log, as seen in code above.*

**Optional/Extra, Algorithm Analysis**

In the ML projects, there is a great deal of algorithm analysis. Think about preparing data and predictions.

*Code from my triangle group Bakery ML Model Predictor and Titanic ML Model*

- Show algorithms and preparation of data for analysis. This includes cleaning, encoding, and one-hot encoding.

![prep](https://files.catbox.moe/jdjj9b.png)

*Filtered out csv file that contained data for predictions by removing it manually or through sql-lite commands like db.drop*

![titanic](https://files.catbox.moe/uy9phs.png)

*Encoding and one-hot encoding are applied to the 'sex' and 'alone' columns of the Titanic dataset. The 'sex' column contains categorical data with values 'male' and 'female'. It's encoded using a lambda function, mapping 'male' to 1 and 'female' to 0. Simple example of encoding categorical values into numerical representations (binary).*

*The 'embarked' column also contains categorical data representing the port of embarkation ('C', 'Q', 'S'). One-hot encoding creates binary columns for each category, indicating the presence (1) or absence (0) of each category. The resulting binary columns are concatenated with the original DataFrame after encoding, and the original 'embarked' column is dropped.*

- Show algorithms and preparation for predictions.

![predict](https://files.catbox.moe/rvt94l.png)

*The predict function takes a payload (a dictionary or JSON object containing features like time/date purchased, etc) as input and predicts an item based on these features using a logistic regression model. Makes prediction based off data stored in filtered csv file, converts payload through encoding categorical data, and uses pandas data frame in order to carry out process.*

- Discuss concepts and understanding of Linear Regression algorithms.

*Used in modeling the relationship between a dependent variable and one or more independent variables. Specifically, used in Titanic and Bakery ml models where we had to determine survival probability or item purchased from multiple factors.*

- Discuss concepts and understanding of Decision Tree analysis algorithms.

*Used for both classification and regression tasks that involve complicated data sets that can;t be solved based off of linear regression. Requires structured input and approach and may struggle with outliers. Especially helpful in titanic model which required a lot of similar data fields related to income and family.*