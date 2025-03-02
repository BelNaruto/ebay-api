# eBay Data API Documentation (Unofficial)

## Introduction

Welcome to the eBay Data API! This powerful API gives you access to a wealth of eBay marketplace data, allowing you to search for items, get pricing information, explore categories, view seller information, and much more. Whether you're building an e-commerce application, conducting market research, or creating a price comparison tool, this API has everything you need to tap into eBay's vast ecosystem.

## Why Use This API?

### Benefits for Developers and Businesses

- **Comprehensive eBay Data**: Access product listings, pricing information, seller details, and more without needing to scrape the eBay website
- **Easy Integration**: Simple RESTful API design makes implementation straightforward
- **Detailed Filtering**: Narrow down search results with specific parameters like price range, condition, shipping options, etc.
- **Market Intelligence**: Track pricing trends, compare similar items, and understand market dynamics
- **Store Research**: Analyze eBay sellers, their inventory, ratings, and special offers
- **International Support**: Get data from different eBay country sites with localization support

### Real-World Applications

- Price comparison tools
- Market analysis dashboards
- Inventory management systems
- Competitive research platforms
- E-commerce extensions and plugins
- Mobile shopping apps
- Deal finders and alerts

## Getting Started

To use the eBay Data API, you'll need to:

1. Sign up for a RapidAPI account
2. Subscribe to the [eBay Data API](https://rapidapi.com/belchiorarkad-FqvHs2EDOtP/api/ebay-data-api)
3. Get your API key
4. Start making requests using your preferred programming language

## Base Url
- https://ebay-data-api.p.rapidapi.com

All API endpoints return JSON responses for easy parsing and handling in your applications.

## API Endpoints

### Search Endpoints

These endpoints help you search for items and get detailed information about search results.

#### 1. Search for Items

```
GET /search
```

Find items on eBay based on various search criteria.

**Query Parameters:**

| Parameter | Default | Description |
|-----------|---------|-------------|
| query | "macbook pro" | Search term for finding items |
| countryIso | "us" | Country ISO code (e.g., "us", "uk", "de") |
| condition | "used" | Item condition ("all", "new", "used") |
| minPrice | 500 | Minimum price filter |
| maxPrice | 1200 | Maximum price filter |
| location | "worldwide" | Location filter ("worldwide", "us_only", "north_america", "europe", "asia") |
| sort | "price_asc" | Sort order for results |
| shipping | "free" | Shipping options filter |
| seller | "top_rated" | Seller rating filter |
| excludeKeywords | "broken damaged" | Keywords to exclude from results |
| page | 1 | Page number for pagination |

**Example Request:**
```
GET /search?query=nintendo%20switch&countryIso=us&condition=new&minPrice=200&maxPrice=350
```

**Response:** A list of matching eBay listings with details like title, price, shipping info, and seller.

#### 2. Get Average Price

```
GET /search/average-price
```

Calculate the average price for a specific product search on eBay. This is incredibly useful for price comparison and determining fair market value.

**Query Parameters:** Same as the `/search` endpoint

**Example Request:**
```
GET /search/average-price?query=iphone%2013&condition=used&countryIso=us
```

**Response:** Average price information for the specified product search, including mean, median, lowest, and highest prices.

#### 3. Search Categories

```
GET /search/categories
```

Find relevant eBay categories for a specific search term. This helps you narrow down your searches to the most relevant category.

**Query Parameters:** Similar to the `/search` endpoint, with `query` and `countryIso` being the most important.

**Example Request:**
```
GET /search/categories?query=sneakers&countryIso=us
```

**Response:** A list of eBay categories related to the search term, including category IDs and names.

#### 4. Get Search Filters

```
GET /search/filters
```

Retrieve available filtering options for eBay searches.

**Example Request:**
```
GET /search/filters
```

**Response:** A comprehensive list of filter options available for eBay searches, such as condition, price ranges, shipping options, etc.

### Item-Specific Endpoints

These endpoints provide detailed information about specific eBay items.

#### 1. Get Item Description

```
GET /item/description
```

Retrieve the full description of a specific eBay item.

**Query Parameters:**

| Parameter | Default | Description |
|-----------|---------|-------------|
| itemUrl | "https://www.ebay.com/itm/326453180272" | Full URL to the eBay item |
| countryIso | "us" | Country ISO code |

**Example Request:**
```
GET /item/description?itemUrl=https://www.ebay.com/itm/123456789&countryIso=us
```

**Response:** The complete HTML description of the item as provided by the seller.

#### 2. Get Similar Items

```
GET /item/similar
```

Find items similar to a specific eBay listing.

**Query Parameters:**

| Parameter | Default | Description |
|-----------|---------|-------------|
| itemUrl | "https://www.ebay.com/itm/326453180272" | Full URL to the eBay item |
| countryIso | "us" | Country ISO code |

**Example Request:**
```
GET /item/similar?itemUrl=https://www.ebay.com/itm/123456789&countryIso=us
```

**Response:** A list of similar items with their details.

#### 3. Get Similar Items (V2)

```
GET /item/similar/v1
```

An alternative method to find similar items using the item ID.

**Query Parameters:**

| Parameter | Default | Description |
|-----------|---------|-------------|
| itemId | "326453180272" | eBay item ID |
| countryIso | "us" | Country ISO code |
| page | "1" | Page number for pagination |

**Example Request:**
```
GET /item/similar/v1?itemId=123456789&countryIso=us&page=1
```

**Response:** A list of similar items with their details.

#### 4. Get Item Reviews

```
GET /item/review
```

Retrieve user reviews for a specific eBay item.

**Query Parameters:**

| Parameter | Default | Description |
|-----------|---------|-------------|
| itemId | "335751891889" | eBay item ID |
| countryIso | "us" | Country ISO code |
| page | "1" | Page number for pagination |
| perPage | "25" | Number of reviews per page |

**Example Request:**
```
GET /item/review?itemId=335751891889&countryIso=us&page=1&perPage=10
```

**Response:** User reviews for the specified item, including ratings and comments.

#### 5. Get Items by Category

```
GET /item/bycategory
```

Find items within a specific eBay category.

**Query Parameters:**

| Parameter | Default | Description |
|-----------|---------|-------------|
| categoryId | "bn_55163226" | eBay category ID |
| countryIso | "us" | Country ISO code |
| page | 1 | Page number for pagination |
| minPrice | 0 | Minimum price filter |
| maxPrice | (none) | Maximum price filter |
| condition | null | Item condition (null=any, 1000=new, 3000=used) |
| sortOrder | "BestMatch" | Sort order ("BestMatch", "EndingSoonest", "PricePlusShippingLowest", "PricePlusShippingHighest") |

**Example Request:**
```
GET /item/bycategory?categoryId=bn_55163226&countryIso=us&page=1&minPrice=50&maxPrice=200
```

**Response:** A list of items in the specified category.

#### 6. Get Items by Category URL

```
GET /item/bycategory/byurl
```

Find items within a category using the category URL.

**Query Parameters:**

| Parameter | Default | Description |
|-----------|---------|-------------|
| categoryUrl | "https://www.ebay.com/b/3D-Printers-Supplies/183062/bn_55163226?_pgn=1&_sop=15" | Full URL to the eBay category |
| countryIso | "us" | Country ISO code |

**Example Request:**
```
GET /item/bycategory/byurl?categoryUrl=https://www.ebay.com/b/Cell-Phones-Smartphones/9355/bn_320094&countryIso=us
```

**Response:** A list of items in the specified category.

### Store Endpoints

These endpoints provide information about eBay stores and their items.

#### 1. Get Store Filters

```
GET /store/filters
```

Retrieve available filtering options for eBay store searches.

**Example Request:**
```
GET /store/filters
```

**Response:** A list of filter options available for eBay store searches.

#### 2. Get Store Information

```
GET /store/info
```

Get information about a specific eBay store.

**Query Parameters:**

| Parameter | Default | Description |
|-----------|---------|-------------|
| storeName | "kingacegoods" | Name of the eBay store |
| countryIso | "us" | Country ISO code |

**Example Request:**
```
GET /store/info?storeName=kingacegoods&countryIso=us
```

**Response:** Detailed information about the store, including store description, feedback score, and other stats.

#### 3. Get Store Items

```
GET /store/items
```

Retrieve items sold by a specific eBay store.

**Query Parameters:**

| Parameter | Default | Description |
|-----------|---------|-------------|
| storeName | "addicted2watches" | Name of the eBay store |
| countryIso | "us" | Country ISO code |
| sorting | (none) | Sort order for results |
| type | (none) | Type of items to retrieve |
| perPage | (none) | Number of items per page |
| page | (none) | Page number for pagination |

**Example Request:**
```
GET /store/items?storeName=addicted2watches&countryIso=us&page=1&perPage=20
```

**Response:** A list of items sold by the specified store.

#### 4. Get Store Reviews

```
GET /store/reviews
```

Retrieve customer reviews for a specific eBay store.

**Query Parameters:**

| Parameter | Default | Description |
|-----------|---------|-------------|
| storeName | "addicted2watches" | Name of the eBay store |
| countryIso | "us" | Country ISO code |
| sorting | (none) | Sort order for reviews |
| type | (none) | Type of reviews to retrieve |
| perPage | (none) | Number of reviews per page |
| page | (none) | Page number for pagination |

**Example Request:**
```
GET /store/reviews?storeName=addicted2watches&countryIso=us&page=1&perPage=20
```

**Response:** A list of customer reviews for the specified store.

#### 5. Get Store Items on Sale

```
GET /store/items/onsale
```

Retrieve items that are currently on sale in a specific eBay store.

**Query Parameters:** Same as the `/store/items` endpoint

**Example Request:**
```
GET /store/items/onsale?storeName=addicted2watches&countryIso=us&page=1&perPage=20
```

**Response:** A list of sale items from the specified store.

### Category Endpoints

These endpoints help you navigate eBay's category structure.

#### 1. Get All Categories

```
GET /categories
```

Retrieve a list of eBay categories.

**Query Parameters:**

| Parameter | Default | Description |
|-----------|---------|-------------|
| countryIso | "us" | Country ISO code |
| page | 1 | Page number for pagination |
| perPage | 25 | Number of categories per page (max 75) |

**Example Request:**
```
GET /categories?countryIso=us&page=1&perPage=50
```

**Response:** A list of eBay categories with their IDs and names.

#### 2. Search Categories

```
GET /categories/search
```

Search for specific eBay categories by keyword.

**Query Parameters:**

| Parameter | Default | Description |
|-----------|---------|-------------|
| query | (required) | Search term for finding categories |
| countryIso | "us" | Country ISO code |
| page | 1 | Page number for pagination |
| perPage | 25 | Number of categories per page (max 75) |

**Example Request:**
```
GET /categories/search?query=electronics&countryIso=us&page=1&perPage=20
```

**Response:** A list of eBay categories that match the search term.

### Shipping & Country Endpoints

These endpoints provide shipping information and country codes.

#### 1. Get Shipping Rates

```
GET /shipping/rates
```

Calculate shipping rates for a specific item to a specific destination.

**Query Parameters:**

| Parameter | Default | Description |
|-----------|---------|-------------|
| itemId | (required) | eBay item ID |
| countryIso | "us" | Country ISO code for the eBay site |
| countryIso2 | "USA" | Country ISO code for the shipping destination |
| shippingZipCode | "20147" | Zip/postal code for shipping calculation |

**Example Request:**
```
GET /shipping/rates?itemId=326453180272&countryIso=us&countryIso2=CAN&shippingZipCode=M5V2N4
```

**Response:** Shipping options and rates for the specified item to the given destination.

#### 2. Get Country ISO Codes

```
GET /countries/iso
```

Retrieve a list of country ISO codes supported by the API.

**Example Request:**
```
GET /countries/iso
```

**Response:** A list of country codes and their full names.

## Best Practices

### Optimizing Your API Usage

1. **Be Specific with Search Terms**: More specific queries yield better results and reduce unnecessary data transfer.

2. **Use Pagination**: When retrieving large sets of data, use the `page` and `perPage` parameters to limit the number of results per request.

3. **Apply Filters**: Use filtering parameters to narrow down results and improve response time.

4. **Cache Responses**: Store API responses that don't change frequently, such as category listings or store information.

5. **Handle Rate Limits**: Be aware of API rate limits and implement appropriate retry mechanisms.

### Error Handling

The API returns standard HTTP status codes:

- **200 OK**: Request successful
- **400 Bad Request**: Missing or invalid parameters
- **401 Unauthorized**: Invalid API key
- **429 Too Many Requests**: Rate limit exceeded
- **500 Internal Server Error**: Server-side error

Always check the response status code and handle errors gracefully in your application.

## Use Cases

### Price Research Tool

Build an application that helps users find the best deals on eBay by comparing prices across different sellers and item conditions.

```javascript
// Example: Finding the average price of a product
async function getAveragePrice(productName) {
  const response = await fetch(`https://ebay-data-api.p.rapidapi.com/search/average-price?query=${encodeURIComponent(productName)}&countryIso=us`);
  const data = await response.json();
  return data;
}
```

### Market Analysis Dashboard

Create a dashboard that tracks pricing trends, seller performance, and category popularity on eBay.

### Inventory Management System

Build a system that helps sellers price their items competitively based on current market conditions.

### Bargain Hunter App

Develop an app that alerts users when items they're interested in are listed below the average market price.

## Conclusion

The eBay Data API provides a powerful way to access and analyze eBay marketplace data. With its comprehensive endpoints and flexible parameters, you can build sophisticated applications that leverage eBay's vast product catalog and seller network.

Whether you're a developer building e-commerce tools, a researcher analyzing market trends, or a business looking to optimize your eBay strategy, this API gives you the data you need to succeed in the eBay ecosystem.

Start exploring the API today and unlock the full potential of eBay data for your projects!

## Support

If you encounter any issues or have questions about the API, please contact our support team through the RapidAPI platform, visit our documentation for additional resources or contact us by email at pintoflowpt@gmail.com.

Happy coding!
