# :file_folder: CodeSyncer - The Ultimate Server Restart Action :arrows_counterclockwise:

Welcome to CodeSyncer, the action that brings your server to life! :boom:

## :rocket: About CodeSyncer

CodeSyncer is a GitHub Action developed by ColdShard Hosting, the coolest hosting company in town! With CodeSyncer, you can effortlessly restart your server hosted on ColdShard's panel, ensuring your code is always up to date and in sync with your GitHub repository. :globe_with_meridians:

## :thinking: How Does CodeSyncer Work?

CodeSyncer is designed to simplify the process of syncing and updating your code on your ColdShard server. When triggered, CodeSyncer performs the following steps:

1. Makes a POST request to the ColdShard panel API, instructing it to restart your server. :arrows_counterclockwise:

2. Your server then pulls the latest code from your GitHub repository, ensuring it's always up to date. :up:

3. Sit back, relax, and watch as your server syncs and updates your code automatically! :popcorn:

## :gear: Getting Started

To get CodeSyncer up and running on your own repository, follow these simple steps:

1. Ensure you have a ColdShard server and an active GitHub repository, with the relevant config on your server. Follow [this](https://gist.github.com/TheUntraceable/ba721afc0cd7b672fcb7a4b728c459bf) guide if you need help. 

2. Generate an API key on the [ColdShard panel](https://panel.coldshard.com/account/api). :key:

3. In your GitHub repository, go to "Settings" :arrow_right: "Secrets" :arrow_right: "New repository secret".

4. Add a secret named `PTERODACTYL_API_KEY` and paste your ColdShard API key as the value. :lock:

5. Create a new workflow file (e.g., `.github/workflows/restart-server.yml`) in your repository.

6. Copy the following code into the workflow file:

```yaml
name: Restart ColdShard Server

on:
  push:
    branches:
      - main

jobs:
  restart_server:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Restart Server
        env:
          API_KEY: ${{ secrets.PTERODACTYL_API_KEY }}
        run: |
          curl -X POST \
            -H "Content-Type: application/json" \
            -H "Authorization: Bearer $API_KEY" \
            -d '{
              "signal": "restart"
            }' \
            "https://panel.coldshard.com/api/client/servers/12334/power"
```

7. Customize the workflow as needed, replacing the server ID with your own.

8. Commit and push the workflow file to your repository.

9. Sit back, relax, and let CodeSyncer handle the rest! Your server will now automatically sync and update your code whenever you push changes to the `main` branch. :tada:

## :pencil: Contributing

We welcome contributions from the community to make CodeSyncer even better! If you have any ideas, bug reports, or feature requests, please open an issue or submit a pull request. Let's collaborate and make code syncing a breeze! :handshake:

## :page_facing_up: License

CodeSyncer is released under the [MIT License](https://opensource.org/licenses/MIT). Feel free to use, modify, and distribute this action as per the terms of the license.

---

We hope you find CodeSyncer useful for keeping your ColdShard server in sync with your GitHub repository. If you have any questions or need assistance, don't hesitate to reach out. Happy coding! :smile::rocket:

[![ColdShard Hosting](https://coldshard.com/media/logo.png)](https://coldshard.com)
