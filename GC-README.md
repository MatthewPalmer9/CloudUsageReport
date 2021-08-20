# Google Cloud
To use Google Cloud and deploy, I first needed to create a free tier account. From the main menu, I scrolled down and clicked on "Compute Engine". At this time, I have created an Virtual Machine instance of Ubuntu where my first move is to open my VM terminal and perform updates to it with `sudo apt-get update && sudo apt-get upgrade`.

- [The Repo I Used to Deploy to the Cloud](https://github.com/matthewpalmer9/mattpdev)

## Step 1
I have download Docker and run `docker run --name repo alpine/git clone https://github.com/matthewpalmer9/mattpdev.git`.

Then, `cd mattpdev` => `docker build -t mattpdev/mattpdev .`.
The `.` means to "define the dockerfile in the current directory".

Then, `docker run -p 80:80:443 mattpdev/mattpdev:latest` to run it locally & confirm all is working.

## Step 2
Next, we go to our Google Cloud account, create a new project, and then search for `Cloud Run`. Then, we `Create a New Service`. This is where we will leverage `Continuous Integration` and `Continuous Deployment`. This is used commonly in DevOps and modern-day deployment.

Here I connected Google Cloud APIs and authenticated my Github, then made sure it knew my repo was on branch `master` and not `main`. Then I chose my build type as `Docker`. In `Advancd Settings`, I specified my port as `443` and kept all other settings as the default.

In the final settings, I allowed all traffic under `Indress` and allowed unauthenticated invocations under `Authentication`, which just means anyone on the web can visit my URL.

# Where can I find your Cloud Deployment?
- [You can find my official cloud deployment here](https://mattpdev-btxywowlba-uc.a.run.app/)