Download Latest JDk or jdk 11
Download Jenkins.war from website
java -jar jenkins.war
by deafult it starts in port 8080

java -jar jenkins.war --httpPort=9090
manually starting in new port


Admin Password Location
C:\Users\ishan\.jenkins\secrets\initialAdminPassword

My Password 5ae6c25fd1424f9d98d219c84bbd2d72

next time when you login 
username is - admin
password is - 5ae6c25fd1424f9d98d219c84bbd2d72


To Shut Down Jenkin Use CTRL + C 

Use NGROK to tunnel local host






-----------------------------------------------------

CRON JOB /SHEDULING

Field	Possible Values	Syntax	Description
[a] – Minute	0 – 59					7 * * * * 	The cron job is initiated every time the system clock shows 7 in the minute’s position.
[b] – Hour	0 – 23					0 7 * * *	The cron job runs any time the system clock shows 7am (7pm would be coded as 19).
[c] – Day	0 – 31					0 0 7 * * 	The day of the month is 7 which means that the job runs every 7th day of the month.
[d] – Month	0 = none and 12 = December		0 0 0 7 *	The numerical month is 7 which determines that the job runs only in July.
[e] – Day of the Week	0 = Sunday and 7 = Sunday	0 0 * * 7 	7 in the current position means that the job would only run on Sundays.

examples
Cron Job	Command
Run Cron Job Every Minute	* * * * * /root/backup.sh
Run Cron Job Every 30 Minutes	30 * * * * /root/backup.sh
Run Cron Job Every Hour	0 * * * */root/backup.sh
Run Cron Job Every Day at Midnight	0 0 * * * /root/backup.sh
Run Cron Job at 2 am Every Day	0 2 * * * /root/backup.sh
Run Cron Job Every 1st of the Month	0 0 1 * * /root/backup.sh
Run Cron Job Every 15th of the Month	0 0 15 * * /root/backup.sh
Run Cron Job on December 1st – Midnight	0 0 0 12 * /root/backup.sh
Run Cron Job on Saturday at Midnight	0 0 * * 6 /root/backup.sh



==========================================================================
This field follows the syntax of cron (with minor differences). Specifically, each line consists of 5 fields separated by TAB or whitespace:
MINUTE HOUR DOM MONTH DOW
MINUTE	Minutes within the hour (0–59)
HOUR	The hour of the day (0–23)
DOM	The day of the month (1–31)
MONTH	The month (1–12)
DOW	The day of the week (0–7) where 0 and 7 are Sunday.
To specify multiple values for one field, the following operators are available. In the order of precedence,

* specifies all valid values
M-N specifies a range of values
M-N/X or */X steps by intervals of X through the specified range or whole valid range
A,B,...,Z enumerates multiple values
To allow periodically scheduled tasks to produce even load on the system, the symbol H (for “hash”) should be used wherever possible. For example, using 0 0 * * * for a dozen daily jobs will cause a large spike at midnight. In contrast, using H H * * * would still execute each job once a day, but not all at the same time, better using limited resources.

The H symbol can be used with a range. For example, H H(0-7) * * * means some time between 12:00 AM (midnight) to 7:59 AM. You can also use step intervals with H, with or without ranges.

The H symbol can be thought of as a random value over a range, but it actually is a hash of the job name, not a random function, so that the value remains stable for any given project.

Beware that for the day of month field, short cycles such as */3 or H/3 will not work consistently near the end of most months, due to variable month lengths. For example, */3 will run on the 1st, 4th, …31st days of a long month, then again the next day of the next month. Hashes are always chosen in the 1-28 range, so H/3 will produce a gap between runs of between 3 and 6 days at the end of a month. (Longer cycles will also have inconsistent lengths but the effect may be relatively less noticeable.)

Empty lines and lines that start with # will be ignored as comments.

In addition, @yearly, @annually, @monthly, @weekly, @daily, @midnight, and @hourly are supported as convenient aliases. These use the hash system for automatic balancing. For example, @hourly is the same as H * * * * and could mean at any time during the hour. @midnight actually means some time between 12:00 AM and 2:59 AM.

Examples:

# Every fifteen minutes (perhaps at :07, :22, :37, :52):
H/15 * * * *
# Every ten minutes in the first half of every hour (three times, perhaps at :04, :14, :24):
H(0-29)/10 * * * *
# Once every two hours at 45 minutes past the hour starting at 9:45 AM and finishing at 3:45 PM every weekday:
45 9-16/2 * * 1-5
# Once in every two hour slot between 8 AM and 4 PM every weekday (perhaps at 9:38 AM, 11:38 AM, 1:38 PM, 3:38 PM):
H H(8-15)/2 * * 1-5
# Once a day on the 1st and 15th of every month except December:
H H 1,15 1-11 *
Time zone specification
Periodic tasks are normally executed at the scheduled time in the time zone of the Jenkins master JVM (currently Asia/Calcutta). This behavior can optionally be changed by specifying an alternative time zone in the first line of the field. Time zone specification starts with TZ=, followed by the ID of a time zone.

Complete example of a schedule with a time zone specification:

    TZ=Europe/London
    # This job needs to be run in the morning, London time
    H 8 * * *
    # Butlers do not have a five o'clock, so we run the job again
    H(0-30) 17 * * *
  
The supported time zones depend on the Java runtime Jenkins is running on. The list of supported time zone IDs on this instance is:

Africa/Abidjan


