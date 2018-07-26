# Magja configuration guide

## Basic configuration

In order to connect to your Magento shop installation, you need to put `magento-api.properties` on your classpath.
Essentially, the properties are self-explanatory:

    # SOAP XML/RPC user
    magento-api-username=<replace with user>

    # SOAP XML/RPC api key
    magento-api-password=<replace with api key>

    # URL of the Magento installation
    # If your shop is installed not using a prefix e.g. /magento
    # please add the prefix to the path:
    # http://<yourmagento-host>/magento/index.php/api/soap/
    magento-api-url=http://<yourmagento-host>/index.php/api/soap/

    # the ID of the default attribute set
    default-attribute-set-id=4

    # the ID of the default root category
    default-root-category-id=2


## Advanced configuration

There are additional configuration properties, which can be set up in the properties file.

### Running behind the proxy

If you want to use the client behind a HTTP proxy, you can specify the settings in `magento-api.properties`:

    # HTTP proxy settings, default is false
    http-proxy-enabled=true
    http-proxy-host=localhost
    http-proxy-port=8080

    # HTTP proxy auth settings, default is false
    http-proxy-auth-enabled=true
    http-proxy-username=user
    http-proxy-password=pass

### Accessing HTTP-Basic Auth protected installation

If your shop is protected with HTTP Basic Authentication, you can pass a username and password using the following properties:

    # HTTP auth settings, default is false
    http-auth-enabled=true
    http-username=user
    http-password=pass
