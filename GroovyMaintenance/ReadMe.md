How to create a Groovy maintenance file

Write your groovy file, with a name "TimerFailedReArm.groovy". Give the code "TimerFailedReArm" to the user to load it.

## Available object

Different object are available in the groovy

### restAPIContext
The RestAPIConext contains these methods:

 public APIClient getApiClient() 
 public APISession getApiSession() 
 public Locale getLocale()
 public ResourceProvider getResourceProvider()
 
### apiAccessor

The Bonita ApiAccessor 
        
    
## apiClient
The Bonita ApiClient

### bonitaToolboxAPI
this object contains theses methods
    public List<Map<String,Object>> executeSqlRequest(String sqlRequest ) {
    public List<Map<String,Object>> executeSqlRequest(String sqlRequest, List<Object>  parameter ) {

    public String decoratorHtml(List<Map<String,Object>> listValues)
    public String decoratorCsv(List<Map<String,Object>> listValues)



## Place holder
In the file, you can set some Place Holder. Syntax is {{<key>[;tips:<type>]}}
For example, you can set

List listFlowNodeid= {{ListFlowsNode}};

if you want to give more information to the user to fulfill the label, use the tips:
List listFlowNodeid= {{ListFlowsNode;tips:Give a list of flownode, with the JSON syntax like [123,234]}};

Attention, the place holder key is then the complete string, if you want to reuse the same place holder in different place.
In the key, don't use {{ and ; because they are considered as separator.

<b>Different parameters</b>
Type: String (default)
The parameter is a string (Input String Widget). The value returned contains ""
Example: 
var myText= {{FirstName}}
WHen the user type Hello, the result is
var myText = "Hello"

Type: TEXT
The parameter is a Text (Text Area Widget). The result is a String.

Type: INTEGER
The parameter is a Number (Input Number Widget). The result is a number.
Example: 
var myAge= {{Age;type:INTEGER}}
WHen the user type 24, the result is
var myAge = 24

Type: LIST
The interface is a STRING, where user can give a list as 23,34,55
The result is a list of String
Example: 
var allAges= {{Ages;type:LIST}}
When the user type 24,44,53 the result is
List allAges = ["24", "44", 53" ];
 
Type: HIDDEN
The parameters is not visible for the user point of view. It is from the REST CALL.

Type: READONLY
The parameter is display, in read only. The value is then the default value.

Type: SELECT
The parameter is display, in a list

String operation= {{operation;
    type:select;
    listoptions:Only Detection,Update form
    default:Only Detection
}}


Type: SQL
The parameter is a SqlRequest. The SqlRequest is executed when the form is displayed (so before the user clicks on Execute).

List listFormIdTaskAuto = {{formIdTaskAuto;
    type:sql;
    sqlrequest:all:SELECT id FROM page WHERE name = 'custompage_taskAutogeneratedForm';
    selecttop:1
    }}
    
This type include different parameters
* sqlrequest:<database>:<sql>
Give the sql to be executed. No ; is acceptable in the request. The sql request can have the placeholder @@systemcurrenttimemillis@@
Multiple sqlrequest can be defined, for different database. The Database Product Name is used. If the execution does not find the correct dabatasename, then 'all' or the default is used.
In the next example, if the database is POSTGRE, then the specific request is not found, and 'all' is used.
Example: {{listCaseId;type:SQL;sqlrequest:H2:select process_instance from processInstance;sqlrequest:ORACLE:select top 3 process_instance from processInstance;sqlrequest:all:select process_instance from processInstance}

The result is an ARRAY of MAP.
select name, age from employee
return
 [ { "NAME": "Pierre", "AGE": 24 }, { "NAME": "Yves", "AGE": 25}]

* colnameresult:UPPERCASE|LOWERCASE
In the result, the name is in UPPER case or not. Default is USER.
The result is then [ { "NAME": "Pierre", "AGE": 24 }, { "NAME": "Yves", "AGE": 25}]


* selecttop:<number>
Return only the top number item. Some database accepts a select top 100, another don't.
Example: {{listCaseid;type=SQL;sqlrequest:select id from process_instance;selectop:10}


Type:JSON
The parameter is a JSON object. User gives for example [ "Paris", "Grenoble", "San Francisco" ]




<b>Others parameters</b>
tips : the input widget get this tips
syntax: tips:<title>
example: {{FirstName;tips:Give your first name}}

label: give a specific label to the user
syntax: label:<name>
example: {{FirstName;label:Your First Name}}


default: give a default value
syntax: default:<name>
example: {{FirstName;default:Pierre}}

