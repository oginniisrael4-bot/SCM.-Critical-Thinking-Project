Project Report: Moving to Git for a Distributed Team
Task 1: Why We Need to Leave SVN
Right now, our team is moving to work from different places, and our old system (SVN) is not going to work for us anymore.

The SVN Problem: SVN relies entirely on one central server. If someone loses internet or the server crashes, they cannot save their work, look at old files, or make branches. It is also really slow because every command has to talk to that main server over the internet.

The Git Advantage: Git is a distributed system. When you copy (clone) the project, you get a full copy of the whole history right on your laptop. You can save your work, check old files, and make branches completely offline. It keeps things fast and means we don't lose everything if one server goes down.

Task 2: Our Team's Git Guide
To keep our main code safe while everyone works on different features at the same time, we are using feature branches.

Feature Branching: Never write code directly on the main branch. Always make a new branch for whatever you are working on.

git checkout main

git pull origin main

git checkout -b feature-user-login

Pull Requests: When your code is ready, push your branch to GitHub and open a Pull Request. Do not merge it yourself! Another team member has to look at your changes first to catch mistakes.

Merging: Once it is approved and passes tests, it gets merged. If your branch falls behind the main branch while you are working, just run git pull origin main on your branch to fix any issues early.

Task 3: Automating with GitHub Actions
We do not want broken code ruining our app. So, I set up a simple automated script in a folder named .github/workflows/test-and-deploy.yml. It runs automatically every time someone pushes code or opens a Pull Request to main.

It tells GitHub to open our code and set up the environment on a clean virtual computer. Then, it runs a command to install the project files and another command to run our tests. If everything passes, it runs a script to deploy the updates to our test server.

How it works: If the tests fail on your branch, GitHub locks the page and blocks you from merging until you fix your code.

Task 4: Keeping Our Code Secure
Since our team is scattered everywhere, we have to lock down our project so nobody can make bad changes.

Branch Protection: We turned this on in the GitHub settings for the main branch. Now, nobody can delete the branch or force a bad upload. It strictly requires at least one teammate to review the code before it can be merged.

SSH Connections: We are banning simple passwords for terminal commands. Every developer has to create a secure key link (an SSH key) on their laptop and upload it to GitHub so we know exactly who is pushing code.

Commit Signing: For extra safety, developers have to sign their work using a security key by running git commit -S -m "message". This puts a "Verified" badge next to their name on GitHub so nobody can fake being someone else.

Task 5: Fixing a Merge Conflict
Two developers edited the exact same file (index.html) at the same time and broke the merge. Here is exactly how I fixed it on my machine.

First, I got the newest version of the project.

git checkout main

git pull origin main

Next, I opened up the broken index.html file. Git puts weird markers inside the file to show you the problem, using arrows and equal signs to separate the two different versions.

I talked to both developers, figured out which code was the correct one, deleted all the weird arrow markers, and saved the file cleanly.

Then, I saved and uploaded the fix.

git add index.html

git commit -m "Fixed merge conflict in index.html headings"

git push origin main

How we stop this from happening again:

Make smaller pull requests: Do not hold onto your code for weeks. Merge small updates every day or two.

Talk more: Tell the team in our chat channel when you are working on core files so others know to update their folders early.
