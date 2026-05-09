# Introduction
A Database must be 
- Reliable: 
	- Tolerating hardware and software faults
	- Human error
- Scalable: 
	- Measuring load and performance
	- Latency percentiles and throughput
- Maintainable
	- Operability
	- simplicity
	- evolvability
***
## Scalability
To first understand scalability, we need to find our load parameters. These parameters differs depending on the architecture of our system. It might be
- requests per second
- waiting users in the lobby
- the ratio or reads and writes on a db
- the hit rate on a cache, etc
# The Twitter example
At 2012, Twitters' main operations were
- Post tweet: A user can publish a new message to their followers
	- 4.6k requests/sec on average
	- 12k requests/sec at peak
- Home timeline: a user can view the posts of people they follow
	- 300k requests/sec 

So, in their architecture, handling even the peak rate of posting tweets, i.e 12k requests/sec, would be fairly easy. ==But the main problem was not due to tweeting volume but due to the fan-out.==
**Fan-out: Each user follows many people and each user is followed by many people**
### Two ways of implementation of this problem that twitter used
#### 1. The relational database approach (FIRST VERSION OF TWITTER USED THIS)
- Post tweet: Posting a tweet simple inserts the tweet in the global records of tweet
- Home timeline: When the users requests their home timeline
	1. Look up all the people the user follows
	2. find all the tweets for each of those users
	3. merge them sorted by their timestamp

Twitter's version:
> get all tweets → append users → match as followee → filter follower_id = current user

```sql
SELECT tweets.*, users.* FROM tweets JOIN users ON tweets.sender_id = users.id JOIN follows ON follows.followee_id = users.id WHERE follows.follower_id = current_user
```

My version:
> start with follows → follower_id primary → extend followee with users → extend with tweets → filter follower_id = current user

```sql
SELECT tweets.*, users.*
FROM follows
JOIN users
  ON follows.followee_id = users.id
JOIN tweets
  ON tweets.sender_id = users.id
WHERE follows.follower_id = current_user
```
- this query is much more selective than the first one

#### 2. The central mailbox of tweets (TWITTER CURRENTLY USES THIS)
- maintain a cache for each user's home timeline
- when a user posts a new tweet
	1. look up all the people who follows this particular user
	2. insert a new tweet in their home timeline cache
However the downside of this approach is that, posting a new tweet now requires a lot of extra work. 
- The before 4.6k average tweet writes now becomes 345k writes/second to the home timeline caches
- But this average hides the fact that some users have wildly large followers count. e.g 30 million, which means 30million writes for their single tweet!

## ==in the example of twitter, the distribution of followers per user is a key load parameter for considering scalability.==

Twitter is now moving to a hybrid approach where most users use the second approach but a small sub-section of users with stupidely large followers count are excepted from this fan-out. Tweets from these account are fetched separately and merged with home timelines when need like in approach 1.
