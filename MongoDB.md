Import it into your local mongo database:

    $ mongoimport -d students -c grades < grades.json

Connect to mongo shell: ``$ mongo`` (interactive js interpreter).

    use students
    db.grades.count()
    
Inserting:

    db.people.insert({"name": "John"})
    
Drop collection:

    db.scores.drop();
    
Run JS:

    $ mongo < myjs.js
    
Query:

    db.people.findOne()
    db.people.find()

HW 2.1. Find all exam scores greater than or equal to 65, and sort those scores from lowest to highest.

    > db.grades.find({ "type" : "exam", "score": { $gte: 65 } }).sort( { "score": 1 } )
    { "_id" : ObjectId("50906d7fa3c412bb040eb5cf"), "student_id" : 22, "type" : "exam", "score" : 65.02518811936324 }
    { "_id" : ObjectId("50906d7fa3c412bb040eb743"), "student_id" : 115, "type" : "exam", "score" : 65.47329199925679 }

HW 2.2. Write a program in the language of your choice that will remove the grade of type "homework" with the lowest score for each student from the dataset in the handout. Since each document is one grade, it should remove one document per student.

    import pymongo
    import sys
    from bson.son import SON
    # pymongo.ASCENDING = 1, pymongo.DESCENDING = -1
    connection = pymongo.MongoClient('mongodb://localhost')
    db = connection.students
    grades = db.grades
    print grades.count()  # 800
    # Remove grades
    sid = -1
    soted_grades = grades.find({"type" : "homework"}).sort([
    	('student_id', pymongo.ASCENDING),
    	('score', pymongo.ASCENDING),
    ])
    for grade in soted_grades:
    	if grade['student_id'] != sid:
    		grades.delete_one(grade)
    	sid = grade['student_id']
    print grades.count()  # 600
    res = grades.find().sort([
    	('score', pymongo.DESCENDING),
    ]).skip(100).limit(1)
    print list(res)
    res = db.grades.find({},{'student_id': 1, 'type': 1, 'score': 1, '_id': 0}).sort([
    	('student_id', pymongo.ASCENDING),
    	('score', pymongo.ASCENDING)
    ]).limit(5)
    print list(res)
    pipeline = [
    	{ '$group' : { '_id' : '$student_id', 'average' : { '$avg' : '$score' } } },
    	{"$sort": SON([("average", -1),])},
    	{ '$limit' : 1 }
    ]
    res = grades.aggregate(pipeline)
    print 'RESULT:', list(res)
    
    # the student_id with the highest average score:
    db.grades.aggregate({
        '$group': {'_id':'$student_id', 'average':{$avg:'$score'}}
    },{
        '$sort':{'average':-1}
    },{
        '$limit':1
    })
