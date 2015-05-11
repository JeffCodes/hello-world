# hello-world
This is my first Git project

I dreamed this day would come.

from bs4 import BeautifulSoup
from urllib2 import urlopen
from time import sleep # be nice


def make_soup(url):
    html = urlopen(url).read()
    return BeautifulSoup(html, "lxml")



html = urlopen('http://www.syntheticgems.org/catmain.asp?cmid=5').read()
soup = BeautifulSoup(html, "lxml")



print html[0:100]

len(html)


soup = make_soup("http://www.syntheticgems.org/catmain.asp?cmid=5")

soup.table.tbody.tr.td.table.tbody.tr.td.a
soup.tbody.tr.td.table.tbody.tr.td.a
soup.tr.td.table.tbody.tr.td.a
soup.td.table.tbody.tr.td.a
soup.table.tbody.tr.td.a



soup.body.table.tr.td.table.tr.td.table.tr.td.table.tr.td.table.tr.td.a
soup.tbody.tr.td.table.tbody.tr.td.a
soup.tr.td.table.tr.td.a
soup.td.table.tr.td.a
soup.table.tbody.tr.td.a

soup.find_all("p", "title")
# [<p class="title"><b>The Dormouse's story</b></p>]

link = 

#This is finds things based on a CLASS!!!
soup.find_all("a", "cl")


soup.tr.td.a
soup.table.tr.td.a


#soup.find('a', class='cl')
last_a_tag = soup.find("a", id="link3")
last_a_tag = soup.find("a", class="cl")






 
BASE_URL = "http://www.chicagoreader.com"
 
def make_soup(url):
    html = urlopen(url).read()
    return BeautifulSoup(html, "lxml")
 
def get_category_links(section_url):
    soup = make_soup(section_url)
    boccat = soup.find("dl", "boccat")
    category_links = [BASE_URL + dd.a["href"] for dd in boccat.findAll("dd")]
    return category_links
 
def get_category_winner(category_url):
    soup = make_soup(category_url)
    category = soup.find("h1", "headline").string
    winner = [h2.string for h2 in soup.findAll("h2", "boc1")]
    runners_up = [h2.string for h2 in soup.findAll("h2", "boc2")]
    return {"category": category,
            "category_url": category_url,
            "winner": winner,
            "runners_up": runners_up}
 
if __name__ == '__main__':
    food_n_drink = ("http://www.chicagoreader.com/chicago/"
                    "best-of-chicago-2011-food-drink/BestOf?oid=4106228")
    
    categories = get_category_links(food_n_drink)
 
    data = [] # a list to store our dictionaries
    for category in categories:
        winner = get_category_winner(category)
        data.append(winner)
        sleep(1) # be nice
 
    print data
