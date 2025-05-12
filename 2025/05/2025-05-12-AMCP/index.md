# Building a Simple Internet Search App Using Anthropic Model Context Protocol

![](<images/amcp cover image.png>)
Created using DALL.E on 12 May 2025

## Author
Aditya Arora (ORCID: 0009-0006-5800-1198)

## Introduction

The Anthropic Model Context Protocol (AMCP) is an open standard protocol that enables developers to provide context to LLMs. It represents a significant advancement in how we interact with AI assistants. By connecting Claude with external tools and services, AMCP enhances Claude's capabilities beyond its built-in knowledge. Today, we'll explore how to create a simple yet powerful search application by connecting Claude's desktop app with Brave Search.
This integration allows Claude to perform real-time internet searches, providing you with current information beyond Claude's knowledge cutoff date. Whether you're researching a topic, fact-checking information, or simply exploring the web, this integration transforms Claude into an even more powerful assistant.
In this tutorial, we'll walk through every step of setting up this integration, from creating a Brave Search account to configuring Claude for seamless search capabilities.

## Understanding the Components

Before diving into the setup process, let's understand the key components involved:

**Claude Desktop App**: Claude is Anthropic's conversational AI assistant that can understand complex requests and generate thoughtful responses. The desktop version brings Claude's capabilities to your computer as a standalone application.

**Brave Search MCP Server**: Brave Search provides privacy-focused web search results. Their Model Context Protocol (MCP) server allows AI assistants like Claude to access their search capabilities through a standardized interface.

**Anthropic Model Context Protocol (AMCP)**: This protocol enables Claude to communicate with external services like Brave Search while maintaining context throughout the conversation. It creates a structured format for data exchange between Claude and third-party tools.

The magic happens when these components work together: you ask Claude a question, Claude recognizes when it needs current information, it queries Brave Search through AMCP, and then provides you with up-to-date answers.

## Prerequisites

Before starting the setup process, make sure you have:

1. **Claude Desktop App**: Download and install the latest version from Anthropic's official website. The app is available for Windows, macOS, and Linux.

2. **Brave Search Account**: You'll need a free account to access their API. 

## Setting Up Brave Search API

Let's start by obtaining your Brave Search API key:

1. **Create a Brave Search Account**:
   - Navigate to https://api-dashboard.search.brave.com/
   - Click on "Sign Up" if you're new, or "Log In" if you already have an account
   - Complete the registration process with your email and password
   - Verify your email address through the link sent to your inbox

2. **Obtain Your API Key**:
   - Select and subscribe to a appropriate services (Web Search is what we need for this tutorial)
   - Go to https://api-dashboard.search.brave.com/app/keys
   - Click on "Create New API Key"
   - Name your key (e.g., "Claude Integration")
   - Copy your new API key and store it securely—you'll need it when configuring Claude

![](<images/Screenshot 2025-05-12 at 10.31.30 am.png>)

The API key serves as your authentication token when Claude makes requests to Brave Search on your behalf.


## Configuring Claude Desktop App for AMCP

Now that you have your Brave Search API key, let's configure Claude to use it. 

### Steps:

1. Open the Claude desktop app and go to Settings
2. Navigate to the "Developer" tab
3. Click on Edit configuration. It will create a ‘claude_desktop_config.json’ file at the proper location. 
4. Or you can manually create this by navigating to the configuration directory:
 - Windows: %APPDATA%\Claude\
 - macOS: ~/Library/Application Support/Claude/
 - Linux: ~/.config/Claude/
6. Add the following JSON structure (replace YOUR_API_KEY_HERE with your actual API key):
```
{
  "mcpServers": {
    "brave-search": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-brave-search"
      ],
      "env": {
        "BRAVE_API_KEY": "YOUR_API_KEY_HERE"
      }
    }
  }
}
```
Save and restart Claude desktop app

## Testing Your Integration

Now that you've set up the integration, it's time to test it! Here are some effective ways to verify everything is working correctly:

1. **Check Specific Recent Facts**:
   - Try asking about recent sports scores, stock prices, or news events
   - Example: "Who won yesterday's match between [Team A] and [Team B]?"

2. **Look for Search Indicators**:
   - When Claude performs a search, you should see a visual indicator or message showing that it's querying Brave Search

    ![](<images/Screenshot 2025-05-12 at 2.14.12 pm.png>)

   - The response should include attribution to Brave Search or otherwise indicate that external information was used

   ![](<images/Screenshot 2025-05-12 at 2.19.15 pm.png>)

3. **Troubleshooting Common Issues**:
   - If searches aren't working, check your API key validity
   - Ensure your internet connection is stable
   - Verify that you haven't exceeded your API usage limits
   - Try restarting the Claude app



## Conclusion and Next Steps

Congratulations! You've successfully integrated Claude with Brave Search using Anthropic Model Context Protocol. This simple yet powerful setup transforms Claude into a more versatile assistant, capable of providing you with current information from across the web.

The integration we've built today is just the beginning. As AMCP continues to evolve, you can explore additional integrations with other services. Some possibilities include:

- Integrating with knowledge bases for specialized information
- Adding image search capabilities
- Exploring news APIs for curated current events

By starting with this simple integration, you've taken an important first step into the expanding ecosystem of AI-powered tools. The combination of Claude's intelligence with external data sources opens up exciting possibilities for productivity, learning, and discovery.

Remember to periodically check for updates to both Claude and Brave Search, as new features and improvements may enhance your experience even further. Happy searching!