# Git workflow for Teams

You're about to start on your group project. Having a strict Git workflow will be essential for things going smoothly. There's several ways to do this, but the technique below will work if you don't have another preferred method. 

You'll be working with *two* repositories. One for your API (rails) server, and one for your static asset server (html, css, js).

### Starting your project

- Create a new project: `git init`
- Create your initial files. For Rails this might be `rails new...` and for the static asset site this might be `yo webapp` using [Yeoman](http://yeoman.io/learning/).
- Ensure that you have a proper `.gitignore` file in place
- Do a `git add .` to add all files
- `git commit -m "Initial code"` to create your first commit
- Go to Github and create a new public repo
- `git add remote upstream git@github.com:REPO_OWNER/REPO_NAME.git` to add the upstream remote to pull changes from
- Now have everyone fork that project on Github to their own accounts
- Add your own fork as the `origin` remote with `git add remote origin git@github.com:YOUR_USERNAME/REPO_NAME.git`

Now stop. Don't make any more changes to Rails, no matter how basic they seem. From here on, you'll need to follow a better structure.

### Adding a feature

Let's say you want to do something basic like add new gems to the Gemfile. Here are the steps to follow: 

1. Create a new issue in your issue tracker. Assign this to a team member and talk about this with your team to make sure you are in agreement as to what the work entails, who will do it, and any larger decisions. *All work must have an issue associated, no matter how small*
2. Whoever is assigned the work will create a new branch for the issue. In the branch name, reference the issue number from your issue tracker and a short description. From the master branch for example I might run `git checkout -b 1_add_testing_gems`. Now I'm on the `1_add_testing_gems` branch and can start doing work.
3. Write tests (optional, but recommended). Tests should reflect work planned in the issue tracker.
4. Write code to fulfill tests, making git commits along the way as tests pass. 
5. Refactor code. Make more git commits.
6. Document your code using rDoc or other comments. Make more git commits.
7. Test deployment to Heroku on a separate staging instance that you control (not the group one)
7. Once the feature is 100% ready, and you want to merge the code and close the issue, do a `git rebase -i HEAD~3` to squash the last 3 git commits into a single one with an excellent commit message. You can change it to HEAD~4 to squash 4 commits, etc.
8. Push your branch to *your* Github remote: `git push origin 1_add_testing_gems`
9. Go to Github and make a Pull Request from your repo to the base repo. In the PR, note the issue # from the issue tracker to the pull request notes.
10. Have another team member review the code changes, and then merge the pull request
11. Switch back to your master branch `git checkout master`
11. Have all team members do a `git pull upstream master` to update your code. If they are on another branch, you can either merge in changes from master (on that feature-branch type `git merge master`), or wait until they are done with their issue and then just pull in cleanly from the `upstream` to their master branch
12. Have one team member deploy your merged code to Heroku to ensure you haven't broken anything in production. If you have written good tests, there should be little cause for things breaking. 
