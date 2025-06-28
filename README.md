# War Tycoon Trading Database (WTTD) API <p align="center">
  <img src="https://wttd.trade/logo.png" alt="WTTD Logo" width="100"/>
</p>

API documentation for WTTD

## Table of Contents

- [Overview](#overview)
- [Base URL](#base-url)
- [Authentication](#authentication)
- [Rate Limiting](#rate-limiting)
- [Endpoints](#endpoints)
  - [Search Skins](#search-skins)
  - [Price History](#price-history)
  - [Top Items](#top-items)
- [Response Format](#response-format)
- [Examples](#examples)
- [Error Handling](#error-handling)

## Overview

The War Tycoon Trading Database API provides endpoints for finding skin information, viewing price history, and getting top items. This is a simple REST API with three main endpoints.

### Features

- Search for skins by name
- Get price history data
- View top items filtered by medals or robux
- Simple query-based interface
- JSON response format

## Base URL

```
https://wttd.trade/api
```

### Available Endpoints:
- `/search?q=<skin name>` - Search for skins by name
- `/items/` - Get all items
- `/items/price-history?limit=<number>` - Get price history data (limit determines number of items, each with full history)
- `/top-items?filter=<medals or robux>` - Get top items (filter is optional)

## Authentication

Currently, no authentication is required for any of the endpoints.

## Rate Limiting

Please be respectful with your requests. While no specific rate limits are documented, avoid making excessive requests to prevent overloading the service.

# Endpoints

## Search Skins

Search for skins by name in the War Tycoon Trading Database.

```http
GET /search?q={skin_name}
```

**Parameters:**
- `q` (string, required): The name or partial name of the skin to search for

**Example Request:**
```
GET https://wttd.trade/api/search?q=dragon
```
**Example Response:**
```json
[
  {
    "id": "skins-244",
    "name": "Dragon Skin",
    "description": "Daily Spin",
    "rarity": "Special",
    "limited": false,
    "robux_price": 0,
    "community_price": "Untradable",
    "animated": false,
    "bullet_VFX": false,
    "type": "skins",
    "demand": 0
  }
]
```
```
```

### Query Examples

- Search for a specific skin/item/vehicle: `?q=wood` | `?q=F-117` | `?q=AA-12`
- Search by partial name: `?q=SEP`

**Note:** The query parameter should be URL-encoded when it contains spaces or special characters.

## All Items

Get all items from the War Tycoon Trading Database.

```http
GET /items/
```

**Parameters:**
- None required

**Example Request:**
```
GET https://wttd.trade/api/items/
```

**Example Response:**
```json
[
  {
    "id": "vehicles-285",
    "name": "F-117N Seahawk",
    "description": "Limited time plane.",
    "rarity": "Mythic",
    "limited": true,
    "robux_price": 1299,
    "community_price": "108.6k",
    "animated": false,
    "bullet_VFX": false,
    "type": "vehicles",
    "demand": 8.1
  },
  {
    "id": "skins-255",
    "name": "Mosaic",
    "description": "A unique skin pattern.",
    "rarity": "Epic",
    "limited": false,
    "robux_price": 199,
    "community_price": "249",
    "animated": false,
    "bullet_VFX": false,
    "type": "skins",
    "demand": 7.2
  }
]
```

## Price History

Get price history data for items in the War Tycoon Trading Database.

```http
GET /items/price-history?limit={number}
```

**Parameters:**
- `limit` (number, required): The number of items to return (each item includes its complete price history)

**Example Request:**
```
GET https://wttd.trade/api/items/price-history?limit=1
```

**Example Response:**
```json
[
  {
    "id": "skins-255",
    "name": "Mosaic",
    "history": [
      {
        "price": 199,
        "date": "2025-05-29T04:12:26.000Z",
        "priceString": "199"
      },
      {
        "price": 250,
        "date": "2025-06-27T20:10:07.000Z",
        "priceString": "250"
      },
      {
        "price": 249,
        "date": "2025-06-28T00:03:40.000Z",
        "priceString": "249"
      },
      {
        "price": 251,
        "date": "2025-06-28T02:59:54.000Z",
        "priceString": "251"
      },
      {
        "price": 249,
        "date": "2025-06-28T03:26:57.000Z",
        "priceString": "249"
      }
    ],
    "latest_date": "2025-06-28 03:26:57"
  }
]
```

## Top Items

Get top items from the War Tycoon Trading Database.

```http
GET /top-items?filter={currency_type}
```

**Parameters:**
- `filter` (string, optional): Filter by currency type - either "medals" or "robux". If not provided, returns all top items.

**Example Request:**
```
GET https://wttd.trade/api/top-items
```

**Example Response:**
```json
[
  {
    "id": "vehicles-285",
    "name": "F-117N Seahawk",
    "description": "Limited time plane.",
    "rarity": "Mythic",
    "limited": true,
    "robux_price": 1299,
    "community_price": "108.6k",
    "animated": false,
    "bullet_VFX": false,
    "type": "vehicles",
    "demand": 8.1
  },
  {
    "id": "Vehicles-297",
    "name": "TOS-01 Buratino",
    "description": "Limited time operation 2025.",
    "rarity": "Mythic",
    "limited": true,
    "robux_price": 1299,
    "community_price": "102.8k",
    "animated": false,
    "bullet_VFX": false,
    "type": "Vehicles",
    "demand": 8.2
  },
  {
    "id": "vehicles-137",
    "name": "Mi24 Superhind",
    "description": "Limited time helicopter.",
    "rarity": "Mythic",
    "limited": true,
    "robux_price": 1199,
    "community_price": "157.1k",
    "animated": false,
    "bullet_VFX": false,
    "type": "vehicles",
    "demand": 9.8
  }
]
```

# Response Format

The API returns JSON responses. For all endpoints:

- **Success**: Returns an array of objects matching the request
- **No Results**: Returns an empty array `[]` 
- **Error**: Returns an error object with details

## Response Object Structures

### Search Endpoint - Skin Object
```json
{
  "id": "string",           // Unique identifier (e.g., "skins-123")
  "name": "string",         // Full name of the skin
  "description": "string",  // Item description
  "rarity": "string",       // Rarity level (Epic, Mythic, Legendary, etc.)
  "limited": "boolean",     // Whether the item is limited edition
  "robux_price": "number",  // Price in Robux
  "community_price": "string", // Community trading price (e.g., "3.2k", "1.8k")
  "animated": "boolean",    // Whether the item has animations
  "bullet_VFX": "boolean",  // Whether the item has bullet visual effects
  "type": "string",         // Item type (skins, vehicles, etc.)
  "demand": "number"        // Demand rating (decimal number)
}
```

### All Items Endpoint - Item Object
```json
{
  "id": "string",           // Unique identifier (e.g., "vehicles-285", "skins-255")
  "name": "string",         // Full name of the item
  "description": "string",  // Item description
  "rarity": "string",       // Rarity level (Epic, Mythic, Legendary, etc.)
  "limited": "boolean",     // Whether the item is limited edition
  "robux_price": "number",  // Price in Robux
  "community_price": "string", // Community trading price (e.g., "108.6k", "249")
  "animated": "boolean",    // Whether the item has animations
  "bullet_VFX": "boolean",  // Whether the item has bullet visual effects
  "type": "string",         // Item type (vehicles, skins, etc.)
  "demand": "number"        // Demand rating (decimal number)
}
```

### Price History Endpoint - History Object
```json
{
  "id": "string",           // Unique identifier for the item
  "name": "string",         // Full name of the item
  "history": [              // Array of price history entries
    {
      "price": "number",    // Price value
      "date": "string",     // ISO 8601 timestamp
      "priceString": "string" // Price as string
    }
  ],
  "latest_date": "string"   // Latest date in readable format
}
```

### Top Items Endpoint - Top Item Object
```json
{
  "id": "string",           // Unique identifier for the item
  "name": "string",         // Full name of the item
  "description": "string",  // Item description
  "rarity": "string",       // Rarity level
  "limited": "boolean",     // Whether the item is limited edition
  "robux_price": "number",  // Price in Robux
  "community_price": "string", // Community trading price
  "animated": "boolean",    // Whether the item has animations
  "bullet_VFX": "boolean",  // Whether the item has bullet visual effects
  "type": "string",         // Item type
  "demand": "number"        // Demand rating
}
```

# Examples

## JavaScript/Node.js

```javascript
// Simple fetch example for searching skins
async function searchSkins(query) {
  const response = await fetch(`https://wttd.trade/api/search?q=${encodeURIComponent(query)}`);
  const skins = await response.json();
  return skins;
}

// Get all items
async function getAllItems() {
  const response = await fetch('https://wttd.trade/api/items/');
  const items = await response.json();
  return items;
}

// Get price history
async function getPriceHistory(limit = 10) {
  const response = await fetch(`https://wttd.trade/api/items/price-history?limit=${limit}`);
  const history = await response.json();
  return history;
}

// Get top items (filter is optional)
async function getTopItems(filter = null) {
  const url = filter 
    ? `https://wttd.trade/api/top-items?filter=${filter}`
    : 'https://wttd.trade/api/top-items';
  const response = await fetch(url);
  const items = await response.json();
  return items;
}

// Usage examples
searchSkins('ak47 redline').then(skins => {
  console.log('Found skins:', skins);
});

getAllItems().then(items => {
  console.log('All items:', items.length);
});

getPriceHistory(5).then(history => {
  console.log('Price history:', history);
});

getTopItems('medals').then(items => {
  console.log('Top medal items:', items);
});

getTopItems().then(items => {
  console.log('All top items:', items);
});

// With error handling
async function searchSkinsWithErrorHandling(query) {
  try {
    const response = await fetch(`https://wttd.trade/api/search?q=${encodeURIComponent(query)}`);
    
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    
    const skins = await response.json();
    return skins;
  } catch (error) {
    console.error('Error searching for skins:', error);
    return [];
  }
}
```

## Python

```python
import requests
import urllib.parse

def search_skins(query):
    """Search for skins by name"""
    encoded_query = urllib.parse.quote(query)
    url = f"https://wttd.trade/api/search?q={encoded_query}"
    
    try:
        response = requests.get(url)
        response.raise_for_status()  # Raises an HTTPError for bad responses
        return response.json()
    except requests.RequestException as e:
        print(f"Error searching for skins: {e}")
        return []

def get_all_items():
    """Get all items from the database"""
    url = "https://wttd.trade/api/items/"
    
    try:
        response = requests.get(url)
        response.raise_for_status()
        return response.json()
    except requests.RequestException as e:
        print(f"Error getting all items: {e}")
        return []

def get_price_history(limit=10):
    """Get price history data"""
    url = f"https://wttd.trade/api/items/price-history?limit={limit}"
    
    try:
        response = requests.get(url)
        response.raise_for_status()
        return response.json()
    except requests.RequestException as e:
        print(f"Error getting price history: {e}")
        return []

def get_top_items(filter_type=None):
    """Get top items, optionally filtered by currency type"""
    url = "https://wttd.trade/api/top-items"
    if filter_type:
        url += f"?filter={filter_type}"
    
    try:
        response = requests.get(url)
        response.raise_for_status()
        return response.json()
    except requests.RequestException as e:
        print(f"Error getting top items: {e}")
        return []

# Usage examples
skins = search_skins("dragon")
print(f"Found {len(skins)} skins")

# Get all items
all_items = get_all_items()
print(f"Total items in database: {len(all_items)}")

# Search for specific skin
ak_skins = search_skins("ak47 redline")
for skin in ak_skins:
    print(f"{skin['name']} - ${skin.get('price', 'N/A')}")

# Get price history
history = get_price_history(5)
print(f"Got {len(history)} price history entries")

# Get top medal items
top_medals = get_top_items("medals")
print(f"Top medal items: {len(top_medals)}")

# Get all top items (no filter)
all_top_items = get_top_items()
print(f"All top items: {len(all_top_items)}")
```

## cURL

```bash
# Basic search
curl "https://wttd.trade/api/search?q=dragon"

# Search with URL encoding for spaces
curl "https://wttd.trade/api/search?q=ak47%20redline"

# Search with verbose output
curl -v "https://wttd.trade/api/search?q=awp"

# Save response to file
curl "https://wttd.trade/api/search?q=dragon" -o dragon_skins.json

# Get all items
curl "https://wttd.trade/api/items/"

# Get price history
curl "https://wttd.trade/api/items/price-history?limit=10"

# Get all top items (no filter)
curl "https://wttd.trade/api/top-items"

# Get top items filtered by medals
curl "https://wttd.trade/api/top-items?filter=medals"

# Get top items filtered by robux
curl "https://wttd.trade/api/top-items?filter=robux"
```

## PHP

```php
<?php
function searchSkins($query) {
    $encoded_query = urlencode($query);
    $url = "https://wttd.trade/api/search?q=" . $encoded_query;
    
    $response = file_get_contents($url);
    
    if ($response === FALSE) {
        return [];
    }
    
    return json_decode($response, true);
}

// Usage
$skins = searchSkins("dragon");
echo "Found " . count($skins) . " skins\n";

foreach ($skins as $skin) {
    echo $skin['name'] . " - $" . $skin['price'] . "\n";
}
?>
```

# Error Handling

The API uses standard HTTP status codes:

- **200 OK**: Successful request, returns skin data (may be empty array if no results)
- **400 Bad Request**: Invalid query parameter
- **404 Not Found**: Endpoint not found
- **500 Internal Server Error**: Server error
- **503 Service Unavailable**: Service temporarily unavailable

## Common Error Scenarios

1. **Empty Query**: Searching with an empty `q` parameter may return all skins or an error
2. **Special Characters**: Ensure proper URL encoding for queries with special characters
3. **Rate Limiting**: Too many requests may result in temporary blocking

## Best Practices

1. **URL Encode Queries**: Always URL encode the query parameter, especially when it contains spaces or special characters
2. **Handle Empty Results**: The API returns an empty array when no skins match the query
3. **Error Handling**: Implement proper error handling for network issues and API errors
4. **Caching**: Consider caching results for frequently searched terms to reduce API calls
5. **Respectful Usage**: Don't make excessive requests; implement reasonable delays between requests

## Notes

- This was made with claude as I have to go on a trip and am not taking my laptop. 
- Tuxuis has not expanded on the public api that much and I do not know if the main api will become available for the public. Mainly because im not on the WTTD team anymore (mb).
- If you learn of more information, please expand on this repo.