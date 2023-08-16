---
title: "Demystifying Server-Side Rendering in Next JS: A Beginner's Guide"
seoDescription: "Demystify Server-Side Rendering in Next JS: A Beginner's Guide to unlock web development potential."
datePublished: Thu Jul 06 2023 21:02:20 GMT+0000 (Coordinated Universal Time)
cuid: cljrmvyrk000509mlc2s44cf6
slug: demystifying-server-side-rendering-in-next-js-a-beginners-guide
canonical: https://dev.to/iamkelv/demystifying-server-side-rendering-in-next-js-a-beginners-guide-55lh
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1688047130419/adf2f1a5-af08-44bf-bae2-e991974dbf96.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1688047381021/ffa121fd-55f8-4684-9d77-c96c2fdd565c.png
tags: javascript, server-side-rendering, nextjs

---

Server-side rendering (SSR) plays a vital role in modern web development, providing enhanced performance, search engine optimization (SEO), and improved user experience. Next.js, a popular React framework, simplifies the implementation of SSR. 

Before server-side rendering, frontend development relied primarily on client-side rendering (CSR) techniques. This involved loading initial HTML from the server and using JavaScript on the client-side (browser) for subsequent interactions and content updates. Single-page applications (SPAs) like React, Angular, and Vue.js became popular, providing dynamic user experiences without full page reloads. Progressive enhancement and pre-rendering were also used. However, SSR emerged as a solution to improve performance, SEO, and user experience by pre-rendering content on the server and delivering optimized initial page loads. SSR combines the benefits of server-side and client-side rendering for enhanced frontend development.

Sever-Side rendering excites fronted developers by offering faster page loads, improved SEO, and increased security.

This article explains server-side rendering in Next.js for beginners by taking the reader through the concept and how server-side rendering is implemented in Next.js app.

### **Introduction to Next.js**

Next.js is a React framework that gives you building blocks to create web applications.

By framework, it means Next.js handles the tooling and configuration needed for React and provides additional architecture, features, and optimization.

Next.js gives you all the features of React to build your UI and provides features such as routing, data fetching, client-side (CSR), and server-side rendering (SSR) for a better developer and end-user experience.

Next.js provides a straightforward project structure, with the key files and directories being:

* **pages**: Contains the pages of your application. Each JavaScript file inside this directory represents a unique route.
    
* **public**: Stores static assets such as images, stylesheets, and fonts.
    
* **components**: Holds reusable React components.
    

### GitHub

The project's GitHub repository can be found [here](https://github.com/iamkelv/server-rendering-article).

### **Prerequisites**

Before getting started, you must have the following prerequisites:

* Basic knowledge of HTML, CSS, and JavaScript.
    
* Familiarity with React.
    
* Understanding of frontend development concepts.
    
* Familiarity with Node.js and npm.
    
* IDE or text editor for coding.
    

### **Setting Up a Next.js Project**

To get started with Next.js, follow these steps:

