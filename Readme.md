[![Build status](https://ci.appveyor.com/api/projects/status/h0x5jv0s8p4ig078/branch/master?svg=true)](https://ci.appveyor.com/project/tparnell8/shodan-net/branch/master)

Visit the official Shodan API documentation at:

[https://developer.shodan.io](https://developer.shodan.io)

This is still in active development, error handling might not well handle well. Best bet when working with any libraries you didn't write..harden your calls!

## APi Docs

You can find doxygen docs [here](http://shodan-csharp-docs.azurewebsites.net/) 

## Installation

`install-package Shodan.Net`

## Getting started

You need to have an Api key. Get your [api key here](http://www.shodanhq.com/api_doc).


Create a shodan client. Note that ShodanClient inerhits from IDisposable, so you should wrap it in a using, or make sure it will be disposed. Shodan client is thread safe, so you should be able to keep 1 object around for many requests.

`var client = new Shodan.Net.ShodanClient("myapiKey");`

Now just query away. You should be able to find all the actions [in the docs](http://shodan-csharp-docs.azurewebsites.net/class_shodan_1_1_net_1_1_shodan_client.html) or just through the docs in intellisense.

```csharp

await client.GetPortsAsync();
await client.GetHostAsync("172.1.1.0");
await client.GetMyIpAsync();


```


## Searching

Searching shodan requires you to build up queries, and facets to make it easier we have used a generator pattern to produce queries.

```csharp

           await client.SearchHosts(
                query: a => a.Withcity("boston")
                      .Withcountry("usa")
                      .Before(DateTime.Now.AddDays(-5)),
                facet: b => b.WithAsn()

                );


```

