[TOC]

# 1. Introducion

## 1.1. Project Purpose

This project KeepFit aims to streamline the fitness journey with an integrated solution that combines diet plans, exercise routines, and equipment management. By providing personalized diet and workout programs, which dynamically adjust to each user’s fitness schedule, it helps users pursue their goals more intelligently and efficiently. The equipment management feature guides users in selecting and optimizing fitness equipment usage. Through smart recommendations and real-time feedback, the project encourages healthy habits, supports the nationwide fitness movement, and fosters the adoption of a healthier lifestyle.

This System Design Model Document (SDM document) aims to comprehensively explain the design model and architecture of the KeepFit system. The document details the overall structure of the system, including the functional modules of each subsystem, the interface relationship, and the data flow process. In addition, the document explores in depth the specific mechanisms of system prototyping, covering all stages, from requirements analysis to system implementation. In order to help to better understand and apply the design models, the document also provides some practical examples, showing how to flexibly configure and expand according to the specific business requirements. These contents will provide clear guidance for development, implementation and subsequent maintenance, and ensure the efficient and stable operation of the system.

## 1.2. Project Scope

Keep-Fit is a Web-based smart fitness software, and the goal is to help users achieve their fitness goals smarter and more effectively. The main scenarios of the system include the selection of fitness tutorial, punching schedule, fitness posture guidance, food equipment recommendation and AI robot chat, etc. VIP members and ordinary users can browse information and participate in the activity after registering and logging in, and choose whether to become uploader. In addition, the platform administrators can maintain the platform order and keep the platform fitness content up to date.

<p align="center" style="display: flex; justify-content: center; gap: 2px;">
  <img src="./assets/Scope1.png" alt="Image 1" style="width: 102px;"/>
  <img src="./assets/Scope2.png" alt="Image 2" style="width: 102px;"/>
  <img src="./assets/Scope3.png" alt="Image 3" style="width: 102px;"/>
  <img src="./assets/Scope4.png" alt="Image 4" style="width: 102px;"/>
  <img src="./assets/Scope5.png" alt="Image 5" style="width: 102px;"/>
  <img src="./assets/Scope6.png" alt="Image 6" style="width: 102px;"/>
  <img src="./assets/Scope7.png" alt="Image 7" style="width: 102px;"/>
</p>

In addition, Keep-Fit also has the following characteristics:

- The platform system operates in a network environment.
- The system has an accurate recommended fitness tutorial algorithm.
- The intelligent system allows users to chat and consult with the AI.
- Have a safe and reliable database to ensure information security.

## 1.3. Glossary of Terms

| English terms                  | Terminology interpretation                                   |
| :----------------------------- | :----------------------------------------------------------- |
| **Keep-Fit**                   | The name of our project, the intelligent fitness platform, is designed to help users achieve their fitness goals smarter and more effectively. |
| **User**                       | The most basic users of the intelligent fitness platform can access the platform through registration, and use the most basic functions of the platform. |
| **VIP Member**                 | Ordinary users can become VIP members by recharging, and VIP members can use the richer functions in the platform, such as some paid tutorials, more intelligent AI chat systems and more accurate recommendation systems. |
| **Uploader**                   | Each kind of user(Users and VIP Members) can become a Uploaders by uploading exercise tutorials and sharing fitness experiences, and the Uploaders can also gain revenue and fans by selling paid fitness tutorials. |
| **Administrator**              | The administrator needs to maintain the order of the platform and the stability of the environment, and can ban the illegal users. You can also make announcements, upload new fitness tutorials, diet combinations and fitness equipment, and so on. |
| **Fitness** **Tutorial**       | Fitness tutorials are uploaded by uploaders or administrators, including paid and free, and cover a variety of fitness categories. |
| **Check-in**                   | After the user selects a fitness tutorial, the system automatically generates daily tasks and plans for the tutorial (the user can also plan the tutorial by himself/herself). Users need to complete the tasks every day to check in. |
| **AI** **Motion Detection**    | Users can upload photos of themselves during their workout process, and the system's AI will automatically check whether the exercise movements meet the specifications and give appropriate suggestions. |
| **Nutritional Composition**    | After the user selects a fitness tutorial, the system will automatically generate the recommended diet package of the tutorial, and give the nutritional composition of the package. Users can also take photos and upload daily diet pictures, and the AI system will automatically identify and give the nutritional content list of the diet. |
| **Reward** **Mechanism**       | Users need to complete the corresponding tasks every day according to the daily plan generated by the system(or tasks planning by himself/heself). After completing the tasks, they can get virtual rewards (such as level growth and platform transaction currency). |
| **Report**                     | Administrators regularly make announcements to various users of the platform, including some important notifications, new tutorials, and the latest feature points on the platform. |
| **Fitness** **Equipment**      | Each fitness course is accompanied by a series of required fitness equipment, the system will give the corresponding purchase links and size size recommendations. |
| **Chat Platform**              | In the chat platform, users can chat not only with their friends, but also with the system's AI robot, which can answer anything about fitness intelligently. |
| **Multi-device Access**        | Users can access and use the functions of the platform through different devices (such as personal computers, tablets, smartphones, etc.). This flexible access approach can improve the user experience and engagement. |
| **Intelligent Recommendation** | The system automatically generates personalized suggestions based on the users' personal information, fitness goals, history, and preferences. |



