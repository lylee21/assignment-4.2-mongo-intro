//mongoDB notes
//start
resources:
https://www.cleancss.com/css-minify/
https://github.com/Skills-Union-NTU-SDI-Program/lesson-4.2-mongo-intro
==

//type this to start mongodb
mongosh 

//create a database (use <database name>)
use mongo-lesson

//create collection (db.createCollection("collection name"))
db.createCollection("invoice")

//insert many- wrapped by [] because it's an array
db.invoice.insertMany([ {"invoiceNo": "invoice_1", "items": [ {"item": "mobile charger", "price": 109.9, "warranty": 3 }, {"item": "pencil", "price": 1.5, "brand": "Dixon" }] }, {"invoiceNo": "invoice_2", "items": [ {"item": "system75", "price": 1000, "warranty": 1 }, {"item": "shipping", "price": 200, "company": "UPS" }] }])

//insert one 
db.invoice.insertOne({"invoiceNo": "invoice_3", "items": [ {"item": "fairy lights", "price": 12.9, "length": 10 }, {"item": "massage ball", "price": 4.9, "color": "green" }] })

//find
db.invoice.find() //finds all
db.invoice.find({invoiceNo:'invoice_1'}) //find invoice_1
db.invoice.find({"items.price":{$lte:10}}) //find items.price less than 10
db.invoice.find({"items.price":{$gte:10}}) //find items.price greater than 10
db.invoice.find({"items.item":/^s/}) //find items.item starting with 's', ^ means start
db.invoice.find({"items.item":/s/}) //find items.item containing 's'
db.invoice.find({"items.item":/s$/}) //find items.item ending with 's'

//update database
db.invoice.updateOne({invoiceNo:'invoice_3'}, {$set: {invoiceNo:'invoice_4'}})
db.invoice.updateMany({}, {$set: {status:'paid'}})
db.invoice.deleteMany({"items.warranty":{"$exists":false}})
db.invoice.deleteOne({"invoiceNo": "invoice_3"})