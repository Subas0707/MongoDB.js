# MongoDB.js
This file include all codes use in mongoDB for beginners

# Installation

1. Clone the repository:
git clone https://github.com/your-username/MongoDB.js.git
cd MongoDB.js

2.Install dependencies:
npm install

3. Create a .env file in the root directory and add your MongoDB URI:
MONGO_URI=your_mongo_connection_string

4.Run the application (ensure MongoDB is running):
node <your-script-name>.js

# Schema
A Person model is defined using Mongoose with the following schema:

name: String (required)
age: Number
favoriteFoods: Array of Strings

code:
const personSchema = new mongoose.Schema({
  name: { type: String, required: true },
  age: Number,
  favoriteFoods: [String]
});

# Functions
createAndSavePerson(done)
Creates a new person and saves them to the database.

js code:

const createAndSavePerson = (done) => {
  const newPerson = new Person({
    name: "John Doe",
    age: 25,
    favoriteFoods: ["Pizza", "Burger"]
  });
  newPerson.save(done);
};


createManyPeople(arrayOfPeople, done)
Adds multiple people to the database.

js code:
const createManyPeople = (arrayOfPeople, done) => {
  Person.create(arrayOfPeople, done);
};
findPeopleByName(personName, done)
Finds all people with a given name.

js code:
const findPeopleByName = (personName, done) => {
  Person.find({ name: personName }, done);
};
findOneByFood(food, done)
Finds one person by a favorite food.

js code:
const findOneByFood = (food, done) => {
  Person.findOne({ favoriteFoods: food }, done);
};
findPersonById(personId, done)
Finds a person by their unique _id.

js code:
const findPersonById = (personId, done) => {
  Person.findById(personId, done);
};
findEditThenSave(personId, done)
Finds a person by their _id, adds "hamburger" to their favoriteFoods, and saves the updated person.

js code:
const findEditThenSave = (personId, done) => {
  Person.findById(personId, (err, person) => {
    person.favoriteFoods.push("hamburger");
    person.save(done);
  });
};
findAndUpdate(personName, done)
Finds a person by name and updates their age to 20.

js code:
const findAndUpdate = (personName, done) => {
  Person.findOneAndUpdate({ name: personName }, { age: 20 }, { new: true }, done);
};
removeById(personId, done)
Removes a person by their _id.

js
Copy code
const removeById = (personId, done) => {
  Person.findByIdAndRemove(personId, done);
};
removeManyPeople(done)
Removes all people whose name is "Mary".

js code:
const removeManyPeople = (done) => {
  Person.remove({ name: "Mary" }, done);
};
queryChain(done)
Performs a chain of operations to find people who like "burrito", sorts them by name, limits the results to two, and hides their age.

js code:
const queryChain = (done) => {
  Person.find({ favoriteFoods: "burrito" })
    .sort({ name: 1 })
    .limit(2)
    .select({ age: 0 })
    .exec(done);
};
