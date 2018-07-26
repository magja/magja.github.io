## Examples

### Category

Get only the basic information of a Product Category, without its dependencies:

    Category category = remoteServiceFactory.getCategoryRemoteService.getByIdClean(2);

Get Product Category with its children:

    Category category = remoteServiceFactory.getCategoryRemoteService.getByIdWithChildren(2);
    for (Category child : category.getChildren()) {
      // do something with the child
    }

Get Product Category with its parent:

    Category category = remoteServiceFactory.getCategoryRemoteService.getByIdWithParent(2);
    Category parent = category.getParent();

Get category with its parent and children:

    Category category = remoteServiceFactory.getCategoryRemoteService.getByIdWithParentAndChildren(2)


### Product

List all products with dependencies (slower)

    List<Product> products = remoteServiceFactory.getProductRemoteService.listAll();

List all products without dependencies (faster)

    List<Product> products = remoteServiceFactory.getProductRemoteService.listAllNoDep()

Create Product

    Product product = new Product();
    product.setSku("DUMMYPRD");
    product.setName("Lovely Umbrella");
    product.setShortDescription("This is a short description");
    product.setDescription("This is a description for Product");
    product.setPrice(250.99);
    product.setCost(100.22);
    product.setEnabled(true);
    product.setWeight(0.500);
    product.setType(ProductTypeEnum.SIMPLE.getProductType());
    product.setAttributeSet(new ProductAttributeSet(4, "Default"));

    // category
    List<Category> categories = new ArrayList<Category>();
    categories.add(new Category(2));
    product.setCategories(categories);


    product.setWebsites(new Integer[] { 1 });
    product.setVisibility(Visibility.CATALOG_SEARCH);

    // inventory
    product.setQty(new Double(20));
    product.setInStock(true);
    product.setMetaTitle("meta title");
    product.setMetaDescription("meta description");
    product.setMetaKeyword("keyword");

    // Optional: you can set the properties directly by-passing the setter like too:
    product.set("meta_description", "one two tree")

    // then, we just instantiate the service to persist the product
    remoteServiceFactory.getProductRemoteService.save(product)

### Customer

Reading the Customers

    List<Customer> customers = remoteServiceFactory.customerRemoteService.list();
