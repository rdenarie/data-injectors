**eXo data-injectors**
==========================

A **data injectors** for eXo that allows administrators to inject content types
 such as: social (users, connections, spaces, membership),forum (post, topic), wiki (wiki page), ecms (pdf, doc, xls,... document), FAQ(category,questions,answers..)


**How to inject:**
----------------------
  
All the injection commands were designed to be invoked via rest service.
The service is named "org.exoplatform.services.bench.DataInjectorService" 
and registered normally to portal container as general component

The format of request link is:
**http://{domain}/{rest}/private/bench/{inject\|reject}/{type}?\[params\]**

So, simply:

1: login to the PLF first 

2: call rest services


 SOCIAL Inject:
-------------------
Users use RESTful service to request to inject or reject data.

We will describe how to use data injectors in eXo Social

**_inject identity:_**

  http://localhost:8080/rest/private/bench/inject/identity?pattern=0000&number=100&prefix=abc
  
===> identity injected successfully!!!
* This call will generate 100 users with prefix=abc
 
**_inject space:_**

  http://localhost:8080/rest/private/bench/inject/space?number=10&fromUser=1000&toUser=1009
  
===> space injected successfully!!!
* This call will generate 10 spaces for each users in the range 1000 - 1009 = 100 spaces
Each user in the range will be the owner (manager) of the space.


**_inject membership:_**

http://localhost:8080/rest/private/bench/inject/membership?type=member&fromUser=100&toUser=120&userPrefix=bench.user&fromSpace=10&toSpace=20&spacePrefix=bench.space
===> membership injected successfully!!!
* This call will add each users in the range 100 - 120 = 20 users to be member for each space in range 10 - 20 = 10 spaces with prefix.

**_inject activity:_**

** for user :

http://localhost:8080/rest/private/bench/inject/activity?number=2&fromUser=0000&toUser=0019&type=user&userPrefix=abc

===> activity injected successfully!!!
 * This call will generate 50 activities for each users in the range 0000 - 0019 = 40 activities
  
** for space :

  http://localhost:8080/rest/private/bench/inject/activity?number=5&fromUser=0010&toUser=0049&type=space&userPrefix=abc&spacePrefix=space

===> activity injected successfully!!!
 * This call will generate 5 activities for each spaces in the range 0010 - 0049 = 200 activities
  
**_inject activity mention:_**

  http://localhost:8080/rest/private/bench/inject/mentioner?number=2&fromUser=0020&toUser=0030&mentioner=abc0050&userPrefix=abc
  
===> mentioner injected successfully!!!

**_inject relationship:_**

 http://localhost:8080/rest/private/bench/inject/relationship?number=19&fromUser=5100&toUser=5119&type=user
* This call will generate 19 relations for each users in the range 5100 - 5119


**FORUM Inject:**
--------------------
We will describe how to use data injectors in eXo Forum

**_inject profile:_**
 http://localhost:8080/rest/private/bench/inject/forumProfile?number=100&prefix=abc.user

===> forumProfile injected successfully!!!
* This call will generate 100 users

**_inject category:_**

 http://localhost:8080/rest/private/bench/inject/forumCategory?number=10&fromUser=1000&toUser=1009

===> forumCategory injected successfully!!!
* This call will generate 10 categories for each users in the range 1000 - 1009 = 100 categories.

**_inject forum:_**

 http://localhost:8080/rest/private/bench/inject/forumForum?number=4&toCat=15&catPrefix=abc.cat&forumPrefix=abc.forum
 
===> forumForum injected successfully!!!
* This call will generate 4 forums for category at 15 position = 4 forums.

**_inject topic:_**

 http://localhost:8080/rest/private/bench/inject/forumTopic?number=10&topicPrefix=abc.topic&fromUser=1000&toUser=1009&userPrefix=abc.user&toForum=19&forumPrefix=abc.forum

===> forumTopic injected successfully!!!
* This call will generate 10 topics for each users in the range 1000 - 1009 into to forum at 19 position = 10(topics) x 10(users) x 1 = 100 topics

**_inject post:_** 

 http://localhost:8080/rest/private/bench/inject/forumPost?number=10&postPrefix=abc.post&fromUser=1000&toUser=1009&userPrefix=abc.user&toTopic=19&topicPrefix=abc.topic
===> forumPost injected successfully!!!
* This call will generate 10 posts for each users in the range 1000 - 1009 into for each topic at 19 position = 10(posts) x 10(users) x 1 = 100 topics 

**_inject membership:_**

 http://localhost:8080/rest/private/bench/inject/forumMembership?type=category&toType=5&typePrefix=abc.cat&fromUser=1000&toUser=1009&userPrefix=abc.user
 
===> forumMembership injected successfully!!!
* This call will generate 10 memberships to category type with name is 'abc.cat5'.

**_inject attachment:_**

 http://localhost:8080/rest/private/bench/inject/forumAttachment?number=10&postPrefix=abc.post&fromPost=1000&toPost=1019&byteSize=50
 
===> forumAttachment injected successfully!!!
* This call will generate 10 attachments for each posts in the range 1000 - 1019 = 20 with total size = 1000 bytes


**TASK Inject:**
-------------------
We will describe how to use data injectors in eXo TASK:

 **_Default for user tasks_ :**  
