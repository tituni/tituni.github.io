## Creating a connection with gitlab and code grade (Moodle)

1. Start connecting with gitlab

![connect via webhooks](./img/connect_via_webhooks.png)

2. Add the deployment key to course-gitlab

Open "Settings" in your gitlab repository, select "Repository" and "Deploy keys". Select "Add new key" and store the given ssh-rsa - key to course-gitlab.

![adding deployment key](./img/add_webhook_ssh.png)

![gitlab repository settings](./img/settings_repository.png)

3. Add webhook to gitlab

Copy URL and token from code grade:
![webhook in codegrade](./img/add_webhook.png)

Create a new webhook in course-gitlab and save URL and token:
![webhook in gitlab](./img/webhooks_gitlab.png)

Select "Push events" and set wildcard to *-grading. Make sure "Enable SSL verification" is selected.

![setup for webhook URL and token, select push events](./img/webhook_3.png)
![setup for webhook enable SSL](./img/webhook_2.png)

The web hook has been created now.

4. Test submission

You can test the hook by selecting "Test"->"Push events" in course-gitlab.

![test web hook with push event](./img/test_hook_gitlab2.png)

To see if test is ok also in code grade:

![see if test succeeded](./img/success_webhook.png)
