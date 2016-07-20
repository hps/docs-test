---
title: Device Services
permalink: /device-services/
layout: default
---

# Device Services (Activation Service)

This is a wrapper for the Activation device service. The first step is to get an activation code from integration@e-hps.com

> Create an HpsActivationServiceConfig object for settings.

{% highlight php %}
<?php
$config = new HpsActivationServiceConfig();
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
config = HpsActivationServiceConfig(is_test=True)
{% endhighlight %}

{% highlight ruby %}
# coming soon
{% endhighlight %}

{% highlight js %}
// coming soon
{% endhighlight %}

## Activate your device and get your API key for the activation code.

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

> Activate your device

{% highlight php %}
<?php
//Create the config as mentioned above
$config = new \HpsActivationServiceConfig();
$config->setIsTest(true); //Use for certifications and develpoment testing.  false by default.

//Create the service with the config object.
$activationService = new HpsActivationService($config);

//activationCode may be obtained from integration@e-hps.com
//$activationCode = 111111;
$apiKeyFromCodeResponse = $activationService->activateDevice("777700857994", $activationCode);
{% endhighlight %}

{% highlight csharp %}
//Create the config as mentioned above
var config = new HpsActivationServiceConfig
{
    IsTest = true
};

//Create the service with the config object.
var activationService = new HpsActivationService(config);

//activationCode may be obtained from integration@e-hps.com
//var activationCode = 111111;
var apiKeyFromCodeResponse = activationService.ActivateDevice("777700857994", activationCode);
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
} catch (Exception e) {
    e.printStackTrace();

    //Handle failure ....
}
{% endhighlight %}

{% highlight python %}
# Create the config as mentioned above
config = HpsActivationServiceConfig(is_test=True)

# Create the service with the config object.
service = HpsActivationService(config)

# activation_code may be obtained from integration@e-hps.com
# activationcode = 111111;
response = self.service.device_activation_key('777700857994', activationcode)
{% endhighlight %}

{% highlight ruby %}
# coming soon
{% endhighlight %}

{% highlight js %}
// coming soon
{% endhighlight %}
