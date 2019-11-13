# Introduction

Forked version of kerstinbach/mycbr-rest-example, slightly modified to work with a different project

# Installing myCBR workbench 
* Install myCBR workbench from http://mycbr-project.org/download.html
* From the workbench, generate a new project case to be used as the mycbr-rest's base

# Installing mycbr SDK
* Clone the project from https://github.com/kerstinbach/mycbr-sdk
* In the root folder, run:
```
mvn clean install
```

# Installing the mycbr-rest
* First clone the project 
* To build it go into its root folder and run: 
```
mvn clean install
```
* In order to deploy the Spring app, run: 
```
java -jar ./target/mycbr-rest-example-1.0-SNAPSHOT.jar 
```
* After Spring has started, you can find the API documentation here: http://localhost:8080/swagger-ui.html#!/
 * CBR Controller contains the myCBR functionalities
* ctrl + C shuts down the server

# Functionalities
* The goal is to provide the entire retrieval, however, so far only the model is working
## GET Requests
 * /case provides the case content
 * /concepts provides all concept names in the project
 * /casebase provides the name(s) of the case bases associated with the project
 * /retieval provides the similarity-based retrieval either by specifying symbols or an id of existing cases
 * /attributes provides a list of attributes and their value types 
 * /values provides the list of allowed values for SymbolDesc attributes and min/max for IntegerDesc/DoubleDesc/FloatDesc
## POST Requests
 * /retrieval allows you to post a query with a number of attributes, e.g.:  
    ```{"Doors": 4, "Model": "e_300_diesel", "Manufacturer": "mercedes-benz","Color":"yellow, blue"}``` 
 * Currently only Symbol, Integer, Double and Float attributes are supported.
 * Currently only Multiple Symbol attributes are supported
 * the number of returned cases can be set, use -1 for returning all
 
# How to customize the rest
* The app requires a myCBR project, which should be put into mycbr-rest-example/src/main/resources
* Edit the CBREngine.java file in mycbr-rest-example\src\main\java\no\ntnu\mycbr:
```
  .
  .
  .
    // modify this if necessary, pointing to point to mycbr-rest-example\src\main\resources
	private static String data_path = System.getProperty("user.dir") + "/src/main/resources/"
	// name of the project file in the resources directory
	private static String projectName = "book_similarity.prj"; 
	// name of the concept to be used 
	private static String conceptName = "Book";
	// name of the csv containing the instances, located in the resources directory
	private static String csv = "Sample_Data.csv";
	// set the separators that are used in the csv file
	private static String columnseparator = ";";
	private static String multiplevalueseparator = ",";
	// name of the case base that should be used; the default name in myCBR is CB_csvImport
	private static String casebase = "CB_csvImport";
  .
  .
  .
	
```
* The docs in http://localhost:8080/swagger-ui.html#!/ will not reflect the change in project, however the API will work dynamically according to the project that is used as the base
