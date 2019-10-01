### Using Azure Application Insights To Hold Custom Logs and Metrics

###### Packages

```C#
using Microsoft.ApplicationInsights.DataContracts;
using Microsoft.ApplicationInsights.Extensibility;
```
###### Custom Telemetry

```C#
//Update this variable to have the actual APPINSIGHTS_INSTRUMENTATIONKEY.
var INSTRUMENTATION_KEY="<APPINSIGHTS_INSTRUMENTATIONKEY>";

//Update this variable to have the default message in the traces.message field.
var MESSAGE = "<TELEMETRY_MESSAGE>";

//Create an instance of TelemetryConfiguration
var config = TelemetryConfiguration.CreateDefault();

//Create an instance of TelemetryCleint
var telemetryClient = new TelemetryClient(config);

//Link to the application insigths resource in Azure.
telemetryClient.InstrumentationKey = INSTRUMENTATION_KEY;

//Create an instance of TraceTelemetry where the parameters is the default message.
var telemetry = new TraceTelemetry(MESSAGE);

//Add all the desired properties that are useful in log analysis. 
//See the following example:
telemetry.Properties.Add("SampleProperty", "PropertyValue");

//Add the telemetry to telemetry client.
telemetryClient.TrackTrace(telemetry);

//Add custom metric to telemetry client.
//See the following example:
telemetryClient.TrackMetric(new MetricTelemetry("SampleCount", 1));
```