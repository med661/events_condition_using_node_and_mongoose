# events_condition_using_node_and_mongoose

const mongoose = require('mongoose');

// Connect to MongoDB
mongoose.connect('mongodb://localhost/calendar', { useNewUrlParser: true });

// Define the event schema
const eventSchema = new mongoose.Schema({
  title: { type: String, required: true },
  start: { type: Date, required: true },
  end: { type: Date, required: true },
});

// Create the Event model
const Event = mongoose.model('Event', eventSchema);

const startDate = new Date('2022-01-01T00:00:00');
const endDate = new Date('2022-01-31T23:59:59');

// Get all events between a start date and end date
Event.find(
{ $and: [
            { start: { $gte: endDate } },
            { end: { $lte: startDate } },
            ]}, (error, events) => {
    if (error) {
      console.log(error);
    } else {
      console.log(events);
    }
});
