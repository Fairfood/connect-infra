This includes how to configure Connect applications, such as the Connect Mobile App and Connect Web.

Prequisites needed to use Connect App:
  - Connect Server Setup
  - Server Configuations like creating Company, Product etc.
  - Connect App Installed

Once the connect server is successfully set up and running you nedd to connect your server with connect app.

- If not set up, follow this guide to 👉 [Setup Server](https://github.com/Fairfood/connect-infra)

- If connect app not installed, follow this guide to 👉 [Install App](https://docs.fairfood.org/install_app)


Configurations required inorder to use the app:
  - Company Creation
  - Product Creation
  - Company Member Creation
  - Company Product mapping
  - Premium Creation(not mandatory)
  - Form Creation(not mandatory)


---


## Accessing the Admin Panel

- **URL**: `{root_url}/connect/admin/`

<img src="/images/admin/login.png" alt="Login screen" />

- **Credentials**: Found in `connect-infra/env/.django.env`  
  The admin user is created during connect server setup by the credentials used in 
  the env


---

## 1.Company Setup and Configuration

We can create a company from Django admin. The name, address and other configs are set up from the admin panel.

 - **Buy Enabled**: If selected the connect app will be having an option to buy the products.
 - **Sell Enabled**: If selected the connect app will be having an option to sell the products.
 - **Only Connect**: If selected the connect app will be a standalone app, the sync with Trace Application will not work. To [Know more about Trace](https://docs.fairfood.org/introduction)
 - **Allow Multiple Login**: If selected the connect app will enables multiple device logins for the user
 - **Make Farmer Private**: If selected the connect app will enable date of birth validation for the farmer passbook. The farmer passbook is a standalone Open API section where farmer details can be accessed using farmer card IDs. If the company to which the farmer belongs has **Make Farmer Private** enabled, users must provide the farmer’s date of birth to view the details.

<img src="/images/admin/buy.png"/>

## Create a Company 

1. Under **Supply Chains**, click **Companies**.
2. On the Companies list page, click **“Add Company”**.
3. Fill in all required fields
4. Click **Save** to create the company.

<img src="/images/admin/add_company.png" alt="Add company" />

For sell enabled companies buyers should be mapped. If the product is received from farmers by the collectors and then given to our buyer company first we will create a buy transaction and we sell the product to the buyer company. 
- **Is Default**: Makes the buyer the default buyer of the company. While selling, this buyer will be selected as default.

<img src="/images/admin/add_company_buyer.png"/>


---

## 2.User Creation and Assignment

A user can be created in the Connect application from Django admin and later mapped to a company. This user can then be assigned various roles and permissions to perform different operations within the connect application.

## Create a User

1. Navigate to **Accounts → Base User**
2. Click **“Add Base User”**.
3. Fill in the fields and save.

<img src="/images/admin/add_base_user.png" alt="Add User" />

4. Now, fill other fields and save.

<img src="/images/admin/user_creation.png" alt="Add User" />


Note: Set the username and email address as the email.

## Map User to Company

1. Navigate to **Supply-Chains → Company Members**
2. Click **“Add Company Member”**.
3. Select the user, company and user type accordingly
4. Save the mapping.

<img src="/images/admin/add_company_member.png" alt="Add Member" />


---


## 3.Product Management

In order to conduct transactions, there must be products associated with the company. Products are also created through the Django admin panel. Once created, products must be mapped to a company.

## Add a Product

A product can be created in the Connect application and later mapped to a company. This product can them be used to perform different operations within the system.

1. Navigate to **Catalogs → Product**
2. Click **“Add Product”**.

<img src="/images/admin/add_product.png" alt="Add Product" />

3. Fill in the detials and save

## Add a Product to Company

1. Navigate to **Supply-Chains → Companies**
2. Select the company which you want to edit.
3. Click on Add company product and select the product

<img src="/images/admin/add_company_product.png" alt="Add Company Product" />

4. Save changes.

- In order to hide product deselect "Is Company Product Active" to make the product invisible in the App.

<img src="/images/admin/product_active.png"/>


---


## 4.Premium Management

Premiums are additional charges applied to transactions. If the premium type is selected as 'per transaction' the premium is applied for transaction once, regardless of the quantity.

Below are some of the fields to configure the Premiums. They are dropdowns and only one can be selected per field.

- **Premium Type**
  - `Per Transaction`: If chosen the premium is applied once for each transaction, regardless of the quantity involved.
  - `Per KG`: If chosen the premium is calculated based on the weight of the product in kilograms.
  - `Per Unit Currency`: If chosen the premium is calculated as percentage or fixed amount relative to the total value of the transaction (based on the currency).
  - `Per Farmer`: If chosen the premium is applied once for each farmer involved, regardless of how much they produce.
- **Applicable Activity**
  - `Buy`: Enabling this make sures that the premium will be used only for buying
  - `Sell`: Enabling this make sures that the premium will be used only for selling
- **Premium Category**
  - `Transaction Premium`: If selected the premium will be used only for transaction.
  - `Payout Premium`: If selected, a new option 'Pay' will be enabled along with buy and sell. This option allows to pay farmers from application.
- **Calculation Type**
  - `Normal`: Used for product premiums only. ie, this premium will only work if the premium is mapped with the product. The premium amount will be applied according to the amount set in the premium.
  - `Manual`: If selected the premium can be entered manually in the app
  - `Options (Dropdown)`: If selected, the app will show predefined options to select premium. The option name and amount can be added from 'add premium option'.
  - `Ranges`: If selected, the app will only accept according to this range specified. The range from, range to and amount can be added from 'add premium range'.

## Add a Premium

1. Navigate to **Catalogs → Premiums**
2. Click **“Add Premium”**.

<img src="/images/admin/add_premium.png"/>

3. Fill in the fields and save.

If the created premiums need to be product-specific, they can be added under the **Company Product** mapping. The premium will only be added while doing transaction with that mapped product only.

## Add product premium

1. Navigate to **Supply-Chains → Companies**
2. Add or edit the relevant **Company Product**.

<img src="/images/admin/add_company_product.png"/>

3. Add or map **Premiums** (e.g., *Kualitas Premium* mapped with *Black Pepper*).
4. Save changes.

Additionally, companies can have **payout premiums** configured. A payout premium 

---


## 5.Dynamic Forms and Field Configuration

If we need to add any field other than inbuilt fields we can add them from Django Admin. Like if we need any extra field while doing transactions we will create a form with form type 'transaction' which enables the extra fields in the form. In order to reflect instantly in the app run 'Hot Fix' from settings. ie, we need to add custom transaction date we create a form with form field label as 'Transaction Date', field type as 'Date' and key as 'transaction_date'

**Form Type**
- Transactions - add extra fields while doing transaction in connect application
- Payments - add extra fields while making payments in connect application
- Farmer - add extra fields while registering farmer in connect application
- Products - add extra fields while creating product in connect application.

Each form is defined in the Form model, and its fields can be customized using the **Form Field**.

## Add Custom Forms

1. Navigate to **Forms → Forms**
2. Click **“Add Form”**.

<img src="/images/admin/add_form.png"/>

4. Add **Form Fields** (types, dropdowns, etc.)

<img src="/images/admin/add_form_field.png"/>

5. Optionally configure **Form Field Configs** to control frontend visibility and behavior.

<img src="/images/admin/add_form_field_config.png"/>

6. Save the form.


---


## 💰 Transactions Interface

All transactions involving buying or selling are recorded and visible under the **Transactions tab** in the application. Users can view the transaction history, but it is important to note that the mobile app only shows **transactions that were synced since the last successful synchronization**. This helps reduce app load time and ensures better offline usability.

The full set of transaction records is available in the **Connect Web Application**, which is designed for more comprehensive data review and administration.

Users can also:

- Filter transactions based on various parameters
- Export the data to CSV


---

## 🔄 Synchronization and Offline Mode

The application is designed to function both **online and offline**, which is critical in rural or low-connectivity environments.

When working offline, any transaction that is performed is stored locally on the device. Once an internet connection becomes available, the system automatically attempts to sync these records with the database.

There are two key options provided for manual synchronization:

1. **Sync**: This option appears in the top-right corner of the app and can be used to manually push pending data to the server if automatic syncing fails.
2. **Hot Sync**: This is a more advanced sync feature used to reset listing and reference data in the mobile app from the database. It **does not delete any database data**. It is especially useful if there are inconsistencies or issues in the mobile data and a fresh pull from the server is required.

---

## 👤 Profile and User Preferences

Under the **Profile tab**, users can update their own personal information. In addition to personal details, users can  customize how the app behaves and displays data.

Settings available include:

- Changing the application language
- Adjusting number formats (e.g., decimal separators, digit grouping)
- Enabling or disabling transaction announcements (e.g., audio or on-screen prompts)

These customizations help improve usability for users operating in different regions or with different preferences.


--- 
