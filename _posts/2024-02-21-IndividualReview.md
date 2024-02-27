---
toc: True
comments: True
layout: post 
title: Individual Review 
description: My CPT feature 
courses: {'compsci': {'week': 24}}
type: plans 
---

# Overview 

Our project is a web-based game that resembles Little Alchemy, a game where you drag icons and combine them to make new elements. **Let'M Cook**, our project, puts a spin on this by instead making baked goods like pastries, cakes, and sweets.  

## Components/Features

- Sandbox: Drag and drop from inventory into ‘oven’ for combining

- Baking: Fetch the recipe from the backend to create a dessert, add points for each recipe found

- Shop: Ingredient organization with opportunity to buy with gained points

- **Leaderboard: Displays user information and orders the users with most points to least points**

- Trading: Allows exchanging ingredients and recipes with friends

## My Feature

My feature is the leaderboard, which uses data from our users api and formats it into a table ranking the users from highest points to lowest points on the table. 

# Component A: Program Code Requirements

In your program, you must include student-developed program code that contains the following: 

**The user (including user actions that trigger events):**

![Shop](https://files.catbox.moe/c7z9hx.png)

- Buying items from the shop allows user to spend points, updating on leaderboard and database schema.

![Bake](https://files.catbox.moe/raurdi.png)

- Clicking the bake button allows user to gain points, updating on leaderboard and database schema.

**Use of at least one list (or other collection type) to represent a collection of data that is stored and used to manage program complexity and help fulfill the program’s purpose**

![userlist](https://files.catbox.moe/pvrmso.png)

- List of user data (name, id, points, etc...) stored in API

- Data fetched from backend to be displayed on leaderboard (Get request)

- Might need to right click and see image in new tab in order to see better...

**At least one procedure that contributes to the program’s intended purpose, where you have defined: ◆ the procedure’s name ◆ the return type (if necessary) ◆ one or more parameters.**

**An algorithm that includes sequencing, selection, and iteration that is in the body of the selected procedure**

![reorder](https://files.catbox.moe/lw5uyf.png)

Procedure uses an algorithm:

- Sequencing: We first sort the data by points in descending order and then clear the current leaderboard table.

- Iteration: We iterate through each user in the sorted data.

- Selection: Within the loop, we check if the user's points meet a certain condition (if they have at least 0 points).

- Sequencing: If the condition is met, we create table rows and cells for each user, populate them with the user's data, and append them to the leaderboard table.

**Calls to student developed procedure**

![call](https://files.catbox.moe/ccavc1.png)

- Initializes procedure and outputs a response if successful

**Instructions for output (tactile, audible, visual, or textual) based on input and program functionality**

![Leaderboard](https://files.catbox.moe/w6gjdi.png)

- Reorders based off points from highest to lowest as shown above.

| Collegeboard Requirements | Me |
|------------------|------------------|
| Instructions for input from one of the following: the user, a device, an online datas stream, a file.  | Our Project allows a user to bake items and purchase ingredients using the points they earned. They must click items in order to spend points and purchase items. Or they can arrange items into a recipe and click bake to gain points and purchase more items. |
| Use of at least one list (or other collection type) to represent a collection of data that is stored and used to manage program complexity and help fulfill the users purpose.  | An example of a collection of data that is stored is user data and points displayed on the leaderboard.|
| At least one procedure that contirubted to the program's intened purpose where you have defined: the name, return type, one or more parameters:  | My reorder leaderboard procedure performs the task of arranging the leaderboard from highest to lowest which is displayed accordingly. |
| An algorithm that includes sequencing, selection, and iteration that is in the body of the selected procedure  | This function shows the sequencing, selection, and iteration as explained above. |
| Calls to your student-developed prodcedure:  | Calls reorder leaderboard function to initialize the process. |

# Component B: Video 

| Collegboard Requirements | My Video |
|------------------|------------------|
| Input to program  | Seen in video, buying products with points from shop and baking items on bake page.  |
| At least one aspect of the functionality of your program| The Leaderboard functionality which reorders the users from highest to lowest points.  |
| Output produced by program:  | The Leaderboard properly displays all data and the users are arranged accordingly.  |
| My video does not have: | any distinguishing information and voice narration  |
| My video is | a .mp4, less than 1 minute in length, less than 30MB in file size.  |

[My Video](https://drive.google.com/file/d/1LSsSAj80p_kaRbLHACz2czgfi7KIzKXf/view?usp=sharing)

**Commits:**

[Frontend](https://github.com/trevorhuang1/lmc-frontend/commits?author=ad1tyad3sa1&since=2024-01-01&until=2024-02-01)

[Backend](https://github.com/trevorhuang1/lmc-backend/commits?author=ad1tyad3sa1)

[Pull Requests](https://github.com/trevorhuang1/lmc-frontend/pulls?q=is%3Apr+is%3Aclosed+author%3Aad1tyad3sa1)



