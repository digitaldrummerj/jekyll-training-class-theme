---
layout: classes-page
title: About
permalink: /about/
---

This is the base Jekyll theme for running workshops/classes.  This theme uses collections for the workshops/classes.  
  

Features:

* Sidebar with list of labs  
* Next/Previous Lab Navigation
* Grouping of Lab Types in Sidebar
* Dynamic generation of navigation based on collection and yaml
* Dynamic pulling in of workshop/classes logo if present 
* Footer at bottom of screen
* Github and Twitter Links
* Todo List that shows when running local to keep track of notes on things for the maintainer to complete
* Ability to run with test site configuration that shows warning that it is the test site and where to find the real site.
* Google Analytics
* Sitemap


Github Repository at [https://github.com/digitaldrummerj/jekyll-training-class-theme](https://github.com/digitaldrummerj/jekyll-training-class-theme)


Theme written by Justin James, [http://digitaldrummerj.me](http://digitaldrummerj.me)


## Running Theme

```bash
$ jekyll serve
```

**Options**

* --incremental -> only build changed pages.  Huge speed increase but doesn't rebuild list of labs
* -o -> open web browser after serve done
* --config _config.yml,_config-local.yml -> build configuration starting with _config.yml

## Adding a New Class


1. In the _classes class add a new folder named after workshop/class
1. In the new workshop/class folder you created, add a new file that will be the home page for the class.  I like to name my home file `00-[Class Name].md` (e.g. 00-ionic.md for an ionic class).  This make it easy to find the home page as you add more files
1. In the `00-[Class Name].md` file add the following Front Matter (FML)

	```
	---
	title: 'Ionic Workshop'
	published: true
	layout: classes-post
	permalink: '/ionic/index'
	type: ionic
	lab: ionic
	ishome: true
	date: 2016-05-22
	excerpt: |
	---
	```

1. In the FML, update the title, permalink, type, lab, and date.  The type and lab can be anything you want (no spaces allowed).
1. Once you write the home page information, you will want to fill in the `excerpt` .  The excerpt needs to be indented to be valid FML.

### Adding New Lab to Class

1. In the workshop/class folder, add a new file and give it an informative name.  I normally start the file name with the lab number just to make it easy to find the right lab file once there are a bunch of labs.
1. In the new file, add the following FML.

	```
	---
	title: ''
	published: true
	type: ionic
	layout: classes-post
	order: 10
	lab: ionic
	length: 20 minutes
	date: 2016-05-16
	---
	```

1. Update the title with the lab name.  I normally start the labs title with `Lab ##:` e.g. Lab 13:
1. Update the type and lab to match the type you used in the class home page 
1. Update the order with the lab number
1. Update the date with the current date.  This will show on the lab as the last revised date
1. Once the lab is written update the length with how long you will think it should take for the lab

### Add a new Extra Lab Page

1. Follow the same instructions as the "Adding New Lab to Class" section but change the type to `[Class Type]extra` e.g. `ionicextra`

### Add Overview Page

1. Follow the same instructions as the "Adding New Lab to Class" section but change the type to `[Class Type]overview` e.g. `ionicoverview`

### Adding Table of Contents to Lab

Wherever you want the Table of Contents add the following bit of markdown.  

```
* TOC
{:toc}
```

>All headers in the file with be added to the table of contents.  

### Remove Headings from the Table of Contents

There are times where you do not want the heading to show up in the table of contents.  There is technically not a way to restrict this but you can fake it by creating a CSS class that matches the styles of the H2 header and use that instead of making the text a real header.

For example to make the "Table of Contents" looks like an H2 header without actually being one, use the following.

```
{:.fake-h2}
Table of Contents
``` 

### Ordering Labs

The order of the labs is controller by the type and order FML.

### Adding a Todo

There is the ability to add a TODO list that only shows up when running locally or when the testsite value is not set in the jekyll config.

To add a TODO it is done through FML by adding a todo attribute

```
todo: |
	* 1st todo
	* 2nd todo
```	

### Adding Images to labs

I don't like typing the image paths over and over again so instead I define a variable at the top of the file with image directory location

	{% raw %}
	{% assign imagedir = "../images/[Dir Name]/" %}
	{% endraw %}

Then to use the imagedir variable to add the imagedir path to the image file name, we prepend the imagedir to the image file name.

```
![Alt Tag]({{"filename.png" | prepend: imagedir }})
```