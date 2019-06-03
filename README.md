# Show databases and collections:
MongoDB Enterprise TestCluster-shard-0:PRIMARY> show databases
admin  0.000GB
local  3.872GB
video  0.001GB
MongoDB Enterprise TestCluster-shard-0:PRIMARY> show collections
movieDetails
moviesScratch

# Simple select:
db.movies.find({mpaaRating: "PG-13"}).pretty()
db.movies.find({cast: ["Jeff Bridges", "Tim Robbins"]}).pretty()

# Match one element of an array field cast:
db.movies.find({cast: "Jeff Bridges"}).count()
db.movies.find({"cast.0": "Jeff Bridges"}).count()

# Return just the title in results
db.movies.find({genre: "Action, Adventure"}, {title: 1})

# Dot notation for complex query 100YWeatherSmall:
db.data.find({"wind.direction.angle": 290}).pretty()

MongoDB Enterprise TestCluster-shard-0:PRIMARY> use video
MongoDB Enterprise TestCluster-shard-0:PRIMARY> db.movieDetails.find({"awards.wins": 2, "awards.nominations": 2}).count()
MongoDB Enterprise TestCluster-shard-0:PRIMARY> db.movieDetails.find({rated: "PG-13", "awards.nominations": 10}).count()

# Query operator syntax:
https://docs.mongodb.com/manual/reference/operator/query/
db.movieDetails.find({writers: {$in: ["Ethan Coen", "Joel Coen"]}}).count()

# Query type
https://docs.mongodb.com/manual/reference/operator/query/type/
db.data.find({atmosphericPressureChange: {$exists: false}}).count()

db.shipwrecks.find({$or: [{watlev: "always dry"}, {depth: 0}]}).count()
db.data.find({sections: {$all: ["AG1", "MD1", "OA1"]}} ).count()
db.data.find({sections: {$size: 2}}).count()

martian = db.movieDetails.findOne({title: "The Martian"})
delete martian._id

db.movieDetails.find({boxOffice: {$elemMatch: {"country": "Germany", "revenue": {$gt: 16}}}})
db.surveys.find({results: {$elemMatch: {score: 7, product: "abc"}}}).count()