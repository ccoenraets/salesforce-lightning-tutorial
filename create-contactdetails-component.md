---
layout: module
title: Module 7&#58; Creating the Contact Details Component
---

## Step 1: Create the ContactDetails Component

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

## Step 4: Add Styles

1. Click **STYLE**

1. Add the following styles

    ```
    .THIS p {
        margin: 20px 0 2px 0;
    }

    .THIS h1 {
        margin: 0 0 10px 0;
    }

    .THIS h3 {
        margin: 4px 0;
    }
    ```

## Step 5: Add the ContactDetails Component to the Application

1. In the Developer Console, go back to the quickContacts application and add the contactDetails component:

    ```
    <div class="container">
        <div class="row">
            <div class="col-sm-4">
                <cc01:SearchBar/>
                <cc01:ContactList/>
            </div>
            <div class="col-sm-8">
                <cc01:ContactDetails/>
            </div>
        </div>
    </div>
    ```

1. Click **Update Preview** to run the application in the browser

    ![](images/app-v5.png)




<div class="row" style="margin-top:40px;">
<div class="col-sm-12">
<a href="create-searchbar-component.html" class="btn btn-default"><i class="glyphicon glyphicon-chevron-left"></i> Previous</a>
<a href="next.html" class="btn btn-default pull-right">Next <i class="glyphicon glyphicon-chevron-right"></i></a>
</div>
</div>
