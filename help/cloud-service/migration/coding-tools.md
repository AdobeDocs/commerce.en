---
title: AI coding tools for extensions
description: Learn how to use the AI tools for creating Commerce App Builder extensions.
feature: App Builder, Cloud
badgeSaas: label="SaaS only" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce as a Cloud Service and Adobe Commerce Optimizer projects only (Adobe-managed SaaS infrastructure)."
role: Developer
level: Intermediate
hide: yes
hidefromtoc: yes
---
# AI coding tools for extensions

When migrating to [!DNL Adobe Commerce as a Cloud Service], you can use the AI coding tools to convert existing [!DNL Adobe Commerce] PHP extensions to [!DNL Adobe Developer App Builder] extensions. You can also use these tools to create new [!DNL App Builder] extensions.

The AI coding tools provide the following benefits:

* **Enhanced development workflow**: Integrated Adobe Commerce development tools.
* **AI-powered assistance**: Context-aware code generation and debugging.
* **Commerce-specific features**: Specialized tools for Adobe Commerce App Builder development.
* **Automated workflows**: Streamlined development and deployment processes.

## Prerequisites

* One of the following coding agents:
   * [Cursor](https://cursor.com/download) (recommended)
   * [Github Copilot](https://github.com/features/copilot)
   * [Google Gemini CLI](https://github.com/google-gemini/gemini-cli)
   * [Claude Code](https://www.claude.com/product/claude-code)
* [Node.js](https://nodejs.org/en/download): LTS version
* Package Manager: [npm](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) or [yarn](https://classic.yarnpkg.com/lang/en/docs/install/#mac-stable)
* [Git](https://github.com/git-guides/install-git): For repository cloning and version control

## Installation

1. Install the latest [Adobe I/O CLI](https://github.com/adobe/aio-cli) globally:

   ```bash
   npm install -g @adobe/aio-cli
   ```

1. Install the following plugins:
   
   * [Adobe I/O CLI Commerce](https://github.com/adobe-commerce/aio-cli-plugin-commerce)
   * [Adobe I/O CLI Runtime](https://github.com/adobe/aio-cli-plugin-runtime)
   * [App Builder CLI](https://github.com/adobe/aio-cli-plugin-app-dev)

   ```bash
   aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce @adobe/aio-cli-plugin-app-dev @adobe/aio-cli-plugin-runtime
   ```

1. Clone the Commerce [integration starter kit](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/create-integration):

   ```bash
   git clone git@github.com:adobe/commerce-integration-starter-kit.git
   ```

1. Navigate to the starter kit directory:

   ```bash
   cd commerce-integration-starter-kit
   ```

1. Install the Commerce AI extensibility tools by running the interactive setup command:

   ```bash
   aio commerce extensibility tools-setup
   ```

  The setup process prompts you with configuration options. For the setup location, choose "Current directory" to install the tools in your current workspace:

  ```shell-session
  ? Where would you like to setup the tools?
  ❯ Current directory
    New directory
  ```

  When selecting the coding agent, Adobe recommends selecting `Cursor` for the best development experience:

  ```shell-session
  ? Which coding agent would you like to use?
  ❯ Cursor
    Copilot
    Gemini CLI
    Claude Code
  ```

  When selecting the package manager, Adobe recommends using `npm` for consistency:

  ```shell-session
  ? Which package manager would you like to use?
  ❯ npm
    yarn
  ```

1. After successfully installing the coding tools, the installation process configures:

   * MCP server integration for Adobe Commerce development
   * Cursor IDE rules for enhanced development experience
   * Commerce-specific development tools and workflows

   The following files are added to your workspace:

   **Cursor**

     * MCP Configuration: `.cursor/mcp.json`
     * Rules Directory: `.cursor/rules/`

   **Copilot**

     * MCP Configuration: `.vscode/mcp.json`
     * Rules Directory: `.github/copilot-instructions.md`

>[!NOTE]
>
>Before deploying your project, you will need to complete the following configuration tasks:
>
>* Log in to [Adobe Developer Console](https://developer.adobe.com/console) using the Adobe I/O CLI.
>* Create an App Builder project (see [Project setup](https://developer.adobe.com/commerce/extensibility/events/project-setup)).
>* Set up environment variables in an `.env` file.
>
>You can complete these configuration steps manually or leverage the AI coding tools to guide you through the process. See [Create an integration](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/create-integration/) for detailed configuration instructions.

## Post-installation configuration

### Log in to the Adobe I/O CLI

After installing the [!DNL Adobe I/O CLI], you must log in any time you want to use the MCP server.

```bash
aio auth login
```

To verify you are logged in, run the following command:

```bash
aio where
```

If you encounter issues, try logging out and logging back in:

```bash
aio auth logout
aio auth login
```

>[!NOTE]
>
>Some features of the MCP server will work without logging in, but the RAG (Retrieval-Augmented Generation) service will not work. The RAG service provides the AI coding agent with real-time access to the complete Adobe Commerce documentation set, enabling it to answer questions and generate code based on current Commerce development practices, APIs, and architectural patterns.
>
>In a future release, the RAG service will be accessible independently without the need to install other tools.

### Cursor

1. Restart the Cursor IDE to load the new MCP tools and configuration.

1. Verify the installation by confirming that the rules are present under the `.cursor/rules/` folder.

1. Enable the MCP server:

   * Open the Cursor MCP Settings using **Cmd+Shift+P** (macOS) or **Ctrl+Shift+P** (Windows and Linux).
   * Type **View: Open MCP Settings**
   * Locate **commerce-extensibility MCP Server** in the list
   * Toggle the server **ON** to enable the coding tools

1. Verify the server status - the Commerce extensibility MCP Server should appear as:

   ```shell-session
   Status: Connected/Active
   Server: commerce-extensibility
   Configuration: Automatically configured via .cursor/mcp.json
   ```

1. Use the following prompt to see if the agent uses the MCP server. If it does not, ask the agent explicitly to use the MCP tools available.

```shell-session
What are the differences between Adobe Commerce PaaS and Adobe Commerce as a Cloud Service when configuring a webhook that activates an App Builder runtime action?
```

### Copilot

1. Restart Visual Studio Code to load the new MCP tools and configuration.

1. Verify the installation by confirming that the `copilot-instructions.md` file exists in the `.github` folder.

1. Enable the MCP server:

   * Open the Extensions Panel by clicking the **Extensions** icon in the Activity Bar on the left sidebar or by using **Cmd+Shift+X** (macOs) or **Ctrl+Shift+X** (Windows and Linux).
   * Click [!UICONTROL **MCP SERVERS - INSTALLED**].
   * Click the gear icon next to [!UICONTROL **commerce-extensibility MCP Server**] and select [!UICONTROL **Start Server**], if the server is stopped.
   * Click the gear icon again, and select [!UICONTROL **Show Output**].

1. Verify the server status. The `MCP:commerce-extensibility` output should match the following:

   ```shell-session
   2025-11-13 12:58:50.652 [info] Starting server commerce-extensibility
   2025-11-13 12:58:50.652 [info] Connection state: Starting
   2025-11-13 12:58:50.652 [info] Starting server from LocalProcess extension host
   2025-11-13 12:58:50.657 [info] Connection state: Starting
   2025-11-13 12:58:50.657 [info] Connection state: Running

   (...)

   2025-11-13 12:58:50.753 [info] Discovered 10 tools
   ```

1. Use the following prompt to see if the agent uses the MCP server. If it does not, ask the agent explicitly to use the MCP tools available.

   ```shell-session
   What are the differences between Adobe Commerce PaaS and SaaS when configuring a webhook that activates an App Builder runtime action?
   ```

## Sample prompt

The following sample prompt creates an extension to send notifications when an order is placed.

```shell-session
Implement an Adobe Commerce SaaS extension that will send an ERP notification when a customer places an order. The ERP notification must be sent as a POST HTTP call to <ERP URL> with the following details in the request JSON body:

Order ID -> orderID
Order Total -> total
Customer Email ID -> emailID
Payment Type -> pType
```

## Prompt commands

In addition to prompting, you can use the `/search-commerce-docs` command to search documentation in conversations with your agent. For example:

```shell-session
/search-commerce-docs "How do I subscribe to Commerce events?"
```

## Best Practices

Adobe recommends following the following best practices when using the AI coding tools:

### Checklist

Before starting any development session:

* Check for `REQUIREMENTS.md`
* Verify MCP tools are working
* Review current phase and goals
* Start with sample code or scaffolded projects

During development:

* Trust the four-phase [protocol](#protocol)
* Request implementation plans for complex development
* Use MCP tools when available
* Test each feature after implementation
* Test locally first, then deploy and test again
* Leverage the coding tools for testing support
* Question unnecessary complexity
* Deploy incrementally for faster development

When starting new chat:

* Provide proper session handoff
* Reference key files with `@`
* Set clear goals for the session
* Use phase-based boundaries

### Workflow

When developing with the AI coding tools, start with sample code or scaffolded projects. This approach ensures you are building on a solid foundation rather than starting from nothing, while also optimizing your AI development workflow.

This also allows you to leverage Adobe's templates and build upon proven patterns and architectures, while keeping established directory structures and conventions.

Consult the following resources to get started:

* [Integration starter kit](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/create-integration)
* [Adobe Commerce starter kit templates](https://github.com/adobe/adobe-commerce-samples/tree/main/starter-kit)
* [Adobe I/O Events starter templates](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/io-events/getting-started-io-events)
* [App Builder sample applications](https://developer.adobe.com/app-builder/docs/resources/sample_apps)

#### Why you should use these resources

* **Proven patterns**: Starter kits embody Adobe's best practices and architectural decisions
* **Faster development**: Reduces time spent on boilerplate and configuration
* **Consistency**: Ensures your extension follows established conventions
* **Maintainability**: Easier to maintain and update when following standard patterns
* **Documentation**: Starter kits come with examples and documentation
* **Community support**: Easier to get help when using standard approaches
* **AI context efficiency**: Use familiar patterns and structures to work with, reducing the need for extensive explanations and improving code generation accuracy
* **Reduced token usage**: Reference existing patterns instead of generating everything from scratch, leading to more efficient conversations and fewer context summarizations

### Protocol

The following four-phase protocol is automatically enforced by the rules system. The tools should follow this protocol automatically when developing extensions:

* Phase 1: Requirements analysis and clarification
  * When asked clarifying questions, provide complete answers.
* Phase 2: Architectural planning and user approval
  * When presented a plan, review it carefully before approving.
* Phase 3: Code generation and implementation
* Phase 4: Documentation and validation

### Request implementation plans for complex development

For complex development involving multiple runtime actions, touchpoints, or integrations, explicitly request that the AI tools create a detailed implementation plan. When you see a high-level plan in [Phase 2](#protocol) that involves multiple components, ask for a detailed implementation plan to break it down into manageable tasks:

```shell-session
Create a detailed implementation plan for this complex development.
```

Complex Adobe Commerce extensions often involve:

* Multiple runtime actions
* Event configuration across multiple touchpoints
* Integration with external systems
* State management requirements
* Testing across multiple components

### Use MCP tools

>[!NOTE]
>
>Before using MCP tools, ensure you are [logged in to the Adobe I/O CLI](#log-in-to-the-adobe-io-cli).

The tooling defaults to MCP tools, but in certain circumstances it can use CLI commands instead. To ensure MCP tool usage, explicitly request them in your prompt.

If you see CLI commands being used and want to use MCP tools instead, use the following prompt:

```shell-session
Use only MCP tools and not CLI commands
```

* MCP tools: aio-app-deploy, aio-app-dev, aio-dev-invoke
* CLI commands: aio app deploy, aio app dev

CLI commands can be used for the following scenarios:

* Complex deployment scenarios
* Debugging specific issues
* When MCP tools have limitations
* One-off operations that do not benefit from MCP integration

### Development

Question unnecessary complexity created by the AI tools.

When unnecessary files are added (`validator.js`, `transformer.js`, `sender.js`) for simple read-only endpoints, use the following prompts:

```shell-session
Why do we need these files for a simple read-only endpoint?
Perform a root cause analysis before adding complexity
Verify if simpler solutions exist
```

### Testing

Use the following best practices when testing:

#### Test each feature after implementation

After completing development of a feature in your implementation plan, test it immediately. Early testing prevents compound issues and makes debugging easier.

* Do not wait until all features are complete
* Test incrementally to catch issues early
* Validate functionality before moving to the next feature

#### Test locally first

Always test locally first using the `aio-app-dev` tool. This provides immediate feedback and allows for faster iteration cycles, easier debugging, and no deployment overhead.

1. Start local development server:

   ```bash
   aio-app-dev
   ```

1. Test actions locally:

   ```bash
   aio-dev-invoke action-name --parameters '{"test": "data"}'
   ```

#### Deploy and test again

Once local testing is successful, deploy and test in the runtime environment. Runtime environments can have different behavior than local development.

1. Deploy to runtime:

   ```bash
   aio-app-deploy
   ```

1. Test deployed actions

1. Use web browser or direct HTTP requests

1. Check activation logs for debugging

#### Leverage the coding tools for testing support

Ask for help with testing. The tools can help with debugging, log analysis, and creating appropriate test data for your specific runtime actions.

**Test runtime actions**:

```shell-session
Help me test the customer-created runtime action running locally
```

**Debug failures**:

```shell-session
Why did the subscription-updated runtime action activation fail?
```

**Check logs**:

```shell-session
Help me check the logs for the last stock-monitoring runtime action invocation
```

**Create test payloads**:

```shell-session
Generate test data for this Commerce event
```

```shell-session
Create a test payload for the customer_save_after event
```

**Find runtime endpoints**:

```shell-session
What's the URL for this deployed action?
```

**Handle authentication**:

```shell-session
How do I authenticate with this external API?
```

**Troubleshoot**:

```shell-session
Help me debug why this action is returning 500 errors
```

### Debugging

Stop and assess when things go wrong. If you encounter issues:

* Stop and assess - Do not continue in a broken state
* Check logs - Use activation logs to identify issues
* Simplify - Remove complexity to isolate problems
* Test incrementally - Fix one issue at a time
* Validate - Test each fix before proceeding

### Deployment

Use the following best practices when deploying:

#### Deploy incrementally

Deploy only modified actions to speed up development. This approach reduces the risk of breaking existing functionality and provides quicker feedback on changes.

* Use MCP tools to deploy specific actions

  ```bash
  aio-app-deploy --actions action-name
  ```

* Deploy individual actions after testing locally
* Deploy incrementally and avoid full application deployments during development

#### Runtime cleanup

After major changes, leverage the tools to clean up orphaned actions. Let the AI tooling handle the cleanup process systematically. It can efficiently identify orphaned actions, verify their status, and safely remove them without manual intervention.

```shell-session
Help me identify and clean up orphaned runtime actions
```

Request the AI tooling to list deployed actions and identify unused ones

```shell-session
List all deployed actions and identify which ones are no longer needed
```

Have the AI tools remove orphaned actions using appropriate commands

```shell-session
Remove the orphaned actions that are no longer part of the current implementation
```

### Monitoring

Use the following best practices when monitoring your application:

#### Watch for context quality indicators

* **Good context**: AI remembers recent decisions, references correct files
* **Poor context**: AI asks for previously provided info, repeats resolved issues

#### Track development velocity

* **High velocity**: Clear progress, minimal clarification needed
* **Low velocity**: Repeated explanations, AI confusion, slow progress

#### Monitor cost efficiency

Track token usage patterns:

* **Efficient**: Low token usage, few context summarizations
* **Inefficient**: High token usage, multiple summarizations, repeated work

## What to avoid

Avoid the following anti-patterns when using the AI coding tools:

* **Do not skip the clarification phase** - Always ensure Phase 1 is completed before implementation.
* **Do not skip testing after each feature** - Test incrementally, don't wait until everything is complete.
* **Do not add complexity without root cause analysis** - Question unnecessary file additions and request proper investigation.
* **Do not declare success without real data testing** - Always test with actual data, not just edge cases.
* **Do not forget runtime cleanup** - Always clean up orphaned actions after major changes.
