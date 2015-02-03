---
layout: module
title: Module 6&#58; Creating the Search Bar Component
---

In this module, you add a SearchBar to allow the user to search contacts by name. You could add the SearchBar to the contactList component, but that would limit the reusability of the component: depending on specific UI requirements, you may want the SearchBar to be directly on top of the list (like you'll do here), integrated in the header, or somewhere else. You also want the ContactList component to display a list of contacts independently of the type of SearchBar you use: regular input field with search button, type ahead search, etc. For these reasons, it is a good idea to decouple the search UI, from the display UI, and create two components: ContactList and SearchBar.

## What you will learn:

- Create custom events
- Communicate between components using events

## Step 1: Create a Custom Event:

Now that we decided to build the SearchBar and the ContactList as two separate components, we need a way for the ContactList to know when the search key changes so that it can retrieve and display the matching contacts. Events enable that kind of communication between components. In this step, you create an event used by the SearchBar component to notify other components when the search key changes.

1. In the Developer Console, click **File** > **New** > **Lightning Event**. Specify **SearchKeyChange** as the bundle name and click **Submit**

1. Implement the event as follows:

    ```
    <aura:event type="APPLICATION">
        <aura:attribute name="searchKey" type="String"/>
    </aura:event>
    ```
    ### Code Highlights:
    - The event holds one argument: the new searchKey


## Step 2: Create the Component

1. In the Developer Console, click **File** > **New** > **Lightning Component**. Specify **SearchBar** as the bundle name and click **Submit**

2. Implement the component as follows:

    ```
    <aura:component>

        <input type="text" class="form-control" onkeyup="{!c.searchKeyChange}"
                placeholder="Search"/>

    </aura:component>
    ```
    ### Code Highlights:
    - This is a very simple component with a single input field.
    - When the user types in a character (**onkeyup**), the **searchKeyChange** function is executed in the component's controller (you'll code that function in the next step).


1. Click **File** > **Save** to save the file


## Step 3: Implement the Controller

1. Click **CONTROLLER**

1. Implement the Controller as follows:

    ```
    ({
        searchKeyChange: function(component, event, helper) {
            var myEvent = $A.get("e.cc01:SearchKeyChange");
            myEvent.setParams({ "searchKey": event.target.value});
            myEvent.fire();
        }
    })
    ```
    ### Code Highlights:
    - First, we get an instance of the SearchKeyChange Event
    - Then, we set the event's searchKey parameter to the current value in the input field
    - Finally, we fire the event so that registered listeners can catch it


## Step 4: Listen for the SearchKeyChange Event in ContactList

1. In the Developer Console, go back to the ContactList component

1. Add a handler for the SearchKeyChange event (right after the init handler):

    ```
    <aura:handler event="cc01:SearchKeyChange" action="{!c.searchKeyChange}"/>
    ```

1. Click **CONTROLLER**

1. Add the searchKeyChange function implemented as follows:

    ```
    searchKeyChange: function(component, event, helper) {
        helper.findByName(component, event.getParam("searchKey"));
    }
    ```

    > Make sure you separate the doInit and the searchKeyChange functions by a comma.

1. Click **HELPER**

1. Add the **findByName** function implemented as follows:

    ```
	findByName : function(component, searchKey) {
        var action = component.get("c.findByName");
        action.setParams({
          "searchKey": searchKey
        });
        action.setCallback(this, function(a) {
        	component.set("v.contacts", a.getReturnValue());
        });
        $A.enqueueAction(action);
	}
    ```

## Step 5: Add SearchBar to the Application

1. In the developer console, go back to the QuickContacts application and add the SearchBar component.

    ```
    <div class="container">
        <div class="row">
            <div class="col-sm-12">
                <cc01:searchBar/>
                <cc01:contactList/>
            </div>
        </div>
    </div>
    ```

1. Click **Update Preview** to run the application in the browser

    ![](images/app-v4.png)

<div class="row" style="margin-top:40px;">
<div class="col-sm-12">
<a href="create-contactlist-component.html" class="btn btn-default"><i class="glyphicon glyphicon-chevron-left"></i> Previous</a>
<a href="create-contactdetails-component.html" class="btn btn-default pull-right">Next <i class="glyphicon glyphicon-chevron-right"></i></a>
</div>
</div>
