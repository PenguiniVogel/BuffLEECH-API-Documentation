### Buff LEECH API Documentation

---

Some content and documentation might change later on.

#### Index

* [API levels explained](#api-levels-explained-)
* [GetItem](#getitem-)
* [GetAllItems](#getallitems-)
* [GetPriceHistory](#getpricehistory-)
* [GetTrends](#gettrends-)
* [GetCurrencyRates](#getcurrencyrates-)

---

#### API levels explained [^](#index)

* Basic (1)
    * Free
    * 120 requests (total) per 24 hours
    * GetAllItems ***not available***
    * GetPriceHistory ***not available***
    * GetTrends ***not available***
    * GetCurrencyRates ***not available***

* Registered (2)
    * You registered your usage
    * 30 requests per hour
    * GetAllItems ***not available***
    * GetPriceHistory ***not available***
    * GetTrends ***not available***
    * GetCurrencyRates ***not available***

* Verified (20)
    * You were manually verified
    * 1 request per minute
    * Access to all endpoints

* Legendary (80)
    * Manually handed out
    * No request limit
    * Access to all endpoints

---

#### GetItem [^](#index)

API level required: **1** or greater.

Optional parameters:
* `currency`: Default `USD`, specify a ISO currency code and the returned price will be in the specified currency.
* `format`: Default `json`, accepted values: `json`, `xml`

**Get item by name** <br>
`GetItem?name=AWP | Dragon Lore` <br>
**Warning:** Item narrowing <br>
What does that mean? `GetItem` only returns ***one*** result sorted by `item_id` ascending,
so in our mentioned example we would receive this response:

```JSON
{
    "name": "AWP | Dragon Lore (Battle-Scarred)",
    "item_id": 34074,
    "asset_info": {
        "defIndex": 9,
        "paintIndex": 344
    },
    "currency_symbol": "$",
    "currency_name": "USD",
    "price_buff": 2477.45,
    "max_buff_buyorder": 2368.29,
    "count_buff_selling": 29,
    "count_buff_buying": 13,
    "price_steam": 0,
    "max_steam_buyorder": 2000,
    "count_steam_selling": 0,
    "count_steam_buying": 8752
}
```

The closer you specify the name, the more likely you will receive the result you are looking for e.g.: <br>
`GetItem?name=Souvenir AWP | Dragon Lore (Field-Tested)`
```JSON
{
    "name": "Souvenir AWP | Dragon Lore (Field-Tested)",
    "item_id": 44946,
    "asset_info": {
        "defIndex": 9,
        "paintIndex": 344
    },
    "currency_symbol": "$",
    "currency_name": "USD",
    "price_buff": 60383.62,
    "max_buff_buyorder": 14.12,
    "count_buff_selling": 22,
    "count_buff_buying": 32,
    "price_steam": 0,
    "max_steam_buyorder": 0,
    "count_steam_selling": 0,
    "count_steam_buying": 0
}
```

**Get item by id** <br>
`GetItem?id=34074` <br>
The `id` parameter specifies the **Buff** item id.
```JSON
{
    "name": "AWP | Dragon Lore (Battle-Scarred)",
    "item_id": 34074,
    "asset_info": {
        "defIndex": 9,
        "paintIndex": 344
    },
    "currency_symbol": "$",
    "currency_name": "USD",
    "price_buff": 2477.45,
    "max_buff_buyorder": 2368.29,
    "count_buff_selling": 29,
    "count_buff_buying": 13,
    "price_steam": 0,
    "max_steam_buyorder": 2000,
    "count_steam_selling": 0,
    "count_steam_buying": 8752
}
```

**XML example** <br>
`GetItem?id=34074&format=xml` <br>
```XML
<response>
    <name>AWP | Dragon Lore (Battle-Scarred)</name>
    <itemId>34074</itemId>
    <assetInfo>
        <defIndex>9</defIndex>
        <paintIndex>344</paintIndex>
    </assetInfo>
    <currency>
        <symbol>$</symbol>
        <name>USD</name>
    </currency>
    <price>
        <buff>2477.45</buff>
        <steam>0</steam>
    </price>
    <buyorder>
        <buff>2368.29</buff>
        <steam>2000</steam>
    </buyorder>
    <selling>
        <buff>29</buff>
        <steam>0</steam>
    </selling>
    <buying>
        <buff>13</buff>
        <steam>8752</steam>
    </buying>
</response>
```

---

#### GetAllItems [^](#index)

API level required: **20** or greater.

Optional parameters:
* `currency`: Default `USD`, specify a ISO currency code and the returned price will be in the specified currency.
* `compact`: Default `false`, specify if the resulting json should be compact or not.
* `search`: Default empty, narrow down the list of items you want to receive by name.

The result is returned by item id ascending.

**Example with no parameters** <br>
`GetAllItems` <br>
Note: This is a truncated response!

```JSON
{
    "currency_symbol": "$",
    "currency_name": "USD",
    "items": [
        "More before...",
        {
            "name": "AWP | Dragon Lore (Battle-Scarred)",
            "item_id": 34074,
            "asset_info": {
                "defIndex": 9,
                "paintIndex": 344
            },
            "price_buff": 2477.45,
            "max_buff_buyorder": 2368.29,
            "count_buff_selling": 29,
            "count_buff_buying": 13,
            "price_steam": 0,
            "max_steam_buyorder": 2000,
            "count_steam_selling": 0,
            "count_steam_buying": 8752
        },
        {
            "name": "AWP | Dragon Lore (Field-Tested)",
            "item_id": 34075,
            "asset_info": {
                "defIndex": 9,
                "paintIndex": 344
            },
            "price_buff": 3951.60,
            "max_buff_buyorder": 3862.98,
            "count_buff_selling": 254,
            "count_buff_buying": 27,
            "price_steam": 0,
            "max_steam_buyorder": 2237.6,
            "count_steam_selling": 0,
            "count_steam_buying": 9297
        },
        "More after..."
    ]
}
```

**Example with `compact=true`** <br>
`GetAllItems?compact=true` <br>
Note: This is a truncated response!
```JSON
{
    "currency_symbol": "$",
    "currency_name": "USD",
    "items": [
        "More before...",
        {
            "name": "AWP | Dragon Lore (Battle-Scarred)",
            "item_id": 34074,
            "price_buff": 2477.45,
            "max_buff_buyorder": 2368.29,
            "price_steam": 0,
            "max_steam_buyorder": 2000
        },
        {
            "name": "AWP | Dragon Lore (Field-Tested)",
            "item_id": 34075,
            "price_buff": 3951.60,
            "max_buff_buyorder": 3862.98,
            "price_steam": 0,
            "max_steam_buyorder": 2237.6
        },
        "More after..."
    ]
}
```

**Example with `compact=true` and `search=AWP | Dragon Lore`** <br>
`GetAllItems?compact=true&search=AWP | Dragon Lore` <br>
Note: This is a partial response!
```JSON
{
    "currency_symbol": "$",
    "currency_name": "USD",
    "items": [
        {
            "name": "AWP | Dragon Lore (Battle-Scarred)",
            "item_id": 34074,
            "price_buff": 2477.45,
            "max_buff_buyorder": 2368.29,
            "price_steam": 0,
            "max_steam_buyorder": 2000
        },
        {
            "name": "AWP | Dragon Lore (Field-Tested)",
            "item_id": 34075,
            "price_buff": 3951.60,
            "max_buff_buyorder": 3862.98,
            "price_steam": 0,
            "max_steam_buyorder": 2237.6
        },
        "More after..."
    ]
}
```

---

#### GetPriceHistory [^](#index)

API level required: **20** or greater. <br>
Returns the price history for the specified item.

Optional parameters:
* `currency`: Default `USD`, specify a ISO currency code and the returned price will be in the specified currency.
* `id`: The Buff Item ID, `search` is ignored if this parameter is provided.
* `search`: Default empty, try finding the item by name.
* `time`: Default `week`, accepted values are: `week`, `month`, `6_months`, `year`

Note: This response is truncated for readability. <br>
**Example with `id=857652`**
```JSON
{
    "currency_symbol": "$",
    "currency_name": "USD",
    "name": "AK-47 | Slate (Factory New)",
    "item_id": 857652,
    "history": [
        [1644224400000, 14.17],
        [1644220800000, 12.31],
        [1644217200000, 13.21],
        [1644213600000, 12.59],
        [1644210000000, 13.16],
        [1644206400000, 13.05],
        [1644202800000, 11.94],
        [1644199200000, 13.17],
        [1644195600000, 13.42],
        [1644188400000, 11.87],
        [1644174000000, 12.16],
        [1644170400000, 12.20],
        [1644166800000, 14.65],
        [1644163200000, 12.89],
        [1644159600000, 66.06],
        [1644156000000, 12.50],
        [1644152400000, 12.29],
        [1644148800000, 13.01],
        [1644145200000, 12.57],
        "More after..."
    ]
}
```

---

#### GetTrends [^](#index)

API level required: **20** or greater. <br>
Returns the current 10 most changed items by price. <br>
Note: This endpoint is still being worked on.

---

#### GetCurrencyRates [^](#index)

API level required: **20** or greater. <br>
Returns the current currency rates. <br>
Note: This response is truncated for readability.
```JSON
{
    "date": "2022-01-19",
    "rates": {
        "More before...": [ ],
        "USD": [
            0.1575223949502113,
            2
        ],
        "More after...": [ ]
    },
    "symbols": {
        "More before...": "...",
        "USD": "$",
        "More after...": "..."
    }
}
```

--- 
