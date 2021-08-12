# Gitlab Runner on Windows w/powershell example

## Create a GitLab Repository
Download the files into a new directory, `git init` a new repository and `git add .` the files to it, add "[ci skip]" to the `git commit` message, then `git push`.
Adding [ci skip] to a commit prevents gitlab from triggering the pipeline, since we don't have a Runner yet.

## Register Gitlab Runner install on Windows
Inside the repository you just created, go to Settings > CI/CD > Runners

Under the 'Set up a specific Runner manually' section, copy the registration token and the gitlab URL.

Download gitlab runner following the instructions in the gitlab CI/CD section
On a windows server where you want to run the Runner:
`cd gitlab-runner`
`.\gitlab-runner.exe register --non-interective --url https://GITLAB_URL --registration-token TOKEN executor shell --locked=false`

Register the Runner as a service
`.\gitlab-runner.exe install`

Start the Runner
`.\gitlab-runner.exe start`

Verify the runner is alive
`.\gitlab-runner.exe verify`
You should see:
`Verifying runner... is alive                        runner=XxXXxXX`

Stop the Runner
`.\gitlab-runner.exe stop`

Uninstall the service
`.\gitlab-runner.exe uninstall`

## Run pipeline on Runner
In your repo, go to CI/CD > Pipelines and Click Run Pipeline

Every time you push changes to the repo, the pipeline will be triggered

## Schedule pipeline to run
Go to your project's CI/CD page > Schedules
Click New Schedule, enter a description, choose the interval pattern and timezone, target granch, tick Active under Activated. Click Save pipeline schedule.

The pipeline will now run as per the schedule