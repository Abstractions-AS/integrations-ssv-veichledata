
# Introduction 
This library allows lookup of information about veichles registered in Norway.
The library requires an API key from [Statens Veivesen](https://www.vegvesen.no/).

The API key can be created using [this link](https://www.vegvesen.no/dinside/data-og-api-er/tilgang-til-api-for-kjoretoyopplysninger/).

# Installation
#### Add the NuGet package
```powershell
Add-Package Abstractions.Integrations.StatensVeivesen.VeichleLookup
```

####  Configure API Key
The library will automatically look for a configuration section named `VeichleLookupService`. To use a different name, configure the options manually.
```json
{
	"VeichleLookupService":
	{
		"ApiKey": "..."
	}
}
```

####  Add service to application in `Program.cs`
```csharp
// add the service
builder.AddVeichleLookupService();

// or
builder.Services.AddVeichleLookupService();
```

# Usage

To perform a lookup, retrieve an `IVeichleLookupService` instance from dependency injection, and
```csharp
var response = await veichleLookupService.LookupLicensePlateAsync("XX00000");
	
// this object contains the entire graph from Statens Veivesen, and is quite verbose
var veichle = response.Veichles[0];

// to get a more light-weight object containing key information, get the summary
var summary = veichle.Summary;	
```
