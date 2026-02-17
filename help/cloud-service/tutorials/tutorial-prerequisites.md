---
title: Ratings extension tutorial prerequisites
description: Learn the prerequisites for the ratings extension lab.
feature: App Builder, Cloud
role: Developer
level: Intermediate
hide: yes
hidefromtoc: yes
---
# Ratings extension tutorial prerequisites (Beta)

>[!NOTE]
>
>The AI tooling used in this tutorial is currently in Beta and could include bugs or other issues.

This page lists the prerequisites and setup steps for [!DNL Adobe Commerce as a Cloud Service] tutorials, such as the [ratings extension tutorial](./ratings-extension.md).

## Adobe Commerce as a Cloud Service prerequisites

* Install the [!DNL Adobe I/O CLI]

   ```bash
   npm install -g @adobe/aio-cli
   ```

* Install the [Adobe I/O CLI Commerce](https://github.com/adobe-commerce/aio-cli-plugin-commerce), [Adobe I/O CLI Runtime](https://github.com/adobe/aio-cli-plugin-runtime), and [App Builder CLI](https://github.com/adobe/aio-cli-plugin-app-dev) plugins:

   ```bash
   aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce @adobe/aio-cli-plugin-app-dev @adobe/aio-cli-plugin-runtime
   ```

* Download an AI-assisted IDE, such as [Cursor](https://cursor.com/download) (recommended), other IDEs, such as Claude Code, Gemini CLI, or Copilot are also supported, but could require modifications to the prompts and other steps in the tutorial.

### Adobe Developer Console prerequisites

1. Navigate to the [Adobe Developer Console](https://developer.adobe.com/console){target="_blank"}.
1. Log in using your email and password.

#### Create a new project

1. Navigate to [Adobe Developer Console](https://developer.adobe.com/).
1. Click [!UICONTROL **Create project from a template**].
1. Select the [!UICONTROL **App Builder**] template.
1. Enter a [!UICONTROL **Project Title**] and [!UICONTROL **App Name**].
1. Ensure the **[!UICONTROL Include Runtime]** checkbox is marked.

   ![Adobe Developer Console project creation with App Builder template selected](../assets/app-builder-template.png){width="600" zoomable="yes"}

1. Click [!UICONTROL **Save**].

#### Add APIs to the workspace

1. Click the [!UICONTROL **Stage**] workspace and then repeat the following steps for each API.

   ![Stage workspace with Add Service option for APIs](../assets/add-apis-workspace.png){width="600" zoomable="yes"}

1. Click [!UICONTROL **Add Service**] and select [!UICONTROL **API**].

1. Select one of the following APIs. You will need to repeat this process for each API listed below:

   * [!UICONTROL **Adobe Services**] filter:
      * [!UICONTROL **I/O Management API**]
      * [!UICONTROL **I/O Events**] API
   * [!UICONTROL **Experience Cloud**] filter:
      * [!UICONTROL **Adobe I/O Events for Adobe Commerce**] API

1. Click [!UICONTROL **Next**].

1. Click[!UICONTROL **Save configured API**].

1. Repeat the previous steps until all APIs are added to the workspace.

   ![Workspace showing all required APIs successfully added](../assets/apis-added.png){width="600" zoomable="yes"}

### Configure the Adobe I/O CLI

1. Clear any existing configuration:

   ```bash
   aio config clear
   ```

   Log in using the [!DNL Adobe I/O CLI]:

   ```bash
   aio auth login -f
   ```

1. Select your organization, project, and workspace, using each of the following commands:

   ```bash
   aio console org select
   ```

   ```bash
   aio console project select
   ```

   ```bash
   aio console workspace select
   ```

   ![Terminal showing Adobe I/O CLI organization project and workspace selection](../assets/cli-configuration.png){width="600" zoomable="yes"}

### Clone the integration starter kit

Clone the Commerce integration starter kit repository and prepare your project:

```bash
git clone https://github.com/adobe/commerce-integration-starter-kit.git extension
cd extension
```

![Terminal output showing the git clone command for the Commerce integration starter kit](../assets/clone-starter-kit.png){width="600" zoomable="yes"}

### Create an .env file

Create your environment configuration file:

```bash
cp env.dist .env
```

Open the `.env` file in a text editor and add the following OAuth credentials:

```shell-session
OAUTH_CLIENT_ID=
OAUTH_CLIENT_SECRET=
OAUTH_TECHNICAL_ACCOUNT_ID=
OAUTH_TECHNICAL_ACCOUNT_EMAIL=
OAUTH_ORG_ID=
```

You can copy these values from the **[!UICONTROL Credential details]** page in [Developer Console](https://developer.adobe.com/) by clicking the **[!UICONTROL OAuth Server-to-Server]** tab on your workspace.

![OAuth Server-to-Server credentials page in Adobe Developer Console](../assets/oauth-credentials.png){width="600" zoomable="yes"}

#### Add the Commerce configuration

Add the following Commerce instance details to your `.env` file:

```shell-session
COMMERCE_BASE_URL=
COMMERCE_GRAPHQL_ENDPOINT=
```

To find these values:

1. Navigate to [Commerce Cloud Service instances](https://experience.adobe.com/#/@commerce/commerce/cloud-service/instances).
1. Click the information icon next to your instance.
1. Copy the REST endpoint as `COMMERCE_BASE_URL`.
1. Copy the GraphQL endpoint as `COMMERCE_GRAPHQL_ENDPOINT`.

#### Set event prefix

Set a temporary value for the event prefix:

```shell-session
EVENT_PREFIX=test
```

### Download workspace configuration

Run the following command to download the workspace configuration file:

```bash
aio console workspace download workspace.json
```

Copy the workspace configuration file to the `scripts` directory:

```bash
cp workspace.json scripts/
```

### Connect local workspace to remote workspace

Link your local project to the remote workspace:

```bash
aio app use workspace.json -m
```

![Terminal showing successful workspace connection with aio app use command](../assets/connect-workspace.png){width="600" zoomable="yes"}

### Install extensibility AI tools

Update the Cursor rules file and MCP configuration to include the `commerce-extensibility-tools` package.

1. Set up the AI-assisted development tools in the `extension` folder using the following commands:

   ```bash
   cd extension
   ```

   ```bash
   aio commerce extensibility tools-setup
   ```

   ![Terminal showing AI extensibility tools setup command output](../assets/install-ai-tools.png){width="600" zoomable="yes"}
## Storefront prerequisites

The following items are required to complete the [storefront](./ratings-extension.md#connect-to-the-storefront) section of [this tutorial](./ratings-extension.md) and display product ratings in your store.

* Install [!DNL Node.js] (version `22.x.x`) and npm (`9.0.0` or higher). Verify your installation:

   ```bash
   node --version
   npm --version
   ```

* Install [Git](https://git-scm.com). Verify your installation:

   ```bash
   git --version
   ```

* Bash shell
  * macOS/Linux: No installation required
  * Windows: Use [Git Bash](https://git-scm.com/install) or [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install)

* [Google Chrome](https://www.google.com/chrome/) - Required for testing the storefront

### Clone the storefront repository

Open your terminal and clone the repository:

```bash
git clone --branch agentic-dev https://github.com/hlxsites/aem-boilerplate-commerce.git storefront
cd storefront
```

### Install dependencies

Install the project dependencies:

```bash
npm install
```
