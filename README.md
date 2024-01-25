### A training project to practice XPath locators with Selenium

#### Notes, in no particular order:

formula: //tag[@attribute='value']
example: //div[@id='row1']/input

// at the start means a relative path, whatever follows it can be found anywhere on the page

[] what's inside the square brackets is called predicate, they are used to locate a specific node or a node with a specific value

##### Single forward slash /  
• short for child node  
• absolute location path  
• selects a root element  


##### Double forward slash //

• short for descendant or self node  
• relative location path  
• selects element anywhere on the page  

//div[@id='rows']//input: any descendant element that is input. If in full relative path, it could look anything like this:
//div[@id='rows']/div/div/input or in fact containing any amount of divs in between

##### Dot in front of an XPath expression

.//input or ./input

relative location path, starting at the context node

.// - means we are using context node, for example:
String label = row.findElement(By.xpath(".//label")).getText(); - this will work in the node "row", but if we remove the dot, the search will be global each time and only the first found element will be output

##### Position and index

count starts at 1, not zero-indexed
//h5[2]
//h5[position()=3]

The point of using "position" is that we can use negative selection:
//h5[position()!=3]

##### Position operators:
    =  
    !=  
    <  
    <=  
    >  
    >=  

last

//h5[last()-1]

learn how to use index properly:
(//div[@class='row'])[2]
we have to take the original XPath in parenthesis

##### Cheetsheet
//tag[index]
//tag1[index1]/tag2[index2]
(//tag1[@attribute='value']/tag2)[index]

#### TODO
Try running it with JUnit (currently with TestNG)

##### XPath functions
text()
contains()
    //hr[contains(@class,'wp-block-separator has-css-opacity')]
or if we use console:
    $x("//button[contains(@id,'_btn')]")
    $x("//p[contains(text(),'see')]")