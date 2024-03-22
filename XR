pip install tweepy
import tweepy
from datetime import datetime

# Twitter API credentials
consumer_key = "2Jz6eDNC1lmFnjKdgpAVKSYAq"
consumer_secret = "joCLK0Aw6K8AtnwnPvUCfgkHyBk7FfRp1tTCdcoYycW0HcxL7s"
access_token = "1546159325470756865-B6sWAOd3oj0zuQEOV1bGsM3fTj74a2"
access_token_secret = "1gFPZnWScpmQCjbt1zFORw6XRFuRnDYkPYAzOdt56OalN"

# Authenticate
auth = tweepy.OAuth1UserHandler(consumer_key, consumer_secret, access_token, access_token_secret)
api = tweepy.API(auth)

def scrape_user_tweets(username, start_date, end_date, max_tweets=100):
    tweets = []
    for tweet in tweepy.Cursor(api.user_timeline, screen_name=username, tweet_mode="extended").items(max_tweets):
        if tweet.created_at >= start_date and tweet.created_at <= end_date:
            tweets.append(tweet)
    return tweets

if __name__ == "__main__":
    username = input("@ExtinctionR")
    start_date_str = input("(2024-01-01)")
    end_date_str = input("(2024-02-28)")
    max_tweets = int(input("100"))

    start_date = datetime.strptime(start_date_str, "%Y-%m-%d")
    end_date = datetime.strptime(end_date_str, "%Y-%m-%d")

    user_tweets = scrape_user_tweets(username, start_date, end_date, max_tweets)

    print(f"Scraped {len(user_tweets)} tweets from {username} between {start_date} and {end_date}:")
    for tweet in user_tweets:
        print(tweet.full_text)
