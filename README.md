# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.

Fill the parts marked '_enter' in the **Tasks** section below.

## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file
2. Acess to the Server for storing the PDF report which is generated every week.
3. Libraries required to perform read operation on the input data csv files (eg: csv, pandas)
4. Libraries or Tools required to generate the PDF reports (eg: Pylatex)
5. API's required to send notifications like email/sms when a new report is available.
6. Libraries required to get system date and time.
7. Libraries for decoding the physical signal values of Battery Telemetrics if the signals are stored in a different format or encoded form.


### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | Yes           | This is part of the software being developed as a PDF report need to be generated.
Counting the breaches       | Yes           | This is part of the software being developed to detect if threshold value is breached.
Detecting trends            | Yes           | This is part of the software being developed
Notification utility        | Yes           | This is part of the software being developed to send notification in case of breach.

### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings.
2. Write Date and Time to the PDF when the reading continuously increases for 30 mins.
3. Write "Invalid input" to the PDF when the csv doesn't contain expected data.
4. Write "Data Unavailable" to the PDF when the csv file is empty or does not exist in the server.
5. Write the count of breaches to the PDF report when the number of times the measured value crosses the threshold value in a month.
6. Write a notification " Report Available", when a new report is available.
7. Write "Success", when a PDF report is stored successfully in the server.


### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input        | Output                      | Faked/mocked part
|--------------------------|--------------|-----------------------------|---
Read input from server     | csv file     | internal data-structure     | Fake the server store
Validate input             | csv data     | valid / invalid             | None - it's a pure function
Notify report availability | pdf file     | Available / Not available             | Fake the notification
Report inaccessible server | csv data     | valid / invalid             | Fake the server store
Find minimum and maximum   | csv data     | Minimum, Maximum           | None - it's a pure function
Detect trend               | csv data     | Battery Telemetrics Value,Date & Time            | None - it's a pure function
Write to PDF               | csv data     | PDF file with Minimum, Maximum, Date & Time Value             | Fake the PDF store
