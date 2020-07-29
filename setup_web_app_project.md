# SETUP WEB APP PROJECT

This document is written by me as a cheat sheet for starting a Enterprise Web App Project. Very much inspired (sprinkled with my own experience) by Doguhan Uluca's fantastic book, buy it here: https://www.packtpub.com/web-development/angular-8-enterprise-ready-web-applications-second-edition#tab-label-product.info.authors.tab  

This is  living document that will be updated when new insights and experiences are gained. 

# DEV ENV SETUP  
Skip this if you are not a developer. This setup can be scripted if needed

1. Install Git and GitHub Desktop, setup credentials (SSH, cache pwd or PA Token?)  
2. Install node via NVM. Only add npm-windows-upgrade to globals (if using windows) all other packages (including Angular CLI) should be local and run via NPX scripting. This is to avoid version conflicts that can arise if project Angular and global Angular CLI are not on same version. 
3. Install VS Code. On linux use .deb package from vscode site to save time, don't recommend snap.
4. Install Docker
5. Setup dev folder, as close to root as possible. Name folder repos or dev
6. Establish workflow and code styling, see section "Team Setup"
7. Generate application via npx @angular/cli new name-of-app.
8. Install VS Code extensions, use extensions.json in .vscode folder for each environment. Se example Angular project on my Github.
9. Setup code styling and linting according to workflow decisions made. See below

# PROJECT SETUP

### Challenges to overcome in modern web application development
- Deliver iteratively and incrementally. Move fast without breaking things.
- Be scalable
- Serve dozens of screens, input types and web browser (of different versions)
- Be usable, be intuitive
- Be accessible
- Manage a team, avoid conflicts in code, style and merges. 
- Groom a prioritized backlog
- Ensure acceptance criteria are clear, concise and concrete

The Pareto principle tells us that 20% of the effort delivers 80% of our goals. This means 80% of our time is spent on details. The be effective we should focus on the 20% buy building LOB apps which we can scale accordingly.  
Adhering to this principle it is very important to create a predictable environment for the team and keep engineering overhead at a minimum.
Also always avoid experimentation in production code, only introduce changes that have been tested in proof-of-concept/small apps and approved by the team.   
All this can be archived by staying close to the **Router-first architecture**. 
- **Enforce** high level thinking
- **Ensure** consensus on features to implement, before you start coding.
- **Plan** for scalability, your codebase/team that can grow
- **Introduce** little engineering overhead

This can be done in steps:

- Develop a roadmap and scope
- Sketch the high level architecture
- Introduce agile project management
- Establish a workflow
- Implement CI
- Discuss deployment and hosting
- Establish testing coverage
- Establish code style and linting rules
- Create a wireframe UX design and discuss styling
- Implement a walking-skeleton
- Design with lazy loading in mind
- Achieve stateless, data driven design

I will now go over this steps one at a time

## Develop a roadmap and scope
In the team establish and write down the requirement specification and paint discuss how we with least amount of overhead can deliver most amount of our apps functionality (Pareto Principle). Always keep scalability in mind.  
Make a list of functionality that is "must haves" (ToDo) and what should be on the "whish list" (Backlog).

## Sketch the high level architecture
Very much linked to above step. Use a tool like draw.io and sketch on a high level how the architecture should look. things to keep in mind:
- Backend requirements
- Frontend requirements
- Enforce decouple architecture (key to scalability). REST API. Multi repo - hard decoupling
- API services
- Authentication and Authorization
- Security layers
- PWA requirements
- State management - how advanced and how many inputs streams are to be handled. > 3 inputs a advanced state management library is recommended, like NgRx.

## Introduce agile project management
Discuss if a Kanban board is enough or if we should go full Scrum from start?
This depends of course on team size. For smaller teams I recommend a simple Kanban to start (depending on team size that is) especially if the Github flow is chosen (see below step). Remember that a low overhead is key to moving fast! A Kanban board can be easily added to Github repos via projects tab.  
Start filling your backlog and todo with the list form step "Develop a roadmap and scope". 

## Which workflow?
- Github flow - recommended for simplicity, low overhead. Read about it here: https://guides.github.com/introduction/flow/
- Git flow
- Trunk based

**GitHub flow explained** 
The GitHub flow lets us deliver value in a reliable stream of changes, will ensuring quality standards at control gates - pull requests.  
*GitHub flow is a branch-based workflow that supports teams and projects where deployments are made regular* - GitHub
In a GitHub flow the master branch should always be deployable to production, changes are introduced via branches directly from the master branch. The steps of the GitHub flow are as follows:
1. Branch - start by making a feature or fix branch, name it accordingly. This way the branches end up like feature road map. Very easy to overlook progress and discuss around.
2. Commit - make commits often to your branch. Makes it easy to revert and discuss around.
3. Create a pull request - when you have pushed your code to the repo and ready to review it, make a pull request. This will initiate CI test and make the code ready for review by the team.
4. Discuss and review - request a review of your code changes, address general or line-level comments and make necessary changes accordingly. When the branch is reviewed and tested you are ready for deployment. 
5. Deploy - before merging code, deploy directly to production or a test server. I the build breaks or issues arise you can always deploy the main/master branch instead. CD with Docker Images makes this process a lot easier and safer.
6. When the code change has been verified in production, the code is ready to merge with the main/master branch. The olf Pull Request will remain as a historical record to go back and review why a change was made. 

## Implement CI
Which tools are out there and which to use
- CircleCI
- Jenkins
- GitLab
- Many more

Discuss following:
- Which CI tools suits or environment and workflow best?
- Pricing
- Features
- Ease of use, remember the engineering overhead shall be kept low!

## Discuss deployment and hosting
Discuss cloud server hosting and how to deploy your app. 
There are many cloud providers out there, biggest ones are:
- AWS
- MS Azure
- Google Cloud
- Digital Ocean

When discussing which cloud provider to use, touch on following:

- Should we implement full CD via Docker images?
- Security and Threats (DDoS protection)
- Scalability
- Availability
- Price

## Establish testing coverage
Discuss how to achieve 100% test coverage which is aimed for and how to solve each part with tooling and automation. Discuss following:
- UI test
- Integration Test
- Unit Test
- CI integration of test automation 

## Which Code Style and Linting?

Agree which Code Style and linting rules that should be used. This should then be configured in the project settings and tested on CI Server. 

## Create a wireframe front-end UX design and discuss styling
Present a UX wireframe design, recommend Sketch as a tool for this.
Should a CSS framework be used - Google Material, Tailwind, Bootstrap?  
If there is no company styling guide in place I highly recommend creating such a document. Look into Storybook as fantastic open source software solution for building and testing a company UI component library!  https://storybook.js.org/

## Implement a walking-skeleton
Start working on a first working-skeleton both front- and backend. Setup simple navigation, APIs and other basic functionality.


MORE TO BE ADDED SOON



