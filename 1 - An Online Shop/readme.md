# Online Shop

In this use case, some thoughts and patterns are explained that can be helpful for several NoSQL data modeling scenarios. [NoSQL Workbench for Amazon DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/workbench.settingup.html) is used since it is a great tool for designing and visualizing data models for Amazon DynamoDB applications.

## Use Case

...
 
 A **customer** visits an online shop, browses through different **products** and places an **order** for some of the **products**. Based on the **invoice**, customer can pay using discount code or gift card and pay for the remaining amount by credit card. Purchased products will be picked from one or several **warehouses** and will be **shipped** to the provided address.
 
 ...

## Entity Relation Diagram
![](resources/AnOnlineShopErd.png)

The existence of Customer, Product and Warehouse entities is independent of any other entity while Invoice and Shipment entities depend on Order entity. When going through each access pattern, the type of entity has an effect on how an item collection is built. Item collection refers to item(s) that have the same partition key.

In order to model the 1:M and M:N relations between entities in this scenario, composite primary key (partition key + sort key) is chosen for this table over simple primary key (partition key). Note that not all the items in the table models a relationship, there are items that represents the entity itself. These items will have the same value for both partition and sort keys.

## Access Patterns

Always start from the data access patterns of the application when designing the data model.

| Access Patterns      |
| :---        | 
| Get customer for a given customerId      | 
| Get product for a given productId   | 
| Get warehouse for a given warehouseId |
| Get a product inventory for all warehouses by a productId |
| Get order for a given orderId |
| Get all products for a given orderId |
| Get invoice for a given orderId |
| Get all shipments for a given orderId |
| Get all orders for a given productId for a given date range |
| Get invoice for a given invoiceId |
| Get all payments for a given invoiceId |
| Get shipment detail for a given shipmentId |
| Get all shipments for a given warehouseId |
| Get inventory of all products for a given warehouseId |
| Get all invoices for a given customerId for a given date range |
| Get all products ordered by a given customerId for a given date range  |