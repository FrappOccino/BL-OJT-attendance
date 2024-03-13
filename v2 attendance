function breakInBtn(){
  var ui = SpreadsheetApp.getUi();
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();

  var response = ui.alert(
    'Break In?',
    '',
    ui.ButtonSet.YES_NO
  )

    if (response == ui.Button.NO) {
      return;
    }

    else{
      var nameEntered;
      var lastName;
      do {
        nameEntered = promptForName(ui);
        lastName = getLastName(nameEntered);
        if (lastName === "who you?") {
          ui.alert('Invalid name', 'Please enter a valid name.', ui.ButtonSet.OK);
        }
      } while (lastName === "who you?");

      var currentTime = new Date();
        var timeString = Utilities.formatDate(currentTime, Session.getScriptTimeZone(), 'HH:mm:ss');

        // check the name entered in spread sheet and the matching current date
        var data = sheet.getDataRange().getValues(); 
        for (var i = 1; i < data.length; i++) {
          if (data[i][0] === nameEntered && new Date(data[i][2]).toDateString() === new Date().toDateString()) {
            sheet.getRange('F' + (i + 1)).setValue(timeString);
            Logger.log('Break In inserted in column G for ' + nameEntered);
            break;
          }
        }
    }
}

function breakOutBtn(){
  var ui = SpreadsheetApp.getUi();
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();

  var response = ui.alert(
    'Break Out?',
    '',
    ui.ButtonSet.YES_NO
  )

    if (response == ui.Button.NO) {
      return;
    }

    else{
      var nameEntered;
      var lastName;
      do {
        nameEntered = promptForName(ui);
        lastName = getLastName(nameEntered);
        if (lastName === "who you?") {
          ui.alert('Invalid name', 'Please enter a valid name.', ui.ButtonSet.OK);
        }
      } while (lastName === "who you?");

      var currentTime = new Date();
        var timeString = Utilities.formatDate(currentTime, Session.getScriptTimeZone(), 'HH:mm:ss');

        // check the name entered in spread sheet and the matching current date
        var data = sheet.getDataRange().getValues(); 
        for (var i = 1; i < data.length; i++) {
          if (data[i][0] === nameEntered && new Date(data[i][2]).toDateString() === new Date().toDateString()) {
            sheet.getRange('G' + (i + 1)).setValue(timeString);

            var breakOutVal = sheet.getRange('G' + (i + 1)).getValue();
            var breakInVal = sheet.getRange('F' + (i + 1)).getValue();
            
            // Calculate the work duration in milliseconds
            var workDurationMillis = breakOutVal.getTime() - breakInVal.getTime();
            
            
            if(workDurationMillis < 3.6e+6 ){
              sheet.getRange('M' + (i + 1)).setValue("Goods");
              
            } else {
              sheet.getRange('M' + (i + 1)).setValue("Over break");

            }
            Logger.log('Break Out inserted in column G for ' + nameEntered);
            break;
          }
        }
    }
}

function timeInBtn(){
  var ui = SpreadsheetApp.getUi();
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();

  var response = ui.alert(
    'Time in?',
    '',
    ui.ButtonSet.YES_NO
  );

  if (response == ui.Button.NO) {
    return;
  }

  else{
    var nameEntered;
    var lastName;
    do {
      nameEntered = promptForName(ui);
      lastName = getLastName(nameEntered);
      if (lastName === "who you?") {
        ui.alert('Invalid name', 'Please enter a valid name.', ui.ButtonSet.OK);
      }
    } while (lastName === "who you?");
    
    var lastRow = sheet.getLastRow();
    var currentTime = new Date();
    var timeString = Utilities.formatDate(currentTime, Session.getScriptTimeZone(), 'HH:mm:ss');

    sheet.getRange('A' + (lastRow + 1)).setValue(nameEntered);
    sheet.getRange('B' + (lastRow + 1)).setValue(lastName);
    sheet.getRange('C' + (lastRow + 1)).setValue(new Date());
    sheet.getRange('D' + (lastRow + 1)).setValue(timeString);

    Logger.log('Name entered: ' + nameEntered);
    Logger.log('Last name inserted: ' + lastName);
    Logger.log('Current time inserted in columns C and D.');
  }
}




