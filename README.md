# NoSql-Challenge

# Eat Safe, Love

## The UK Food Standards Agency evaluates various establishments across the United Kingdom, and gives them a food hygiene rating. You've been contracted by the editors of a food magazine, Eat Safe, Love, to evaluate some of the ratings data in order to help their journalists and food critics decide where to focus future articles.

# Part 1: Database and Jupyter Notebook Set Up:

establishments = db['establishments']

# Part 2: Update the Database:

## 1. An exciting new halal restaurant just opened in Greenwich, but hasn't been rated yet. The magazine has asked you to include it in your analysis. Add the following restaurant "Penang Flavours" to the database.

  establishments.insert_one(new_restaurant)

## 2. Find the BusinessTypeID for "Restaurant/Cafe/Canteen" and return only the BusinessTypeID and BusinessType fields.

  query = {'BusinessType': 'Restaurant/Cafe/Canteen'}
  fields = ['BusinessTypeID', 'BusinessType']

  establishments.find_one(query, fields)

## 3. Update the new restaurant with the BusinessTypeID you found.

  establishments.update_one(new_restaurant, {'$set': {'BusinessTypeID': 1}})

## 4. The magazine is not interested in any establishments in Dover, so check how many documents contain the Dover Local Authority. Then, remove any establishments within the Dover Local Authority from the database, and check the number of documents to ensure they were deleted.

  establishments.delete_many({'LocalAuthorityName': 'Dover'})
  pprint(establishments.count_documents({'LocalAuthorityName': 'Dover'}))

## 5. Some of the number values are stored as strings, when they should be stored as numbers.

  establishments.update_many({}, [{'$set': {'geocode.longitude': {'$toDouble': '$geocode.longitude'}, 
                                         'geocode.latitude': {'$toDouble': '$geocode.latitude'}}}]
                          )

establishments.update_many({}, [ {'$set':{ "RatingValue" : {'$toInt': "$RatingValue"}}} ])

  
# Part 3: Exploratory Analysis:
1. Which establishments have a hygiene score equal to 20?
There are 41 establishments with hygeine score of 20.

2. Which establishments in London have a RatingValue greater than or equal to 4?
There are 33 establishments in London that have a RatingValue greater than or equal to 4.

3. What are the top 5 establishments with a RatingValue of 5, sorted by lowest hygiene score, nearest to the new restaurant added, "Penang Flavours"?
The top 5 establishments with a RatingValue  of 5, sorted by lowest hygeine score are, Howe and Co Fish and Chips - Van 17, Plumstead Manor Nursery, Atlantic Fish Bar, Iceland, and Volunteer.

4.  How many establishments in each Local Authority area have a hygiene score of 0? Sort the results from highest to lowest
There are 55 documents in the result.

