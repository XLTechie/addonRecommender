# Add-on Recommender
An NVDA add-on which recommends other add-ons based upon the applications a user runs.

This is more of an idea for an add-on, than an add-on itself.
If you are interested in the concept, or in contributing, please contact me.

## Design

As I envision it currently, this is intended to be a global plugin, which will:

* Ship with a list of available appModule add-ons.
    + Eventually I would like to convert this to drawing its data from an RSS feed or the like.
* Upon NVDA launch:
    + Examine the list of installed plugins.
    + For any appModule plugin which we know of but is not installed, create a stub appModule for the application in question.

### Stubs:

Each stub appModule will include the following elements:
* Some cleanup code that deletes this appModule if it some how got separated from the global plugin, and the global plugin is no longer installed. (Necessary? Possible?)
* A call to the reactToStub method provided by the main plugin, giving it the name of the add-on which relates to this application.

Somehow, these need to be kept from being visible in the add-on manager, because they really aren't add-ons, just hooks.
Currently, I imagine doing them as individual app modules, but if I can find a better way, I will.

### The reactToStub method

The reactToStub method does the following when it receives the name of an add-on:
1. Check whether the add-on is in the userIgnored list. If so, return.
2. Display a dialog stating that an add-on is available, and offer three options:
    * Get more information
    * Don't show this again for this add-on.
    * Close
3. If get more information was selected: browse to the add-on page on nvaccess.org.
4. If Don't show this again was selected: add this add-on to the userIgnored list.

## Ideas for future versions

* User option to display as toast notifications, instead of interrupting dialogs.
* Settings page to allow editing of the userIgnored list.
