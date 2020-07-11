---
toc: true
layout: post
description: A minimal example of using markdown with fastpages.
categories: [annotation]
title: All you need to know about CVAT
---
# All you need to know about CVAT

Why did we need the tool?
Why this tool?
How did we decide this tool? 
What to keep in mind while using this tool? 
How to backup the data in CVAT? 
How to import/export data in CVAT?

I will be covering different aspects that I considered while deciding the annotation tool that will be used by 2500 people in our company. 
1. Ease of Setup
2. Ease of usage
3. Bulk Data Extraction/Upload
4. Types of annotations supported
5. Ability to Scale
6. Backup and Restore
7. Technology stack
8. Community and Documentation

### Ease of Setup


A treat awaits in this section if you have worked with docker compose before, CVAT is very easy to setup as the source code contains necessary docker compose files which makes complete setup a breeze in your local. Repo also features an instruction documentation which is comprehensively written and covers every line of code that needs to be executed in order to get the tool running.  

Complete setup is nicely segregated into docker-compose files with docker apps named cvat,cvat_ui, cvat_db. 
There are two ways to go ahead with setting up the tool, the easier way of deploying it in a VM and a little longer way on Kubernetes. A VM with enough firepower to run an instance of Postgres, Django backend and a react app to support the number of users that you expect to access the tool simultaneously should be alright. An example: I was able to support 200+ users(some of them were automated scripts) in a single VM with the analytics component running using a Standard D5 v2 (16 vcpus, 56 GiB memory) Azure VM. The power of your VM needs to be proportionately increased if you wish to use the additional components like deep learning model based auto labelling. 
If you choose to deploy the tool in Kubernetes, you could benefit from the auto-scaling functionality for each app inside CVAT. Kubernetes YAML files are not available as part of source code and hence you might need to create them yourself. I recommend [Kompose](https://kompose.io) to create Kubrnetes YAML from docker compose files. 

### Ease of Usage

CVAT is developed considering the desktop based user interface, which means we need to keep expectations lower while trying to use it on mobile or tablets. The desktop UI although not fancy, is very feature rich and achieves the goal of labeling images and videos with ease.There's a long list of keyboard shortcuts supported, you don't necessarily need to remember every shortcut, simply pick and choose which help you speed up, I found the shortcut for creating shapes and rectangles for labelling to be very useful. Keyboard shortcuts combined with the feature rich app make labelling task smooth. The application also features a task assignment and task process flow using which larger teams can collaborate by assigning tasks to a specific user and updating the current status of task for others to see. 

### Data Extraction/ Upload

## Basic setup

Jekyll requires blog post files to be named according to the following format:

`YEAR-MONTH-DAY-filename.md`

Where `YEAR` is a four-digit number, `MONTH` and `DAY` are both two-digit numbers, and `filename` is whatever file name you choose, to remind yourself what this post is about. `.md` is the file extension for markdown files.

The first line of the file should start with a single hash character, then a space, then your title. This is how you create a "*level 1 heading*" in markdown. Then you can create level 2, 3, etc headings as you wish but repeating the hash character, such as you see in the line `## File names` above.

## Basic formatting

You can use *italics*, **bold**, `code font text`, and create [links](https://www.markdownguide.org/cheat-sheet/). Here's a footnote [^1]. Here's a horizontal rule:

---

## Lists

Here's a list:

- item 1
- item 2

And a numbered list:

1. item 1
1. item 2

## Boxes and stuff

> This is a quotation

{% include alert.html text="You can include alert boxes" %}

...and...

{% include info.html text="You can include info boxes" %}

## Images

![]({{ site.baseurl }}/images/logo.png "fast.ai's logo")

## Code

You can format text and code per usual 

General preformatted text:

    # Do a thing
    do_thing()

Python code and output:

```python
# Prints '2'
print(1+1)
```

    2

Formatting text as shell commands:

```shell
echo "hello world"
./some_script.sh --option "value"
wget https://example.com/cat_photo1.png
```

Formatting text as YAML:

```yaml
key: value
- another_key: "another value"
```


## Tables

| Column 1 | Column 2 |
|-|-|
| A thing | Another thing |


## Tweetcards

{% twitter https://twitter.com/jakevdp/status/1204765621767901185?s=20 %}


## Footnotes



[^1]: This is the footnote.