1. Install [Node.js](https://nodejs.org/en) and npm (Node Package Manager) if you haven't already.
    
2. Open your terminal and run the following command to install the Next.js CLI globally: npm install create-next-app.
    
3. Create a new Next.js project by executing npx create-next-app my-next-app in your desired project directory.
    
4. Once the project is created, navigate to the project directory using cd my-next-app or the name you choose to give your project directory.
    
5. Start the development server with the command npm run dev.
    
6. Open your browser and visit [http://localhost:3000](http://localhost:3000) to see your Next.js application running.
    

### **Understanding Server Side Rendering (SSR)**

Server-side rendering involves generating HTML on the server and sending it to the client (browser). Unlike client-side rendering (CSR), where HTML is generated in the browser, SSR offers several advantages, such as improved page load times, SEO friendliness, and better initial rendering which equally provide a better user experience.

### **Creating Pages with Server-Side Rendering**

Let's create a basic page that utilizes server-side rendering in Next.js. Follow these steps:

1. Inside the **pages** directory, create a new JavaScript file called **users.js**.
    
2. In **users.js**, define a functional React component representing the Users page.
    

```javascript
import React from 'react';

const Users = ({ users }) => {
  return (
    <div>
      <h1>Users</h1>
      <ul>
        {users.map((user) => (
          <li key={user.id}>{user.name}</li>
        ))}
      </ul>
    </div>
  );
};

export async function getServerSideProps() {
  // Fetch data from jsonplaceholder API 
  const response = await fetch('https://jsonplaceholder.typicode.com/users');
  const users = await response.json();
  return {
    props: {
      users,
    },
  };
}
export default Users;
```

In the code above, you define the **Users** component that renders a list of users fetched from the [jsonplaceholder](https://jsonplaceholder.typicode.com/) API.

The `getServerSideProps`  function allows you to bring data on the server side and pass it as props to your page component. It runs on every request made to the page, making it suitable for dynamic data that needs to be fetched at runtime. The getServerSideProps function takes an object as an argument with the following properties:

**context**: The `context` object contains information about the current request, such as the request parameters `context.params`, query parameters `context.query`, and the HTTP request `context.req` and response context.res objects.

* **params**: The params property within the context object contains the dynamic route parameters specified in the page's filename. For example, if you have a dynamic page with the filename **\[userId\].js**, the corresponding value of params would contain the actual userId value from the URL.
    
* **query**: The query property within the context object contains the query parameters passed in the URL. For example, if the URL is **/user?id=1**, `context.query` would be `{ id: '1' }`.
    

The getServerSideProps function should be defined as an async function that returns an object with the following properties:

* **props**: The props property is an object that contains the data you want to pass to your page component. The data can be fetched from an API, a database, or any other data source. The props object will be serialized and sent to the client.
    
* **revalidate**: The revalidate property is optional and determines how frequently Next.js should re-generate the page on the server. It specifies the number of seconds after which a new request will trigger a re-rendering of the page. This is useful for pages that have data that frequently changes. For example, revalidate: 10 will regenerate the page every 10 seconds to make sure the page is up to date.
    
* The **getServerSideProps** function asynchronous enables efficient handling of data fetching operations during server-side rendering in Next.js, ensuring that the server remains responsive and can handle multiple requests concurrently.
    

Run the Next.js development server with npm run dev and visit [http://localhost:3000/users](http://localhost:3000/users). You should see the Users page with the list of users rendered on the server.

### **Handling Dynamic Routes**

Next.js provides an intuitive way to handle dynamic routes. Here's an example of creating dynamic routes and fetching data for those routes:

1. Create a new file called **\[userId\].js** inside the page's directory.
    
2. In **\[userId\].js**, define a functional React component representing the dynamic route.
    

```javascript
import React from 'react';

const Post = ({ user }) => {
  return (
    <div>
      <h1>{user.title}</h1>
      <p>{user.body}</p>
    </div>
  );
};

export async function getServerSideProps({ params }) {
  const response = await fetch(`https://jsonplaceholder.typicode.com/users/${params.userId}`);
  const user= await response.json();
  return {
    props: {
      user,
    },
  };
}
export default Post;
```

![](https://paper-attachments.dropboxusercontent.com/s_66E3C48CB4B2E3CF1527CF02EE5C5C61DE4AFB2126819700BCA222A581A14145_1688496136734_2.gif align="left")

In this example, you create a dynamic route that fetches a specific user based on the userId parameter passed in the URL. The fetched user is then rendered on the server side.

### **Conclusion**

Server-side rendering is a powerful technique that enhances the performance and SEO of web applications. Next.js simplifies the implementation of server-side rendering by providing a seamless development experience. In this beginner's guide, you explored the basics of server-side rendering in Next.js, including setting up a project, creating pages with server-side rendering, implementing pre-rendering and caching, and handling dynamic routes.

You can view the source code [**here**](https://github.com/iamkelv/server-rendering-article)

I hope you have learned a lot from this article. Feel free to drop your comments 😊

I'd love to connect with you on [**Twitter**](https://twitter.com/iam_kelvinjnr) | [**LinkedIn**](https://www.linkedin.com/in/iamkelv/) | [**GitHub**](https://github.com/iamkelv)

# Resources

[**Next JS Official Documentation**](http://nextjs.org/)

[Jsonplaceholder API Documentation](https://jsonplaceholder.typicode.com/)