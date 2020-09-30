# Desktop-Notifier
This is a simple desktop notifier made using python.

### Pre-Requisites:
- Requests: Requests is an elegant and simple HTTP library for Python, built for human beings.
- xml.etree.ElementTree: etree.ElementTree module implements a simple and efficient API for parsing and creating XML data.

### Importing libraries:

         import requests 
         import xml.etree.ElementTree as ET 
  
url of news rss feed 

         RSS_FEED_URL = "http://www.hindustantimes.com/rss/topnews/rssfeed.xml"    
  
         def loadRSS():
         
utility function to load RSS feed 
create HTTP request response object 

             resp = requests.get(RSS_FEED_URL) 
  
return response content 

             return resp.content 
  
         def parseXML(rss): 
         
utility function to parse XML format rss feed 
create element tree root object 

             root = ET.fromstring(rss) 
  
Create empty list for news items 

             newsitems = [] 
  
iterate news items 

             for item in root.findall('./channel/item'): 
                 news = {} 
  
iterate child elements of item 

                 for child in item: 
  
special checking for namespace object content:media
            
                     if child.tag == '{http://search.yahoo.com/mrss/}content': 
                         news['media'] = child.attrib['url'] 
                     else: 
                         news[child.tag] = child.text.encode('utf8') 
                 newsitems.append(news) 
                 
return news items list 

             return newsitems 
  
         def topStories(): 

main function to generate and return news items 

load rss feed 

             rss = loadRSS() 

parse XML

             newsitems = parseXML(rss) 
             return newsitems 
