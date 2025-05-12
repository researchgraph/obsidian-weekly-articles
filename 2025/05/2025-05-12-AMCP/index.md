# Building a Simple Internet Search App Using Anthropic Model Context Protocol

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
   - After logging in, go to https://api-dashboard.search.brave.com/app/keys
   - Click on "Create New API Key"
   - Name your key (e.g., "Claude Integration")
   - Select the appropriate services (Web Search is what we need for this tutorial)
   - Copy your new API key and store it securely—you'll need it when configuring Claude

3. **Understand Usage Limits**:
   - Free tier accounts typically have daily or monthly query limits
   - Take note of these limits to avoid unexpected service interruptions
   - Consider upgrading to a paid plan if you anticipate heavy usage

The API key serves as your authentication token when Claude makes requests to Brave Search on your behalf. Never share this key publicly, as others could use it and consume your search quota.

## Configuring Claude Desktop App for AMCP

Now that you have your Brave Search API key, let's configure Claude to use it. We'll cover two methods: the user interface approach and manual JSON configuration.

### Method 1: Using the Claude Desktop App UI (Recommended for Beginners)

1. Open the Claude desktop app
2. Click on the gear icon in the lower-left corner to access Settings
3. Navigate to the "Developer" tab
4. Look for the "Model Context Protocol" or "MCP" section
5. Click "Add Service" and fill in the following details:
   - Service Name: "Brave Search"
   - Service Type: "Web Search"
   - API Endpoint: "https://api.search.brave.com/mcp/v1/web"
   - Authentication Type: "Bearer Token"
   - Token: [Paste your API key here]
6. Configure additional parameters:
   - Results Count: 5 (adjust as needed)
   - Safe Search: Moderate (options: off, moderate, strict)
7. Click "Test Connection" to verify everything works
8. Save your configuration

### Method 2: Manual Configuration via JSON File (Advanced Method)

For more technical users who prefer direct configuration:

1. Close the Claude desktop app if it's running
2. Navigate to the configuration directory:
   - Windows: `%APPDATA%\Claude\`
   - macOS: `~/Library/Application Support/Claude/`
   - Linux: `~/.config/Claude/`
3. Create or edit a file named `claude_desktop_config.json`
4. Add the following JSON structure (replace YOUR_API_KEY_HERE with your actual API key):

```json
{
  "mcp_services": {
    "brave_search": {
      "name": "Brave Search",
      "endpoint": "https://api.search.brave.com/mcp/v1/web",
      "auth": {
        "type": "bearer",
        "token": "YOUR_API_KEY_HERE"
      },
      "parameters": {
        "count": 5,
        "safe_search": "moderate"
      }
    }
  }
}
```

5. Save the file and restart the Claude desktop app

### Comparison of Methods

The UI method is more user-friendly and provides immediate feedback, making it ideal for beginners. The JSON method offers more precise control and can be easily backed up or version-controlled. Choose the approach that best fits your comfort level with technical configuration.

## Testing Your Integration

Now that you've set up the integration, it's time to test it! Here are some effective ways to verify everything is working correctly:

1. **Start with a Current Events Query**:
   - Ask Claude: "What are the latest developments in renewable energy technology?"
   - Since this likely includes information beyond Claude's knowledge cutoff, it should trigger a search

2. **Check Specific Recent Facts**:
   - Try asking about recent sports scores, stock prices, or news events
   - Example: "Who won yesterday's match between [Team A] and [Team B]?"

3. **Look for Search Indicators**:
   - When Claude performs a search, you should see a visual indicator or message showing that it's querying Brave Search
   - The response should include attribution to Brave Search or otherwise indicate that external information was used

4. **Troubleshooting Common Issues**:
   - If searches aren't working, check your API key validity
   - Ensure your internet connection is stable
   - Verify that you haven't exceeded your API usage limits
   - Try restarting the Claude app

A successful test will show Claude smoothly incorporating search results into its responses, providing you with up-to-date information while maintaining its helpful, conversational tone.

## Example Use Cases

Now that your integration is working, here are some valuable ways to use this new capability:

### Research Assistance
- Ask Claude to find recent studies or papers on specific topics
- Request summaries of current research trends
- Compare different viewpoints on emerging technologies

### Fact-Checking
- Verify claims by asking Claude to search for supporting or contradicting evidence
- Check statistics or quotations against current sources
- Validate information from social media or news articles

### Finding Current Information
- Get the latest news on specific topics
- Check current prices, rates, or statistics
- Find information about recent events or developments

### Educational Queries
- Support learning with up-to-date information on any subject
- Find teaching resources or examples
- Explore different perspectives on academic topics

## Best Practices

To get the most out of your Claude + Brave Search integration, follow these best practices:

### Crafting Effective Search Queries
- Be specific about what information you need
- Include relevant time frames or date ranges when appropriate
- Use clear, concise language to help Claude understand your search intent

### Understanding Limitations
- Remember that search results depend on what's available online
- Not all information may be indexed by Brave Search
- Complex or ambiguous queries might yield less relevant results

### Privacy Considerations
- Be mindful that search queries are sent to Brave Search
- While Brave is privacy-focused, consider omitting personal details from searches
- Review Brave's privacy policy to understand how your data is handled

### When to Use Search vs. Claude's Built-in Knowledge
- Use search for current events, recent developments, or specific facts
- Rely on Claude's built-in knowledge for conceptual understanding, analysis, or historical information
- Combine both capabilities for comprehensive responses on complex topics

## Conclusion and Next Steps

Congratulations! You've successfully integrated Claude with Brave Search using Anthropic Model Context Protocol. This simple yet powerful setup transforms Claude into a more versatile assistant, capable of providing you with current information from across the web.

The integration we've built today is just the beginning. As AMCP continues to evolve, you can explore additional integrations with other services. Some possibilities include:

- Connecting to weather services for real-time forecasts
- Integrating with knowledge bases for specialized information
- Adding image search capabilities
- Exploring news APIs for curated current events

By starting with this simple integration, you've taken an important first step into the expanding ecosystem of AI-powered tools. The combination of Claude's intelligence with external data sources opens up exciting possibilities for productivity, learning, and discovery.

Remember to periodically check for updates to both Claude and Brave Search, as new features and improvements may enhance your experience even further. Happy searching!