MotorBackTV
Version: 0.1.2 BETA

------------
I. Introduction
------------
This program can be used for automating back tests using trade strategies on tradingview.com.  Users must have an account
on tradingview.com, be familiar with saving/editing chart layouts, and how to choose/utilize back testing strategies.

------------
II. PC Requirements
------------
OS: Windows 8 or newer (developed/tested on Windows 10) (Linux and MAC support pending)
Java: Java 8 or newer  (developed/tested on Java 8)
Browser: FireFox or Chrome

NOTE: Program Developed and Tested With Browser Installed At Default Locations...
	C:\Program Files\Mozilla Firefox\firefox.exe
	C:\Program Files (x86)\Google\Chrome\Application\chrome.exe
	
------------
III. Quick Start Directions (see README in zip file for detailed instructions)
------------
Sample configuration options and files are provided to quickly get the program running once extracted on the users PC.
1. Complete the browser choice properties section starting around "line 130" in the motorBackConfig.properties file.
2. Set back test strategy starting around "line 200" in the "motorBackConfig.properties" file.
3. Double click the motorBackTV_vX.XX.jar file to start the program.

------------
IV. File List
------------
motorBackConfig.properties		- Contains the setup configuration for each back test execution
motorBackReporter_v0.1_beta.xlsm	- MS Excel document capable of generating detailed report of back test results
motorBackTV_v0.1.2_beta.jar		- Program executable file, double click to initiate back test after configuration is complete
binanceUSDT.txt				- Sample list of USDT pairs		
binanceBTC.txt				- Sample list of BTC pairs
binanceETH.txt				- Sample list of ETH pairs
candleList1.txt				- Sample list of candle/ordersize
(6) *.csv files				- Sample CSV files that can be imported into the Excel Workbook
README.txt				- This file describing program contents and operations
folderStructureExample.JPG		- Folder structure example

chromedriver.exe		- NOT SUPPLIED - Required file for program use of the Chrome browser. 
				      	         Download  here: http://chromedriver.chromium.org/downloads
geckdriver.exe			- NOT SUPPLIED - Required file for program use of the FireFox browser. 
						 Download here: https://github.com/mozilla/geckodriver/releases
-------------
V. Folder List
-------------
motorBackOutputs		- REQUIRED - Location of program output files which include four types of log files for each test run.
pairLists			- Location of pair list files
candleLists			- Location of candle list files
chromedriver_win32		- NOT SUPPLIED - Location of chromedriver.exe which is used in conjunction with the Chrome browser
geckodriver-v0.23.0-win64   	- NOT SUPPLIED - Location of geckdriver.exe which is used in conjunction with the FireFox browser

-------------
VI. Program Inputs
-------------
The program takes three files for input, a properties file, a pair list file and a candle/orderSize list file.  The text files are
read by the program from top to the first blank/empty line.  Any text below this blank line will not effect the operation of the program
and can be used to store alternate lists and notes. The program home directory is where the location of the autoBackTV_vX.XX.jar
file is saved.

Properties File - This file contains the configuration options for each back test.

Pair List - This file will be used to acquire the list of pairs that will be tested.  Currently, the format of each pair value can be
read in the file as carriage-return separated values or comma separated values or a combination of both. Each pair can be a combination
of the exchange and currency with a colon for separation (ex. "BINANCE:XRPUSDT") or just the currency (ex. XRPUSDT).  If only the
currency is found, the exchange property in the configuration file will be used as the exchange.  The format of these pairs must be in
the same format accepted in Trading View's pair search box or the pair will not be found and flagged as invalid. 
See provided sample files.

Candle/OrderSize List - This file will be used to acquire the list of candles and order sizes that will be tested. Currently, the format 
of each candle/orderSize value will be read in the file as comma separated values or carriage-return separated values or a combination of
both. Each value must be a combination of a candle and order size, separated by a colon (ex. "candle=5:ordersize=100" = 5 minute candle 
with 100 order size). The candle size value format must match what is acceptable by Trading View or it will not be recognized by 
Trading View, see below examples and the provided sample files.
	- Digits for minutes, or first letter of the word for longer candles.
	- Examples: 1, 5, 30, 60, 1440, H, 2H, 6H, D, 5D, 3W, 6M

-------------
VII. Program Outputs
-------------
The program will output four files after each execution: motorBackRunLog, motorBackRunDataLog, motorBackData CSV file, and
motorBackTradeListData CSV file. Samples of these files are provided to help potential users setup the configuration options and test 
the report generator.

motorBackRunLog - Will include a step by step summary of the program actions and information attempting to describe encountered issues.
Any pair/candle combination that results in "NO DATA" in the "Strategy Tester" or as an invalid entry will be detected and skipped.
These types of occurrences will be noted in this file for later review by the user.

motorBackRunDataLog.txt - This is a read friendly data file that includes the data points stored in the "Overview" tab of 
the "Strategy Tester" window.

motorBackData.csv - This is a CSV output of the data points stored in the "Overview" tab of the "Strategy Tester" window.  This 
file can be imported into the supplied Excel Report Generator.  See sample CSV files in "motorBackOutputs" folder.

motorBackTradeListData.csv - This is a CSV output of the data stored in the "List of Trades" tab of the "Strategy Tester" window.  This 
file can be imported into the supplied Excel Report Generator.  See sample CSV files in "motorBackOutputs" folder.

-------------
VIII. Program Status and Live Options
-------------
After the program starts and initializes the browser window, a small status console will appear showing three cancel/abort options
(Stop After Current Pair, Stop After Current Candle, and ABORT NOW) and three status indicators (Current Pair, Current Candle,
and a information field with granular program statuses). Once a cancel option is clicked, depending on the custom "confirmationPrompt" 
setting in the properties file, a prompt will show to confirm the action.

-------------
XI. MS Excel Report Generator
-------------
Supplied is a single MS Excel document capable of generating a detailed report of the data collected from the "Overview" and 
"List of Trades" tabs in the "Strategy Tester" tab of Trading View.  The Excel document reads the "motorBackOutputs" folder for
CSV files to import. This folder name must remain the same, if changed, a new one will be created. On the first tab of the Excel file,
three button options are given, "Create Trade Summary Report", "Create Trade List Report", and "Reset Report". The result of each
report type will be the creation of a "RawData" worksheet that basically stores the data from the imported CSV file, and separate 
worksheets for each pair that is tested. See sample CSV files in "motorBackOutputs" folder.

Create Trade Summary Report - Creates a report that summarizes the Trading View "Overview" tab which includes the data points
(Net Profit, Total Closed Trades, Percent Profitable, Profit Factor, Max Drawdown, Avg Trade, Avg No. of Bars In Trades) and
basic graphs for each data point. For example, a test with 30 pairs and 30 candles will generate a workbook with 30 worksheets that 
includes 210 graphs (7 graphs per worksheet).

Create Trade List Report - Creates a report which summarizes the "List of Trades" tab data that includes the data and generated 
"Equity vs Drawdown" graphs, similar to ones that are shown in the "Overview" tab for each pair. For example, a test with 30 pairs and
10 candles will generate a workbook with 30 worksheets and 300 graphs (10 graphs per worksheet). Due to Excel memory limitations, a
limit for number of graphs that can be generated per worksheet is set at 100. For pairs with more than 100 tested candles, the generated
graphs will be split over multiple worksheets.  For example, a pair with 250 tested candles will require 3 worksheets. While the report
is being generated, a progress bar will be shown with information displaying the progress status, pair by pair and candle by candle.

NOTE: 	TradingView Chart History Limits:
	Free account - 5,000 candles/bars are available for testing
	Paid account - 10,000 candles/bars are available for testing