# Import package
import tweepy
import json

# Store OAuth authentication credentials in relevant variables
access_token = "893472552936382468-huNxRsyYKfqT3LcuYBfAJktnDTap00b"
access_token_secret = "ZWvy1xMLZL4R43o7P0RkOJJk4LI02PMTW6t8CFiW6wDVV"
consumer_key = "LMDyYkChUODHEgA1qqHN43hD8"
consumer_secret = "RkxKvQ2nyOQqeCQe8yEYLfqXBUkQT8V2fzXWRPPbAed9bl9c2g"


# Pass OAuth details to tweepy's OAuth handler
auth = tweepy.OAuthHandler(consumer_key,consumer_secret)
auth.set_access_token(access_token,access_token_secret)

class MyStreamListener(tweepy.StreamListener):
    def __init__(self, api=None):
        super(MyStreamListener, self).__init__()
        self.num_tweets = 0
        self.file = open("tweets.txt", "w")

    def on_status(self, status):
        tweet = status._json
        self.file.write( json.dumps(tweet) + '\n' )
        self.num_tweets += 1
        if self.num_tweets < 100:
            return True
        else:
            return False
        self.file.close()

    def on_error(self, status):
        print(status)

# Initialize Stream listener
l = MyStreamListener()

# Create you Stream object with authentication
stream = tweepy.Stream(auth,l)


# Filter Twitter Streams to capture data by the keywords:
k=input("Enter the keyword: ").strip().split()
print("Please wait for few min for the output")
stream.filter(track=k)


# String of path to file: tweets_data_path
tweets_data_path="tweets.txt"

# Initialize empty list to store tweets: tweets_data
tweets_data=[]

# Open connection to file
tweets_file = open(tweets_data_path, "r")
# Read in tweets and store in list: tweets_data
for line in tweets_file:
    tweet=json.loads(line)
    tweets_data.append(tweet)

# Close connection to file
tweets_file.close()

# Print the keys of the first tweet dict
print(tweets_data[0].keys())
print(tweets_data[0]["entities"])

di={}
l1=[y["user"]["name"] for y in tweets_data]
l2=[y["user"]["statuses_count"] for y in tweets_data]
l3=[]
for y in tweets_data:
    
    a=(y["entities"]["urls"])
    
    if a==[]:
        l3.append(0)
    else:
        l3.append(a)
l4=[]        
for x in l3:
    if x==0:
        l4.append("link not used")
    else:
        l4.append(x[0]["expanded_url"])
        
        
        
di["NAMES"]=l1
di["COUNT OF TWEETS"]=l2
di["LINK REPORT"]=l4


# Import package
import pandas as pd

# Build DataFrame of tweet texts and languages
df = pd.DataFrame(di)


# Print head of DataFrame
print(df.head(n=100))



