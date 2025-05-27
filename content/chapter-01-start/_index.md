---
title: Getting Started
menuTitle: Getting Started
weight: 10
---

## Prerequisite

The Prerequisite steps are one-time steps that are needed to setup the editing and publishing environment. Once the environment is setup correctly, all you need to do are
the editing and publishing steps in the next section.

1. You need **vscode**, **git** and **hugo** installed on you laptop

   - Download and install VSCode from [the VSCode home page](https://code.visualstudio.com/download)
     - In VSCode, extensions can enhance the editing experience.
       Click the extensions button on the left side toolbar, search and install these extensions:
       - Hugo Language and Syntax Support
       - Code Spell Checker
       - Markdown All in One
   - Install **git**:

     ```sh
     brew install git
     ```

   - Install **hugo**:

   {{<tabs>}}
   {{% tab title="Windowns" icon="fab fa-windows" %}}

   Download the latest install package from the gohugo [Github Releases Page](https://github.com/gohugoio/hugo/releases).

   {{% /tab %}}
   {{% tab title="Linux" icon="fab fa-ubuntu" %}}
   For Ubuntu or Debian:

   ```sh
   sudo apt install hugo
   ```

   {{% /tab %}}
   {{% tab title="macOS" icon="fab fa-apple" %}}
   With macOS you can do

   ```sh
   brew install hugo
   ```

   {{% /tab %}}
   {{</tabs>}}

1. Make sure you can access the internal GitLab: https://svl-devops-gitlab01.fortilab.fortinet.com
   Login by clicking the OIDC FAC button, with Fortinet credential.

   ![gitlab login screen](gitlab_login.png)
   {{% notice info %}}
   Login by clicking the **DevOps OIDC FAC** button, then use your Fortinet credentials on the Corporate SSO page.
   Do **not** use the GitLab username password fields.
   {{% /notice %}}

1. In GitLab, you need to copy your public ssh key to gitlab to be able to use git with ssh

   - Click the user icon at the top right corner of the page.
   - Select **edit profile** from the drop down menu
   - Then click **SSH Keys** from the left panel.
   - Copy and paste your ssh public key in your computer to the **Key** text area on that page.
   - Click **Add Key** button.

1. Your project will be assigned with a name and an url to the gitlab repository. For example: **sdwan-advanced** and `git@svl-devops-gitlab01.fortilab.fortinet.com:tec-content/sdwan-advanced.git`. We will use **PROJECT_NAME** and **GIT_URL** in all examples from now on.

   The following steps are run in the terminal of your computer to download and initialize the documents:

   1. Clone the gitlab projec. These commands create a new folder with the name of [PROJECT_NAME] and download the project there:

      ```shell
      git clone [GIT_URL]
      cd [PROJECT_NAME]
      ```

   1. Open the project in vscode (You can also use VSCode's GUI to open the [PROJECT_NAME] folder):

      ```sh
      vscode .
      ```

   1. Start hugo server. The hugo server monitors all changes in the folder and allows you to preview in realtime the result as you are editing the documents:

      ```sh
      hugo server
      ```

      From the output of the hugo server, you will see the web pages are prepared. In the end the last few lines of the output will be something like:

      ```text
      Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
      Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
      Press Ctrl+C to stop
      ```

   1. The output of the command will show you the preview URL (http://localhost:1313/). Open it in your browser to preview.
   1. From this point on, you can use VSCode to edit the documents, and the browser will automatically show your editing result.
