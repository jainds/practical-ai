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


## Ease of Setup


A treat awaits in this section if you have worked with docker compose before, CVAT is very easy to setup as the source code contains necessary docker compose files which makes complete setup a breeze in your local. Repo also features an instruction documentation which is comprehensively written and covers every line of code that needs to be executed in order to get the tool running.  

Complete setup is nicely segregated into docker-compose files with docker apps named cvat,cvat_ui, cvat_db. 
There are two ways to go ahead with setting up the tool, the easier way of deploying it in a VM and a little longer way on Kubernetes. A VM with enough firepower to run an instance of Postgres, Django backend and a react app to support the number of users that you expect to access the tool simultaneously should be alright. An example: I was able to support 200+ users(some of them were automated scripts) in a single VM with the analytics component running using a Standard D5 v2 (16 vcpus, 56 GiB memory) Azure VM. The power of your VM needs to be proportionately increased if you wish to use the additional components like deep learning model based auto labelling. 
If you choose to deploy the tool in Kubernetes, you could benefit from the auto-scaling functionality for each app inside CVAT. Kubernetes YAML files are not available as part of source code and hence you might need to create them yourself. I recommend [Kompose](https://kompose.io) to create Kubrnetes YAML from docker compose files. Scalability is an important aspect while considering a tool for production deployment. In order to make sure that the tool works for foreseeable growth in number of users. App can be scaled easily since everything is nicely wrapped into docker containers. 

## Ease of Usage

The application's desktop UI although not fancy, is very feature rich and achieves the goal of labeling images and videos with ease.There's a long list of keyboard shortcuts supported and you don't necessarily need to remember every shortcut, simply pick and choose which help you speed up. I found the shortcut to create poly shapes and rectangles during labelling as very useful. Keyboard shortcuts combined with the feature rich app make labelling task slick and smooth. The application also features a task assignment and task process flow using which larger teams can collaborate by assigning tasks to a specific user and updating the current status of task for others to see. CVAT is developed considering the desktop based user interface, which means we need to keep expectations lower while trying to use it on mobile or tablets. CVAT also features a command line interface which enables you to perform simple CRUD operations on task.

## Data Extraction/ Upload

A Django app in backend and react UI as frontend, CVAT is quite covered with options to upload data via UI or CLI. App works on a unique task based system, each upload is created as a task in the system. The task can then be further assigned to different users for labelling, quality check, etc. When using the UI to upload data, you don't need to worry about label formatting because the app takes care of it. CLI based upload requires data to be structured in specific formats before it can be processed. I recommend CLI to perform automated scripts based data upload and UI when actual human is performing the uplaod and labelling task. 

Extraction of data is a very important step which will have to be performed by every team on regular basis. CVAT supports extraction of data in a format by both interfaces i.e. UI and CLI. A user can go to a task and there's option to extract the data in various supported formats. when trying to extract multiple data points or tasks in CVAT, UI based extraction might seem time consuming . CLI comes to rescue here, extraction of data in any supported format is super simple using CLI. An important thing to note here is CVAT currently doesn't support bulk extraction or upload of data using UI.

The dev team also mentiond about datumaro dataset framework which can be used to transform, merge, extract multiple datasets from CVAT. I was not able to get it working and therefore no comments on that. 

## Annotations Format Supported

I am borrowing a table available in CVAT documentation to show the formats supported. It supports all major community defined data label formats. The labels covers the spectrum of classification, obejct detection and segmentation tasks in computer vision.


| Annotation format                                                                          | Import | Export |
| ------------------------------------------------------------------------------------------ | ------ | ------ |
| [CVAT for images](cvat/apps/documentation/xml_format.md#annotation)                        | X      | X      |
| [CVAT for a video](cvat/apps/documentation/xml_format.md#interpolation)                    | X      | X      |
| [Datumaro](datumaro/README.md)                                                             |        | X      |
| [PASCAL VOC](http://host.robots.ox.ac.uk/pascal/VOC/)                                      | X      | X      |
| Segmentation masks from [PASCAL VOC](http://host.robots.ox.ac.uk/pascal/VOC/)              | X      | X      |
| [YOLO](https://pjreddie.com/darknet/yolo/)                                                 | X      | X      |
| [MS COCO Object Detection](http://cocodataset.org/#format-data)                            | X      | X      |
| [TFrecord](https://www.tensorflow.org/tutorials/load_data/tf_records)                      | X      | X      |
| [MOT](https://motchallenge.net/)                                                           | X      | X      |
| [LabelMe 3.0](http://labelme.csail.mit.edu/Release3.0)                                     | X      | X      |

## Backup and Restore

All images/videos uploaded are stored in docker volume cvat_data and the respective label data is stored in postgres. Postgres data is stored in docker volume cvat_db. In order to backup the complete app data, you can simply create volume backup for these two volumes in form of .tar files. 
Configuring the said docker volumes to a persistent storage like S3 or azure blob would enable you to setup automated cloud backup for these volumes. 
Restoration is as simple as backup by using docker commands. 

## Community

CVAT community is available on github and gitter. I have personally found them responding faster on gitter compared to raising issues on github. 




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
