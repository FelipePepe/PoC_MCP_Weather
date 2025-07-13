# PoC MCP Weather Server

A Proof of Concept implementation of a Model Context Protocol (MCP) server that provides weather information services to AI clients.

## Overview

This MCP server exposes a single weather tool that allows AI clients to retrieve real-time weather data for any city. The server acts as a bridge between language models and external weather APIs through the standardized MCP interface.

## Architecture

The system consists of three main components:

- **MCP Server**: Handles protocol communication and tool registration
- **Weather Tool**: Processes city queries and fetches weather data
- **External APIs**: Open-Meteo services for geocoding and weather data

## Installation

```bash
npm install
```

## Usage

Start the MCP server:

```bash
node init.js
```

The server will listen for MCP client connections via stdio transport.

## Available Tools

### fetch-weather

Retrieves weather information for a specified city.

**Parameters:**
- `city` (string): Name of the city to get weather for

**Returns:**
- Weather data including temperature, precipitation, humidity, and other meteorological information
- Error message if city is not found

## Implementation Details

The server implementation follows a two-stage API integration pattern:

1. **Geocoding**: Converts city names to coordinates using Open-Meteo Geocoding API
2. **Weather Retrieval**: Fetches weather data using coordinates from Open-Meteo Weather API

## Dependencies

- `@modelcontextprotocol/sdk`: MCP protocol implementation
- `zod`: Schema validation for inputs

## API Endpoints Used

- Geocoding: `https://geocoding-api.open-meteo.com/v1/search`
- Weather: `https://api.open-meteo.com/v1/forecast`

## Error Handling

The tool includes comprehensive error handling for:
- Invalid or non-existent city names
- API request failures
- Malformed responses

## Example Response

```json
{
  "content": [
    {
      "type": "text",
      "text": "{\n  \"hourly\": {\n    \"temperature_2m\": [...],\n    \"precipitation\": [...],\n    \"relative_humidity_2m\": [...]\n  }\n}"
    }
  ]
}
```
```

**Notes**

This documentation covers the complete PoC MCP Weather server implementation. [2](#1-1)  The server registers a single weather tool that performs geocoding followed by weather data retrieval. [3](#1-2)  The server uses stdio transport for client communication, making it compatible with various MCP clients.

Wiki pages you might want to explore:
- [Overview (FelipePepe/PoC_MCP_Weather)](/wiki/FelipePepe/PoC_MCP_Weather#1)
```

