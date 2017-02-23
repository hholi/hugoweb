+++
comments = true
draft = false
share = true
slug = "site-workflow"
author = ""
menu = "main"
tags = ["Hugo","Lightroom","github", "deploy"]
image = ""
title = "My workflow for posts"
date = "2017-02-23"
+++

# How the site is updated

Here I describe the steps to get a new post on the site.
This will serve as my reference for future work.


### Prepare images in Lightroom
After doing the initial image adjustment I tag them such that they are included in my collection for web.
The selected images is exported in smaller dimension and compressed format suitable for the web.
The export is saved as a template with image processing settings and export location within my local git working folder. The location is `website/static/images`.

### Creating the post
In the hugo website folder I run `hugo new post/title-of-the-post.md` which create the html files. 
The first section in the md file is the frontmatter with the post metadata:

```js
+++
comments = true  
draft = true  
share = true
slug = ""
author = ""
menu = ""
tags = ["tag1", "tag2"]
image = ""
title = "title of the post"
date = "2017-02-23"
+++
```


If I want an image on top of the page I set `image = "images/photo.jpg"`

When adding images in the post I use `![image title](/images/ilustrate.jpg)`



### Reviewing the post
In a new terminal in folder website I run `hugo -D server`  
This will:
- generate the files to distribute, including drafts
- start a web server on http://localhost:1313/
- listen for changes in the files and regenerate so I can watch changes as I save edits

### Auto deploy
When the post is done I push my changes to the GitHub master branch.  
Then the server I use updates the web pages provided. This is done via a webhook that GitHub use to inform the web server that the branch has been updated.
I had great help in this article setting it up:  https://serversforhackers.com/video/automating-deployment-from-github

