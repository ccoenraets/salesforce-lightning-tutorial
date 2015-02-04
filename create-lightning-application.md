---
layout: module
title: Module 4&#58; Creating the Lightning Application
---

In this module, you create the QuickContacts Lightning Application and you use Bootstrap to define a basic layout for the application.

## What you will learn
- Create a Lightning Application in the Developer Console
- Use Static Resources in a Lightning Application
- Preview your Lightning Application in the browser


## Steps

1. In the Developer Console, click **File** > **New** > **Lightning Application**. Specify **QuickContacts** as the bundle name and click **Submit**

2. Implement the application as follows:

    ```
    <aura:application>

        <link href='/resource/bootstrap/' rel="stylesheet"/>

        <div class="navbar navbar-default navbar-static-top" role="navigation">
            <div class="container">
                <div class="navbar-header">
                    <a href="#" class="navbar-brand">Lightning Contacts</a>
                </div>
            </div>
        </div>

        <div class="container">
            <div class="row">
                <div class="col-sm-12">
                    Contact list goes here
                </div>
            </div>
        </div>

    </aura:application>
    ```

    ### Code Highlights:
    - The **link** tag references the bootstrap style sheet uploaded as a static resource in [module 2](setup-environment.html)
    - The application uses Bootstrap to implement a basic layout for the application
    - Lightning applications can include Lightning components and regular HTML markup

1. Click **File** > **Save** to save the file

1. Click **Preview** (upper right corner)

    ![](images/app-preview.jpg)

1.  Preview the application in the browser

    ![](images/app-layout.png)


<div class="row" style="margin-top:40px;">
<div class="col-sm-12">
<a href="create-apex-controller.html" class="btn btn-default"><i class="glyphicon glyphicon-chevron-left"></i> Previous</a>
<a href="create-contactlist-component.html" class="btn btn-default pull-right">Next <i class="glyphicon glyphicon-chevron-right"></i></a>
</div>
</div>
