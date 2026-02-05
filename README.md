# REACT TUTORIAL 
class curriculum for coding temple

## 1. React Setup, JSX, Components & Props Tutorial
=============================================

Introduction
------------

Welcome to your first React tutorial! In this comprehensive guide, you'll learn the fundamentals of React development, including setting up your development environment, understanding JSX syntax, and creating reusable components with props. By the end of this tutorial, you'll have a solid foundation in React that will prepare you for building interactive web applications.

What you'll learn:

-   How to set up a React development environment with Vite
-   Understanding JSX syntax and its rules
-   Creating functional components
-   Passing and using props effectively
-   Component composition patterns
-   Best practices for React development

Why this matters:\
React is one of the most popular JavaScript libraries for building user interfaces. It's used by companies like Facebook, Netflix, Airbnb, and many others. Learning React will give you the skills to build modern, interactive web applications and prepare you for a career in frontend or full-stack development.

Concepts Overview
-----------------

### What is React?

React is a JavaScript library for building user interfaces, particularly web applications. It was created by Facebook (now Meta) in 2013 and has become the industry standard for frontend development.

Key characteristics of React:

-   Component-based: UI is built using reusable components
-   Declarative: You describe what the UI should look like, and React handles the how
-   Virtual DOM: React uses a virtual representation of the DOM for efficient updates
-   One-way data flow: Data flows down from parent to child components
-   JSX: A syntax extension that allows you to write HTML-like code in JavaScript

### Why Use React?

1.  Reusability: Components can be reused across your application
2.  Maintainability: Code is organized into logical, manageable pieces
3.  Performance: Virtual DOM makes updates efficient
4.  Ecosystem: Huge community and extensive third-party libraries
5.  Industry Standard: Most companies use React for frontend development
6.  Full-stack Ready: Works well with backend technologies like Flask

### Development Environment Setup

#### Node.js and npm

React applications require Node.js, a JavaScript runtime environment. Node.js comes with npm (Node Package Manager), which we use to install and manage dependencies.

Installation:

