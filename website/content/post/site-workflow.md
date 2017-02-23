+++
comments = true
draft = true
share = true
slug = "site-workflow"
author = ""
menu = "Workflow"
tags = ["Hugo","Lightroom","github"]
image = ""
title = "My workflow for posts"
date = "2017-02-23"
+++

# How the site is updated

This will serve as my reference for future work.

## Step by step


### Prepare images in Lightroom
After doing the initial image adjustment I tag them such that they are included in my collection for web.
The selected images is exported in small and compressed format suitable for web.
The export is saved as a template with compressions settings and location within my local git working folder.

### Creating the post
In the hugo website folder I run `hugo new post/title-of-the-post.md` which create the html files. 
The first section in the md file is the frontmatter:

```js
+++
comments = true  
draft = false  
share = true
slug = "site-workflow"
author = ""
menu = "Workflow"
tags = ["Hugo","Lightroom","github"]
image = ""
title = "My workflow for posts"
date = "2017-02-23"
+++
```


If I want an image on top of the page I set `image = "images/photo.jpg"`

When adding images in the post I use `![image title](/images/ilustrate.jpg)`

When adding a block of code ?


### Reviewing the post
In a new terminal in folder website I run `hugo -D server`  
This will:
- generate the files to distribute 
- start a web server on http://localhost:1313/
- listen for changes in the files and regenerate so I can watch changes as I save edits

### Auto deploy
When the post is done I push my changes to the GitHub master branch.  
Then the server I use updates the web pages provided. This is done via a webhook that GitHub use to inform the web server that the branch has been updated.
I had great help in this article setting it up:  https://serversforhackers.com/video/automating-deployment-from-github

