# dorado-blog

> A simple Blog

<!-- Scope Limitations
We are just interested in the frontend part, skip any kind of persistent data storage or backend components you'd normally need
Skip authentication / login etc this is not required
Layout / Visual should be functional for the requirements but no need to make it fancy with gfx, focus should be the code and structure of the project setup
Content editing / additions don't need to be persistent, you can just keep them in memory until page reload.

Requirements
General
Make sure your code is clean, well structured and easily understood and extendable by other developers.

Technical
Your implementation needs to utilize the Vue.js framework (you can choose v1 or v2 of the framework to your liking)
The layout styling needs to be done in vanilla CSS, don't use a ready framework / library like bootstrap (SASS / LESS other css pre-compilers are fine if you prefer)
As data source and structure use this http://files.doradogames.com/6b3e864a0ac7 JSON sample, we will pretend it's fetched via a backend API call, so you can load it like a file


Functional
Show a generic list of articles with headers and summary (use the first 100 chars of the text as summary) as the start page
Add a filter to the generic list that allows the user to filter the articles by category (BONUS: add a free text filter as well that filters the summary)
Clicking on an article should show details of the article with full description and comments if there are any
Add a comment form to the detail view that adds new comments to the selected article in memory and shows it if you recall the details (without browser refresh, persistency is NOT required) -->

## Build Setup

```bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```

For detailed explanation on how things work, consult the [docs for vue-loader](http://vuejs.github.io/vue-loader).
