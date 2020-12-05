---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "The Importance of Reproducible Code"
subtitle: ""
summary: "Lessons learned from the perspective of a newbie"
authors: [Sarah Berger]
tags: []
categories: []
date: 2020-11-30T19:34:08-05:00
lastmod: 2020-11-30T19:34:08-05:00
featured: false
draft: false
disable_comments: true

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---
Write my post here `a=1`

```r

#this is some r code

a = 2
b= 3
y = a+b
print(y)

```
That was some code


## The importance of reproducible code

Last year I was quickly thrown into the world of coding and statistics with R. I had taken some undergraduate statistics courses that involved using R, but all that really taught me how to do was copy and paste the instructor's code to complete an assignment. 

Google became my new best friend. My searches got more and more specific (see: "insert funny and specific google search here") and yet stackoverflow still seemed to have an answer!

While I was able to put out fires and stumble my way through an analysis, what I had in my file was a bit of a mess. Here are some sins I have learned to avoid:
1. I didn't comment anything
2. The script wasn't in order so I would have to run things line by line
3. I had no clear naming conventions and would end up working with dataframes called data_clean_3 (not knowing if there was a data_clean_4) and what that meant