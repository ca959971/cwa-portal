## Introduction

Welcome to the CWA Erie Hack portal. This portal is developed by DigitalC for the purpose of storing and redirecting data for the
2017 Erie Hack event. This document gives a basic overview of different components of the portal and offer developers
basic instructions on how to manage and modify features in the portal.

## Module Overview

In a very high level, this application has three primary modules: Datasets, Toolkits, and Users.

### Users

For Guest, they can only see the home page
For Signed-in users, they can only see and download the datasets
For admin, you can create, add, delete and update datasets.




### Datasets

Datasets have three views: the dataset list, the dataset view, and dataset creation view.


####*Dataset List*

This is a list of datasets that are avaliable for the hack. I implemented an angular filter function on the left that searches and sort
data in real time. Reference list-datasets.client.controller.js and list-datasets.client-view.html for what I did specifically. Read
documentation[here](https://docs.angularjs.org/api/ng/filter/filter)for angular filter




####*Dataset View*

This is the place where individual datasets are displayed. Nothing special here,
it is styled in a card-like fashion, with all information displayed. Things to do:


####*Dataset Creation*

This is the place where datasets are created. The page links to the Angular front end for uploading. It is not perfect,
but functioning. Few things to do here:

####*Dataset Update*

This is the same as the dataset creation page, default of Yo generated modules. However, right now you can't update or delete files
already uploaded. You have to delete the entire dataset to do it. Few things to do:

* You can create an entirely new layout for the page, that offers a file management system. But conceptually it is pretty complex
since you need to interact with the File data model. You can choose to keep it as is since users won't be able to see it.

####Toolkit

This is the module that is newly constructed per request of CWA. The gist of the idea is that it can serve as a place for participants
to find tools available to them. The structure is similar to that of dataset, but much simplier (used Yo generator Module generation function)

##Deployment and Maintance

The project is version controlled and shared on Github. You can reach it at[here](https://github.com/su20yu1919/cwa-data-portal)
