---
title: Device Services
permalink: /device-services/
layout: default
---

# Device Services (Activation Service)
This is a wrapper for the Activation device services

The first step is to register for device activation to generate an activation code.  This code can then register the device and generate the secret API key to use for other services.

## Create an ActivationServiceConfig object for settings.

{% highlight php %}
$config = new \HpsActivationServiceConfig();
$config->setIsTest(true); //Use for certifications and develpoment testing.  false by default.
{% endhighlight %}

{% highlight csharp %}
var config = new HpsActivationServiceConfig
{
	IsTest = true, //Use for certifications and develpoment testing.  false by default.
};
{% endhighlight %}

{% highlight java %}
HpsActivationServiceConfig config = new HpsActivationServiceConfig();
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

{% highlight php %}
//Create the config as mentioned above
$config = new \HpsActivationServiceConfig();
$config->setIsTest(true); //Use for certifications and develpoment testing.  false by default.

//Create the service with the config object.
$orcaService = new HpsActivationService($config);

//activation_code may be obtained from integration@e-hps.com
//$ActivationCode = 111111;
$apiKeyFromCodeResponse = $orcaService->activateDevice("777700857994", $ActivationCode);
{% endhighlight %}

{% highlight csharp %}
//Create the config as mentioned above
var config = new HpsActivationServiceConfig {...}

//Create the service with the config object.
var orcaService = new HpsActivationService(config);

//activation_code may be obtained from integration@e-hps.com
// var ActivationCode = 111111;
var apiKeyFromCodeResponse = orcaService.ActivateDevice("777700857994", ActivationCode);
{% endhighlight %}

{% highlight java %}
//Create the config as mentioned above
HpsActivationServiceConfig config = new HpsActivationServiceConfig();
config.IsTest = true; //Use for certifications and develpoment testing.  false by default.


HpsActivationService service = new HpsActivationService(config);
HpsDeviceActivationKeyResponse response = null;

//activation_code may be obtained from integration@e-hps.com
// var activationCode = 111111;
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

{% highlight js %}
// coming soon
{% endhighlight %}
