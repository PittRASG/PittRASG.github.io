# How to update the PittRASG website


## Getting Started
The PittRASG website is built with Jekyll where new pages can be written in HTML, Markdown or both. In short, Jekyll is a static website generator that turns our files into a complete website. More information about Jekyll can be found here: https://jekyllrb.com/

## Prerequisites
To get started you first have to have Jekyll installed. If you are on a Mac you can use the following command:

```
$ gem install bundler jekyll
```

For Linux:
https://jekyllrb.com/docs/installation/other-linux/

For Windows:
https://jekyllrb.com/docs/installation/windows/

The process to install Jekyll for windows is a little complicated and if you don't want to go through it, you can just update the website on your laptop and instead of previewing it on your local machine, you can directly push it to Github and view the changes there. 

In order to clone the website to your local machine, follow the instructions below:
```
$ git clone https://github.com/PittRASG/PittRASG.github.io.git
$ cd PittRASG
$ bundle install
$ bundle exec jekyll serve
```

The website is then served at http://localhost:4000/ , where you can preview it before pushing to Github. You may have to refresh a couple times. 

## Directory Structure

In this section, I am going to over the most important folders that you may want to change. Feel free to explore the other folders, if there is something specific that you want to change. I wrote most of the pages in HTML, because that is what I am most comfortable with, but pages can also be written in Markdown.

### _pages
The **_page** folder contains the list of pages written in Markdown that represent the pages in the navbar (navigation bar). In this case, we have the about page (about.md), projects page (projects.md), software page (software.md), teams page (team.md).

The projects.md and sofware.md pages are responsible for display a list of projects and software respectively. Therefore, they do not need to be changed. In order to create an entry for your project, you would create a new file inside the **_projects** folder and the projects.md file automatically knows to display it. Similarly, to create an entry about software tools that you are developing, you would create it inside the **_software** folder.

The team.md page is a page that contains information about the people in the group. I have already structured it and included placeholders and you just have to change your name, image and description. Moreover, if you would like to include a photo, place it inside the **assets/img** folder.

### _posts
The **_posts** folder contains files, each representing a post. If you would like to create a new post, just create a new file inside this folder and it will be automatically be displayed inside the blogs page. Feel free to copy paste existing files as a starter file. 

### _projects
The **_projects** folder contains project files. In order to create an entry about your project, create a new file in this folder and it is automatically displayed in the projects page. Feel free to copy paste exisiting files in the folder as a starter for your own. Then, you just have to change the content.

### _software
The **_software** folder works in the same way as the **_projects** folder. Refer back to that section. 

## Pushing your changes

Once you are finished, you can push your changes to Github with the following commands:

```
$ git add .
$ git commit -m "Description about your changes"
$ git push origin master
```

Then, you can view your changes in http://pittrasg.github.io/ 
