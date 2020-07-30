# SETUP ANGULAR WEB APP PROJECT

This document is written by me as a high level cheat sheet for starting a new Angular web app project. Very much inspired (sprinkled with my own experience) by [Doguhan Uluca's fantastic book.](https://www.packtpub.com/web-development/angular-8-enterprise-ready-web-applications-second-edition#tab-label-product.info.authors.tab)  

This is a living document that will be updated as new insights and experiences are gained. Feel free to contribute with your own experiences of web app development.   

# ANGULAR DEV ENV SETUP  
This part is aimed for myself and developers setting up their Angular development environment on a new machine. Most of the process can easily be scripted.   

1. Install Git and GitHub Desktop, setup credentials (SSH, cache pwd or PA Token?)  
2. If using Linux or Windows WSL, I highly recommend installing node via [Node Version Manager](https://github.com/nvm-sh/nvm). Avoid installing global packages as much as possible. This is to avoid version conflicts that can arise if the project version of Angular and the global Angular CLI version are not on the same version. 
3. Install VS Code. On Linux add the official repo from VS Code team to your package manager, don't recommend snap.
4. Install Docker
5. Setup a dedicated dev folder, as close to root as possible.
6. Establish workflow and code styling, see next section "PROJECT SETUP"
7. Generate application via ```npx @angular/cli new name-of-app```.
8. Install VS Code extensions, agree within the team over a minimum set of extensions and add them to the extensions.json in .vscode folder (exclude .vscode/extensions.json from .gitignore).
9. Setup code styling and linting according to team/project/company decisions made. Add the config files needed to enforce this to source and script tests for CI server.

Fantastic setup example in these config files: https://github.com/duluca/local-weather-app

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

The Pareto principle tells us that 20% of the effort delivers 80% of our goals. This means 80% of our time is spent on details. To be effective we should focus on the 20% were can get the most job done, with least amount of effort. In our case this is by building Line-of-Business apps which we can scale accordingly.  
Adhering to this principle it is very important to create a predictable environment for the team and keep engineering overhead at a minimum, focus on what really matters.
Also always avoid experimentation in production code, only introduce changes that have been tested in proof-of-concept/small apps and approved by the team.   
All this can be archived by staying close to the **Router-first architecture** as stated by Doguhan Uluca:
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

I will now go over these steps one at a time.

## Develop a roadmap and scope
In the team establish and write down the **requirement specification** and discuss how you with the least amount of overhead can deliver most amount of your apps functionality (Pareto Principle). 
Discuss who is the user of your app and their needs of UX and security. 
Make a list of functionality that is "must haves" (ToDo board) and what should be on the "whish list" (Backlog board).

## Sketch the high level architecture
Very much linked to above step. Use a tool like [draw.io](https://app.diagrams.net/) and sketch on a high level how the architecture should look. Things to keep in mind:
- Backend requirements, scalability
- Frontend requirements, scalability
- How to enforce a decoupled architecture (key to scalability). REST API. Dependency Injection. Multi repo - hard decoupling
- API services
- Authentication and Authorization
- Security layers
- PWA requirements
- State management - how advanced and how many inputs streams are to be handled. > 3 inputs a advanced state management library is recommended, like NgRx.

## Introduce agile project management
Discuss if a Kanban board is enough or if we should go full Scrum from start?
This of course depends on team size. For smaller teams I recommend a simple Kanban to start  especially if the Github workflow is chosen (see below step). Remember that a low overhead is key to moving fast and delivering value! A Kanban board can be easily added to Github repos via projects tab.  
Start filling your backlog and todo with the list made during step "Develop a roadmap and scope". 

## Which workflow?
- Github flow - recommended for simplicity, suits web apps perfect, low overhead. Read about it here: https://guides.github.com/introduction/flow/
- Git flow
- Trunk based

**GitHub flow explained** 

*GitHub flow is a branch-based workflow that supports teams and projects where deployments are made regularly* - GitHub

The GitHub flow lets us deliver value in a reliable stream of changes, while ensuring quality standards at control gates - via pull requests.  
In a GitHub flow the master branch should always be deployable to production, changes are introduced via branches directly from the master branch. The steps of the GitHub flow are as follows:
1. Branch - start by making a feature or fix branch, name it accordingly. This way the branches end up like a feature road map. Makes it very easy to overlook progress and discuss around.
2. Commit - make commits often to your branch. Makes it easy to revert.
3. Create a pull request - when you have pushed your code to the repo and are ready to review it, make a pull request. This will initiate CI test and make the code ready for review by the team.
4. Discuss and review - request a review of your code changes, address general or line-level comments and make necessary changes accordingly. When the branch is reviewed and tested you are ready for deployment. 
5. Deploy - before merging code, deploy directly to production or a test server, which ever suit your business best. If the build breaks or issues arise you can always deploy the main/master branch instead. Continuous Deployment with Docker Images makes this process a lot easier and safer.
6. When the code change has been verified in production, the code is ready to merge with the main/master branch. The old Pull Request will remain as a historical record to go back and review why and how a change or fix was made. 

## Implement CI
Which tools are out there and which to use
- CircleCI
- Jenkins
- GitLab
- Many more

Discuss following:
- Which CI tools suits our environment and workflow best?
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
Discuss how to achieve 100% test coverage and how to solve each part with tooling and automation. Discuss following:
- UI test
- Integration Test
- Unit Test
- CI integration of test automation 

## Which Code Style and Linting?

Agree which Code Style and linting rules that should be used. This should then be configured in the project settings and tested on CI Server. 

## Create a wireframe front-end UX design and discuss styling
Present a UX wireframe design, recommend [Sketch](https://www.sketch.com/) as a tool for this.
Should a CSS framework be used - Google Material, Tailwind, Bootstrap?  
If there is no company styling guide in place I highly recommend creating such a document. Look into [Storybook](https://storybook.js.org/) as fantastic open source software solution for building and testing a company UI component library! 

## Implement a walking-skeleton
Start working on a first working-skeleton both front- and backend. Setup and test simple navigation, APIs and other basic functionality.

MORE TO BE ADDED SOON



