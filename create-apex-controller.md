---
layout: module
title: Module 3&#58; Creating the ContactController Class
---

Lightning applications make it easy to work with data. In this module, you create an Apex controller that allows your Lightning application to retrieve contacts, or to search contacts by name or by id.

## What you will learn
- Create an Apex Controller that exposes data and logic to the client application


## Steps

1. In Salesforce, click your name in the upper right corner of the screen. In the dropdown menu, click **Developer Console**.

    ![](images/devconsole.jpg)

1. In the Developer Console, click **File** > **New** > **Apex Class**. Specify **ContactController** as the class name and click **OK**.

2. Implement the class as follows:

    ```java
    public with sharing class ContactController {

        @AuraEnabled
        public static List<Contact> findAll() {
            return [SELECT id, name, phone FROM Contact LIMIT 50];
        }

        @AuraEnabled
        public static List<Contact> findByName(String searchKey) {
            String name = '%' + searchKey + '%';
            return [SELECT id, name, phone FROM Contact WHERE name LIKE :name LIMIT 50];
        }

        @AuraEnabled
        public static Contact findById(String contactId) {
            return [SELECT id, name, title, phone, mobilephone, Account.Name
                        FROM Contact WHERE Id = :contactId];
        }


    }
    ```


    ### Code Highlights:
    - **ContactController** is a regular controller class with methods to retrieve contacts (findAll),  or to search contacts by name (findByName) or by id (findById).
    - The **@AuraEnabled** method annotation makes a method available to Lightning applications

1. Click **File** > **Save** to save the file


<div class="row" style="margin-top:40px;">
<div class="col-sm-12">
<a href="setup-environment.html" class="btn btn-default"><i class="glyphicon glyphicon-chevron-left"></i> Previous</a>
<a href="create-lightning-application.html" class="btn btn-default pull-right">Next <i class="glyphicon glyphicon-chevron-right"></i></a>
</div>
</div>
