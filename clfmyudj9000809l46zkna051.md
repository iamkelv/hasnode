---
title: "Mastering Asynchronous Workflows with Redux Toolkit and Thunk Actions"
seoTitle: "Async Redux Toolkit & Thunk Actions"
seoDescription: "Simplify Redux store logic with Redux Toolkit and Thunk Actions. Optimize state management with a simplified API"
datePublished: Fri Mar 24 2023 19:59:21 GMT+0000 (Coordinated Universal Time)
cuid: clfmyudj9000809l46zkna051
slug: mastering-asynchronous-workflows-with-redux-toolkit-and-thunk-actions
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/SyvsTmuuZyM/upload/4a60f8c4b23f4bb0af4ed7e6bdc496dd.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1679690453632/a10dd83e-8b2c-4653-b2a4-aa37d4ca2a44.jpeg
tags: javascript, reactjs, redux, redux-toolkit, thunk-actions

---

### Introduction 🎯

Learn how to simplify the process of writing and managing complex asynchronous logic in your Redux store with Redux Toolkit. This popular library from the Redux team provides a simplified API for handling asynchronous workflows, including the ability to dispatch Thunk Actions.

In this article, we'll walk through an example of using Thunk Actions with Redux Toolkit to fetch data from an API and display it on the screen. Follow along and see how you can efficiently manage the state of your application in a predictable and scalable way.

### Prerequisites 🎯

1. Setting up a react application.
    
2. How to install and setup redux-toolkit
    
3. Have basic knowledge of redux-toolkit.
    
4. Basic knowledge of javascript will be good.
    

Redux is a popular state management library for JavaScript applications. It allows developers to manage the state of their applications in a predictable and scalable way. One of the key features of Redux is the ability to dispatch asynchronous actions using middleware, such as the `redux-thunk` middleware.

However, writing and managing complex asynchronous logic with `redux-thunk` can be difficult, especially in larger applications. That's where Redux Toolkit comes in. Redux Toolkit is a new library from the Redux team that provides a simplified API for writing and testing asynchronous logic in your Redux store.

One of the key features of Redux Toolkit is the `createSlice` function, which allows you to easily create and manage your Redux store state and actions. In addition to `createSlice`, Redux Toolkit also includes the ability to dispatch Thunk Actions, which allows you to write asynchronous logic in your actions.

Let's look at an example to see how we can use Thunk Actions with Redux Toolkit to handle a complex asynchronous workflow in our application.

## **Example: Fetching Data from an API**

Suppose we have a React application that needs to fetch products from an API and display it on the screen. With Redux Toolkit, you can write a Thunk Action to handle this process and dispatch it from your component.

In this article, we will be using the [dummyjson](https://dummyjson.com/products) API for better understanding.😊

Here's an example of how we might write a Thunk Action to fetch products from our API:

```javascript
import { createSlice, createAsyncThunk } from '@reduxjs/toolkit';
import axios from 'axios';

export const fetchData = createAsyncThunk(
  'fetchData',
  async () => {
    const response = await axios.get('https://dummyjson.com/products');
    return response.products;
  }
);

const productSlice = createSlice({
  name: 'products',
  initialState: {
    products: [],
    loading: false,
    error: null,
  },
  reducers: {},
  extraReducers: {
    [fetchData.pending]: (state) => {
      state.loading = true;
    },
    [fetchData.fulfilled]: (state, action) => {
      state.data = action.payload;
      state.loading = false;
      state.error = null;
    },
    [fetchData.rejected]: (state, action) => {
      state.loading = false;
      state.error = action.error;
    },
  },
});

export const { } = productSlice.actions;
export default productSlice.reducer;
```

In this example, we use the `createAsyncThunk` function from Redux Toolkit to create an asynchronous Thunk Action. The first argument to `createAsyncThunk` is the name of the action, and the second argument is an asynchronous function that returns the data we want to fetch from the API.

We then use the `createSlice` function from Redux Toolkit to create a slice for our data. In the `extraReducers` object, we handle the three possible states of the Thunk Action: `pending`, `fulfilled`, and `rejected`.

With this setup, we can dispatch the `fetchData` Thunk Action from our component using the `useDispatch` hook from the `react-redux` library:

```javascript
import React, { useEffect } from 'react';
import { useDispatch, useSelector } from 'react-redux';
import { fetchData } from './dataSlice';

const DataList = () => {
  const dispatch = useDispatch();
  const { products, loading, error } = useSelector((state) => state.products);

  useEffect(() => {
    dispatch(fetchData());
  }, [dispatch]);

  if (loading) {
    return <div>Loading...</div>;
  }

  if (error) {
    return <div>Error: {error.message}</div>;
  }

  return (
    <ul>
      {products.map((product) => (
        <li key={product.id}>{product.title}</li>
      ))}
    </ul>
  );
};

export default ProductList;
```

In this example, we use the `useDispatch` hook to get the `dispatch` function from the Redux store. We then use the `useEffect` hook to dispatch the `fetchData` Thunk Action when the component is mounted.

We also use the `useSelector` hook from the `react-redux` library to get the data, loading, and error state from the Redux store.

Finally, we render the component based on the state of the data fetch. If the data is loading, we display a "Loading..." message. If there is an error, we display the error message. If the data was successfully fetched, we display a list of the data.

## **Conclusion 🎯**

In this article, we learned how to use Thunk Actions with Redux Toolkit to handle complex asynchronous workflows in our Redux store. With Redux Toolkit, we can write asynchronous logic in our actions and efficiently manage the state of our application in a predictable and scalable way.

Isn't it simple?🤗 Let me know what you think.

Try it out in your own projects and see the difference it can make!

I hope you find these resources helpful 😊

I'd love to connect with you on [**Twitter**](https://twitter.com/iam_kelvinjnr) | [**LinkedIn**](https://www.linkedin.com/in/iamkelv/) | [**GitHub**](https://github.com/iamkelv)

See you in my next blog article. Take care!!!

### Resources

* [Redux-toolkit documentation](https://redux-toolkit.js.org/rtk-query/usage/migrating-to-rtk-query#thunk-action-creator)
    
* [Dummyjson](https://dummyjson.com/)
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1679660533425/e6e64a37-712a-438e-a220-5dbfc4b55299.gif align="center")