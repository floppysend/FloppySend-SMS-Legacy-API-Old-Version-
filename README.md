## FloppySend SMS API ( Old Version )
FloppySend provide APIs for SMS in old version, where user can use username & password as request parameters, 
you may get your SMS legacy password from your [accoutn dashboard](https://app.floppysend.com/) at Legacy Api settings. 

Request Types
 - GET: If the request is get method you need to append params as query string inside the params section
 - POST: If request is post method you need to append params as x-www-form-urlencoded inside the body of the request

```
https://api.floppy.ai/smslegacy
```

#### Parameters
  | Parameter | Type | Required | Description |
  | --------- | ---- | -------- | ----------- |
  | Username | String | Yes | username for the user can be seen in the account page under legacy tab |
  | Password | String | Yes | password for the user can be seen in the account page under legacy tab which the user can change |
  | To | String | Yes | | number/numbers sending to |
  | From | String | Yes | sender which will appear to the user |
  | Dcs | String | Yes | if message contains unicode: 8, if message doenst contain unicode: 0 |
  | Text | String | Yes | message body |
  | Sched | String | Optional | iso format |
  
#### SMS Legancy API Responses
```JSON
{
    "Result": "Success",
    "Datainfo": 
    [
        {
            "Status": "Sent",
            "ID": "Response_Id",
            "Error_Code": "0",
            "Error_Desc": "0"
        }
    ]
}                   
```

#### SMS Legancy API Code Sample
```PHP
//PHP

<?php

$curl = curl_init();
curl_setopt_array($curl, array(
        CURLOPT_URL => 'https://api.floppy.ai/smslegacy',
        CURLOPT_RETURNTRANSFER => true,
        CURLOPT_ENCODING => '',
        CURLOPT_MAXREDIRS => 10,
        CURLOPT_TIMEOUT => 0,
        CURLOPT_FOLLOWLOCATION => true,
        CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
        CURLOPT_CUSTOMREQUEST => 'POST',
        CURLOPT_POSTFIELDS =>
        'username={your_user_name}&password={your_password}&to={to_number}&from={sender}&dcs={dcs}&text={message_body}',
        CURLOPT_HTTPHEADER => array(
        'Content-Type: application/x-www-form-urlencoded'
        ),
    ));
$response = curl_exec($curl);
curl_close($curl);
echo $response;
```

```Ruby
//Ruby

require "uri"
require "net/http"
url = URI("https://api.floppy.ai/smslegacy")
https = Net::HTTP.new(url.host, url.port)
https.use_ssl = true
request = Net::HTTP::Post.new(url)
request["Content-Type"] = "application/x-www-form-urlencoded"
request.body =
"username={your_username}&password={your_password}&to={to_number}&from={sender}&dcs={dcs}&text={message_body}"
response = https.request(request)
puts response.read_body
```

```Java
//JAVA
//The OkHttpClient is an external package, you need to install it before making the request, 
//And don't forget to add user permission for the internet inside "\MyApplication\app\src\main\AndroidManifest.xml"
//Also, you need to add required dependencies inside "MyApplication\app\build.gradle"

OkHttpClient client = new OkHttpClient().newBuilder()
.build();
MediaType mediaType = MediaType.parse("application/x-www-form-urlencoded");
RequestBody body = RequestBody.create(mediaType,
"username={your_username}&password={your_password}&to={to_number}&from={sender}&dcs={dcs}&text={message_body}");
Request request = new Request.Builder()
.url("https://api.floppy.ai/smslegacy")
.method("POST", body)
.addHeader("Content-Type", "application/x-www-form-urlencoded")
.build();
Response response = client.newCall(request).execute();
```

```C#
//C#

var client = new RestClient("https://api.floppy.ai/smslegacy");
client.Timeout = -1;
var request = new RestRequest(Method.POST);
request.AddHeader("Content-Type", "application/x-www-form-urlencoded");
request.AddParameter("username", "{your_username}");
request.AddParameter("password", "{your_password}");
request.AddParameter("to", "{to_number}");
request.AddParameter("from", "{sender}");
request.AddParameter("dcs", "{dcs}");
request.AddParameter("text", "{message_body}");
IRestResponse response = client.Execute(request);
Console.WriteLine(response.Content);
```

```Javascript
//NodeJs
//Make sure to import Axios and install npm packages before doing the request

var axios = require('axios');
var qs = require('qs');
var data = qs.stringify({
'username': 'YOUR-USER-NAME',
'password': 'YOUR-PASSWORD',
'to': 'TO-NUMBER',
'from': 'FROM-SENDER',
'dcs': '0',
'text': 'MESSAGE-BODY',
'sched': 'Time-IsoFormat' 
});

var config = {
  method: 'post',
  url: 'https://api.floppy.ai/smslegacy',
  headers: { 
    'Content-Type': 'application/x-www-form-urlencoded'
  },
  data : data
};

axios(config)
     .then(function (response) {
       console.log(JSON.stringify(response.data));
     })
     .catch(function (error) {
       console.log(error);
     });
```
