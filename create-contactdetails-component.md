---
layout: module
title: Module 7&#58; Creating the Contact Details Component
---

## Step 1: Create a custom event:

1. In the Developer Console, click **File** > **New** > **Lightning Component**. Specify **ContactDetails** as the bundle name and click **Submit**

1. Implement the component as follows:

    ```
    <aura:component controller="cc01.ContactController">

        <aura:handler event="aura:locationChange" action="{!c.locationChange}"/>
        <aura:attribute name="contact" type="Contact" default="{'sobjectType': 'Contact'}"/>

        <div class="details">
            <h1>{! v.contact.Name }</h1>
            <h3>{! v.contact.Account.Name }</h3>
            <h3>{! v.contact.Title }</h3>
            <p>{! v.contact.Phone }</p>
            {! v.contact.MobilePhone }
        </div>

    </aura:component>
    ```

1. Click **File** > **Save** to save the file


## Step 2: Implement the Controller

1. Click **CONTROLLER**


1. Implement the Controller as follows:

    ```
    ({
        locationChange : function(component, event, helper) {
            var token = event.getParam("token");
            if (token.indexOf('contact/') === 0) {
                var contactId = token.substr(token.indexOf('/') +1);
                helper.findById(component, contactId);
            }
        }
    })
    ```

## Step 3: Implement the Helper

1. Click **HELPER**

1. Implement the helper as follows:

    ```
    ({
        findById : function(component, contactId) {
            var action = component.get("c.findById");
            action.setParams({
              "contactId": contactId
            });
            action.setCallback(this, function(a) {
                component.set("v.contact", a.getReturnValue());
            });
            $A.enqueueAction(action);
        }
    })
    ```

## Step 4: Add the contactDetails Component to the Application

1. In the Developer Console, go back to the quickContacts application and add the contactDetails component:

    ```
    <div class="container">
        <div class="row">
            <div class="col-sm-4">
                <cc01:searchBar/>
                <cc01:contactList/>
            </div>
            <div class="col-sm-8">
                Details
            </div>
        </div>
    </div>
    ```

1. Click **Update Preview** to run the application in the browser


<div class="row" style="margin-top:40px;">
<div class="col-sm-12">
<a href="Creating-the-Application.html" class="btn btn-default"><i class="glyphicon glyphicon-chevron-left"></i> Previous</a>
<a href="Accessing-Data-using-SOQL-and-DML.html" class="btn btn-default pull-right">Next <i class="glyphicon glyphicon-chevron-right"></i></a>
</div>
</div>
