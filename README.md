# -rakuten-auto-post
import requests
import tweepy
import random

APP_ID = "楽天のApplication ID"

url = "https://app.rakuten.co.jp/services/api/IchibaItem/Search/20220601"

params = {
    "applicationId": APP_ID,
    "keyword": "日焼け止め",
    "hits": 30
}

res = requests.get(url, params=params).json()

item = random.choice(res["Items"])["Item"]

title = item["itemName"][:60]
link = item["affiliateUrl"]

tweet = f"""
おすすめ商品☀️

{title}

{link}

#楽天アフィリエイト
"""

client = tweepy.Client(
    consumer_key="API_KEY",
    consumer_secret="API_SECRET",
    access_token="ACCESS_TOKEN",
    access_token_secret="ACCESS_SECRET"
)

client.create_tweet(text=tweet)

print("投稿成功")
