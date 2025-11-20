---
title: Ratings extension tutorial prerequisites
description: Learn the prerequisites for the ratings extension lab.
role: Developer
hide: yes
hidefromtoc: yes
---
# Ratings extension tutorial prerequisites

This page lists the generic prerequisites and other manual setup steps for tutorials using [!DNL Adobe Commerce as a Cloud Service] and your storefront, such as the [ratings extension tutorial](./ratings-extension.md).

## Extension prerequisites

Before you begin, complete the following prerequisites:

* Install the [!DNL Adobe I/O CLI]

   ```bash
   npm install -g @adobe/aio-cli
   ```

* Install the Commerce plugin

  ```bash
  aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce
  ```

* Download an AI-assisted IDE, such as [Cursor](https://cursor.com/download) (recommended), other IDEs, such as Claude Code, Gemini CLI, or Copilot are also supported, but could require modifications to the prompts and other steps in this tutorial.
<!-- 
### Create a new project on Adobe Developer Console

1. Navigate to [Adobe Developer Console](https://developer.adobe.com/).
1. Click [!UICONTROL **Create project from a template**].
1. Select the [!UICONTROL **App Builder**] template.
1. Enter a [!UICONTROL **Project Title**] and [!UICONTROL **App Name**].
1. Ensure the **[!UICONTROL Include Runtime]** checkbox is marked.

   ![Create project with App Builder template](./assets/app-builder-template.png){width="600" zoomable="yes"}

1. Click **Save**.

### Add APIs to the workspace

1. Click the [!UICONTROL **Stage**] workspace and then repeat the following steps for each API.

   ![APIs added to workspace](./assets/add-apis-workspace.png){width="600" zoomable="yes"}

1. Click [!UICONTROL **Add Service**] and select [!UICONTROL **API**].

1. Select the [!UICONTROL **Adobe Services**] filter and select one of the following APIs:

   * [!UICONTROL **I/O Management API**]
   * [!UICONTROL **I/O Events**]

1. Select the [!UICONTROL **Experience Cloud**] filter and select one of the following APIs:

   * [!UICONTROL **Adobe I/O Events for Adobe Commerce**]

1. Click [!UICONTROL **Next**].

1. Click[!UICONTROL **Save configured API**].

1. Repeat the previous steps until all APIs are added to the workspace.

   ![APIs added to workspace](./assets/apis-added.png){width="600" zoomable="yes"} -->

### Log in to the Adobe Developer Console

1. Navigate to the [Adobe Developer Console](https://developer.adobe.com/console){target="_blank"}.
1. If you are already logged in, click your profile icon in the top-right and click the **Sign out** button.
1. Log in using your email and password.
1. If you are prompted to add a secondary email address or phone number, click **Not now**.
1. When you are prompted to select an organization profile, select **Adobe Commerce Labs**.

   ![select-organization](./assets/select-org.png){width="600" zoomable="yes"}

1. If you are prompted to accept the terms and conditions, click the link to read the terms, then click **Accept and continue**.

   ![accept-terms](./assets/accept-terms.png){width="600" zoomable="yes"}

### Configure the AIO CLI

1. Clear the existing configuration:

   ```bash
   aio config clear
   ```

   Log in using the AIO CLI:

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

   ![CLI configuration](./assets/cli-configuration.png){width="600" zoomable="yes"}

### Clone integration starter kit

Clone the Commerce integration starter kit repository and prepare your project:

```bash
git clone --branch adl https://github.com/adobe/commerce-integration-starter-kit.git extension
cd extension
```

![Clone starter kit](./assets/clone-starter-kit.png){width="600" zoomable="yes"}

### Create the .env file

Create your environment configuration file:

```bash
cp env.dist .env
```

<!-- Open the `.env` file in a text editor and add the following OAuth credentials:

```text
OAUTH_CLIENT_ID=
OAUTH_CLIENT_SECRET=
OAUTH_TECHNICAL_ACCOUNT_ID=
OAUTH_TECHNICAL_ACCOUNT_EMAIL=
OAUTH_ORG_ID=
```

You can copy these values from the **[!UICONTROL Credential details]** page in [Developer Console](https://developer.adobe.com/) by clicking the **[!UICONTROL OAuth Server-to-Server]** tab on your workspace.

![OAuth credentials](./assets/oauth-credentials.png){width="600" zoomable="yes"}

#### Add the Commerce configuration

Add the following Commerce instance details to your `.env` file:

```text
COMMERCE_BASE_URL=
COMMERCE_GRAPHQL_ENDPOINT=
```

To find these values:

1. Go to [Commerce Cloud Service instances](https://experience.adobe.com/#/@commerce/commerce/cloud-service/instances).
1. Click the information icon next to your assigned seat.
1. Copy the REST endpoint as `COMMERCE_BASE_URL`.
1. Copy the GraphQL Endpoint as `COMMERCE_GRAPHQL_ENDPOINT`.

#### Set event prefix

Set a temporary value for the event prefix:

```text
EVENT_PREFIX=test
```
 -->

### Download workspace configuration

Run the following command to download the workspace configuration file:

```bash
aio console workspace download workspace.json
```

### Connect local workspace to remote workspace

Link your local project to the remote workspace:

```bash
aio app use workspace.json -m
```

![Connect to workspace](./assets/connect-workspace.png){width="600" zoomable="yes"}

### Install extensibility AI tools

1. Set up the AI-assisted development tools in the `extension` folder using the following commands:

   ```bash
   cd extension
   ```

   ```bash
   aio commerce extensibility tools-setup
   ```

   ![Install AI tools](./assets/install-ai-tools.png){width="600" zoomable="yes"}

## Storefront prerequisites

The following items are required to complete the [storefront](#connect-to-the-storefront) section of this tutorial and see the product ratings in your store.
<!-- 
* Install [!DNL Node.js] (version `22.x.x`) and npm (`9.0.0` or higher). Verify your installation:

   ```bash
   node --version
   npm --version
   ```

* Install [Git](https://git-scm.com) (Optional) - Required only if [cloning the repository directly](#option-a-clone-the-repository-recommended)(recommended), not needed if you [download the zip file](#option-b-download-the-zip-file). Verify your installation:

  ```bash
  git --version
  ```

* Bash shell
  * macOS/Linux: No installation required
  * Windows: Use [Git Bash](https://git-scm.com/install) or [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install).

* [Google Chrome](https://www.google.com/chrome/) - Required for testing the storefront -->

### Get the project files

You can obtain the project files in one of two ways:

<!-- 
#### Option A: Clone the repository (recommended) -->

If you have [!DNL Git] installed, open your terminal and clone the repository:

```bash
git clone --branch agentic-dev https://github.com/hlxsites/aem-boilerplate-commerce.git storefront
cd storefront
```

<!-- #### Option B: Download the zip file

If you don't have [!DNL Git] installed:

1. Download the project zip file from: [https://github.com/hlxsites/aem-boilerplate-commerce/archive/refs/heads/agentic-dev.zip](https://github.com/hlxsites/aem-boilerplate-commerce/archive/refs/heads/agentic-dev.zip)
1. Extract the zip file to a folder on your machine.
1. Open your terminal and navigate into the unzipped folder:

   ```bash
   cd path/to/aem-boilerplate-commerce-agentic-dev
   ``` -->

### Install root dependencies

Install the main project dependencies:

```bash
npm install
```

This will install all the necessary packages for the storefront application.

### Install MCP server dependencies

Navigate to the MCP server directory and install its dependencies:

```bash
cd mcp-server
npm install
cd ..
```

<!-- ### Configure environment variables

The MCP server requires certain environment variables to connect to the RAG service.

Create a `.env` file in the `mcp-server` directory:

```bash
cd mcp-server
cp env.example .env
```

Edit the `.env` file and add the following values (we'll provide the actual URL during the lab):

```env
RAG_MODE=worker
WORKER_RAG_URL=<provided-during-lab>
```
 -->

### Enable MCP in Cursor

The Model Context Protocol (MCP) server provides AI agents with access to [!DNL Adobe Commerce] Storefront documentation.

#### Open Cursor MCP settings

![Open Cursor MCP Settings](./assets/cursor-mcp-settings.png){width="600" zoomable="yes"}

1. Open [!DNL Cursor]
1. Go to **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**

#### Enable and configure MCP features

The project includes an MCP configuration file at `.cursor/mcp.json`. This file should already be configured to use the local MCP server.

Verify the MCP configuration:

1. Ensure the "commerce-documentation-rag" server is listed and enabled

The configuration should look similar to this:

![MCP Configuration](./assets/mcp-configuration.png){width="600" zoomable="yes"}

>[!NOTE]
>
>The `start-mcp.sh` script will automatically load the environment variables from your `.env` file in the `mcp-server` directory.

#### Restart Cursor

After enabling MCP and configuring the server:

1. Quit [!DNL Cursor] completely
1. Reopen [!DNL Cursor] and open the `aem-boilerplate-commerce` project

#### Verify MCP connection

Check that the MCP server is running correctly:

1. Open a new chat in [!DNL Cursor]
1. Look for an indicator showing the MCP server is connected (usually in the chat interface)
1. Try asking a question like: "Search the storefront docs for information about slots"

If the MCP server is working, you should see relevant documentation results.

![MCP Connection Verified](./assets/mcp-connection-verified.png){width="600" zoomable="yes"}
