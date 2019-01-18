# Setup schema + Model

`var mongoose = require('mongoose');`

_1) create schema.._

`var UserSchema = new mongoose.Schema({schema-object})`

```javascript
sample_schema :
{
    name: String
    memberOn: {
        type: Date,
        default: Date.now()
    },
    location: Array,
    activeToday: Boolean,
    employer: {
        type: Schema.ObjectId,
        ref: 'Company'}
    //EMBEDDED SUB DOCUMENT
    bio: {
        age: Number,
        address: String,
        heightInCms: Number,
        nationality: String }
}
```

_2) then export Schema as a 'Model'_

```module.exports = mongoose.model('User', UserSchema)```

# Create functions

_1) install npm dependencies_
npm i --save mongoose body-parser express

_2) require the relevant Model in the file that has functions that will use the Model_

`const User = require(./Models/User)`

_3) connect to DB_

`mongoose.connect(<DB URI string>)`

___Finding Items From DB___
1. `<Model>.find({}).exec((err, documents)=>{})` -> returns all 'documents' in the collection that bears the name of this Model
so User.find({}) will fetch all User documents from the 'users' collection that Mongoose automatically created when exporting the model.  

2. `<Model>.findOne({_id: 'XXXXX'}).exec((err, document)=>{}) `   This will need the `body-parser` npm package to access the path variable that connotes the id of the document we want to receive.  The path variable looks like this: example.com/path/:id. Accessing the `:id` variable depends on what environment you're in - for example, Lambda Functions makes these accessible in the events object that gets passed into the lambda function when invoked.  If you're using an express app then it will look like:
```javascript
app.get('/path/:id', (req, res)=>{
    let id = req.params.id
    ///use id in findOne()
})
```

___Post an item to DB___
__setup for express__
We need to use `body-parser` to get JSON off the url.
```javascript
app.use(bodyParser.json())
app.use(bodyParser.urlencoded({
  extended: true
}));
```

___use the Mongoose create method___

The usual way of using this is with an established Schema.  Let's assume its a book schema with three fields : title, author and category.  We then would have an express post route that creates a new Book object from the Schema, sets its properties/fields and saves. It looks like this:
```javascript
app.post('/book', function(req, res) {
  var newBook = new Book();

  newBook.title = req.body.title;
  newBook.author = req.body.author;
  newBook.category = req.body.category;

  newBook.save(function(err, book) {
    if(err) {
      res.send('error saving book');
    } else {
      console.log(book);
      res.send(book);
    }
  });
});
```

__NB: Note how the above does NOT use the Mongoose Create method?__

Method 2 uses it, as below:
```javascript
app.post('/book2', function(req, res) {
  Book.create(req.body, function(err, book) {
    if(err) {
      res.send('error saving book');
    } else {
      console.log(book);
      res.send(book);
    }
  });
});
```

___Update with findOneAndUpdate()___
This Mongoose method takes 4 arguments
1. the query/conditions which looks like `{_id: req.params.id}`
2. the update which looks like `{ $set: { title: req.body.title } }`
3. a config option (if you want to create a document where none currently exists, default is false) - `{upsert: true}`
4. the callback that takes in two arguments, the error (if any) and the updated Document

See below:
```javascript
app.put('/book/:id', function(req, res) {
  Book.findOneAndUpdate({
    _id: req.params.id
    },
    { $set: { title: req.body.title }
  }, {upsert: true}, function(err, newBook) {
    if (err) {
      res.send('error updating ');
    } else {
      console.log(newBook);
      res.send(newBook);
    }
  });
});
```