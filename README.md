### Buff LEECH API Documentation

---

Some content and documentation might change later on.

#### Index

* [API levels explained](#api-levels-explained-)
* [GetItem](#getitem-)
* [GetAllItems](#getallitems-)
* [GetCurrencyRates](#getcurrencyrates-)

---

#### API levels explained [^](#index)

* Basic (1)
    * Free
    * 120 requests (total) per 24 hours
    * GetAllItems ***not available***
    * GetCurrencyRates ***not available***

* Registered (2)
    * You registered your usage
    * 30 requests per hour
    * GetAllItems ***not available***
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
