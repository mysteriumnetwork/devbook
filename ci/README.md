# Continuous Integration

We use pipeline based [Gitlab CI/CD for Github](https://about.gitlab.com/solutions/github/).  
It creates a read-only mirror which is updated upon a push event from Github's webhook.
Pipeline build statuses are reported back to Github.

## Runner types

Gitlab assigns jobs to runners (workers) based on tags and their availability. We have 2 types of runners (with corresponding tags). To assign your job to the runner, use the relevant tag.

- `go`: a shell runner with go and some related tools pre-installed. Useful when you use docker for integration testing, so you cannot use docker runner. Example of usage: [node/go](https://github.com/mysteriumnetwork/node/blob/master/.gitlab-ci.yml)
- `docker`: a general purpose docker runner which when provided with a needed docker image can be used for anything, from go to web projects. Example of usage: [feedback/go](https://github.com/mysteriumnetwork/feedback/blob/master/.gitlab-ci.yml) [terms/go+js](https://github.com/mysteriumnetwork/terms/blob/master/.gitlab-ci.yml)

**Rule of the thumb**: if you don't use docker CLI in CI, then use `docker` runner.

## How to setup a Gitlab mirror for CI

Github:

1. **IMPORTANT!** Add our team user as a collaborator (**admin** permission level) to the project (for Gitlab to create webhooks automatically). After initial setup is done, you may demote permission level to **write**.

Gitlab:

1. Login using team user
2. https://gitlab.com/mysteriumnetwork → `New Project → CI/CD for external repo → Connect repositories from: Github`
3. Find the project in `From GitHub` column. 
4. **IMPORTANT!** In `To GitLab` column, select `Groups/mysteriumnetwork`.
![Import Github project](../assets/img/ci/import-github-project.png)
5. Click `Connect`

That's all.  
If everything went well, Gitlab will mirror updates whenever you push to any branch in Github repo.   
If the project has `.gitlab-ci.yml`, Gitlab will run build pipeline and report build status back to the Github.

## Post mirror setup

- We use group runners in Gitlab, under [mysteriumnetwork group](https://gitlab.com/groups/mysteriumnetwork/-/settings/ci_cd).  
To utilize them, disable Shared runners (that are enabled by default for new projects) in your project → `Settings → CI / CD → Runners`
