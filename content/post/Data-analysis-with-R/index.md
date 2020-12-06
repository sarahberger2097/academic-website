---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "The Importance of Reproducible Code"
subtitle: ""
summary: ""
authors: []
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

After I started conducting data analysis in R, I quickly realized that making your code easily reproducible is one of the most important steps to improving your research workflow. Trust me, I learned some of these lessons the hard way. The major benefits of making your code easy to understand and easy to reproduce are:

* You can share code easily with others and they won’t be unable to run it or be completely lost 
* A few months down the line you can come back to your code and actually understand what the heck was going on
* You’re bound to make less errors
* It makes writing and reading code a much more pleasant experience 

##### My top tips for making your code readable and reproducible in RStudio: 


1. Start by creating an R project (.RProj file) in a new folder on your computer. This allows you to have a separate directory for each project you work on. You can then add your script and any files you might need into the folder with the RProj and have a simple working directory. Then when loading files into your code, you can use relative file paths. If you need to share the project, you can easily zip it and send it to someone else, and all the necessary files will already be in there (with no need to change the file paths)!

{{< figure src="new.project.png" >}}

2. I like to use RMarkdown for my scripts. With RMarkdown you can integrate code “chunks” with plain text, making it easy to organize and explain your code. You can also “knit” the document to create either a PDF or an html file. A great resource for understanding RMarkdown is this [cheat sheet](https://rstudio.com/wp-content/uploads/2015/02/rmarkdown-cheatsheet.pdf).

3. Make sure to load all packages at the top of your code. If you need to install the packages, make sure to delete or comment out that code.

{{< figure src="load.packages.png" >}}

4. Make sure your code runs in order. If you aren't sure if your code runs in order, clear your global environment and restart your session and see if the script runs as a whole. It can sometimes be tempting to test stuff out and run things line by line, but this will make it much harder for you or anyone else to reproduce. Another benefit to using RMarkdown is that your document won’t knit properly unless it can run altogether.

5. Add comments to your code. This will make it so much easier for others and future you to understand what you were doing. I like to split my code up into sections and add a general explanation of what I am doing and why at the beginning of each section. Then within the body of the code, I will use #comments to explain the individual steps. You don’t need to comment literally every line, but make sure to annotate what is not obvious. 

6. Try to make the names of your objects informative and intuitive. It's also best not to make them too similar to each other in case you mix them up. For example having two tables called `data_clean` and `data_cleaner` will probably lead to some confusion. 

These are just some tips that I've found useful, but make sure to do what works for you! Good luck and happy coding :smile: 
