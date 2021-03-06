To use this script you can pass the following attributes:
    username: Username of a specific twitter account (without @)
       since: The lower bound date (yyyy-mm-aa)
       until: The upper bound date (yyyy-mm-aa)
 querysearch: A query text to be matched
        near: A reference location area from where tweets were generated
      within: A distance radius from "near" location (e.g. 15mi)
   maxtweets: The maximum number of tweets to retrieve
   toptweets: Only the tweets provided as top tweets by Twitter (no parameters required)
      output: A filename to export the results (default is "output_got.csv")

Examples:
# Example 1 - Get tweets by username [barackobama]
python Exporter.py --username "barackobama" --maxtweets 1

# Example 2 - Get tweets by query search [europe refugees]
python Exporter.py --querysearch "europe refugees" --maxtweets 1

# Example 3 - Get tweets by username and bound dates [barackobama, '2015-09-10', '2015-09-12']
python Exporter.py --username "barackobama" --since 2015-09-10 --until 2015-09-12 --maxtweets 1

# Example 4 - Get the last 10 top tweets by username
python Exporter.py --username "barackobama" --maxtweets 10 --toptweetsThe MIT License (MIT)

Copyright (c) 2016 Jefferson Henrique

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
# Get Old Tweets Programatically
A project written in Python to get old tweets, it bypass some limitations of Twitter Official API.

## Details
Twitter Official API has the bother limitation of time constraints, you can't get older tweets than a week. Some tools provide access to older tweets but in the most of them you have to spend some money before.
I was searching other tools to do this job but I didn't found it, so after analyze how Twitter Search through browser works I understand its flow. Basically when you enter on Twitter page a scroll loader starts, if you scroll down you start to get more and more tweets, all through calls to a JSON provider. After mimic we get the best advantage of Twitter Search on browsers, it can search the deepest oldest tweets.

## Prerequisites
This package assumes using Python 2.x. The Python3 "got3" folder is maintained as experimental and is not officially supported.

Expected package dependencies are listed in the "requirements.txt" file for PIP, you need to run the following command to get dependencies:
```
pip install -r requirements.txt
```

## Components
- **Tweet:** Model class to give some informations about a specific tweet.
  - id (str)
  - permalink (str)
  - username (str)
  - text (str)
  - date (date)
  - retweets (int)
  - favorites (int)
  - mentions (str)
  - hashtags (str)
  - geo (str)

- **TweetManager:** A manager class to help getting tweets in **Tweet**'s model.
  - getTweets (**TwitterCriteria**): Return the list of tweets retrieved by using an instance of **TwitterCriteria**. 

- **TwitterCriteria:** A collection of search parameters to be used together with **TweetManager**.
  - setUsername (str): An optional specific username from a twitter account. Without "@".
  - setSince (str. "yyyy-mm-dd"): A lower bound date to restrict search.
  - setUntil (str. "yyyy-mm-dd"): An upper bound date to restrist search.
  - setQuerySearch (str): A query text to be matched.
  - setTopTweets (bool): If True only the Top Tweets will be retrieved.
  - setNear(str): A reference location area from where tweets were generated.
  - setWithin (str): A distance radius from "near" location (e.g. 15mi).
  - setMaxTweets (int): The maximum number of tweets to be retrieved. If this number is unsetted or lower than 1 all possible tweets will be retrieved.
  
- **Main:** Examples of how to use.

- **Exporter:** Export tweets to a csv file named "output_got.csv".

## Examples of python usage
- Get tweets by username
``` python
	tweetCriteria = got.manager.TweetCriteria().setUsername('barackobama').setMaxTweets(1)
	tweet = got.manager.TweetManager.getTweets(tweetCriteria)[0]
	  
    print tweet.text
```    
- Get tweets by query search
``` python
	tweetCriteria = got.manager.TweetCriteria().setQuerySearch('europe refugees').setSince("2015-05-01").setUntil("2015-09-30").setMaxTweets(1)
	tweet = got.manager.TweetManager.getTweets(tweetCriteria)[0]
	  
    print tweet.text
```    
- Get tweets by username and bound dates
``` python
	tweetCriteria = got.manager.TweetCriteria().setUsername("barackobama").setSince("2015-09-10").setUntil("2015-09-12").setMaxTweets(1)
	tweet = got.manager.TweetManager.getTweets(tweetCriteria)[0]
	  
    print tweet.text
```
- Get the last 10 top tweets by username
``` python
	tweetCriteria = got.manager.TweetCriteria().setUsername("barackobama").setTopTweets(True).setMaxTweets(10)
	# first one
	tweet = got.manager.TweetManager.getTweets(tweetCriteria)[0]
	  
    print tweet.text
```

## Examples of command-line usage
- Get help use
```
    python Exporter.py -h
``` 
- Get tweets by username
```
    python Exporter.py --username "barackobama" --maxtweets 1
```    
- Get tweets by query search
```
    python Exporter.py --querysearch "europe refugees" --maxtweets 1
```    
- Get tweets by username and bound dates
```
    python Exporter.py --username "barackobama" --since 2015-09-10 --until 2015-09-12 --maxtweets 1
```
- Get the last 10 top tweets by username
```
    python Exporter.py --username "barackobama" --maxtweets 10 --toptweets
```
l x m l = = 3 . 5 . 0 
 
 p y q u e r y = = 1 . 2 . 1 0 
 
 