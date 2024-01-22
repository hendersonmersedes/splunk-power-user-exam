# splunk-power-user-exam
## Study notes for the Splunk Power User exam


	1. Field extractions
	2. Fields aliases
	3. Calculated fields
	4. Lookups
	5. Event types
	6. Tags

	• App vs Add-ons: 
		○ Apps usually reside on the search head and can be visibly displayed when you drop down the apps menu
		○ Add-ons are something that can be added to the splunk instance
		○ Apps and add-ons can be for the same vendor
	• Searching:
		○ Time picker
		○ Search history
		○ Search modes: Fast(pulls less data), Smart, Verbose(pulls the most data)
		○ Job tab
		○ Save search as report or alert
		○ Zoom in and out
		○ Field menu on the left
	• Knowledge Objects (KOs)
		○ Knowledge objects are user-defined entities that enrich your existing data
		○ These include:
			§ Reports
			§ Alerts
			§ Dashboards
			§ Datasets
			§ Field extractions- fields are extracted at index time and again at search time. host, source, source type
				□ The field extractor utility creates new fields. Provides two field extraction methods: rex and delimiters
				□ Regular expression method works best with unstructured event data
				□ Delimiter method is for structured event data: data from files with headers ; Events are Separated by a common or space
				□ ways to access the field extractor :
					® Bottom of the fields sidebar - Extract New Fields
					® From the field extractions page in Settings
					® When you add data with a fixed Source type
					® From the All Fields dialog box
					® Access from a specific event
			§ Calculated fields -Calculated fields can reference all types of field extractions and field aliasing, but they cannot reference lookups, event types, or tags
			§ Event types - sift through huge amounts of data, find patterns and create alerts reports
			§ Lookups - provides data enrichment by mapping a select value in an event to a field in another data source (.csv files, Geospatial .kmz files, KVStore collections)
			§ Tags - assign names to specific field and value combos includes event type, host, source, or source type. You can use a tag to group .. Use tag :: <field> =<tagname> or tag=<tagname>:
			§ Field Aliases -  an alternate name that you assign to a field. A field can have multiple aliases but each alias applies to only one field.
		○ Shareables, reusable and searchable based on the permissions
		○ Managed by the knowledge manager (owner of the dashboard)
	• Fields
		○ Fields are key value pairs, searchable by name, ability to search multiple fields at once
		○ Sidebar tells you about the fields
		○ You can create more selected fields
		○ Fields window
		○ The "!=" excludes items from the search
		○ _raw and _time are included in the search results by default
		○ "fields + __" or "fields - ___"
	• SPL
		○ Colors: 
			§ Orange: command modifiers
			§ Blue: commands (stats, table, rename, sort, etc.)
			§ Green: arguments (limit, span)
			§ Purple: functions (aggregate- sum, avg, max, min, etc)
		○ Pull data, set your command, determine your functions, call your arguments
		○ Table - sorts values into a table view
		○ Rename
		○ Fields
		○ Dedup - removes duplicate values
		○ Commands:
			§ Search - retrieves events from indexes or filter the results of a previous Search command in the pipeline. Can also be used in a subsearch.
			§ Where - uses eval-expressions to filter search results.
			§ fillnull - replaces null values w/ a specified value [value= <string >], 
			§ Sort - A to Z values or Z to A
	• Transforming your search
		○ Transform commands: order the search results into a data table. Used for statistical purposes. Toggles search modes.
		○ Chart - returns results in a table format
		○ Timechart - time used as the x-axis , you can use the Split-by field.  If you use eval, split-by is required.
		○ Addtotals
		○  TOP finds the top common values of a field
		○  RARE finds the least common values
		○  STATS calculates statistics(count, dc, sum, avg, list, values, etc.)
	• Transaction commands: 
		○ Finds transactions based on events that meet various constraints. These are made up of _raw text).  The transaction command adds two fields to the raw events, duration and eventcount
		○ Maxspan- maximum length of time in seconds, minutes, hours or days that the events can span
		○ Maxpause - maximum length of time in seconds, minutes, hours or data for the pause between the events in a transaction
		○ Startswith - marks the beginning of a new transaction
		○ Endswith - marks the end of a transaction
	
	• Manipulating data: 
		○ EVAL - calculates an expression and puts the resulting value into a search results field.
			§ If the field name that you specify does not match a field in the output, a new field is added to the search results.
			§ If the field name that you specify matches a field name that already exists in the search results, the results of the eval expression overwrite the values in that field.
		○ WHERE - uses eval-expressions to filter search results. Must be Boolean expressions (true or false) cant place before first | in the SPL, use with functions
		○ SEARCH - can be placed anywhere in the SPL,  implied at the beginning of any search
	• Creating and Managing Fields
		○ Field extraction:
			§ erex - extract data from a field when you do not know the regular expression to use.
				□ The values extracted from the fromfield argument are saved to the field.
			§ rex- extract fields using regular expression named groups, or replace or substitute characters in a field using sed expressions.
		○ 3 ways to get to field extractor:
			§ Event action drop down menu
			§ Settings -- Fields -- Field extractions
			§ Event sidebar
	• Lookup:  invokes field value lookups; create or upload
		○ Can either be the name of a CSV file that you want to use as the lookup or the name of a stanza in the transforms.conf file that specifies the location of the lookup table file
		○ Add additional fields to search for
		○ Fields will be added to the fields bar menu
	• Creating Tags and Event types
	• Creating Workflow Actions
	• Creating Data Models
		○ Dataset is a collection of data you define and maintain
		○ There are 3 types - lookups and data models (knowledge objects) and table datasets
			§ Lookups - table files and definitions ( csv)
			§ Data model datasets - arranged hierarchically with a root and Child datasets. Child datasets inherit fields from their parent dataset.
		○ Data models drive the Pivot tool. When a Pivot user designs a pivot report, they select the data model that represents the category of event data to work with. Then select a dataset within that data model. Datamodel datasets can get their fields from custom field extractions, lookups and eval expressions
	• Visualization
		○ Charts:
			§ Timechart - stats aggregation applied to a field to produce a chart with time used as the X-axis. You can use a split-by clause where each distinct value of the split-by field becomes a series in the chart. If you use an eval expression, split-by is REQUIRED.
			§ Chart - returns your results in a table format. Must specify a statistical function when using this command (aggregate functions: count, avg, min, max)
			§ Iplocation - the easiest way to generate a map from events with associated IP addresses
			§ Geostats - generates stats to display geo data & summarize the data on maps
			§ Addtotals - computes the sum of all numeric fields for each result (addcoltotals, stats)
			§ Trendline - computes moving averages of fields ( trendtype: sma, ema, wma)
				□ Sma(simple moving average) and wma(weighted moving average) both compute a sum over the period of most recent values
				□ Ema - exponential moving average 
		○ Reports
			§ Anything that is a search can be saved as a report
			§ Set to run on a schedule
			§ Actions - link to search
			§ Tokens - $token$
		○ Alerts
			§ Run on schedule or real-time
			§ Fire when a condition is met
			§ Create trigger actions
				□ Log, send email, webhooks, 
				□ custom action - built-in webhook alert to send notifications to aweb resource
			§ Create trigger conditions
				□ Per result, number of results, custom, throttle
			§ Throttle an alert to reduce its triggering frequency and limit alert action behavior
	• Macros
    Reusable chunks of SPL that you can insert into other searches. Surround with backtick characters
	1. Settings → Advanced search → Search Macros
	2. Click NEW to create a Search macro
	3. Enter a unique name
	4. put the pipe Character in the search string before the search macro reference
	Ø Save quick mathematical equations using the eval command
	Ø Hot buckets are the only writable buckets 
	Ø Warm-data is getting older
	Ø Cold-
	Ø Frozen-not searchable

    Calculated Fields - fields added to events at search time that perform calculations. Define fields with eval expressions 
    Field  Aliases 
    -Normalize your data
    • Apply multiple fields to the same field alias
    -The original name is not affected post field aliases

    Transactions - group of conceptually related events that span time
	• Transactions include: . Different events from the same source & host Different events from 9 diff sources / same host : Similar ' events - y. from . diff hosts /diff sources
    Use cases: Share session ID, message queue event, purchase fulfillment event
    CIM: Common Information Model.
    •  CIM validation and a common action model
