🌟  Social Media Analysis Using SQL 🌟
📌 Overview
This project dives into Social Media Data Analysis using SQL, creating and interacting with a database that mimics a real-world social media platform. From tracking user activity to analyzing hashtags, posts, and follower interactions, this project demonstrates SQL’s power to extract valuable insights.

🏗️ Database Schema
The database is named social_media and consists of these main tables:

Users: Stores user profiles, emails, and bios.
Post: Contains photo/video posts with captions and locations.
Comments: Tracks comments on posts by users.
Likes: Includes post likes and comment likes.
Follows: Represents follower-followee relationships.
Hashtags: Tracks popular tags and user-tag interactions.
Key constraints include:

Photo size: Limited to 5MB.
Video size: Limited to 10MB.
Timestamps: To track all user interactions.
🛠️ SQL Queries & Insights
1️⃣ Location of Users 📍
Find users posting from key locations:

sql
Copy code
SELECT * FROM post WHERE location IN ('agra', 'maharashtra', 'west bengal');
2️⃣ Most Followed Hashtags 🔥
Identify trending hashtags based on follow count:

sql
Copy code
SELECT hashtag_name AS 'Hashtags', COUNT(hashtag_follow.hashtag_id) AS 'Total Follows'  
FROM hashtag_follow, hashtags  
WHERE hashtags.hashtag_id = hashtag_follow.hashtag_id  
GROUP BY hashtag_follow.hashtag_id  
ORDER BY COUNT(hashtag_follow.hashtag_id) DESC LIMIT 5;
3️⃣ Inactive Users 🚫
Who hasn’t posted anything?

sql
Copy code
SELECT user_id, username AS 'Most Inactive User' FROM users WHERE user_id NOT IN (SELECT user_id FROM post);
4️⃣ User Who Liked Every Post (Bot Check 🤖)
Find suspiciously active users:

sql
Copy code
SELECT username, COUNT(*) AS num_likes  
FROM users  
INNER JOIN post_likes ON users.user_id = post_likes.user_id  
GROUP BY post_likes.user_id  
HAVING num_likes = (SELECT COUNT(*) FROM post);
5️⃣ Followers > 40 🚀
Users with the highest follower count:

sql
Copy code
SELECT followee_id, COUNT(follower_id) AS follower_count  
FROM follows  
GROUP BY followee_id  
HAVING follower_count > 40  
ORDER BY COUNT(follower_id) DESC;
📊 Project Highlights
Data Insights: Uncover active users, hashtag trends, and suspicious bot-like activity.
Database Design: Emphasis on scalability and real-world application.
Constraints & Validations: Ensure logical and clean data storage.
📁 Repo Contents
Schema: schema.sql to create and configure the database.
Queries: queries.sql contains SQL scripts for analysis.
Readme: Detailed project documentation.
🚀 Contributions
Feel free to fork this repo, improve queries, or expand the analysis. Let’s make social media data more insightful! 😊

Let me know if you'd like additional changes or enhancements! ​
