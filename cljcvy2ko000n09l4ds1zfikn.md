---
title: "BudPay Integration: The Easy Way to Accept Payments on Your Next JS App"
seoTitle: "BudPay Integration Guide: Accept Payments Securely on Your Next.js App"
seoDescription: "Integrate BudPay: Securely accept payments on your Next.js app. Streamline the process, and enhance UX. Step-by-step guide for seamless payment integration."
datePublished: Mon Jun 26 2023 13:19:22 GMT+0000 (Coordinated Universal Time)
cuid: cljcvy2ko000n09l4ds1zfikn
slug: budpay-integration-the-easy-way-to-accept-payments-on-your-next-js-app
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1687392203542/32aba7be-c471-4f81-89b3-4fd04f083611.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1687392316034/f52289fa-ef3f-48ea-96df-473e47432531.png
tags: integration, payment

---

### Introduction

[**BudPay**](https://www.budpay.io/) is a powerful payment gateway that provides a simple and secure way to accept payments in your web applications. In this tutorial, I will walk you through the process of integrating BudPay into your Next.js application, allowing you to easily accept payments from your users. By following the steps below, you'll be able to seamlessly integrate BudPay into your Next js app and start accepting payments quickly and efficiently.

### Prerequisites:

Before getting started, make sure you have the following in place:

1. A BudPay account. This is necessary to integrate BudPay into your app or website. You can create one at [Budpay.com](https://budpay.com)
    
2. Basic knowledge of Next js and JavaScript.
    
3. Nodejs is installed on your machine.
    

### **Step 1: Create a Next.js Application**

To begin, let's create a new Next.js application. Open your terminal and run the following commands:

```bash
npx create-next-app budpay-integration
cd budpay-integration
```

This will create a new Next.js project and navigate you into the project directory.

### **Step 2:** BudPay React Js Library

Next, we need to install the necessary dependencies for integrating BudPay. Run the following command to install the `budpay` package:

```bash
npm i budpay-react-v2
```

* `npm install` is the command to install Node.js packages and their dependencies.
    
* `budpay-react-v2` is the package name for the BudPay integration library.
    

By running this command, npm will download the BudPay package from the npm registry and install it into your project.

After running the command, npm will automatically download and install the BudPay package and its dependencies. Once the installation process is complete, you can proceed with the next steps of the integration process.

### **Step 3: Create a BudPay Account**

If you haven't already, head over to the [**BudPay website**](https://budpay.com/) and create an account. Once you've signed up and logged in, you'll be able to retrieve your BudPay API credentials in the account setting as shown below.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687391660916/dd6e2e62-18bc-4556-adaa-328f2a7da7b6.png align="center")

This will generate a secret key for you which we will be using later in this article.

### **Step 4: Initialize BudPay**

To use BudPay in your Next.js application, you need to initialize it with the API credentials that we generated in our previous step. we will be importing the `BudPayButton` and `closeBudPayPaymentModal` components from the **budpay-react-v2** package that was installed earlier by adding the code below:

```javascript
import { BudPayButton, closeBudPayPaymentModal } from 'budpay-react-v2'
```

After importing the `BudPayButton` and `closeBudPayPaymentModal` from your Budpay package, you can create a configuration object that will hold the payment information by adding the code below:

```javascript
const config = {
  api_key: 'sk_live_*******************', 
  reference: '', 
  email: 'test@test.com',
  amount: '1000',
  first_name: 'Kelvin',
  last_name: 'Moses',
  currency: 'NGN', 
};
```

* **api\_key**: This is your secret key obtained from BudPay. It is a unique identifier that authorizes your requests to the BudPay API. Make sure to replace **'sk\_live\_\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*'** with the actual secret key that you generated from your BudPay account.
    
* **reference**: This property represents a reference or identifier for the payment. You can generate a unique reference yourself and replace the empty string `''` with it. Alternatively, if you leave it empty, the BudPay API will generate a reference for you.
    
* **email**: This property represents the email address of the customer making the payment. It should be set to the customer's email address for communication and transaction purposes.
    
* **amount**: This property represents the amount of the payment. It specifies the value of the transaction in the specified currency. The value `'100'` represents 100 units of the specified currency.
    
* **first\_name**: This property represents the first name of the customer making the payment. It should be set to the customer's first name.
    
* **last\_name**: This property represents the last name of the customer making the payment. It should be set to the customer's last name.
    
* **currency**: This property specifies the currency in which the payment is made. The value `'NGN'` represents the Nigerian Naira. You can change it to `'GHS'` for Ghana Cedis or `'USD'` for US Dollars, depending on your desired currency.
    

By populating these properties with the appropriate values, you can create a configuration object that provides the necessary details for making a payment request to BudPay. Once you have this configuration set up, you can pass it as an argument when making a payment request using the BudPay API.

### **Step 5: Populating our Configuration Object with Dynamic Data with useState Hook**

```javascript
import React, { useRef, useState } from 'react'
import { Inter } from 'next/font/google'
const inter = Inter({ subsets: ['latin'] })

import { BudPayButton, closeBudPayPaymentModal } from 'budpay-react-v2'

export default function Home() {
  const [email, setEmail] = useState()
  const [amount, setAmount] = useState()
  const [firstName, setFirstName] = useState()
  const [last_name, setLastName] = useState()
  const [currency, setCurrency] = useState()


 return (
    <main></main>
}
```

In the provided above code, there are several `useState` hooks used to create state variables and their corresponding setter functions. Each state variable represents a piece of data captured from the user input. Here's an explanation of the code:

* The `useState` hook is used to create state variables and their setter functions. The initial value for each state variable is `undefined` because no initial value is provided in the `useState` calls.
    

Each state variable is paired with its corresponding setter function (`setEmail`, `setAmount`, `setFirstName`, `setLastName`, and `setCurrency`). These setter functions are used to update the values of the state variables later on.

The `config` object is then defined using these state variables to populate its properties:

```javascript
import React, { useRef, useState } from 'react'
import { Inter } from 'next/font/google'
const inter = Inter({ subsets: ['latin'] })

import { BudPayButton, closeBudPayPaymentModal } from 'budpay-react-v2'

export default function Home() {
  const [email, setEmail] = useState()
  const [amount, setAmount] = useState()
  const [firstName, setFirstName] = useState()
  const [last_name, setLastName] = useState()
  const [currency, setCurrency] = useState()

const config = {
  api_key: 'sk_test_*******************************', 
  reference: '', 
  email: email,
  amount: amount,
  first_name: firstName,
  last_name: last_name,
  currency: currency,
};

 return (
    <main></main>
}
```

### **Step 6: Create a Payment Form**

Now let's create a simple payment form component. inside the **Home** component and add the following code in our return main container:

```javascript
import React, { useRef, useState } from 'react'
import { Inter } from 'next/font/google'
const inter = Inter({ subsets: ['latin'] })

import { BudPayButton, closeBudPayPaymentModal } from 'budpay-react-v2'

export default function Home() {
  const [email, setEmail] = useState()
  const [amount, setAmount] = useState()
  const [firstName, setFirstName] = useState()
  const [last_name, setLastName] = useState()
  const [currency, setCurrency] = useState()

  const config = {
    api_key: 'sk_test_*****************************************',
    reference: '', 
    email: email,
    amount: amount,
    first_name: firstName,
    last_name: last_name,
    currency: currency, 
  }

  return (
    <main
      className={`flex min-h-screen flex-col items-center justify-between p-24 ${inter.className}`}
    >
      <div>
        <h1>PayForm</h1>
        <form className="flex flex-col" onSubmit={(e) => e.preventDefault()}>
          <label htmlFor="email">Email</label>
          <input
            type="email"
            onChange={(e) => setEmail(e.target.value)}
            name="email"
            id="email"
          />
          <label htmlFor="amount">Amount</label>
          <input
            type="number"
            name="amount"
            id="amount"
            onChange={(e) => setAmount(e.target.value)}
          />
          <label htmlFor="first_name">First Name</label>
          <input
            type="text"
            name="first_name"
            id="first_name"
            onChange={(e) => setFirstName(e.target.value)}
          />
          <label htmlFor="last_name">Last Name</label>
          <input
            type="text"
            name="last_name"
            id="last_name"
            onChange={(e) => setLastName(e.target.value)}
          />
          <label htmlFor="currency">Currency</label>
          <select
            name="current"
            id="currency"
            onChange={(e) => setCurrency(e.target.value)}
          >
            <option value="NGN" key="NGN">
              NGN
            </option>
            <option value="GHS" key="GHS">
              GHS
            </option>
            <option value="USD" key="USD">
              USD
            </option>
          </select>
        </form>
      </div>
    </main>
  )
}
```

We have just added a payment form and another thing that is remaining is creating our budPay Configuration object by adding the code below:

```javascript
const budPayConfig = {
  ...config,
  text: 'Pay with BudPay',
  btnSize: 'medium', // small, medium, large
  callback_url: 'localhost:3000',
  callback: function (response) {
    closeBudPayPaymentModal() // this will close the modal programmatically
    // this happens after the payment is completed successfully if callback_url is not provided
    alert(
      'Payment complete! Reference: ' +
        response.reference +
        ', Status: ' +
        response.status,
    );
  },
  onClose: function (response) {
    console.log(response);
    alert('Transaction was not completed, window closed.');
  },
};
```

* **budPayConfig:** is an extended configuration object that includes the properties from the `config` object as well as additional properties specific to BudPay integration.
    
* **...config:** spreads the properties of the `config` object into the `budPayConfig` object, allowing it to inherit the same properties for BudPay integration.
    
* **text:** represents the text to be displayed on the BudPay payment button. In this case, it is set to `'Pay with BudPay'`.
    
* **btnSize:** determines the size of the BudPay payment button. It can be set to `'small'`, `'medium'`, or `'large'`.
    
* **callback\_url:** specifies the URL that BudPay should redirect to after the payment is completed successfully. In this example, it is set to localhost:3000.
    
* **callback:** This is a callback function that will be called after the payment is completed successfully. It receives a `response` object containing information about the payment, such as the reference and status. In this example, the function calls `closeBudPayPaymentModal()` which we imported from the **budpay-react-v2** package to close the payment modal programmatically and displays an alert with the payment details.
    
* **onClose:** This is a callback function that will be called if the BudPay payment window is closed before the payment is completed. It receives a `response` object and in this example, logs the response to the console and displays an alert indicating that the transaction was not completed.
    

### Step 7: Adding BudPay Pay Button

We have now created our form and configuration objects. Now what is left is to add a buy button to the payment form so that users can use it to trigger the BudPay Modal.

The BudPayButton component that we imported from **budpay-react-v2'** allow us to use the buy button and pass our budPayConfig object as a prop.

```javascript
 <BudPayButton {...budPayConfig} />
```

The code `<BudPayButton {...budPayConfig} />` is how you can use the `budPayConfig` object to configure and render a BudPay payment button component.

In this case, `BudPayButton` is a component that accepts props to configure and render the BudPay payment button. The spread operator `{...budPayConfig}` is used to pass all the properties from the `budPayConfig` object as props to the `BudPayButton` component.

By passing the `budPayConfig` object as props to the `BudPayButton` component, you are providing all the necessary configuration options for the BudPay integration, including the API key, payment details, button text, button size, callbacks, and more. The `BudPayButton` component will then handle the rendering and functionality of the BudPay payment button based on the provided configuration.

```javascript
import React, { useRef, useState } from 'react'
import { Inter } from 'next/font/google'
const inter = Inter({ subsets: ['latin'] })

import { BudPayButton, closeBudPayPaymentModal } from 'budpay-react-v2'

export default function Home() {
  const [email, setEmail] = useState()
  const [amount, setAmount] = useState()
  const [firstName, setFirstName] = useState()
  const [last_name, setLastName] = useState()
  const [currency, setCurrency] = useState()

  const config = {
    api_key: 'sk_test_********************************', // Replace with your secret key
    reference: '', 
    email: email,
    amount: amount,
    first_name: firstName,
    last_name: last_name,
    currency: currency,
  }

  const budPayConfig = {
    ...config,
    text: 'Pay with BudPay',
    btnSize: 'medium', 
    callback_url: 'localhost:3000',
    callback: function (response) {
      closeBudPayPaymentModal() 
      alert(
        'Payment complete! Reference: ' +
          response.reference +
          ', Status: ' +
          response.status,
      )
    },
    onClose: function (response) {
      console.log(response)
      alert('Transaction was not completed, window closed.')
    },
  }

  return (
    <main
      className={`flex min-h-screen flex-col items-center justify-between p-24 ${inter.className}`}
    >
      <div>
        <h1>PayForm</h1>
        <form className="flex flex-col" onSubmit={(e) => e.preventDefault()}>
          <label htmlFor="email">Email</label>
          <input
            type="email"
            onChange={(e) => setEmail(e.target.value)}
            name="email"
            id="email"
          />
          <label htmlFor="amount">Amount</label>
          <input
            type="number"
            name="amount"
            id="amount"
            onChange={(e) => setAmount(e.target.value)}
          />
          <label htmlFor="first_name">First Name</label>
          <input
            type="text"
            name="first_name"
            id="first_name"
            onChange={(e) => setFirstName(e.target.value)}
          />
          <label htmlFor="last_name">Last Name</label>
          <input
            type="text"
            name="last_name"
            id="last_name"
            onChange={(e) => setLastName(e.target.value)}
          />
          <label htmlFor="currency">Currency</label>
          <select
            name="current"
            id="currency"
            onChange={(e) => setCurrency(e.target.value)}
          >
            <option value="NGN" key="NGN">
              NGN
            </option>
            <option value="GHS" key="GHS">
              GHS
            </option>
            <option value="USD" key="USD">
              USD
            </option>
          </select>

          <BudPayButton {...budPayConfig} />
        </form>
      </div>
    </main>
  )
}
```

### Conclusion

In this article, we learned how to seamlessly integrate BudPay, a payment gateway, into a Next.js application. By following a few simple steps, we set up a form to capture user input and configured BudPay with the necessary API key and payment details. We then rendered the BudPay payment button component, allowing users to make payments easily.

Integrating BudPay into your Next.js app provides a secure and efficient way to accept payments. Whether you're running an e-commerce store or offering subscription-based services, BudPay simplifies the payment process, enabling a seamless user experience.

Congratulations! You have just integrated BudPay into your Next js App. 😊.

You can view the source code [**here**](https://github.com/iamkelv/budpay-integration)

Hope you have learned a lot from this article 😊😊

I'd love to connect with you on [**Twitter**](https://twitter.com/iam_kelvinjnr) | [**LinkedIn**](https://www.linkedin.com/in/iamkelv/) | [**GitHub**](https://github.com/iamkelv)

# Resources

[Next JS Official Documentation](http://nextjs.org/)

[BudPay Developers Documentation](https://devs.budpay.com/api)