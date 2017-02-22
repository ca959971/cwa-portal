## Introduction

Welcome to the CWA Erie Hack portal. This portal is developed by DigitalC for the purpose of storing and redirecting data for the
2017 Aquahacking event. This document gives a basic overview of different components of the portal and offer developers
basic instructions on how to manage and modify features in the portal.

## Module Overview

In a very high level, this application has three primary modules: Datasets, Toolkits, and Users.

### Users

Users is a pre-defined module
by MEAN.JS so you don't need to do a lot of changing to make sure that it is running smoothly. It is worth to mention user permissions
For Guest, they can only see the home page
For Signed-in users, they can only see and download the datasets
For admin, you can create, add, delete and update datasets.
As of now you need to change your account to admin manually in MongoDB database, in a collection called Users. The method you are
looking for is called FindOneAndUpdate, [Reference Here](https://docs.mongodb.com/v3.2/reference/method/db.collection.findOneAndUpdate/)


Few things to perhaps add:

* The "forgot password" feature did not work when I tested it locally, test it after deloyment to make sure it is functioning correctly
* CWA also requested a more comprehensive "Data Sharing Agreement" to be signed when user register. As of now I only put a phrase in that state the agreement,
check with CWA to make sure if the sharing-agreement as-is is okay or they need a pop-up and checkbox when user registers.
* Add ReCAPTHA to registration, to prevent bot traffic. [Tutorial](https://codeforgeek.com/2016/03/google-recaptcha-node-js-tutorial/)

### HomePage

Home page is already styled according to CWA standard, it is in the core folder of the project. You can find the styling at core.css. The only
thing to do:

* Modify the logo and favicon as CWA needs it.

### Datasets

Datasets have three views: the dataset list, the dataset view, and dataset creation view.

Things in general to do that still need finish:

* Update dataset with new files or delete existing files (maybe a dedicated dataset management interface)
* Delete dataset files when the dataset itself is deleted (completed, but bulk delete crashes the server)
* Some small UI bugs in the dataset creation page (sometimes error message does not show)
* Figure out a way to distinguish files with the same name.

####*Dataset List*

This is a list of datasets that are avaliable for the hack. I implemented an angular filter function on the left that searches and sort
data in real time. Reference list-datasets.client.controller.js and list-datasets.client-view.html for what I did specifically. Read
documentation[here](https://docs.angularjs.org/api/ng/filter/filter)for angular filter

This is the module where I did most of my work. The trick here is to implement some sort of data management structure where
files are being uploaded and stored in the backend server after users upload it. The way this is accomplished is to use a
AngularJS module called ng-file-upload in the front end and Node module called Multer in the back end to accomplish this task.

What I did was setting up an upload and download api using Multer in datasets.server.routes.js, and then use Angular routing to call the API in
datasets.client.controller.js. Remember that API calls in javascript is async, meaning that you need to do the variable assignment
in the callback.

Things to do here:

* For each dataset, for admin, add two buttons to remove and edit datasets
* Another that I haven't had time to figure out, is when filtering for category, I want to display a list of unique categories.
However, a dataset might have multiple categories, so we need a way to, in controller, look into each dataset and come up with a list
of unique categories. A workaround of the problem is to just manually define all the categories and not worry about it. Same apply for tags.


####*Dataset View*

This is the place where individual datasets are displayed. Nothing special here,
it is styled in a card-like fashion, with all information displayed. Things to do:

* Figure out a better way of styling the presentation of the files

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
