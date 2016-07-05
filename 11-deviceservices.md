---
title: Device Services
permalink: /device-services/
layout: default
---

# Device Services (Orca Service)

This is a wrapper for the Orca device services. The first step is to register for device activation to generate an activation code.  This code can then register the device and generate the secret API key to use for other services.


## Create an OrcaServiceConfig object for settings.

{% highlight csharp %}
var config = new HpsOrcaServiceConfig
{
	DeviceId = 5315938,
	LicenseId = 101433,
	UserName = "777700857994",
	Password = "$Test1234",
	SiteId = 101436,
	SiteTrace = "trace0001",
	VersionNumber = "1234",
	IsTest = true, //Use for certifications and develpoment testing.  false by default.
	ApplicationId = "Mobuyle Retail",
	HardwareTypeName = "Heartland Mobuyle"
};
{% endhighlight %}

{% highlight java %}

HpsOrcaServiceConfig config = new HpsOrcaServiceConfig();
config.setDeviceId(5315938);
config.setLicenseId(101433);
config.setPassword("$Test1234");
config.setUserName("777700857994");
config.setSiteId(101436);
config.setSiteTrace("trace0001");
config.setVersionNumber("1234");
config.ApplicationId = "Mobuyle Retail";
config.HardwareTypeName = "Heartland Mobuyle";
config.IsTest = true; //Use for certifications and develpoment testing.  false by default.
{% endhighlight %}

{% highlight python %}
# coming soon
{% endhighlight %}

{% highlight ruby %}
# coming soon
{% endhighlight %}

{% highlight js %}
// coming soon
{% endhighlight %}

## Register to get a device activation code (in results and emailed).

### Parameters:

Parameter | Description
--------- | -----------
merchantId | String with the assigned merchantID
email | String with the email address to be sent the activation code.

### Returns: DeviceActivationResponse

Parameter | Description
--------- | -----------
MerchantId | Issued merchant ID
DeviceId | This deviceID
Email | The email address sent the activation code
ApplicationId | Device fields
HardwareTypeName | Device fields
SoftwareVersion | Device fields
ConfigurationName | Device fields
PeripheralName | Device fields
PeripheralSoftware | Device fields

{% highlight csharp %}

//Create the config as mentioned above
var config = new HpsOrcaServiceConfig {...}

//Uses the vendors credentials rather than the merchants.
config.UserName = "admin";
config.Password = "password";

//Create the service with the config object.
var orcaService = new HpsOrcaService(config);

var activationCodeResponse = orcaService.DeviceActivationRequest("777700857994", "someone@someplace.com");

{% endhighlight %}

{% highlight java %}

//Create the config as mentioned above
//Uses the vendors credentials rather than the merchants.
config.setUserName("admin");
config.setPassword("password");

HpsOrcaService service = new HpsOrcaService(config);
HpsDeviceActivationResponse response = null;
try {
	response = service.deviceActivationRequest("777700857994", "someone@someplace.com");
	if (response != null)
	{
		activationCode = response.activationCode;
	}

}catch (Exception e) {
	e.printStackTrace();

	//Handle failure ....
}

{% endhighlight %}

## Activate your device and getting your API key for the activation code.

### Parameters:

Parameter | Description
--------- | -----------
merchantId | String with the assigned merchantID
activationCode | String with the activation code.

### Returns: DeviceActivationKeyResponse

Parameter | Description
--------- | -----------
MerchantId | Issued merchant ID
DeviceId | This deviceID
ApplicationId | Device fields
ActivationCode | The activation code
SecretApiKey | The API used in future calls. Store securely.

{% highlight csharp %}
//Create the config as mentioned above
var config = new HpsOrcaServiceConfig {...}

//Add merchants credentials
config.UserName = "777700857994";
config.Password = "$Test1234";

//Create the service with the config object.
var orcaService = new HpsOrcaService(config);

var apiKeyFromCodeResponse = orcaService.ActivateDevice("777700857994", activationCodeResponse.ActivationCode);

{% endhighlight %}

{% highlight java %}
//Create the config as mentioned above
//Add merchants credentials
config.setUserName("777700857994");
config.setPassword("$Test1234");

HpsOrcaService service = new HpsOrcaService(config);
HpsDeviceActivationKeyResponse response = null;

try {
    response = service.activateDevice("777700857994", activationCode);
    if (response != null)
    {
        apiKey = response.apiKey;
    }
} catch (Exception e){
    e.printStackTrace();

    //Handle failure ....
}
{% endhighlight %}

{% highlight python %}
# coming soon
{% endhighlight %}

{% highlight ruby %}
# coming soon
{% endhighlight %}

## Get your API key for the registered device.

### Returns: String - SecretApiKey

{% highlight csharp %}

//Create the config as mentioned above
var config = new HpsOrcaServiceConfig {...}

//Add merchants credentials
config.UserName = "777700857994";
config.Password = "$Test1234";
config.SiteId = 101436;
config.LicenseId = 101433;

//Create the service with the config object.
var orcaService = new HpsOrcaService(config);

string apiKey = orcaService.GetDeviceAPIKey();

{% endhighlight %}

{% highlight java %}

//Create the config as mentioned above
//Add merchants credentials
config.setUserName("777700857994");
config.setPassword("$Test1234");
config.setSiteId(101436);
config.setLicenseId(101433);
config.setDeviceId(5315938);

HpsOrcaService service = new HpsOrcaService(config);

try {
	String response = service.getDeviceAPIKey();
	return response;
}catch (Exception e){
	e.printStackTrace();

	//Handle failure ....
}

{% endhighlight %}

## Get device parameters.

### Returns: String - JSON of various parameters

{% highlight csharp %}

//Create the config as mentioned above
var config = new HpsOrcaServiceConfig {...}

//Add you secret API key
config.SecretApiKey = apiKey;

//Create the service with the config object.
var orcaService = new HpsOrcaService(config);

try
{
	string response = orcaService.GetDeviceParameters();
	return response;
}
catch (Exception e)
{
	//No parameters found throws server 400 messages.
	return "No Parameters";
}

{% endhighlight %}

{% highlight java %}

//Create the config as mentioned above
//Add the api key
config.setSecretAPIKey(apiKey);

HpsOrcaService service = new HpsOrcaService(config);

try {
	String response = service.getDeviceParameters();
	return response;   //JSON String
}catch (Exception e){
	e.printStackTrace();
	return "No Parameters";
	//No parameters found throws server 400 messages.
}

{% endhighlight %}
