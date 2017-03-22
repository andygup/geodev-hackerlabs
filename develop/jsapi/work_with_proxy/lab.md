### Working with proxy

This lab covers the basics for allowing public, _no-login-required_ access to secure ArcGIS Online or Portal services secured with OAuth. 

PRE-REQUISITE: Before starting this lab make sure you have a working web server installed on your laptop. Common web servers include IIS and Apache.

1. Create two new folders under your local web server root directory. Let's name one `geodev-hackerlabs` and the other `proxy`. We'll work with the `proxy` directory later on in the lab.

```javascript

    C:InetPub/wwwroot/
    ├──proxy/
    └──geodev-hackerlabs/

```

2. In the `geodev-hackerlabs` folder create a subdirectory called `working_with_proxy`. Copy the [index.html](index.html) file from this lab into your new folder.  

```javascript

    C:InetPub/wwwroot/
    ├──proxy/    
    └──geodev-hackerlabs/
       └──working_with_proxy/
          └──index.html

```

3. Now, in `index.html` modify the `proxyUrl` property so that it points to your local webserver directory path, for example:
 
```javascript

  urlUtils.addProxyRule({
        urlPrefix: "route.arcgis.com",
        proxyUrl: "http://localhost/proxy/proxy.ashx"
    });

```

4. We'll switch gears here and set up the proxy. Clone or download the [github.com/esri/resource-proxy](https://github.com/Esri/resource-proxy) repository to your laptop. 

5. Find the resource-proxy type that works best for your webserver such as DotNet, Java or PHP. Then copy the contents of that folder into the `proxy` folder on your local web server. Your filesystem should now look similar to this:

```javascript

    C:InetPub/wwwroot/
    ├──proxy/
    │  └──Web.config
    │  └──proxy.ashx
    │  └──proxy.config
    │  └──proxy.xsd 
    └──geodev-hackerlabs/
       └──working_with_proxy/
          └──index.html

```

6. Go to [https://developers.arcgis.com/dashboard](https://developers.arcgis.com/dashboard) and [Register a New Application](https://developers.arcgis.com/applications/#/new/). 

7. Within the `proxy.config` under `serverUrls` add a new `serverUrl` for the route service. Add the `clientId` and `clientSecret` from the application you registered in the previous step.

```xml

	<serverUrl url="https://route.arcgis.com"
        clientId="6Xo1d-example-9Kn2"
        clientSecret="5a5d50-example-c867b6efcf969bdcc6a2"
        matchAll="true"/>

```

8. Load your local copy of `index.html` into your browser using the pattern `http://[your_local_web_server]/geodev-hackerlabs/`, then click on the map to add driving direction route stops. Be sure to check the developer console for any errors and fix them. You should be able to access the route service without manually log in.

# Bonus

* To learn about implementing app logins and figuring out how to get the `clientId` and `clientSecret` programmatically go [here](https://developers.arcgis.com/authentication/accessing-arcgis-online-services/).

* For more info on proxy configuration settings check out the [Resource-Proxy docs](https://github.com/Esri/resource-proxy/blob/master/README.md#proxy-configuration-settings) or the [Working with Proxy Services article](https://developers.arcgis.com/authentication/working-with-proxies/).
