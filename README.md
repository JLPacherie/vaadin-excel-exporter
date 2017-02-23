# vaadin-excel-exporter for Vaadin 7

vaadin-excel-exporter is a utility add-on for Vaadin 7. It is a single point solution providing consistent and configurable support for 
exporting data of Vaadin Table, Tree Table and Grid in Excel format.

## Why do we need this addon?

1) Exporting the screen data is a frequent task required in most of the applications. There are several 
helper technologies such as POI which help us in bringing the Export feature in place but a developer 
needs to take it up every time he wants to implement.
2) Vaadin providing so many components for representation of data such as Table, Tree Table and Grid, 
which again raises a need for a utility that is easy and configurable to be used with varied component 
wihtout the pain of writing the logic to generate the Excel.
3) A consistent excel format throughout the application which would enhance user experience.
4) Can be integrated with any Vaadin application with just few lines of configuration code.

## What dependencies are required?
JDK 1.7 or above
POI 3.9
POI-OOXML 3.9
Apache Commons IO library (http://commons.apache.org/io/) v2.2
net.karneim.pojobuilder 3.4.0 and above

## Features

It is highly configurable and provides configuration at three levels namely File Level, Sheet Level, Component Level.

### For each file you can configure
- List of Sheets
- Export File Name
- Generated By
- Export Type (xlsx or xls)

### For each sheet you can configure
- Sheet Name
- Report Title Row
- Generated By Row
- List of Components inside the sheet
- FieldGroup - for showing filters selected on the screen for the selected data
- Additional Header Info - HashMap for custom data (Key Value Pair)
- Date Format
- Number Formats
- XSSFCellStyle for each content section of the screen

Note that the Number formats by itself manages the thousand separator and decimal point 
for different locales. For Eg: For English the decimal point is (.) and thousand separator is (,), but for 
German locale it is the reverse. But the code handles it by its own.

### For each component you can configure
- Component - Tree table or Grid or Table
- It supports all kinds of containers - Indexed, BeanItem, Hierarchical
- Visible properties
- Properties requiring date formatting
- Properties requiring Float formatting
- Properties requiring Integer formatting
- Column Header Texts
- Component Header and Content Styles
- Column Freeze and Header Freeze feature
- Provide Column Formatters. Use built in Suffix, Prefix formatters.
- Multiple Header Rows
- Multiple Footer Rows

However, if none of these are specified, it would generate the Excel with default values and styles.

## Online demo
http://bonprix.jelastic.servint.net/vaadin-excel-exporter-demo/

## Usage

### Maven

```xml
<dependency>
    <groupId>org.vaadin.addons</groupId>
	<artifactId>vaadin-excel-exporter</artifactId>
	<version>1.0.4</version>
</dependency>

<repository>
   <id>vaadin-addons</id>
   <url>http://maven.vaadin.com/vaadin-addons</url>
</repository>
```

No widgetset required.

## Download release

Official releases of this add-on are available at Vaadin Directory. For Maven instructions, download and reviews, go to http://vaadin.com/addon/vaadin-excel-exporter

## Building and running demo

git clone https://github.com/bonprix/vaadin-excel-exporter
mvn clean install
cd demo
mvn jetty:run

To see the demo, navigate to http://localhost:8080/

## Development with Eclipse IDE

For further development of this add-on, the following tool-chain is recommended:
- Eclipse IDE
- m2e wtp plug-in (install it from Eclipse Marketplace)
- Vaadin Eclipse plug-in (install it from Eclipse Marketplace)
- JRebel Eclipse plug-in (install it from Eclipse Marketplace)
- Chrome browser

### Importing project

Choose File > Import... > Existing Maven Projects

Note that Eclipse may give "Plugin execution not covered by lifecycle configuration" errors for pom.xml. Use "Permanently mark goal resources in pom.xml as ignored in Eclipse build" quick-fix to mark these errors as permanently ignored in your project. Do not worry, the project still works fine. 

### Debugging server-side

If you have not already compiled the widgetset, do it now by running vaadin:install Maven target for vaadin-excel-exporter-root project.

If you have a JRebel license, it makes on the fly code changes faster. Just add JRebel nature to your vaadin-excel-exporter-demo project by clicking project with right mouse button and choosing JRebel > Add JRebel Nature

To debug project and make code modifications on the fly in the server-side, right-click the vaadin-excel-exporter-demo project and choose Debug As > Debug on Server. Navigate to http://localhost:8080/vaadin-excel-exporter-demo/ to see the application.

### Debugging client-side

Debugging client side code in the vaadin-excel-exporter-demo project:
  - run "mvn vaadin:run-codeserver" on a separate console while the application is running
  - activate Super Dev Mode in the debug window of the application or by adding ?superdevmode to the URL
  - You can access Java-sources and set breakpoints inside Chrome if you enable source maps from inspector settings.
 
## Release notes


### Version 1.0.1
- Initial release

### Version 1.0.2
- Added Getters for extension

### Version 1.0.3
- Added Column Formatter Logic

- Also developed three formatters as built in formatters namely
- SuffixColumnFormatter(String suffix) // can add suffix to the container/model value such as $, %, kg etc...
- PrefixColumnFormatter(String prefix // can add prefix to the container/model value 
- BooleanColumnFormatter(String trueValue, String falseValue) // Give meaningful alias to true and false like Yes/No, Active/De-Active etc.. Requires the column to be also set withBooleanFormattingProperties

- Note: For columns mentioned in withFloatFormattingProperties and withIntegerFormattingProperties, the above formatting gets applied after the Integer and Float formatting is performed on the container/model value.

- Updated the Demo Project to show case the same.

### Version 1.0.4
- Added ComponentHeaderConfiguration and ComponentFooterConfiguration

- These would allow the user to configure multiple headers and footers for each component.

- The ComponentHeaderConfiguration provides support for Grid.HeaderRow so in case you have appended headers in your grid, you can pass them directly to the header configuration.
- However, it also supports custom header through String[]
- You can also merge the header cells by specifying the start property, end property and display string in the MergedCell bean.

- Similar support is available for ComponentFooterConfiguration

- Updated the Demo Project to showcase the same. Also you can refer to the advance snipped section for example.

### Version 1.0.5

- Added support for nested properties in case of BeanItemContainer.

- Resolved issues raised in git
- https://github.com/bonprix/vaadin-excel-exporter/issues/3
- https://github.com/bonprix/vaadin-excel-exporter/issues/9
- https://github.com/bonprix/vaadin-excel-exporter/pull/16

## Roadmap

Recently Released :
- Reflecting some column generator logic as well in the Excel. For Example suffixes cm, kg, $ etc...

Upcoming releases:
- Specifying Excel Column types as Date, Number sustaining their formatting
- Specifying a row header which can allow horizontal data as well.
- Export of selected records wherever applicable
- Legend for better understanding

## Issue tracking

The issues for this add-on are tracked on its github.com page. All bug reports and feature requests are appreciated. 

## Contributions

Contributions are welcome, but there are no guarantees that they are accepted as such. Process for contributing is the following:
- Fork this project
- Create an issue to this project about the contribution (bug or feature) if there is no such issue about it already. Try to keep the scope minimal.
- Develop and test the fix or functionality carefully. Only include minimum amount of code needed to fix the issue.
- Refer to the fixed issue in commit
- Send a pull request for the original project
- Comment on the original issue that you have implemented a fix for it

## License & Author

Add-on is distributed under Apache License 2.0. For license terms, see LICENSE.txt.

vaadin-excel-exporter is written by Kartik Suba @ Direction Software Solutions, India.
For Client: Bonprix Handelsgesellschaft mbH

# Developer Guide

## Getting started

Here is a simple example on how to try out the add-on component:

```java
/* Configuring Components */
ExportExcelComponentConfiguration componentConfig1 = new ExportExcelComponentConfigurationBuilder().withTable(this.tableWithBeanItemContainer) //Your Table or component goes here
                                                                                                           .withVisibleProperties(this.tableWithBeanItemContainer.getVisibleColumns())
                                                                                                           .withColumnHeaderKeys(this.tableWithBeanItemContainer.getColumnHeaders()) 
                                                                                                           .build();
/* Configuring Sheets */
ArrayList<ExportExcelComponentConfiguration> componentList1 = new ArrayList<ExportExcelComponentConfiguration>();
componentList1.add(componentConfig1);

ExportExcelSheetConfiguration sheetConfig1 = new ExportExcelSheetConfigurationBuilder().withReportTitle("Excel Report")
                                                                                               .withSheetName("Excel Report")
                                                                                               .withComponentConfigs(componentList1)
                                                                                               .withIsHeaderSectionRequired(Boolean.TRUE)
                                                                                               .build();
                                             
/* Configuring Excel */
ArrayList<ExportExcelSheetConfiguration> sheetList = new ArrayList<ExportExcelSheetConfiguration>();
sheetList.add(sheetConfig1);

ExportExcelConfiguration config1 = new ExportExcelConfigurationBuilder().withGeneratedBy("Kartik Suba")
                                                                                .withSheetConfigs(sheetList)
                                                                                .build();

ExportToExcelUtility<DataModel> exportToExcelUtility = new ExportToExcelUtility<DataModel>(this.tableWithBeanItemContainer.getUI(), config1, DataModel.class);
exportToExcelUtility.setSourceUI(UI.getCurrent());
exportToExcelUtility.setResultantExportType(ExportType.XLSX);
exportToExcelUtility.export();
```

For a more comprehensive example, see src/test/java/org/vaadin/template/demo/DemoUI.java