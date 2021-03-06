## Installation

Add the this repository's `git clone` url to your container's `app.yml` file, at the bottom of the `cmd` section:

```yml
hooks:
  after_code:
    - exec:
        cd: $home/plugins
        cmd:
          - mkdir -p plugins
          - git clone https://github.com/discourse/docker_manager.git
          - git clone https://github.com/discourse/discourse-slack-official.git
```

Rebuild your container:

```
cd /var/discourse
git pull
./launcher rebuild app
```

## Configuration

1. Go to the **[Incoming Webhooks](https://slack.com/apps/new/A0F7XDUAZ-incoming-webhooks)** configuration page for your Slack instance. Pick a channel, and click the big green "Add incoming webhook Integration" button. (You only need to do this once, even if you have multiple Discourse instances.)
 
    ![Big green button page](http://i.imgur.com/HZDncCP.png)

2. Scroll down to **Integration Settings** and copy the "Webhook URL".

    ![New Webhook Page](https://cloud.githubusercontent.com/assets/1386403/16739200/f92dbee8-4766-11e6-9e4a-03289337a91b.png)
    
3. Go to your Discourse settings page, found at `<your-discourse-url>/admin/site_settings/category/plugins`. In the **slack outbound webhook url** field, paste the webhook URL you copied from Slack.

    ![Discourse Slack Plugin Settings Page](http://i.imgur.com/wXwkSFR.png)

4. Select the **Enable checkbox**, and save all the changed settings. That's it! You're done! 

By default, every new post on your Discourse will now create a Slack message in the channel you specified in step one. To change your notification defaults, go to `/admin/plugins/slack` on your Discourse:

![Discourse Slack plugin notification defaults](http://i.imgur.com/ea8kvbE.png)

Or set up an [optional slash command](./README-SLASHCOMMAND.md) to change your notifications settings directly from Slack.



## Todo
- [ ] Enable unfurling on private Discourse instances
- [ ] Handle content OneBoxing on the Discourse end
