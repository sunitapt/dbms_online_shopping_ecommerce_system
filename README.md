
# Online shopping Management DBMS Project
As a part of our University Curriculum, we made this project for Database Management Systems (DBMS).
This project contains theoretical as well as implementation in MySQL.
If you liked the repo do star it.

## Pre-requisite

- Oracle SQL Server (or) Oracle Community Edition

- MySQL server 

- Mysql Workbench



## Contents
- Mini world and Project Description	
- Basic structure	
  - Functional requirements	  
  - Entity Relation (ER) diagram and constraints	  
  - Relational database schema	
- Implementation	
  - Creating tables	
  - Inserting data	  
- Queries
  - Basic queries	  
  - PL/SQL function	  
  - Triggers	  


#### This project was completed by @sunitapt 	
## 1. Mini world and Description

In this modern era of online shopping, no seller wants to be left behind, moreover, due to its simplicity the shift from offline selling model to an online selling model is witnessing a rampant growth.<br>
Therefore, as an engineer, our job is to ease the path of this transition for the seller.
Amongst many things that an online site requires the most important is a database system. Hence in this project, I am planning to design a database where small clothing sellers can sell their products online.

## 2. Basic Structure

### 2.1 Functional requirement

- A new user can register on the website.
- A customer can see details of the product present in the cart
- A customer can view his order history.
- Admin can start a sale with a certain discount on every product.
- Customers can filter the product based on the product details.
- A customer can add or delete a product from the cart.
- A seller can unregister/ stop selling his product.
- A seller/ customer can update his details.
- Admin can view the products purchased on a particular date.
- Admin can view a number of products sold on a particular date.
- A customer can view the total price of the product present in the cart unpurchased.
- Admin can view details of the customer who have not purchased anything.
- Admin can view total profit earned from the website.
- Admin can add sealeman details.
- Admin can details of shipping.
- Admin can see details of active and inactive clients/customers.


### 2.2 Entity Relation Diagram
![ERD_DBMS_CP](https://user-images.githubusercontent.com/47025719/79017672-8a5b4b00-7b8f-11ea-902a-ed7c981d1996.png)
Details of tables:
  1)Product_master
            A.p_details -[FK]payment details, This attribute is common between payment and 
                      product master table.
	B.product_sales- Information of product sales
	C.product_description -detailed information of product which are there to sale 
	D.product_no -[PK]product has given a unique id i.e number .user ordered some specific  
                       a product  which is named by some product number
 	E.product_price -prices of products 
	F.quantity_available -multivalued attribute - this is a multivalued attribute which
                  describes available quantities.
	G.product_type -Types of product.categories like women, men,etc.  
2.sales_order_details
           A.order_no-[PK]user orders some specific product and it has some order number.
	B.product_no- [FK]product has given a unique id i.e number. user ordered some specific  
                       a product  which is named by some product number
C.amt-price of product 
	D.quantity_no- how many quantities are ordered by the user is indicated by quantity number

3. Sales_order -
	A.order_date-date on which user ordered product 
	B.salesman_no-[FK]salesman who will deliver order to user 
	C.client_no- [FK]user number,id ,etc.
	D.order_no-[PK]user orders some specific product and it has some order number.

4.salesman_master 
	A.salesman_no-[PK]salesman unique id 
	B.salesman_pincode-pincode id of salesman 
	C.salesman_city-city of salesman 
	D.salesman_name-name of salesman
	E.salesman_phone_no-salesman phone number 

5.client-
	A.client_mobile-mobile number of client
	B.user_id-[FK]user id of client to log in to web/app
	C.client_email-email id of client for creation of workspace for user
	D.client_pincode-pincode of client,address requirement
	E.client_address-address of client for delivery purpose
	F.client_name-name of client 
	G.client_no-[PK]unique id of client which is primary key of this table 
	H.client_city-city of client for address purpose for delivery.
	

6.App_user -
	A.user_wish_list-user wants to wish to buy this product 
	B.user_id-[FK]user id of client/user user id is necessary for log in to the web/app
	C.user_cart-user added product to buy the product
	D.user_address-address of user 
	E.user_name-name of user for log in to the app/website
	F.user_mobile-mobile number of user 
	G.user_pincode-pincode of user for location purpose.
	H.user_email-email address of the user for login purpose.

7.user_log_in
	A.user_password-password of the user for security purposes.
	B.user_username-username of user for login purpose
	C.user_id-[PK]user id of user for login app/website.

## 3. Implementation

You can directly copy and paste all the commands from the text given here into the SQL console to create and insert values into your table.

### 3.1 Creating Tables
```sql
1.
create table user_login
(
user_email_id varchar(20),
user_password int(11),
 primary key(user_email_id)
);

2.
create table app_user_one
(
user_email_id varchar(20),
user_mobile int(11),
user_cart varchar(20),
user_wishlist varchar(20),
primary key(user_email_id)
);

3.
create table app_user_two
(
user_email_id varchar(20),
user_streetno int(11),
user_city varchar(20),
primary key(user_email_id);
);

4.
create table app_user_three(
user_email_id varchar(20),
user_state varchar(20),
user_pincode int(11),
primary key(user_email_id)
);

5.
create table client_one
(
client_no int(11),
client_name varchar(20),
client_email varchar(20),
client_mobile int(11),
user_email_id varchar(20),
 primary key(client_no),
foreign key(user_email_id) references app_user_one(user_email_id),
foreign key(user_email_id) references app_user_two(user_email_id),
foreign key(user_email_id) references app_user_three(user_email_id),
 foreign key(user_email_id) references app_user_one(user_email_id)
);

6.
create table client_two
(
client_no int(11),
client_streetno int(11),
primary key(client_no)
);

7.
create table client_three
(
client_no int(11),
client_pincode int(11)
);

8.
 create table salesman_master
(
salesman_no int(11),
salesman_name varchar(20),
salesman_phoneno int(11),
salesman_pincode int(11),
primary key(salesman_no);
);

9.
create table sales_order
(
order_no int(11),
order_date date,
salesman_no int(11),
client_no int(11),
foreign key (order_no) references sales_order_details(order_no),
foreign key (client_no) references client_one(client_no),
foreign key (salesman_no) references salesman_master(salesman_no),
foreign key (order_no) references sales_order_details(order_no)
);

10.
create table sales_order_details
(
order_no int(11),
product_no int(11),
quantity_no int(11),
primary key(order_no),
foreign key (product_no) references product_master_one(product_no),
foreign key (product_no) references product_master_two(product_no)
);

11.
create table payment_one
(
pay_id int(11),
pay_amt int(11),
pay_date date,
pay_customer_id int(11),
primary key(pay_id)
);

12.
create table payment_two
(
pay_id int(11),
pay_details_cash varchar(20),
pay_details_online varchar(20),
primary key(pay_id)
);

13.
create table product_master_one
(
product_no int(11),
pay_id int(11),
product_price int(11),
quantity_available int(11),
primary key(product_no)
foreign key (pay_id) REFERENCES payment_one(pay_id),
foreign key (pay_id) REFERENCES payment_two(pay_id)
);

14.
create table product_master_two
(
product_no int(11),
product_sizeforcustomer varchar(20),
product_colour varchar(20),
primary key(product_no)
);
### 3.2 Inserting Values

These are some demo values. Full data will be updated in future commits
## 4. Queries

### 4.1 Basic Queries

#### If the customer wants to see details of the product present in the cart

```sql