1.  Visit [nodejs.org](https://nodejs.org/)
2.  Download the LTS (Long Term Support) version
3.  Run the installer and follow the setup wizard
4.  Verify installation:
```bash
node --version
npm --version
```

#### Vite vs Create React App

We're using Vite instead of Create React App because:

-   Faster: Uses native ES modules and faster bundling
-   Modern: Built with modern tools and practices
-   Better DX: Improved developer experience
-   Smaller: Smaller bundle sizes

Creating a new React project with Vite:

```bash
npm create vite@latest my-app-name --  --template react
cd my-app-name
npm install
npm run dev
```

Code Examples
-------------

### Basic React Component

Here's a simple React component:

```jsx
// Greeting.jsx\
function  Greeting({ name })  {
return  <h1>Hello,  {name}!</h1>;
}

export  default Greeting;
```


Key points:

-   Function name starts with capital letter (PascalCase)
-   Returns JSX (HTML-like syntax)
-   Accepts props as function parameters
-   Must be exported to use elsewhere

### JSX Fundamentals

JSX (JavaScript XML) is a syntax extension that allows you to write HTML-like code in JavaScript.

#### Basic JSX Syntax

`function  App()  {\
const title =  "Welcome to React";\
const isLoggedIn =  true;

return  (\
<div className="app">\
<h1>{title}</h1>\
{isLoggedIn &&  <p>You are logged in!</p>}\
<button onClick={()  =>  alert('Hello!')}>\
Click me\
</button>\
</div>\
);\
}

`

#### JSX Rules

1.  Single Parent Element: JSX must return a single parent element`// ❌ Wrong - multiple elements\
    return  (\
    <h1>Title</h1>\
    <p>Description</p>\
    );

    // ✅ Correct - wrapped in div\
    return  (\
    <div>\
    <h1>Title</h1>\
    <p>Description</p>\
    </div>\
    );

    // ✅ Correct - using React Fragment\
    return  (\
    <>\
    <h1>Title</h1>\
    <p>Description</p>\
    </>\
    );

    `
2.  Use className instead of class:`// ❌ Wrong\
    <div class="container">

    // ✅ Correct\
    <div className="container">

    `
3.  Self-closing tags must have a slash:`// ❌ Wrong\
    <img src="image.jpg">

    // ✅ Correct\
    <img src="image.jpg"  />

    `
4.  JavaScript expressions in curly braces:`const name =  "Dylan";\
    const age =  25;

    return  (\
    <div>\
    <p>Name:  {name}</p>\
    <p>Age:  {age}</p>\
    <p>Next year:  {age +  1}</p>\
    </div>\
    );

    `

### Props in React

Props (short for properties) are how you pass data from parent to child components.

#### Basic Props Usage

`// Card.jsx - Child component\
function  Card({ title, description, image })  {\
return  (\
<div className="card">\
<img src={image} alt={title}  />\
<h3>{title}</h3>\
<p>{description}</p>\
</div>\
);\
}

// App.jsx - Parent component\
function  App()  {\
return  (\
<div>\
<Card\
title="React Tutorial"\
description="Learn React fundamentals"\
image="https://via.placeholder.com/300x200"\
/>\
<Card\
title="JavaScript Basics"\
description="Master JavaScript concepts"\
image="https://via.placeholder.com/300x200"\
/>\
</div>\
);\
}

`

#### Props with Default Values

`function  Button({ text, color =  "blue", size =  "medium"  })  {\
return  (\
<button\
className={`btn btn-${color} btn-${size}`}\
>\
{text}\
</button>\
);\
}

// Usage\
<Button text="Click me"  />\
<Button text="Submit" color="green" size="large"  />

`

#### Props with Objects and Arrays

`function  UserProfile({ user, skills, isOnline })  {\
return  (\
<div className="profile">\
<img src={user.avatar} alt={user.name}  />\
<h2>{user.name}</h2>\
<p>{user.email}</p>\
{isOnline &&  <span className="online-indicator">Online</span>}

<div className="skills">\
<h3>Skills:</h3>\
<ul>\
{skills.map((skill, index)  =>  (\
<li key={index}>{skill}</li>\
))}\
</ul>\
</div>\
</div>\
);\
}

// Usage\
const user =  {\
name:  "Dylan Smith",\
email:  "dylan@example.com",\
avatar:  "https://via.placeholder.com/100x100"\
};

const skills =  ["JavaScript",  "React",  "Python",  "Flask"];

<UserProfile\
user={user}\
skills={skills}\
isOnline={true}\
/>

`

### Component Composition

Component composition is the practice of building complex UIs by combining simple components.

#### Layout Components

`// Header.jsx\
function  Header({ title, navigation })  {\
return  (\
<header className="header">\
<h1>{title}</h1>\
<nav>\
{navigation.map((item, index)  =>  (\
<a key={index} href={item.href}>\
{item.label}\
</a>\
))}\
</nav>\
</header>\
);\
}

// Footer.jsx\
function  Footer({ copyright, year })  {\
return  (\
<footer className="footer">\
<p>&copy;  {year}  {copyright}</p>\
</footer>\
);\
}

// Layout.jsx\
function  Layout({ children, title, navigation, copyright, year })  {\
return  (\
<div className="layout">\
<Header title={title} navigation={navigation}  />\
<main className="main-content">\
{children}\
</main>\
<Footer copyright={copyright} year={year}  />\
</div>\
);\
}

// App.jsx\
function  App()  {\
const navigation =  [\
{  href:  "#home",  label:  "Home"  },\
{  href:  "#about",  label:  "About"  },\
{  href:  "#contact",  label:  "Contact"  }\
];

return  (\
<Layout\
title="My Website"\
navigation={navigation}\
copyright="My Company"\
year="2024"\
>\
<h2>Welcome to my website!</h2>\
<p>This is the main content area.</p>\
</Layout>\
);\
}

`

#### Card Component with Composition

`// Card.jsx\
function  Card({ children, className =  ""  })  {\
return  (\
<div className={`card ${className}`}>\
{children}\
</div>\
);\
}

// CardHeader.jsx\
function  CardHeader({ title, subtitle })  {\
return  (\
<div className="card-header">\
<h3>{title}</h3>\
{subtitle &&  <p className="subtitle">{subtitle}</p>}\
</div>\
);\
}

// CardBody.jsx\
function  CardBody({ children })  {\
return  (\
<div className="card-body">\
{children}\
</div>\
);\
}

// CardFooter.jsx\
function  CardFooter({ children })  {\
return  (\
<div className="card-footer">\
{children}\
</div>\
);\
}

// Usage\
function  App()  {\
return  (\
<Card className="featured">\
<CardHeader\
title="React Tutorial"\
subtitle="Learn the basics"\
/>\
<CardBody>\
<p>This is a comprehensive tutorial on React fundamentals.</p>\
<ul>\
<li>Components</li>\
<li>Props</li>\
<li>JSX</li>\
</ul>\
</CardBody>\
<CardFooter>\
<button>Read More</button>\
<button>Share</button>\
</CardFooter>\
</Card>\
);\
}

`

Practical Exercises
-------------------

### Exercise 1: Basic Component Creation

Create a `Welcome` component that displays a personalized greeting.

Requirements:

-   Accept `name` and `timeOfDay` props
-   Display "Good morning/afternoon/evening, [name]!"
-   Include a welcome message

Solution:

`function  Welcome({ name, timeOfDay })  {\
const greeting =  `Good ${timeOfDay}, ${name}!`;

return  (\
<div className="welcome">\
<h2>{greeting}</h2>\
<p>Welcome to our application!</p>\
</div>\
);\
}

// Usage\
<Welcome name="Dylan" timeOfDay="morning"  />

`

### Exercise 2: Product Card Component

Create a `ProductCard` component for an e-commerce site.

Requirements:

-   Display product name, price, and image
-   Show if product is on sale
-   Include an "Add to Cart" button
-   Handle out-of-stock products

Solution:

`function  ProductCard({\
name,\
price,\
originalPrice,\
image,\
isOnSale,\
inStock\
})  {\
const discount = originalPrice ?\
Math.round(((originalPrice - price)  / originalPrice)  *  100)  :  0;

return  (\
<div className="product-card">\
<img src={image} alt={name}  />\
<h3>{name}</h3>

<div className="price">\
<span className="current-price">${price}</span>\
{isOnSale && originalPrice &&  (\
<>\
<span className="original-price">${originalPrice}</span>\
<span className="discount">{discount}% off</span>\
</>\
)}\
</div>

<button\
disabled={!inStock}\
className={inStock ?  "add-to-cart"  :  "out-of-stock"}\
>\
{inStock ?  "Add to Cart"  :  "Out of Stock"}\
</button>\
</div>\
);\
}

// Usage\
<ProductCard\
name="Wireless Headphones"\
price={99.99}\
originalPrice={149.99}\
image="https://via.placeholder.com/200x200"\
isOnSale={true}\
inStock={true}\
/>

`

### Exercise 3: Navigation Component

Create a `Navigation` component with responsive design.

Requirements:

-   Display navigation items
-   Show active state
-   Include mobile menu toggle
-   Handle click events

Solution:

`function  Navigation({ items, activeItem, onItemClick })  {\
const  [isMobileMenuOpen, setIsMobileMenuOpen]  =  useState(false);

return  (\
<nav className="navigation">\
<div className="nav-brand">\
<h2>My App</h2>\
<button\
className="mobile-menu-toggle"\
onClick={()  =>  setIsMobileMenuOpen(!isMobileMenuOpen)}\
>\
☰\
</button>\
</div>

<ul className={`nav-items ${isMobileMenuOpen ?  'open'  :  ''}`}>\
{items.map((item, index)  =>  (\
<li key={index}>\
<a\
href={item.href}\
className={activeItem === item.label ?  'active'  :  ''}\
onClick={(e)  =>  {\
e.preventDefault();\
onItemClick(item.label);\
}}\
>\
{item.label}\
</a>\
</li>\
))}\
</ul>\
</nav>\
);\
}

// Usage\
const navItems =  [\
{  label:  "Home",  href:  "#home"  },\
{  label:  "About",  href:  "#about"  },\
{  label:  "Services",  href:  "#services"  },\
{  label:  "Contact",  href:  "#contact"  }\
];

<Navigation\
items={navItems}\
activeItem="Home"\
onItemClick={(item)  => console.log(`Clicked: ${item}`)}\
/>

`

Best Practices
--------------

### Component Naming

-   Use PascalCase for component names
-   Use descriptive names that indicate purpose
-   Avoid generic names like "Component" or "Item"

`// ✅ Good\
function  UserProfile()  {  }\
function  ProductCard()  {  }\
function  NavigationMenu()  {  }

// ❌ Bad\
function  component()  {  }\
function  card()  {  }\
function  menu()  {  }

`

### Props Design

-   Use descriptive prop names
-   Provide default values when appropriate
-   Keep props simple and focused
-   Use TypeScript or PropTypes for type checking

`// ✅ Good\
function  Button({ text, variant =  "primary", size =  "medium"  })  {  }

// ❌ Bad\
function  Button({ t, v, s })  {  }

`

### File Organization

-   One component per file
-   Use descriptive file names
-   Group related components in folders
-   Keep components small and focused

`src/\
├── components/\
│ ├── ui/\
│ │ ├── Button.jsx\
│ │ ├── Card.jsx\
│ │ └── Input.jsx\
│ ├── layout/\
│ │ ├── Header.jsx\
│ │ ├── Footer.jsx\
│ │ └── Layout.jsx\
│ └── features/\
│ ├── UserProfile.jsx\
│ └── ProductList.jsx

`

### JSX Best Practices

-   Use meaningful variable names
-   Extract complex logic into separate functions
-   Use conditional rendering appropriately
-   Keep JSX readable and well-formatted

`// ✅ Good\
function  UserList({ users, showOnlineOnly })  {\
const filteredUsers = showOnlineOnly\
? users.filter(user  => user.isOnline)\
: users;

return  (\
<div className="user-list">\
{filteredUsers.map(user  =>  (\
<UserCard key={user.id} user={user}  />\
))}\
</div>\
);\
}

// ❌ Bad\
function  UserList({ u, s })  {\
return  (\
<div>\
{s ? u.filter(x  => x.o).map(x  =>  <div key={x.id}>{x.n}</div>)  : u.map(x  =>  <div key={x.id}>{x.n}</div>)}\
</div>\
);\
}

`

Common Pitfalls
---------------

### 1\. Forgetting to Export Components

`// ❌ Wrong - component not exported\
function  MyComponent()  {\
return  <div>Hello</div>;\
}

// ✅ Correct - component exported\
function  MyComponent()  {\
return  <div>Hello</div>;\
}\
export  default MyComponent;

`

### 2\. Using class instead of className

`// ❌ Wrong\
<div class="container">

// ✅ Correct\
<div className="container">

`

### 3\. Not Providing Keys for Lists

`// ❌ Wrong - missing keys\
{items.map(item  =>  <li>{item.name}</li>)}

// ✅ Correct - with keys\
{items.map(item  =>  <li key={item.id}>{item.name}</li>)}

`

### 4\. Mutating Props

`// ❌ Wrong - mutating props\
function  UserCard({ user })  {\
user.name =  "New Name";  // Don't do this!\
return  <div>{user.name}</div>;\
}

// ✅ Correct - props are read-only\
function  UserCard({ user })  {\
return  <div>{user.name}</div>;\
}

`

### 5\. Not Handling Missing Props

`// ❌ Wrong - could cause errors\
function  UserCard({ user })  {\
return  <div>{user.name.toUpperCase()}</div>;\
}

// ✅ Correct - handle missing props\
function  UserCard({ user })  {\
if  (!user)  return  <div>No user data</div>;\
return  <div>{user.name?.toUpperCase()}</div>;\
}

`

Additional Resources
--------------------

### Official Documentation

-   [React Official Docs](https://react.dev/)
-   [JSX in React](https://react.dev/learn/writing-markup-with-jsx)
-   [Components and Props](https://react.dev/learn/passing-props-to-a-component)

### Learning Resources

-   [React Tutorial](https://react.dev/learn/tutorial-tic-tac-toe)
-   [React Examples](https://react.dev/learn/your-first-component)
-   [Vite Documentation](https://vitejs.dev/)

### Tools and Extensions

-   [React Developer Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi) - Browser extension for debugging
-   [VS Code React Extensions](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-typescript-next) - Better React development experience

### Practice Projects

1.  Personal Portfolio: Build a portfolio website using components
2.  Todo List: Create a simple todo list with components
3.  Weather App: Build a weather display using components
4.  Blog Layout: Create a blog layout with header, content, and sidebar

### Next Steps

After mastering components and props, you'll be ready to learn:

-   State management with `useState`
-   Event handling and user interactions
-   Side effects with `useEffect`
-   Form handling and validation
-   Routing with React Router

Remember: Practice is key to mastering React. Build projects, experiment with different patterns, and don't be afraid to make mistakes. Each error is a learning opportunity!
