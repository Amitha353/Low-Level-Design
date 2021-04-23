### Design Amazon - Online Shopping System

* Amazon (amazon.com) is the world’s largest online retailer.

#### Requirements:
1. Users should be able to add new products to sell.
2. Users should be able to search for products by their name or category.
3. Users can search and view all the products, but they will have to become a registered member to buy a product.
4. Users should be able to add/remove/modify product items in their shopping cart.
5. Users can check out and buy items in the shopping cart.
6. Users can rate and add a review for a product.
7. The user should be able to specify a shipping address where their order will be delivered.
8. Users can cancel an order if it has not shipped.
9. Users should get notifications whenever there is a change in the order or shipping status.
10. Users should be able to pay through credit cards or electronic bank transfer.
11. Users should be able to track their shipment to see the current state of their order.

#### Actors
1. Admin: Mainly responsible for account management and adding or modifying new product categories.
2. Member: Members can perform can search the catalog, add/remove items to the shopping cart, they can place orders and add new products to sell.
3. System: Mainly responsible for sending notifications for orders and shipping updates.
4. Guest: All guests can search the catalog, add/remove items to the shopping cart, as well as become registered members.

#### Top UseCases:
1. Add/update products; whenever a product is added or modified, we will update the catalog.
2. Search for products by their name or category.
3. Add/remove product items in the shopping cart.
4. Check-out to buy product items in the shopping cart.
5. Make a payment to place an order.
6. Add a new product category.
7. Send notifications to members with shipment updates.

#### Classes
1. Account: 2 Accounts- Admin, members
2. Guest: Guests can search for and view products, and add them in the shopping cart.
3. Catalog: Users of our system can search for products by their name or category. This class will keep an index of all products for faster search.
4. Product: Each Product will belong to a ProductCategory.
5. ProductReview: Any registered member can add a review about a product.
6. ShoppingCart: Users will add product items that they intend to buy to the shopping cart.
7. Item: Product item that the users will be buying or placing in the shopping cart (Pen).
8. Order
9. OrderLog
10. ShipmentLog
11. Notification
12. Payment


#### Code:

##### 1. Enums, data types, and constants

```
public enum OrderStatus {
      UNSHIPPED, PENDING, SHIPPED, COMPLETED, CANCELED, REFUND_APPLIED;
}

public enum AccountStatus {
       ACTIVE, BLOCKED, BANNED, COMPROMISED, ARCHIVED, UNKNOWN;
}

public enum  ShipmentStatus {
       PENDING, SHIPPED, DELIVERED, ON_HOLD;
}

public enum  PaymentStatus {
       UNPAID, PENDING, COMPLETED, FILLED, DECLINED, CANCELLED, ABANDONED, SETTLING, SETTLED, REFUNDED;
}

public class Address {
  private String streetAddress;
  private String city;
  private String state;
  private String zipCode;
  private String country;
}
```

##### 2. Account, Customer, Admin, and Guest
* These classes represent different people that interact with our system:

```
public class Account {
  private String username;
  private String password;
  private String name;
  private String email;
  private int phone;
  private boolean status;
  Private Address shippingAddress;
  private String[] creditCards;
  private String[] bankAccounts;
  
  public Account(username, password, name, email, phone, status, creditCards, bankAccounts) {
    //Initialize
  }
  
  public void addProduct() {}
  
  public void addProductReview() {}
  
  public boolean resetPassword() {}
}

public class Customer() {
  private List<Product> cart;
  private double order;
  
  public int getShoppingCart() {
     return cart;
  }
  
  public void addItem(Product item) {
    cart.add(item);
  }
  
  public void removeItem(Product item) {
    cart.remove(item);
  }
  
 public class Guest extends Customer {
  public void registeredAccount() {}
 }

  public class Member extends Customer {
    public void placeOrder() {}
  }
}
```


##### 3. ProductCategory, Product, and ProductReview
* Classes related to a product

```
public class ProductCategory {
  private String name;
  private String description;
}

public class ProductReview {
  private int rating;
  private int review;
  private String reviewer;
}

public class Product {
  private int id;
  private String name;
  private String description;
  private float price;
  private String category;
  private int available_item_count = 0;
  private String seller_account;
  
  public int get_available_count() {
    return available_item_count;
  }
  
  public void updatePrice(float new_price) {
    this.price = new_price;
  }
}
```

##### 4. ShoppingCart, Item, Order, and OrderLog
* Users will add items to the shopping cart and place an order to buy all the items in the cart.

```
public class Item {
  private int id;
  private int quantity;
  private float price;
  
  public void updateQuantity(int quantity) {}
  
}

public class ShoppingCart {
  private Product[] items;
  
  public void addItems(Product item) {}
  
  public void removeItem(Product item) {}
  
  public void updateItemQuantity(Product item, int quantity) {}
  
  public Product[] getItems() {
    return items;
  }
  
  public void checkout() {
  }
}

public class OrderLog {
  private int ordernumber;
  private Date creationDate;
  private OrderStatus status;
}

class Order {
  private int ordernumber;
  private OrderStatus status;
  private Date orderDate;
  private OrderLog[] orderLog;
  
  public Order sendshipment() {
  }
  
  public void makepPyment() {}
  
  public void addOrderLog() {}
}
```

4. Shipment, ShipmentLog, and Notification: 
* After successfully placing an order, a shipment record will be created:

```
class ShipmentLog {
  private String shipment_number;
  private ShipmentStatus status;
  private Date creationdate;
}

class Shipment {
  private int shipment_number;
  private ShipmentStatus shipment_method;
  private Date shipmentdate;
  private Date estimatedarrival;
  private ShipmentLog[] shipmentLogs;
  
  public void addShipmentLog(ShipmentLog shipmentLog) {}
}

class Notification {
  private int notificationId;
  private Date createdOn;
  private String content;
  
  public Notification sendNotification(Account account) {}
}
```

 5. Search Interface and Catalog:
 
 ```
 public interface Search {
  public List<Book> searchByTitle(String title);
  public List<Book> searchByAuthor(String author);
  public List<Book> searchBySubject(String subject);
  public List<Book> searchByPubDate(Date publishDate);
}

public class Catalog implements Search {
  private HashMap<String, List<Product>> productNames;
  private HashMap<String, List<Product>> productCategories;

  public List<Product> searchByName(String query) {
    return productNames.get(query);
  }

  public List<Book> searchByCategory(String query) {
    return productCategories.get(query);
  }
}
```


https://github.com/tssovi/grokking-the-object-oriented-design-interview/blob/master/object-oriented-design-case-studies/design-amazon-online-shopping-system.md

