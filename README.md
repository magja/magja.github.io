# Welcome to Magja

Magento is a popular and emerging open-source e-commerce platform written in PHP with a market share of [around 30%](https://en.wikipedia.org/wiki/Magento).
Magja provides a Java Connector for Magento's Core API that allows easy integration with the shop installation and allows for exchange data offered by the API.
In doing so, Magja bridges the gap between the PHP system and Java ecosystem by offering a Java-Style client for integration in any kind  of applications.

## Core Features
Magja currently provides the following features:
- Basic support for Magento 1.x SOAP API V1
- Allows access to:
  - Product data
  - Product media
  - Product link
  - Product categories
  - Product attributes
  - Country data
  - Region data
  - Customer data
  - Order data
  - Invoice data
  - Cart data
- Open for custom extensions of the API (without code generation)

## Getting started

## Installation and configuration

Magja artifacts are available in the Sonatype Maven repository. Please put the following repository definition into your `pom.xml`:

    <repositories>
      <repository>
        <id>sonatype</id>
        <name>Sonatype Repository</name>
        <url>http://oss.sonatype.org/content/groups/public</url>
      </repository>
    </repositories>

and add the dependency to your project:

    <dependency>
      <groupId>com.google.code.magja</groupId>
      <artifactId>magja</artifactId>
      <version>1.0.3-SNAPSHOT</version>
    </dependency>

to get started. In order to connect to your Magento Shop installation, you need to put `magento-api.properties` on your classpath.
You can copy an example properties from samples folder. Essentially, the properties are self-explanatory:

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

## Basic usage

Magja is offering a set of services which can be used to access the Magento API. A service can be obtained
from the `RemoteServiceFactory` instance. The sample usage is demonstrated below:

    Logger log = LoggerFactory.getLogger("logger");
    RemoteServiceFactory remoteServiceFactory = new RemoteServiceFactory(MagentoSoapClient.getInstance());
    ProductRemoteService productService = remoteServiceFactory.getProductRemoteService();

    Product product = new Product();
    product.setSku("0001-QWER-12090");
    product.setName("Milk");

    try {
      productService.add(product);

      List<Product> allProducts = productService.listAll();
      for (Product shopProduct : allProducts) {
        log.info("{}", shopProduct);;
      }

    } catch (ServiceException e) {
      log.error("Error manipulating products", e);
    } catch (NoSuchAlgorithmException e) {
      log.error("Error manipulating products", e);
    }

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