* Generate for 10 users (from bench.user0000 to bench.user0009) 15 projects with 42 tasks in + 10 incoming tasks (tasks without project).
 Each tasks have 2 tags and 2 comments. 70% of tasks are completed

 http://localhost:8080/rest/private/bench/inject/PersonnalTaskInjector
 
 ===> PersonnalTaskInjector injected successfully!!!
 
 
 **_Specific for user tasks_**
 
 * Generate for 10 users (from abcuser000010 to abcuser000019) **15 projects** with **42 tasks** in + 10 incoming tasks (tasks without project). 
   Each tasks have 2 tags and 2 comments. 70% of tasks are completed.
 
  http://localhost:8080/rest/private/bench/inject/PersonnalTaskInjector?prefix=abcuser&suffix=6&from=10&to=20
  
   ===> PersonnalTaskInjector injected successfully!!!
 
 
 * Generate for 10 users (from bench.user0000 to bench.user0009) **30 projects** with **10 tasks** in + 5 incoming tasks (tasks without project).
   Each tasks have 3 tags and 15 comments. 70% of tasks are completed.
  
  http://localhost:8080/rest/private/bench/inject/PersonnalTaskInjector?nbProject=30&nbTaskPerProject=10&nbIncomingTask=5&nbTagPerTask=3&nbComPerTask=15
  
   ===> PersonnalTaskInjector injected successfully!!!
 
 
 * Generate for 10 users (from bench.user0000 to bench.user0009) **15 projects** with **42 tasks** in + 10 incoming tasks (tasks without project). 
   Each tasks have 2 tags and 2 comments. 0% of tasks are completed
 
 http://localhost:8080/rest/private/bench/inject/PersonnalTaskInjector?perCompleted=0
 
  ===> PersonnalTaskInjector injected successfully!!!
 
 _**Default for space tasks**_
 
 * Generate for 10 space (from benchspace0000 to benchspace0009) **15 projects** with **42 tasks** in. 
   Each tasks have 2 tags and 2 comments. 70% of tasks are completed.
   
 http://localhost:8080/rest/private/bench/inject/PersonnalTaskInjector?type=space
 
 ===> PersonnalTaskInjector injected successfully!!!
 
 
**FAQ Inject:**
------------------
We will describe how to use data injectors in eXo FAQ 

  **_inject profile:_**
  
 http://localhost:8080/rest/private/bench/inject/faqProfile?number=10&userPrefix=abc.user
 
   ===> faqProfile injected successfully!!!
 * This call will generate 10 users which user prefix is "abc.user"
 
 **_inject category:_** 
 
   http://localhost:8080/rest/private/bench/inject/faqCategory?number=10&catPrefix=abc.cat
 
   ===> faqCategory injected successfully!!!
 * This call will generate 10 categories which category prefix is "abc.cat".
 
 
 **_inject question:_** 
 
   http://localhost:8080/rest/private/bench/inject/faqQuestion?number=10&catPrefix=abc.cat&toCat=0&userPrefix=abc.user&toUser=1&quesPrefix=abc.ques
   
   ===> faqQuestion injected successfully!!!
 * This call will generate 10 questions which question prefix is "abc.ques" to category "abc.cat0" which owns by user "abc.user1".
 
 
 **_inject answer:_** 
 
   http://localhost:8080/rest/private/bench/inject/faqAnswer?number=10&fromQues=0&toQues=2&quesPrefix=abc.ques&answerPrefix=abc.answer
   
   ===> faqAnswer injected successfully!!!
 * This call will generate 10 answers which answer prefix is "abc.answer" to questions "abc.ques0", "abc.ques1" and "abc.ques2".
 
 
 **_inject comment:_** 
 
   http://localhost:8080/rest/private/bench/inject/faqComment?number=10&toQues=0&quesPrefix=abc.ques&commentPrefix=abc.comment
   
   ===> faqComment injected successfully!!!
 * This call will generate 10 comments which comment prefix is "abc.comment" to question "abc.ques0".
 
 
 **_inject attachment:_** 
 
   http://localhost:8080/rest/private/bench/inject/faqAttachment?number=10&fromQues=0&toQues=2&quesPrefix=abc.ques&byteSize=50
   
   ===> faqAttachment injected successfully!!!
 * This call will generate 10 attachments which each file size is 50 bytes to question "abc.ques0", "abc.ques1" and "abc.ques2"
 
 
 **_inject Membership:_** 
 
   http://localhost:8080/rest/private/bench/inject/faqMembership?type=category&toType=0&typePrefix=abc.cat&fromUser=0&toUser=2&userPrefix=abc.user
   
   ===> faqMembership injected successfully!!!
 * This call will generate 3 memberships to category type with name is 'abc.cat0'
 
 
  **Poll Inject :** 
  -------------------
  
 We will describe how to use data injectors in eXo Poll
 
**_inject grp:_** 
 
 http://localhost:8080/rest/private/bench/inject/pollGroup?number=20&prefix=abc.group
 
 ===> pollGroup injected successfully!!!
 * This call will generate 20 groups.
 
 
**_inject poll:_**
  
   ****_Public:_**
   
   http://localhost:8080/rest/private/bench/inject/pollPoll?pollType=public&number=10&pollPrefix=pub.poll
   
   ===>  pollPoll injected successfully!!!
   * This call will generate 10 public polls.
  
  
   ****_Private:_** 
   
   http://localhost:8080/rest/private/bench/inject/pollPoll?pollType=private&number=10&pollPrefix=pri.poll&groupPrefix=abc.group&toGroup=1
   
   ===> pollPoll injected successfully!!!
   * This call will generate 10 polls for the group abc.group1.
    
**_inject vote:_**
 
   http://localhost:8080/rest/private/bench/inject/pollVote?fromPoll=1&toPoll=100&pollPrefix=bench.poll&fromUser=10&toUser=50&userPrefix=abc.user
   
   ===> pollVote injected successfully!!!
    
   * This call will voting 99 public polls from 1 to 100 with polls have prefix is bench.poll and with 40 users voting have index is from 10 to 50 with prefix is abc.user.
    
    
    
   **Note**:
   ----------
   WIKI inject and ECMS inject doesn't work, So it must be reviewed ..
 
 
 
 


