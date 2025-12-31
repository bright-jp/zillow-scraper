# Zillow Scraper

[![Promo](https://github.com/luminati-io/LinkedIn-Scraper/blob/main/Proxies%20and%20scrapers%20GitHub%20bonus%20banner.png)](https://brightdata.jp/products/web-scraper/zillow) 

このリポジトリでは、Zillowデータをスクレイピングするための2つの異なる方法を提供しています：
1. 基本的なデータ収集向けの無料・小規模スクレイパー
2. 大規模データ抽出向けのエンタープライズグレードAPIソリューション

## Table of Contents
- [Free Zillow Data Scraper](#free-zillow-data-scraper)
- [Limitations of Free Scraper](#limitations-of-free-scraper)
- [Zillow Scraper API](#zillow-scraper-api)
  - [Key Features](#key-features)
  - [Quick Start Guide](#quick-start-guide)
  - [Zillow Property Details by URL](#1-zillow-property-details-by-url)
  - [Zillow Properties Listing by Filters](#2-zillow-properties-listing-by-filters)
  - [Zillow Properties Listing by URL](#3-zillow-properties-listing-by-url)
  - [Zillow Price History](#4-zillow-price-history)
- [No-Code Scraper Option](#no-code-scraper-option)
- [Additional Options](#additional-options)
- [Support & Resources](#support--resources)

## Free Zillow Data Scraper
無料スクレイパーでは、Zillowの検索ページから小規模に物件データを収集できます。

### Input Requirements
| Parameter | Required | Description |
|-----------|----------|-------------|
| coords    | Yes      | 境界座標 [west, east, south, north] |
| pages     | Yes      | スクレイピングするページ数 |

### Implementation
スクレイパーを使用するには、以下のコード内の座標とページ数を、お住まいの場所およびデータ要件に合わせて変更してください：
```python
# free_zillow_scraper/property_data.py
def get_search_params():
    return (
        -118.668176,  # West longitude
        -118.155289,  # East longitude
        33.703652,    # South latitude
        34.337306,    # North latitude
        5             # Number of pages to scrape
    )
```

**ヒント：** 地理座標は、任意の場所のZillow検索ページ内にある`<script>`タグから取得できます。次のタグを探してください：
```bash
<script id="__NEXT_DATA__" type="application/json">
```

### Sample Output
```json
{
    "id": "20595672",
    "price": "$1,599,900",
    "zestimate": 1605500,
    "location": {
        "address": "2215 Wellington Rd, Los Angeles, CA 90016",
        "city": "Los Angeles",
        "state": "CA",
        "zip": "90016",
        "coordinates": {"lat": 34.036064, "lon": -118.33622},
    },
    "details": {
        "beds": 4,
        "baths": 3.0,
        "area_sqft": 1886,
        "lot_acres": 8577.0,
        "property_type": "SINGLE_FAMILY",
    },
    "listing": {
        "status": "House for sale",
        "days_on_zillow": 5,
        "broker": "ehomes",
        "url": "https://www.zillow.com/homedetails/2215-Wellington-Rd-Los-Angeles-CA-90016/20595672_zpid/",
    },
},
```

## Limitations of Free Scraper
無料のZillowスクレイパーは小規模なデータ抽出には有効ですが、以下の制限があります：

- **Rate Limiting:** Zillowは数回スクレイピングした後にリクエストをブロックします。
- **IP Blocking:** 同一IPアドレスから頻繁にスクレイピングすると、BANされる可能性があります。
- **Limited Scalability:** 大量のデータ収集には不向きです。
- **Captcha:** Zillowは自動化されたリクエストをブロックするためにCAPTCHAを表示する場合があります。
- **Honeypots:** Zillowはボットを検出してブロックするために、ホニーポットのトラップを使用しています。

大規模なスクレイピングには、以下で説明する **Zillow Scraper API** の利用をご検討ください。

##  Zillow Scraper API
Bright Dataの[Zillow Scraper API](https://brightdata.jp/products/web-scraper/zillow)は、自前のインフラを構築または保守することなく、大規模なZillowデータをスケーラブルかつ信頼性高く、手間なく抽出できるソリューションです。

### Key Features
- **Scalable & Reliable:** 大量かつリアルタイムのデータ収集に最適化されています。
- **Anti-Blocking:** プロキシローテーションとCAPTCHA解決を内蔵しています。
- **Legal Compliance:** GDPRおよびCCPAに完全準拠しています。
- **Global Coverage:** あらゆる地域や言語からデータにアクセスできます。
- **Real-Time Data:** 最小限の遅延で最新データを取得できます。
- **Advanced Filtering:** 精密なフィルターでデータ抽出をカスタマイズできます。
- **Pay-as-You-Go:** 成功したレスポンスに対してのみ課金されます。
- **Free Trial:** 開始用にAPIコール20回分が無料で含まれます。
- **Dedicated Support:** 24時間365日の技術支援を提供します。
- **No-Code Option:** APIまたはノーコードスクレイパーでZillowデータをスクレイピングできます。

### Quick Start Guide
- **Sign Up:** [Bright Data account](https://brightdata.jp/)を作成してください。
- **Get API Token:** ダッシュボードから[API key](https://docs.brightdata.com/general/account/api-token)を取得してください。
- **Choose Endpoint:** 以下の利用可能なAPIエンドポイントから選択してください。

## 1. Zillow Property Details by URL
物件URLを指定して、物件詳細を収集します。

<img width="700" alt="zillow-properties-listing-information" src="https://github.com/luminati-io/zillow-scraper/blob/main/zillow-images/zillow-properties-listing-information.png" />

### Input Parameters
| Parameter | Required | Description            |
|-----------|----------|------------------------|
| `url`       | Yes      | Zillow物件URL   |


### Example Request
#### Python Code:
```python
properties = [
    {"url": "https://www.zillow.com/homedetails/73-Beverly-Park-Ln-Beverly-Hills-CA-90210/20533547_zpid/"},
    {"url": "https://www.zillow.com/homedetails/1945-N-Edgemont-St-Los-Angeles-CA-90027/20809871_zpid/"}
]
```

👉 Complete Python script: [zillow_properties.py](https://github.com/luminati-io/Zillow-Scraper/blob/main/zillow_api_scraper/zillow_properties.py)

#### cURL Command:
```bash
curl -H "Authorization: Bearer YOUR_API_TOKEN" \
     -H "Content-Type: application/json" \
     -d '[
           {
             "url": "https://www.zillow.com/homedetails/2506-Gordon-Cir-South-Bend-IN-46635/77050198_zpid/?t=for_sale"
           }
         ]' \
     "https://api.brightdata.com/datasets/v3/trigger?dataset_id=gd_lfqkr8wm13ixtbd8f5&include_errors=true"
```

### Response Schema
```json
{
    "property_overview": {
        "address": "73 Beverly Park Ln, Beverly Hills, CA 90210",
        "price": "$89,900,000",
        "status": "FOR_SALE",
        "living_area": "28,500 sq ft",
        "lot_size": "2.68 acres",
        "bedrooms": 9,
        "bathrooms": 22,
    },
    "key_features": {
        "highlights": [
            "85-foot infinity lap pool",
            "Two kitchens (including commercial-grade)",
            "5,000 sq ft primary suite",
            "Screening room",
            "Gated community with guard",
        ],
        "views": ["City", "Ocean", "Mountain", "Canyon"],
    },
    "financial": {
        "last_sold": "2021-04-08 for $28,500,000",
        "property_tax_rate": "1.18%",
        "monthly_hoa": "$6,216",
    },
}
```

👉 これは部分的なレスポンスです。物件の完全な詳細については、[full JSON response](https://github.com/luminati-io/Zillow-Scraper/blob/main/zillow_api_data/zillow_properties.json)をご覧ください。

## 2. Zillow Properties Listing by Filters
ロケーションおよびその他の条件を使用して物件を検索します。

<img width="700" alt="zillow-properties-listing-by-input" src="https://github.com/luminati-io/zillow-scraper/blob/main/zillow-images/zillow-properties-listing-by-input.png" />

💡 **Note:** 一部の物件には複数ユニットが含まれる場合があり、その結果、複数のレコードが生成されることがあります。結果を制限するには、[Limit per input](https://docs.brightdata.com/scraping-automation/web-scraper-api/overview#limit-records)を使用してください。

### Input Parameters
| Parameter       | Required | Description                                          |
|---------------|----------|------------------------------------------------------|
| `location`      | Yes      | 郵便番号、都市、または州を指定できます。                   |
| `listingCategory` | Yes    | オプション：Sold、House for rent、House for sale。       |
| `HomeType`      | Yes      | ZillowのHome type（例：Houses、Apartments、Townhomes）。 |


### Example Request
#### Python Code:
```python
filters = [
    {"location": "92027", "listingCategory": "Sold", "HomeType": "Houses"},
    {"location": "New York", "listingCategory": "House for rent", "HomeType": "Condos"},
    {"location": "Colorado", "listingCategory": "", "HomeType": ""},
]
```
👉 Complete Python script: [zillow_discovered_properties.py](https://github.com/luminati-io/Zillow-Scraper/blob/main/zillow_api_scraper/zillow_discovered_properties.py)

#### cURL Command:
```bash
curl -H "Authorization: Bearer YOUR_API_TOKEN" \
     -H "Content-Type: application/json" \
     -d '[{"location": "New York", "listingCategory": "House for rent", "HomeType": "Houses"},
          {"location": "02118", "listingCategory": "House for sale", "HomeType": "Condos"},
          {"location": "Colorado", "listingCategory": "", "HomeType": ""}]' \
     "https://api.brightdata.com/datasets/v3/trigger?dataset_id=gd_lfqkr8wm13ixtbd8f5&include_errors=true&type=discover_new&discover_by=input_filters"
```

### Response Schema
```json
{
    "address": {
        "streetAddress": "569 Hayward Pl",
        "city": "Escondido",
        "state": "CA",
        "zipcode": "92027",
    },
    "homeStatus": "SOLD",
    "bedrooms": 4,
    "bathrooms": 2,
    "livingArea": 1446,
    "livingAreaUnits": "Square Feet",
    "lotSize": 5933,
    "lotAreaUnits": "Square Feet",
    "homeType": "SINGLE_FAMILY",
    "yearBuilt": 1987,
    "lastSoldPrice": 689000,
    "dateSoldString": "2022-08-11",
    "zestimate": 818100,
    "rentZestimate": 3752,
    "schools": [
        {
            "name": "Glen View Elementary School",
            "distance": 0.6,
            "rating": 5,
            "grades": "K-5",
        },
        {
            "name": "Hidden Valley Middle School",
            "distance": 1.2,
            "rating": 5,
            "grades": "6-8",
        },
        {
            "name": "Orange Glen High School",
            "distance": 1.4,
            "rating": 5,
            "grades": "9-12",
        },
    ],
    "url": "https://www.zillow.com/homedetails/569-Hayward-Pl-Escondido-CA-92027/16696746_zpid/",
}
```

👉 これは部分的なレスポンスです。物件の完全な詳細については、[full JSON response](https://github.com/luminati-io/Zillow-Scraper/blob/main/zillow_api_data/zillow_discovered_properties.json)をご覧ください。

## 3. Zillow Properties Listing by URL
Zillowの検索ページURLを使用して、直接物件を検索します。

<img width="700" alt="zillow-properties-listing-by-url" src="https://github.com/luminati-io/zillow-scraper/blob/main/zillow-images/zillow-properties-listing-by-url.png" />


💡 **Note:** 一部の物件には複数ユニットが含まれる場合があり、その結果、複数のレコードが生成されることがあります。結果を制限するには、[Limit per input](https://docs.brightdata.com/scraping-automation/web-scraper-api/overview#limit-records)を使用してください。


### Input Parameters:
| Parameter | Required | Description                          |
|-----------|----------|--------------------------------------|
| `url`       | Yes      | 完全な検索パラメータを含む、直接のZillow検索URL |

### Example Request
#### Python Code:
```python
urls = [
    {"url": "https://www.zillow.com/south-bend-in/?searchQueryState=%7B%22pagination%22%3A..."},
    {"url": "https://www.zillow.com/new-york-ny/rentals/?searchQueryState=%7B%22isMapVisible%22%3A..."},
    {"url": "https://www.zillow.com/sands-point-ny/rentals/?searchQueryState=%7B%22isMapVisible%22%3A..."},
]
```
👉 Complete Python script: [zillow_discovered_properties_by_url.py](https://github.com/luminati-io/Zillow-Scraper/blob/main/zillow_api_scraper/zillow_discovered_properties_by_url.py)

#### cURL Command:
```bash
curl -H "Authorization: Bearer YOUR_API_TOKEN" \
     -H "Content-Type: application/json" \
     -d '[{"url": "https://www.zillow.com/south-bend-in/?searchQueryState=%7B%22pagination%22%3A..."}]' \
     "https://api.brightdata.com/datasets/v3/trigger?dataset_id=gd_lfqkr8wm13ixtbd8f5&include_errors=true&type=discover_new&discover_by=url"
```

### Response Schema:
```json
{
    "zpid": 77029580,
    "address": {
        "streetAddress": "1937 Churchill Dr",
        "city": "South Bend",
        "state": "IN",
        "zipcode": "46617",
    },
    "price": 435000,
    "bedrooms": 4,
    "bathrooms": 4,
    "livingArea": 3197,
    "lotAreaValue": 0.46,
    "lotAreaUnits": "Acres",
    "yearBuilt": 1968,
    "homeStatus": "FOR_SALE",
    "zestimate": 420400,
    "lastSoldPrice": 134000,
    "dateSold": "2013-05-20",
    "schools": [
        {"name": "McKinley Elementary School", "rating": 4},
        {"name": "Edison Intermediate Center", "rating": 2},
        {"name": "Rise Up Academy At Eggleston", "rating": 1},
    ],
    "mortgageRates": {"thirtyYearFixedRate": 6.536},
    "listingProvidedBy": {"name": "Eric M Bomkamp", "phoneNumber": "574-360-2569"},
    "url": "https://www.zillow.com/homedetails/1937-Churchill-Dr-South-Bend-IN-46617/77029580_zpid/",
}
```
👉 これは部分的なレスポンスです。物件の完全な詳細については、[full JSON response](https://github.com/luminati-io/Zillow-Scraper/blob/main/zillow_api_data/zillow_discovered_properties_by_url.json)をご覧ください。

## 4. Zillow Price History
物件の価格履歴を収集します。

<img width="700" alt="zillow-price-history" src="https://github.com/luminati-io/zillow-scraper/blob/main/zillow-images/zillow-price-history.png" />

### Input Parameters

| Parameter | Required | Description            |
|-----------|----------|------------------------|
| `url`       | Yes      | Zillow物件URL。   |

### Example Request
#### Python Code:

```python
urls = [
    {"url": "https://www.zillow.com/homedetails/8305-Blue-Heron-Way-Raleigh-NC-27615/6468808_zpid/"},
    {"url": "https://www.zillow.com/homedetails/930-3rd-St-SE-Hickory-NC-28602/71557289_zpid/"},
]
```
👉 Complete Python script: [zillow_price_history.py](https://github.com/luminati-io/Zillow-Scraper/blob/main/zillow_api_scraper/zillow_price_history.py)

#### cURL Command:
```bash
curl -H "Authorization: Bearer YOUR_API_TOKEN" \
     -H "Content-Type: application/json" \
     -d '[{"url": "https://www.zillow.com/homedetails/8305-Blue-Heron-Way-Raleigh-NC-27615/6468808_zpid/"},
          {"url": "https://www.zillow.com/homedetails/930-3rd-St-SE-Hickory-NC-28602/71557289_zpid/"}]' \
     "https://api.brightdata.com/datasets/v3/trigger?dataset_id=gd_lxu1cz9r88uiqsosl&include_errors=true"
```

### Response Schema:
```json
{
    "url": "https://www.zillow.com/homedetails/8305-Blue-Heron-Way-Raleigh-NC-27615/6468808_zpid/",
    "zpid": "6468808",
    "date": "2020-11-13T00:00:00.000Z",
    "event": "Sold",
    "price": 440000,
    "price_per_squarefoot": 127,
    "source": "Doorify MLS",
    "timestamp": "2025-02-09T16:56:42.074Z",
}
```
👉 これは部分的なレスポンスです。物件の完全な詳細については、[full JSON response](https://github.com/luminati-io/Zillow-Scraper/blob/main/zillow_api_data/zillow_price_history.json)をご覧ください。

## No-Code Scraper Option
Bright Data **No-Code Scraper** は、プログラミングなしでZillowデータを収集できる、ユーザーフレンドリーな方法を提供します。
- 数分でスクレイパーを設定できます。
- データ収集プロセス全体を自動化できます。
- 複数の形式で結果を直接ダウンロードできます。

詳細な手順については、[Getting Started guide](https://github.com/luminati-io/Zillow-Scraper/blob/main/no-code-scraper.md)をご覧ください。

## Additional Options
以下のパラメータでデータ収集を微調整できます：

| **Parameter**       | **Type**   | **Description**                                            | **Example**                  |
|---------------------|------------|------------------------------------------------------------|------------------------------|
| `limit`             | `integer`  | 入力ごとの最大結果数                                   | `limit=10`                   |
| `include_errors`    | `boolean`  | トラブルシューティング用のエラーレポートを取得                     | `include_errors=true`        |
| `notify`            | `url`      | 完了時に通知を受け取るためのWebhook通知URL  | `notify=https://notify-me.com/` |
| `format`            | `enum`     | 出力形式（例：JSON、NDJSON、JSONL、CSV）         | `format=json`                |

💡 **Pro Tip:** データは[external storage](https://docs.brightdata.com/scraping-automation/web-data-apis/web-scraper-api/overview#via-deliver-to-external-storage)または[webhook](https://docs.brightdata.com/scraping-automation/web-data-apis/web-scraper-api/overview#via-webhook)へ配信できます。

## Support & Resources
- **API Documentation:** [Bright Data Docs](https://docs.brightdata.com/scraping-automation/web-scraper-api/trigger-a-collection)
- **Scraping Best Practices:** [Avoid Getting Blocked](https://brightdata.jp/blog/web-data/web-scraping-without-getting-blocked)
- **Technical Support:** [Contact Us](mailto:support@brightdata.com)