# Continuous integration with Jenkins

This repositry contains inforamtion regarding setting up a continuous integration pipeline with Jenkins, done as part of DevOps training at Sparta Global. 

## Dependencies

- Jenkins installed or available on a server accesible online
- To have it installed on host machine, there are steps available on their website
```https://www.jenkins.io/download/```

## What is Jenkins
- An automation software, written in Java. Its principle use is with continuous integration
- This enables projects to be continuously built and tested
- Thus overall software delivery is faster and can enables working with testing and deployment software
- It uses the pipeline-as-a-code concept, enabling automation

## Jenkins set up
**Creating a project**
1. Click on ```New item```
2. Enter descripton of project
3. Discord old builds ticked normally
	- Restrict builds to 2
	- This will reduce the unnneccesary builds saved
4. Enter github repositry under github project tickbox
5. Restrict where project can be run
	- Tick then fill in box with sparta-ubuntu-node
	- This may have to be inserted multiple times
6. Source code
	- Use git per industry standard
	- Copy link to repositry as ssh per git clone syntax
	- Means jenkins will need verified keys

**Adding SSH key to jenkins**
1. follow steps to generate github SSH Key(in .ssh folder)
2. https://docs.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent
3. Once done go to repostries > add credentials > Jenkins.
4. Kind is SSH username
5. ID and description is dependent on contect e.g eng67max - public ID
6. SSH private key is got by ```cat key_name``` (in .ssh folder)
7. Private key is generated ssh key
8. Add key then select it. 
9. SSH public key is got by ```cat key_name.public``` (in .ssh folder)
10. This is then pasted into Github SSH keys list. 
11. Reselect your credentials and it should work

**Build Triggers**
1. Github hook trigger for GITScm polling
2. Go onto the specific repo on github
3. Settings > webhook > add webhook
4. Insert ```http://jenkins.spartaglobal.academy:8080/github-webhook/```
	- Before github-webhook/ the URL is interchange for what server works
5. Just the push event as lots of people on small server (will likely change)
6. This should auto trigger the server to build your code

**Build environment**
1. May need to provide secret files(dont for this example)
2. Provide Node and npm bin folder to path

**Build**
1. Add execute shell step
2. Add below command. Will automatically listen to github and test code
```
cd app/
npm install
npm test
``` 

## Modifying Jenkins for continuous integration
**Setting email notification**
- Go to office 365 connector
- Select add webhook
- Add name then follow instructions on question mark near URL box
- It may take a few commits for it to update

**The code checked is code from the develop branch (not the master branch)**
- Specify branch under source code management to :origin/develop

**The git publisher plugin pushes the master branch once tests pass**
- Additional behaviour after build
- Push only if build succeds
- Merge results
- Add branch
	- Branch to push: ```master```
	- Target remote name: ```origin```

## Theory
**What is an API**
- APIs allow apps to communicate wtih each other
- Stands for Application Programming Interface
- It governs the access points for the server

**Web hook**
- Inverted API call
- API call = When you ask employer if you got the job
- Inverted is where you are ready to recieve a call
- Github repositry needs link to Jenkins with this concept so it knows what to send and where to
        - Need to configure this

**Using web hook**
- Jenkins will listen for git changes
- These will then be directed to a test environment

## Web app

