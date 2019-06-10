# AppVeyor 🡒 Discord Webhook

If you are looking for a way to get build (success/fail) status reports from
[AppVeyor](https://appveyor.com) in [Discord](https://discordapp.com), stop
looking. You've came to the right place.

Rest aside and just follow the guide below and stay notified of your build
status.

## Requirements
-  You should be using AppVeyor for testing codes.
-  A Discord Server where notifications will be posted.
-  5 minutes
-  A cup of coffee ☕

## Guide
1.  Create a webhook in your Discord Server ([Guide](https://support.discordapp.com/hc/en-us/articles/228383668-Intro-to-Webhooks)).

1.  Copy the **Webhook URL**.

1.  Go to your project settings (for which you want status notifications)
    in AppVeyor and add an environment variable called `WEBHOOK_URL` and paste
    the **Webhook URL** you got in the previous step.

    ![Add environment variable in AppVeyor](https://i.imgur.com/dk2mdSW.png)

1.  Add these lines to the `appveyor.yml` file of your repository.

    ```yaml
    on_success:
      - ps: Invoke-RestMethod https://raw.githubusercontent.com/DiscordHooks/appveyor-discord-webhook/master/send.ps1 -o send.ps1
      - ps: ./send.ps1 success $env:WEBHOOK_URL
    on_failure:
      - ps: Invoke-RestMethod https://raw.githubusercontent.com/DiscordHooks/appveyor-discord-webhook/master/send.ps1 -o send.ps1
      - ps: ./send.ps1 failure $env:WEBHOOK_URL
    ```

1.  Grab your coffee ☕ and enjoy! And, if you liked this, please ⭐**Star**
    this repository to show your love.

### Note
-  If you face any issues in the scripts (and you're sure it's not on your side),
please consider opening an issue and I'll fix it ASAP.
-  If you want to improve the scripts, feel free to open a pull request.

### See Also
-  [Travis CI -> Discord Webhook](https://github.com/DiscordHooks/travis-ci-discord-webhook)
-  [GitLab CI -> Discord Webhook](https://github.com/DiscordHooks/gitlab-ci-discord-webhook)