function timeOutButton() {
  var ui = SpreadsheetApp.getUi();
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();

  var response = ui.alert(
    'Time out?',
    '',
    ui.ButtonSet.YES_NO
  );

  if (response == ui.Button.NO) {
    return;
  } else {
    var nameEntered;
    var lastName;
    do {
      nameEntered = promptForName(ui);
      lastName = getLastName(nameEntered);
      if (lastName === "who you?") {
        ui.alert('Invalid name', 'Please enter a valid name.', ui.ButtonSet.OK);
      }
    } while (lastName === "who you?");

    var currentTime = new Date();
    var timeString = Utilities.formatDate(currentTime, Session.getScriptTimeZone(), 'HH:mm:ss');

    var data = sheet.getDataRange().getValues();
    for (var i = 1; i < data.length; i++) {
      if (data[i][0] === nameEntered && new Date(data[i][2]).toDateString() === new Date().toDateString()) {
        sheet.getRange('E' + (i + 1)).setValue(timeString);

        var timeOutVal = sheet.getRange('E' + (i + 1)).getValue();
        var timeInVal = sheet.getRange('D' + (i + 1)).getValue();
        
        // Calculate the work duration in milliseconds
        var workDurationMillis = timeOutVal.getTime() - timeInVal.getTime();
        
        // Convert milliseconds to hours, minutes, seconds
        var hours = Math.floor(workDurationMillis / (1000 * 60 * 60));
        var minutes = Math.floor((workDurationMillis % (1000 * 60 * 60)) / (1000 * 60));
        var seconds = Math.floor((workDurationMillis % (1000 * 60)) / 1000);
        
        // Format the work duration as HH:mm:ss
        var formattedDuration = hours.toString().padStart(2, '0') + ':' +
                                minutes.toString().padStart(2, '0') + ':' +
                                seconds.toString().padStart(2, '0');

        // Set the formatted work duration in column L
        sheet.getRange('L' + (i + 1)).setValue(formattedDuration);

        Logger.log('Time out inserted in column E for ' + nameEntered + timeString + " workDuration: " + formattedDuration + " TimeOut: " + timeOutVal + " TimeIn: " + timeInVal);
        break;
      }
    }
  }
}




function promptForName(ui) {
  var input = ui.prompt('Enter name:');
  return input.getResponseText();
}

function getLastName(nameEntered) {
  switch (nameEntered.toLowerCase()) {
    case "kurt":
      return "garcia";
    case "jeff":
      return "wong";
    case "cyjay":
      return "cunanan";
    case "joshuac":
      return "carbungco";
    case "joshuan":
      return "lee";
    case "mark":
      return "santos";
    default:
      return "who you?";
  }
}

function onEdit(e) {
  updateCountdown();
}

function onOpen() {
  updateCountdown();
}

function updateCountdown() {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  var targetDate = new Date(sheet.getRange('U1').getValue());

  var now = new Date();
  var timeDiff = targetDate - now;

  if (timeDiff <= 0) {
    sheet.getRange('O28').setValue('Countdown completed!');
  } else {
    var days = Math.floor(timeDiff / (1000 * 60 * 60 * 24));
    var hours = Math.floor((timeDiff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
    var minutes = Math.floor((timeDiff % (1000 * 60 * 60)) / (1000 * 60));
    var seconds = Math.floor((timeDiff % (1000 * 60)) / 1000);

    sheet.getRange('O28').setValue(days + ' days ' + hours + ' hours ' + minutes + ' minutes ' + seconds + ' seconds');
  }
}
