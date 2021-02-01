<p align = "center"> <a href="https://www.opencartbrasil.com.br/"> <img src = "https://forum.opencartbrasil.com.br/ext/sitesplat/flatbootsminicms/ images / logo / logo -color.png "alt =" OpenCart Brasil "> </a>
</p>

<p align = "center">
<a href="./LICENSE"> <img src = "https://img.shields.io/github/license/opencartbrasil/opencart-rest-api.svg" alt = "License"> </a>
</p>

## Presentation

REST API for OpenCart 2 and 3, which allows access to all database tables including those that are not native to OpenCart.

Access control to the REST API is done through the API key that is registered in the OpenCart administration.

Related projects:

  - [PHP-CRUD-API V1] (https://github.com/mevdschee/php-crud-api/tree/v1): PHP script that adds a REST API with direct access to the database (Single file PHP script that adds a REST API).

## Requirements

 1. PHP 5.3 or higher.
 2. PDO library enabled in PHP.
 3. OpenCart 2.1.0.2 or higher.
 3. OpenCart 3.0.0.0 or higher.

## Installation

 1. Download: https://github.com/opencartbrasil/opencart-rest-api/archive/master.zip
 2. Unzip the zip file, and upload the ** api.php ** and ** config_api.php ** files to your store's root directory.

**Ready!**
 
## Configuration

 1. Access the administration of your store, and go to the menu ** Settings → Manage Users → API ** (System → Users → API).
 2. Click the "** New **" button (Add New), in the "** API Name **" field (API Name) place "** API REST **", just below, click the "* * Generate ** "(Generate) to create your" ** API Key ** ", in the" ** Situation ** "(Status) field select the option" ** Enable ** "(Enabled), and click on "** Save **" button.
 
## Extra configurations (Extra Configuration)

### Restrict API access by IP (Restrict access IP):

Access the administration of your store, and go to the menu ** Settings → Manage Users → API ** (System → Users → API), locate the API with the name "** API REST **", click on the button "** Edit ** "(Edit), click on the tab" ** IP Address ** "(IP Addresses), click the button" ** Add IP ** "(Add IP), add the IP you want to have access to API, and click the "** Save **" button.
 
Now edit the file "** config_api.php **", and find the line:

`` php
define ('RESTRICT_IP', false);
``

And change to:

`` php
define ('RESTRICT_IP', true);
``

Finally, save your changes to the file.

### Record the log of accesses made through the API (Log Access API):

Edit the file "** config_api.php **", and find the line:

`` php
define ('SESSION_LOG', false);
``

And change to:

`` php
define ('SESSION_LOG', true);
``

If using OpenCart 3, find the line:

`` php
define ('OPENCART_V3', false);
``

And change to:

`` php
define ('OPENCART_V3', true);
``

Save the changes to the file, and you can view the access logs through the administration of your store, in the menu ** Settings → Manage Users → API ** (System → Users → API), locate the API with the name " ** REST API ** ", click the" ** Edit ** "button (Edit), and click the" ** Session ** "tab (Session).

## Usage

Access your store's URL, including the api.php file at the end, as shown:

`` http
http://www.yourdomain.com/api.php
``

It is necessary to inform your API Key in all API URLs that will be accessed, passing it in the request header with the name key having as value your API Key.

Example:

`` js
key = mMAnvMIaP7zPHnF7hBi23ebGyIU6sp2eWRfdi08yNWOo8wRXPAWgCol
``

Otherwise, you will receive the error message:

`` js
{"API Error": "Key not found!"}
``

Any database table will be accessible via the API, regardless of whether it is native to OpenCart or not, to access data or send data, you must request or send HTTP requests using the verbs GET, POST, PUT or DELETE.

The URLs are formed following the pattern (The URLs are formed following the pattern):

`` http
http: //domain/api.php/table_name/ {id}
``

`` http
http: //domain/api.php/table_name/ {id}
``

In the example below, we request all product data from the oc_product table:

`` http
GET http://www.yourdomain.com/api.php/oc_product/
``

In this other example, we request the product data with the product_id column equal to 40 in the oc_product table:

`` http
GET http://www.yourdomain.com/api.php/oc_product/40
``

### Complete documentation (Documentation)

[PHP-CRUD-API V1 MANUAL] (https://github.com/mevdschee/php-crud-api/blob/v1/README.md)

## Access to the OpenCart REST API (Access to the REST API OpenCart)

### - Listing the products: In PHP (PHP Script) GET:

`` php
<? php
$ headers = array ();
$ headers [] = 'Content-Type: application / json';
$ headers [] = 'key: mMAnvMIaP7zPHnF7hBi23ebGyIU6sp2eWRfdi08yNWOo8wRXPAWgCol'; // // Replace key value for API key OpenCart (Only numbers and letters)

$ ch = curl_init ();
curl_setopt_array ($ ch, [
CURLOPT_URL => 'http://www.yourdomain.com/api.php/oc_product/', //