# 2. 

**Fitness Tutorial Section**

| API Interface                               | Method | Parameters                      | Description                                                  |
| ------------------------------------------- | ------ | ------------------------------- | ------------------------------------------------------------ |
| /api/tutorial/tutorialSearch                | GET    | token, keyword                  | Through this interface, users find the relevant fitness tutorial through keyword search and return a list of matching tutorials. |
| /api/tutorial/{tutorialID}/tutorialInfo     | GET    | token, tutorialId               | The interface uses the user to obtain the details of the specified fitness course, including the course name, introduction, duration, difficulty, etc. |
| /api/tutorial/{tutorialID}/tutorialPurchase | POST   | token, tutorialId               | The user buys the specified unlocked tutorial through this interface to return whether the purchase is successful. |
| /api/tutorial/{tutorialID}/tutorialPlay     | GET    | token                           | Users can watch the purchased or unlocked fitness tutorial videos through this interface. |
| /api/tutorial/{tutorialID}/planGenerate     | POST   | token, tutorialId               | This interface can generate a personalized fitness plan and return the generated plan content. |
| /api/tutorial/{tutorialID}/planAIadjust     | PUT    | token, tutorialId               | The user adjusts the fitness plan through this interface, and changes it according to the suggestions of AI assistance. |
| /api/tutorial/{tutorialID}/fitProgress      | POST   | token, tutorialId               | The user uploads the fitness training data through this interface, and the system tracks the user's fitness progress. |
| /api/tutorial/{tutorialID}/dataAnalysis     | GET    | token, tutorialId               | The system provides the data analysis function, show the user's fitness performance and trend, and generate the analysis report. |
| /api/tutorial/progressReport                | GET    | token, tutorialId, reportType   | Users can export detailed fitness progress reports in different formats, view data, trends, and suggestions for improvement. |
| /api/tutorial/{tutorialID}/tutorialCheckin  | POST   | token, actionId,imgUrl/videoUrl | Users upload photos or videos during the fitness process through the interface to punch in, and the system detects the standardization of AI movements. |
| /api/tutorial/rewardGet                     | GET    | token, tutorialId               | The corresponding virtual reward obtained after the user completes the task and clocks in is recorded in the database. |
| /api/tutorial/tutorialRecommendation        | POST   | token                           | The system recommends suitable tutorials and plans based on the user's fitness history and progress, and returns a personalized recommendation list. |
| /api/tutorial/newTutorialUpload             | POST   | token, newTutorialContents      | The Uploader uploads a new fitness tutorial through this interface, and submits the basic information of the tutorial (such as the tutorial name, brief introduction, length, difficulty, etc.). |
| /api/tutorial/tutorialApprove               | PUT    | token, newTutorialContents      | The administrator reviews the newly uploaded tutorial through this interface. After the audit, the tutorial becomes available, and the failure information is returned. |
| /api/tutorial/releaseComment                | POST   | token, tutorialId, comment      | The user evaluates the specified tutorial through this interface. |
| /api/tutorial/commentApprove                | PUT    | token, tutorialId, comment      | The administrator reviews the user's tutorial evaluation through this interface, and the approved evaluation will be displayed on the tutorial page. |

