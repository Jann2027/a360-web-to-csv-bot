# A360 Web-to-CSV Bot

An Automation Anywhere A360 bot that opens a web page, captures plan details
(price and validity), keeps only the plans priced between 500 and 2000, and
writes them to a CSV file with headers.

## Tools
Automation Anywhere A360 (Community Edition), Google Chrome, CSV

## Bot flow
1. Open the web page in Chrome (a specific browser, not the default)
2. Loop while the next plan element exists, using a loop counter
3. Capture price and validity with Get Property > HTML InnerText
4. If price > 500 AND price < 2000, write the row to the CSV
5. Increment the loop counter
6. Close the browser

## What I learned
- Choose a specific browser in the Open command, because the default browser
  can differ between machines and break the bot.
- A window variable with a wildcard (*) in the title keeps the bot working when
  the page title changes.
- Plan elements differ only by a number in their XPath, so a Number variable
  is incremented in a loop and converted to a String to build each XPath.
- Captured values are strings, so they must be converted to numbers before
  the price comparison.
- Log to File creates the file if it does not exist. Write the header row once
  (overwrite mode), then append each row.
- Adding the date to the file name creates a fresh file each day without losing
  earlier data.
- Test after every change. Mistakes like a disabled command or a file name not
  updated inside the loop only show up when you run the bot.

**output: CSV with plans between 500 and 2000**
(images/tutorial-output-csv.png)

**Filter logic: If price > 500 AND price < 2000**
(images/tutorial-if-condition.png)
