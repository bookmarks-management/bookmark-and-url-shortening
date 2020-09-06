# Bookmark and URL shortening
## Problem statement

Any organization will have several digital components across various platform(like micro services, widgets, documentations, monitoring dashboards etc).

The easiest way to have the references of all these components is through bookmarks. 
However, bookmarks has to be imported and exported inorder to share it with any one like a new joiner. 
In bookmarks, **you cannot detail more about what these bookmarks** are about by providing additional information through short description or an image(s) or customized icons(s).

Even if you try to centralize it by exporting them and storing in a repository, **every time team need to re-import** those bookmarks from the centralized repository
to get update on changed or added or removed URL(s). 
It also becomes complex when you already have bookmarks and then **importing could result in overlapping**.

**It also becomes hard when we want to share many such lengthy urls** such as kibana dashboard urls. 
A shorter url will become easy to share in this case.

## Requirements and goals

### Functional requirements
* User should generate short URLs which will expire after a standard default time span. 
* User should also be able to specify the expiration date. 

_By above these two, we can solve the problem of generating tiny URLs quickly and sharing it with others_

* User should be able to create cards representing the url where each card has a short title, brief description and a customizable picture. 
* Default picture would be the favicon of the serving application. A sample pen sketch is as below:

![Card](/images.png)

* User should be able to group cards in terms of tribes, feature teams, platforms or application. This would be like a catalog. User should be able to share the group urls.
A sample pen sketch is as below:

![Group cards](/imagesp-cards.png)

* Each card should be a short url with the re-direction to the original url. 
This short url will have **no expiration as it belongs to a group**.
The generation of this short **url should be dynamic and unique and could carry some contextual information too**.

_For example:_ Let us imagine we have a URL


> http://someapp:5601/app/kibana#/dashboard/target_new_prod_dashboard?_g=(refreshInterval:(display:Off,pause:!f,value:0),time:(from:now-7d,mode:quick,to:now))&_a=(filters:!(),options:(darkTheme:!f),panels:!((col:1,id:ogn-data-received-vs-ogn-data-saved,panelIndex:1,row:1,size_x:5,size_y:4,type:visualization),(col:1,id:missing-ogn-information,panelIndex:2,row:5,size_x:5,size_y:5,type:visualization),(col:6,id:distribution-of-new-production-types,panelIndex:3,row:1,size_x:4,size_y:8,type:visualization)),query:(query_string:(analyze_wildcard:!t,query:'*')),title:target_new_prod_dashboard,uiState:())

Group Context | Example
------------- | -------------
None | http://tiny/klsjd73
User | http://{user-name}/klsjd73
Tribe | http://{tribe-name}/klsjd73
platform\application | http://{ft-name}/klsjd73

* The creator of the group will be the admin(role) user after which s\he will be able to add one or more admin user who would have authority to make changes. 
Only admin user(s) can remove a user from admin role. 
At any point of time there must be at least one admin user for the group.
* Admin user(s) of the group should be able to authorize a card to be displayed on the group, make changes like updating or deleting card(s).
Unless the admin user approves the card or its changes, it will not be displayed on the group page.
* A normal user i.e. not an admin user can suggest changes to an existing card. 
The changes are to be queued in order to be approved by the group's admin user(s).
* User should be able to share the group page enlisting all the cards of that group
* Admin user(s) should be able to import or export

### Non-functional requirements

* The system should be highly available. This is required because, if our service is down, all the URL redirections will start failing.
* URL's redirection should happen in real-time with minimal latency.
* Shortened links i.e. klsjd73 should not be guessable (not predictable).
* System should be maintainable, easy to adapt any new changes.
* Try to use the concept of [web components](https://www.webcomponents.org/introduction) or widgets. 
The cards need to be re-usable and support multiple browser with any underlying library or framework i.e. we can take the card\group and embed in an application or platform.
* All the behaviours needs to be exposed as RESTful api's with open api specification documentation which can be tried with "Try out" in order to try out the api's.
* **We strongly recommend you to set-up [CI\CD](https://engineering-stream-hackathon.github.io/challenge/#/?id=cicd) right from the beginning of the project.**

### Extended requirements

* Metrics: _Example:_ how many times a redirection happened? How many users are using your group ? etc...
* Our service should also be accessible through REST APIs by other services.
* If you have any other ideas or features that could add more business value (optional).

## Technology stack

* Backend
  * Language: Java (AdoptOpenJDK 11 and above)
  * Framework: Spring, spring-boot, spring-cloud
* Frontend
  * Typescript
  * Framework: React
* Database
  * PostgreSQL
    
