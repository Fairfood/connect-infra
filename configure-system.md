
## Accessing the Admin Panel

- **URL**: `{root_url}/connect/admin/`

<img src="/images/admin/login.png" alt="Login screen" />

- **Credentials**: Found in `connect-infra/env/.django.env`  
  The admin user is created during instance setup by the credentials used in 
  the env

---

## Create a Company

1. In the sidebar, under **Supply Chains**, click **Companies**.
2. On the Companies list page, click **“Add Company”** (top-right).
3. Fill in all required fields
4. Click **Save** to create the company.

<img src="/images/admin/add_company.png" alt="Add company" />

- **Buy Enable**: Enable buying from farmers (default: enabled)
- **Sell Enable**: Allow company to sell stocks (requires buyer setup)
- **Only Connect**: Skips syncing (used for Connect-specific companies)
- **Allow Multiple Login**: Enables multiple device logins
- **Make Farmer Private**: Hides farmer names from open APIs

For sell enabled companies buyers should be mapped.
- **Is Default**: Is the company the default buyer

<img src="/images/admin/add_company_buyer.png"/>

---

## Create a User

1. Navigate to **Accounts → Base User**
2. Click **“Add Base User”**.
3. Fill in the fields and save.

<img src="/images/admin/add_base_user.png" alt="Add User" />

4. Now, fill other fields and save.

<img src="/images/admin/user_creation.png" alt="Add User" />


Note: Set the username and email address as the email.

---

## Map User to Company

1. Navigate to **Supply-Chains → Company Members**
2. Click **“Add Company Member”**.
3. Select the user, company and user type accordingly
4. Save the mapping.

<img src="/images/admin/add_company_member.png" alt="Add Member" />

---

## Add a Product

1. Navigate to **Catalogs → Product**
2. Click **“Add Product”**.

<img src="/images/admin/add_product.png" alt="Add Product" />

3. Fill in the detials and save

---

## Add a Product to Company

1. Navigate to **Supply-Chains → Companies**
2. Select the company which you want to edit.
3. Click on Add company product and select the product

<img src="/images/admin/add_company_product.png" alt="Add Company Product" />

4. Save changes.

- In order to hide product Tick "Is Company Product Active" to make the product invisible in the App.

<img src="/images/admin/product_active.png"/>


---

## Add a Premium

1. Navigate to **Catalogs → Premiums**
2. Click **“Add Premium”**.

<img src="/images/admin/add_premium.png"/>

3. Fill in the fields and save.

- **Premium Type**
  - `Per Transaction`: The premium is applied once for each transaction, regardless of the quantity involved.
  - `Per KG`: The premium is calculated based on the weight of the product in kilograms.
  - `Per Unit Currency`: The premium is a percentage or fixed amount relative to the total value of the transaction (based on the currency).
  - `Per Farmer`: The premium is applied once for each farmer involved, regardless of how much they produce.
- **Applicable Activity**
  - `Buy`: Applies only when buying
  - `Sell`: Applies only when selling
- **Premium Category**
  - `Transaction Premium`: Related to transactions
  - `Payout Premium`: For payments only
- **Calculation Type**
  - `Normal`: Used for product premiums, entered manually
  - `Manual`: Entered manually
  - `Options (Dropdown)`: Uses predefined options
  - `Ranges`: Uses value ranges

---

## Add product premium

1. Navigate to **Supply-Chains → Companies**
2. Add or edit the relevant **Company Product**.

<img src="/images/admin/add_company_product.png"/>

3. Add or map **Premiums** (e.g., *Kualitas Premium* mapped with *Black Pepper*).
4. Save changes.

---

## Add Custom Forms 

1. Navigate to **Forms → Forms**
2. Click **“Add Form”**.
3. Select **Form Type**:
   - `Transactions`: For transaction creation
   - `Farmer`: For farmer registration
   - `Payment`: Shown during payment
   - `Product`: Shown when specific products are used (must be added in Company Product)

<img src="/images/admin/add_form.png"/>

4. Add **Form Fields** (types, dropdowns, etc.)

<img src="/images/admin/add_form_field.png"/>

5. Optionally configure **Form Field Configs** to control frontend visibility and behavior.

<img src="/images/admin/add_form_field_config.png"/>

6. Save the form.

--- 