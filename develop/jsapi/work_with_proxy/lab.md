### Working with proxy

This lab covers the basics for setting up a proxy for use with ArcGIS Online or Portal-based services.

Consider hosting your own proxy if you are accessing services that aren't CORS-based or if you want to
allow public access to secure services and save users from having to log-in.

1. Create a new folder in your local web server directory. This requires that you have IIS, Apache or similar web server
already set up on your laptop.

2. Clone or download the [github.com/esri/resource-proxy](https://github.com/Esri/resource-proxy) repository.

3. Copy the [index.html](index.html) file from this lab into your new folder. 

4. Copy the proxy folder into the root directory of your web server, for example your webserver
directory might look like this:

```javascript

    C:InetPub/wwwroot/
    ├──resource-proxy/
    │  └──DotNet/
    │  │  └──Web.config
    │  │  └──proxy.ashx
    │  │  └──proxy.config
    │  │  └──proxy.xsd
    │  └──Java/
    │  └──PHP/  
    └──geodev-hackerlabs/
       └──working_with_proxy/
          └──index.html

```

5. In `index.html` modify the `proxyUrl` property to your local webserver directory path, for example:
 

```javascript

  urlUtils.addProxyRule({
        urlPrefix: "route.arcgis.com",
        proxyUrl: "http://[yourmachine]/resource-proxy/DotNet/proxy.ashx"
    });

```

6. Within the `proxy.config` under `serverUrls` add a new `serverUrl` for the service that you want to share. Here is an example:


```xml

	<serverUrl url="https://route.arcgis.com"
        clientId="6Xo1d-example-9Kn2"
        clientSecret="5a5d50-example-c867b6efcf969bdcc6a2"
        matchAll="true"/>

```

To read about implementing app logins and figuring out where to get the `clientId` and `clientSecret` go [here](https://developers.arcgis.com/authentication/accessing-arcgis-online-services/).

For more info on proxy configuration settings go [here](https://github.com/Esri/resource-proxy/blob/master/README.md#proxy-configuration-settings).

8. Load `index.html` into your browser and check the developer console for any errors.