FusionCharts VisualForce Api
============================

A visualforce component for drawing fusion charts (XT). 
This is currently alpha, you might find some features missing. Feel free to raise a github issue.

This is a visualforce component that will let you draw fusion charts without coding on client.

Quick Start
===========

### Get Fusion Charts
You can download evaluation version from [here](http://www.fusioncharts.com/download/trials/). 
You will need to upload all the charts as static resources.

1. Unzip the archive
2. Obtain `Charts` folder and compress it into a zip file
3. Go to **Salesforce | Setup | Develop | Static Resources | New** upload the zip under the name `FusionCharts`

### Upload the component

1. Go to **Salesforce | Setup | Develop | Components | New**
2. Copy the contents of [component.xml](./component.xml) and save under the name `fusioncharts`

Now you are setup to use Fusioncharts Visualforce API inside your apex pages. To demonstrate and test, use the following instructions.

### Setup Controller
You will need to setup a apex controller to provide data to render the charts. The component will accept the name and the @RemoteAction method of this controller which will provide data. You can use sample contoller provided [here](Example/Controller).

1. Go to **Salesforce | Setup | Developer Console** and create a new apex class.
2. Copy the code of example controller into this class. Although JSON could dynamically be generated using apex JSON api, for the purpose of this example, I chose to send JSON string directly. You can serialize any of your apex objects into JSON using [Apex JSON API](http://wiki.developerforce.com/page/Getting_Started_with_Apex_JSON).

### Create your first chart
#### This is important
Now you can draw your first fusion chart on an apex page.

1. Go to **Salesforce | Setup | Develop | Pages | New**
2. You can create your first fusion chart here using `<c:fusioncharts/>` xml tag. It is as attributes of this tag that you will use the component api. Anything that you would have provided as an attribute to `<chart/>` tag in XML api, or as a `chart` property in FusionCharts JSON api, you will provide as an attribute to this component. *Caution* Not all attributes are supported at the moment.

For quickstart copy the contents of [example apex page](Example/apexpage.xml) and save it under the name `fusionchart`
3. Now hit the page https://your-salesforce-domain/apex/fusionchart. You will see a pie chart and a Column3D chart appear.

Thats about it for this quick start tutorial. See it in action [here](https://saas-platform-8087--c.ap1.visual.force.com/apex/FusionCharts)

The How To
==========

If you are coming from FusionCharts XML background, it will probably be pretty straightforward to you. Basically you can create a fusion chart using `<c:fusioncharts/>` xml tag. It is as attributes of this tag that you will use the component api. Anything that you would have provided as an attribute to `<chart/>` tag in FusionCharts XML api, or as a `chart` property in FusionCharts JSON api, you will provide as an attribute to this component. *Caution* Not all attributes are supported. At the moment only attributes mentioned in Quick Start Chart configuration in [fusioncharts developer documentation](http://docs.fusioncharts.com/charts/) are supported. But in future we are planning comprehensive coverage of FusionCharts API.

## The required attribute for the component are

* `chartId`: A unique id for the chart. This will be the id of html div tag holding the chart. The actual id of the FusionChart object would be the `chartId` provided by you preceded by `fc-`. So if you have provided `chartId="mychart"`, the FusionChart object id would be `fc-mychart`. You will need this if you want to obtain refernce of your charts in your client scripts.
* `chart`: As usual with FusionChart javascript api, provide relative path of the actual chart file that you want to draw. If you have uploaded your FusionChart files as static resources as mentioned in the quickstart guide you should be able to refernce them by `chart="{!URLFOR($Resource.FusionCharts, 'Charts/<chart-name>[.swf]')}"`
* `width`
* `height`
* `dataController`: The data controller name followed by a `.` and the @RemoteAction method name which will provide the actual data. Currently only JSON data is supported. As with FusionCharts JSON api, data should come wrapped inside property named `data`. Like so `{data: [... The actual array of data ...]}`

An optional attribute is `debugMode`. Setting it to 1 will draw the chart in debug mode and will print debug information.

Other attributes are exactly the same as in FusionCharts XML data API. You can refer to them on official documentation site.

TODO
====
~~Support for XML data~~
If multiple chart components are used on same page, the FusionCharts script is loaded multiple times. Make it so that the script is loaded only once.
Complete coverage of FusionCharts API.
Major refactoring of the code.
Trenlines and Style.

Bugs, Questions, and Suggestions
================================
Feel free to raise a github issue.

Licence
=======
MIT