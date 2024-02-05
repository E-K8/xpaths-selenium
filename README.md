### A training project to practice XPath locators with Selenium

Expanded [XPath cheatsheet](https://devhints.io/xpath) 

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

##### XPath functions
text()
contains()
    //hr[contains(@class,'wp-block-separator has-css-opacity')]
or if we use console:
    $x("//button[contains(@id,'_btn')]")
    $x("//p[contains(text(),'see')]")

//tag[starts-with(@attribute, 'beginning')]  
    $x("//input[starts-with(@class, 'input')]") 
    //input[starts-with(@class, 'input')]

//tag[starts-with(text(), 'beginning')]  
    //p[starts-with(text(), 'Test case')]
    $x("//p[starts-with(text(),'This page contains')]")

//tag[not(@attribute='value')]
    //tag[not(text()='value')]
//tag[not(contains(@attribute,'partial value'))]
    //tag[not(starts-with(text(),'beginning'))]

##### XPath Operators

or  
$x("//button[@name='Add' or @name='Remove']")
$x("//button[@name='Add' or @id='remove_btn']")

and  
$x("//button[@class and @name='Save']")

not  
//button[@class='btn' and not(@style='display: none;')]
//button[@class='btn'][not(@style='display: none;')]

##### Wildcards

$x("//*[@class]")  
$x("//button[@*='btn']")

##### XPath Axes

axisname::nodetag[predicate]  
//div[@id='row1']/parent::div  

[//]: # (not advisable↓)
//section/ol[2]/li[2] - not advisable as list elements can be added later

$x("//h5[contains(text(),'Test case 2')]/following-sibling::ol[1]/li[2]") - looks unnecessarily complicated, but is more robust

//li[text()='Verify text saved']/parent::ol/preceding-sibling::h5[1] - will select the first closest element relative to our element

##### Locate relative elements
//div[./input] = //input/parent::div

//div/input = //input[parent::div] 
//input[parent::div[@id='row2']] = //div[@id='row2']/input

##### Selecting several elements
$x("//h2 | //h5")

$x("//div[@id='row1']/button | //div[@id='row1']/input")

##### SVG
Normal XPath syntax doesn't apply  
//*[@y='11']  
//*[name()='rect' and @y='11']  
//*[name()='symbol' and @id='icon-amazon']/* - any child under the last element  or to be more specific:  
//*[name()='symbol' and @id='icon-amazon']/*[name()='path']

##### Inspect disappearing elements (stop page load)

###### Method 1
Open console  
• Type in setTimeout(()=>{debugger;},5000);  
• Press Enter  
• We’ve got 5 seconds now to make out element appear. Once it appeared, wait until the debugger starts. We can use the element for as long as we don’t resume the debugger (for example, using element picker: square with an arrow)

###### Method 2
In DevTools:  
• click on Sources tab  
• locate Event Listener Breakpoints  
• select the event, eg. Mouse->click (tick the box)  
In the browser window:  
• click the element that triggers desired action (it will be paused in debugger)  
• step over the next function (F10) until you achieve visibility of the element  
• select the element on the page to inspect it (arrow withing a square icon in DevTools or ctrl+shift+C)  
• when you're done, untick the box in  Event Listener Breakpoints
