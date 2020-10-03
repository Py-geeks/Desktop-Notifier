# Desktop-Notifier
This is a simple desktop notifier made using python.

### Importing libraries:
   
         import feedparser
         import notify2
         import time
         import os
  

         f = feedparser.parse("http://feeds.bbci.co.uk/news/rss.xml")
         
Here feedparser will parse the news data from the feed URL. The parsed data will be in the form of dictionary.


         ICON_PATH = os.getcwd() + "/icon.ico"
         
If you want to set any icon in the notification then here we are setting the Icon path. This is optional.


         notify2.init('News Notify')
         
Here we are initializing the notify2 using the init method of notify2. Initialize the D-Bus connection. Must be called before you send any notifications, or retrieve server info or capabilities.
 
         for newsitem in f['items']: 
                 n = notify2.Notification(newsitem['title'], 
                                          newsitem['summary'], 
                                          icon=ICON_PATH 
                                          )
                                          
Looping from the parsed data to get the relevant information like news title, short summary and setting the notification icon using the Notification method of the notify2 lib.

         n.set_urgency(notify2.URGENCY_NORMAL)

Set the urgency level to one of URGENCY_LOW, URGENCY_NORMAL or URGENCY_CRITICAL

         n.show()

This method will show the notification on the Desktop

         n.set_timeout(15000)

Setting the time to keep the notification on the desktop (in milliseconds). I have set here as 15 seconds.

         time.sleep(1200)
         
This will usually display the news notification every 20 mins. You can set the time as per your requirement.
