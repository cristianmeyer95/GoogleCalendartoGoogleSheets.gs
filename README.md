# GoogleCalendartoGoogleSheets.gs
Unique and original workflow to automatically update 
function updateCalendar()
{
  var spreadsheet = SpreadsheetApp.getActiveSheet();
    var eventCal = CalendarApp.getCalendarById('37628bbf188e30a0059739322755059842c411c36bfccbecfdc1c65c4a2e199c@group.calendar.google.com');            

  //Please note: Months are represented from 0-11 (January=0, February=1). Ensure dates are correct below before running the script.
  var fromDate = new Date(2020,5,1,0,0,0); //This represents June 1st 2020
  var toDate = new Date(2040,5,30,0,0,0); //This represents June 30th 2030
  
  
  //Search for events between fromdate and todate with given search criteria
  var events = eventCal.getEvents(fromDate,toDate);
  for(var i=0; i<events.length;i++) //loop through all events
  {
    var ev = events[i];
    Logger.log('Event: '+ev.getTitle()+' found on '+ev.getStartTime()); // Log event name and title
      ev.deleteEvent(); // delete event
  }


  
  var spreadsheet = SpreadsheetApp.getActiveSheet();
   
    var eventCal = CalendarApp.getCalendarById('37628bbf188e30a0059739322755059842c411c36bfccbecfdc1c65c4a2e199c@group.calendar.google.com');            

var schedule = spreadsheet.getDataRange().getValues();
schedule.splice(0, 5);
 
 
 // Check the event doesn't exist
 schedule.forEach(function(entry) {
    var crew = entry[7];
   
var newjob = eventCal.createEvent( entry[4], entry[2], entry[3]);
 var jobdetails = newjob.setDescription(entry[6]);
  var location = newjob.setLocation(entry[5]); })  
 
}
  function onOpen() {

var ui = SpreadsheetApp.getUi();
ui.createMenu('Sync to Calendar')
.addItem('Sync To Google Calendar', 'updateCalendar' )
.addToUi()
}
