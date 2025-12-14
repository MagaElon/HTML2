# HTML2
HTML
from html.parser import HTMLParser
from urllib.request import urlopen

class HeaderParser(HTMLParser):
  def __init__(self):
      super().__init__()
      self.foundOLTag = False
      self.wordsNextToOLTag = []

  def handle_starttag(self, tag, attrs):
          if tag.lower() == "ul":
              self.foundOLTag = True
          elif tag.lower() == "li":
              self.foundOLTag = False

  def handle_endtag(self, tag):
      if tag.lower() in "ol":
          self.foundOLTag = False

  def handle_data(self, data):
      if self.foundOLTag:
          self.wordsNextToOLTag.append(data.strip())

  def getWordsNextToOLTag(self):
      return self.wordsNextToOLTag

def testParser(url):
      content = urlopen(url).read().decode()
      parser = HeaderParser()
      parser.feed(content)
      return parser.getWordsNextToOLTag()

print(testParser('http://facweb.cdm.depaul.edu/asettle/web/list1.html'))

from html.parser import HTMLParser
from urllib.request import urlopen

class ImageTagCounter(HTMLParser):
   def __init__(self):
       super().__init__()
       self.count = 0
   def handle_starttag(self, tag, attrs):
       if tag == "img":
           self.count += 1

   def returnNumberOfImgTags(self):
       return self.count

def testParser(url):
   content = urlopen(url).read().decode()
   parser = ImageTagCounter()
   parser.feed(content)
   return parser.returnNumberOfImgTags()
maga = "https://www.grumpycats.com/"
print(testParser(maga))
#2e
#Should we code the handle_endtag or  handle_data for this code?
# No, We don't need handle_endtag or  handle_data in this code. Because handle_entag tags for 'img' are not needed bc 'img' is a self closing tag
#handle_data. we only need to count the number of 'img' tags.

from html.parser import HTMLParser
from urllib.request import urlopen

class CountCatInImageAlt(HTMLParser):
   def __init__(self):
       super().__init__()
       self.cat_count = 0
   def handle_starttag(self, tag, attrs):
       if tag == "img":
           for attr_name, attr_value in attrs:
               if attr_name == "alt" and "cat" in attr_value.lower():
                   self.cat_count = self.cat_count + 1

   def returnNumberOfImgTags(self):
       return self.cat_count

def testParser(url):
   content = urlopen(url).read().decode()
   parser = CountCatInImageAlt()
   parser.feed(content)
   return parser.returnNumberOfImgTags()
maga2 = "https://www.grumpycats.com/" 
print(testParser(maga2))

from html.parser import HTMLParser
from urllib.request import urlopen

class CountColorAttribute(HTMLParser):
   def __init__(self):
       super().__init__()
       self.count = 0

   def handle_starttag(self, tag, attrs):
       if tag == "font":
           for attr_name, attr_value in attrs:
               if attr_name == "color":
                   self.count += 1
                   

   def returnNumber(self):
       return self.count

def testParser(url):
   content = urlopen(url).read().decode()
   parser = CountColorAttribute()
   parser.feed(content)
   return parser.returnNumber()
maga3 = "https://codehs.com/editor/html/16671154/2351949/index.html"
print(testParser(maga3))
