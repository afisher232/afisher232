pip install tweepy
import tweepy
from datetime import datetime

# Twitter API credentials
consumer_key = "your_consumer_key"
consumer_secret = "your_consumer_secret"
access_token = "your_access_token"
access_token_secret = "your_access_token_secret"

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
    username = input("Enter the Twitter username: ")
    start_date_str = input("Enter the start date (YYYY-MM-DD): ")
    end_date_str = input("Enter the end date (YYYY-MM-DD): ")
    max_tweets = int(input("Enter the maximum number of tweets to scrape: "))

    start_date = datetime.strptime(start_date_str, "%Y-%m-%d")
    end_date = datetime.strptime(end_date_str, "%Y-%m-%d")

    user_tweets = scrape_user_tweets(username, start_date, end_date, max_tweets)

    print(f"Scraped {len(user_tweets)} tweets from {username} between {start_date} and {end_date}:")
    for tweet in user_tweets:
        print(tweet.full_text)
