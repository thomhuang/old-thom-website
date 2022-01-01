---
layout: page
title:  Recipe-App
description:  An application programmed in Python geared towards the home cook. Our app works to retrieve data from www.SeriousEats.com and utilize the information to query recipes containing specific ingredients/authors/cuisines/etc. directly to the user.
---
<style>
.center {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 50%;
}
</style>

<a href="https://www.github.com/thomhuang/recipe-app/" target="_blank">Recipe-App</a> is an application programmed in Python geared towards the home cook. Often times, home cooks have trouble finding recipes, not to mention those that work with what they have in their pantry and this hopefully solves this issue. Thus, our app works to retrieve data from www.SeriousEats.com and utilize the information to query recipes containing specific ingredients/authors/cuisines/etc. directly to the user.

It is created using `scrapy`, `pandas`, `SQLite3`, and `PyQt5`.

Below are images with explanations of each aspect of the application:

<img src="/assets/images/recipe_app_prompt.jpg" class="center">

This is the initial window, where the user can choose between various categories to search for.

<img src="/assets/images/recipe_app_search.jpg" class="center">

This is the window that is shown if you search `pizza` under the `Recipe Title` category. It displays all the recipes contained in the database that cotain the word `pizza` in their title.

<img src="/assets/images/recipe_app_info.jpg" class="center">

Lastly, this is all the scraped information of the recipe displayed according to the made GUI, where you can redirect to other recipes that have similar `tags`.



