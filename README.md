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

Why this matters:
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
// Greeting.jsx
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

```jsx
function  App()  {
const title =  "Welcome to React";
const isLoggedIn =  true;

return  (
<div className="app">
<h1>{title}</h1>
{isLoggedIn &&  <p>You are logged in!</p>}
<button onClick={()  =>  alert('Hello!')}>
Click me
</button>
</div>
);
}

```

#### JSX Rules

1.  Single Parent Element: JSX must return a single parent element

```jsx
❌ Wrong - multiple elements
return  (
<h1>Title</h1>
<p>Description</p>
);

// ✅ Correct - wrapped in div
return  (
<div>
<h1>Title</h1>
<p>Description</p>
</div>
);

// ✅ Correct - using React Fragment
return  (
<>
<h1>Title</h1>
<p>Description</p>
</>
);

```
2.  Use className instead of class:
```jsx
// ❌ Wrong
<div class="container">

// ✅ Correct
<div className="container">

```

3.  Self-closing tags must have a slash:
```jsx
// ❌ Wrong
<img src="image.jpg">

// ✅ Correct
<img src="image.jpg"  />

```
4.  JavaScript expressions in curly braces:
```jsx
const name =  "Dylan";
const age =  25;

return  (
<div>
<p>Name:  {name}</p>
<p>Age:  {age}</p>
<p>Next year:  {age +  1}</p>
</div>
);

```

### Props in React

Props (short for properties) are how you pass data from parent to child components.

#### Basic Props Usage

```jsx
// Card.jsx - Child component
function  Card({ title, description, image })  {
return  (
<div className="card">
<img src={image} alt={title}  />
<h3>{title}</h3>
<p>{description}</p>
</div>
);
}

// App.jsx - Parent component
function  App()  {
return  (
<div>
<Card
title="React Tutorial"
description="Learn React fundamentals"
image="https://via.placeholder.com/300x200"
/>
<Card
title="JavaScript Basics"
description="Master JavaScript concepts"
image="https://via.placeholder.com/300x200"
/>
</div>
);
}

```

#### Props with Default Values

```jsx
function  Button({ text, color =  "blue", size =  "medium"  })  {
return  (
<button
className={```btn btn-${color} btn-${size}```}
>
{text}
</button>
);
}

// Usage
<Button text="Click me"  />
<Button text="Submit" color="green" size="large"  />

```

#### Props with Objects and Arrays

```jsx
function  UserProfile({ user, skills, isOnline })  {
return  (
<div className="profile">
<img src={user.avatar} alt={user.name}  />
<h2>{user.name}</h2>
<p>{user.email}</p>
{isOnline &&  <span className="online-indicator">Online</span>}

<div className="skills">
<h3>Skills:</h3>
<ul>
{skills.map((skill, index)  =>  (
<li key={index}>{skill}</li>
))}
</ul>
</div>
</div>
);
}

// Usage
const user =  {
name:  "Dylan Smith",
email:  "dylan@example.com",
avatar:  "https://via.placeholder.com/100x100"
};

const skills =  ["JavaScript",  "React",  "Python",  "Flask"];

<UserProfile
user={user}
skills={skills}
isOnline={true}
/>

```

### Component Composition

Component composition is the practice of building complex UIs by combining simple components.

#### Layout Components

```jsx
// Header.jsx
function  Header({ title, navigation })  {
return  (
<header className="header">
<h1>{title}</h1>
<nav>
{navigation.map((item, index)  =>  (
<a key={index} href={item.href}>
{item.label}
</a>
))}
</nav>
</header>
);
}

// Footer.jsx
function  Footer({ copyright, year })  {
return  (
<footer className="footer">
<p>&copy;  {year}  {copyright}</p>
</footer>
);
}

// Layout.jsx
function  Layout({ children, title, navigation, copyright, year })  {
return  (
<div className="layout">
<Header title={title} navigation={navigation}  />
<main className="main-content">
{children}
</main>
<Footer copyright={copyright} year={year}  />
</div>
);
}

// App.jsx
function  App()  {
const navigation =  [
{  href:  "#home",  label:  "Home"  },
{  href:  "#about",  label:  "About"  },
{  href:  "#contact",  label:  "Contact"  }
];

return  (
<Layout
title="My Website"
navigation={navigation}
copyright="My Company"
year="2024"
>
<h2>Welcome to my website!</h2>
<p>This is the main content area.</p>
</Layout>
);
}

```

#### Card Component with Composition

```jsx
// Card.jsx
function  Card({ children, className =  ""  })  {
return  (
<div className={```card ${className}```}>
{children}
</div>
);
}

// CardHeader.jsx
function  CardHeader({ title, subtitle })  {
return  (
<div className="card-header">
<h3>{title}</h3>
{subtitle &&  <p className="subtitle">{subtitle}</p>}
</div>
);
}

// CardBody.jsx
function  CardBody({ children })  {
return  (
<div className="card-body">
{children}
</div>
);
}

// CardFooter.jsx
function  CardFooter({ children })  {
return  (
<div className="card-footer">
{children}
</div>
);
}

// Usage
function  App()  {
return  (
<Card className="featured">
<CardHeader
title="React Tutorial"
subtitle="Learn the basics"
/>
<CardBody>
<p>This is a comprehensive tutorial on React fundamentals.</p>
<ul>
<li>Components</li>
<li>Props</li>
<li>JSX</li>
</ul>
</CardBody>
<CardFooter>
<button>Read More</button>
<button>Share</button>
</CardFooter>
</Card>
);
}

```

Practical Exercises
-------------------

### Exercise 1: Basic Component Creation

Create a ```Welcome``` component that displays a personalized greeting.

Requirements:

-   Accept ```name``` and ```timeOfDay``` props
-   Display "Good morning/afternoon/evening, [name]!"
-   Include a welcome message

Solution:

```jsx
function  Welcome({ name, timeOfDay })  {
const greeting =  ```Good ${timeOfDay}, ${name}!```;

return  (
<div className="welcome">
<h2>{greeting}</h2>
<p>Welcome to our application!</p>
</div>
);
}

// Usage
<Welcome name="Dylan" timeOfDay="morning"  />

```

### Exercise 2: Product Card Component

Create a ```ProductCard``` component for an e-commerce site.

Requirements:

-   Display product name, price, and image
-   Show if product is on sale
-   Include an "Add to Cart" button
-   Handle out-of-stock products

Solution:

```jsx
function  ProductCard({
name,
price,
originalPrice,
image,
isOnSale,
inStock
})  {
const discount = originalPrice ?
Math.round(((originalPrice - price)  / originalPrice)  *  100)  :  0;

return  (
<div className="product-card">
<img src={image} alt={name}  />
<h3>{name}</h3>

<div className="price">
<span className="current-price">${price}</span>
{isOnSale && originalPrice &&  (
<>
<span className="original-price">${originalPrice}</span>
<span className="discount">{discount}% off</span>
</>
)}
</div>

<button
disabled={!inStock}
className={inStock ?  "add-to-cart"  :  "out-of-stock"}
>
{inStock ?  "Add to Cart"  :  "Out of Stock"}
</button>
</div>
);
}

// Usage
<ProductCard
name="Wireless Headphones"
price={99.99}
originalPrice={149.99}
image="https://via.placeholder.com/200x200"
isOnSale={true}
inStock={true}
/>

```

### Exercise 3: Navigation Component

Create a ```Navigation``` component with responsive design.

Requirements:

-   Display navigation items
-   Show active state
-   Include mobile menu toggle
-   Handle click events

Solution:

```jsx
function  Navigation({ items, activeItem, onItemClick })  {
const  [isMobileMenuOpen, setIsMobileMenuOpen]  =  useState(false);

return  (
<nav className="navigation">
<div className="nav-brand">
<h2>My App</h2>
<button
className="mobile-menu-toggle"
onClick={()  =>  setIsMobileMenuOpen(!isMobileMenuOpen)}
>
☰
</button>
</div>

<ul className={```nav-items ${isMobileMenuOpen ?  'open'  :  ''}```}>
{items.map((item, index)  =>  (
<li key={index}>
<a
href={item.href}
className={activeItem === item.label ?  'active'  :  ''}
onClick={(e)  =>  {
e.preventDefault();
onItemClick(item.label);
}}
>
{item.label}
</a>
</li>
))}
</ul>
</nav>
);
}

// Usage
const navItems =  [
{  label:  "Home",  href:  "#home"  },
{  label:  "About",  href:  "#about"  },
{  label:  "Services",  href:  "#services"  },
{  label:  "Contact",  href:  "#contact"  }
];

<Navigation
items={navItems}
activeItem="Home"
onItemClick={(item)  => console.log(```Clicked: ${item}```)}
/>

```

Best Practices
--------------

### Component Naming

-   Use PascalCase for component names
-   Use descriptive names that indicate purpose
-   Avoid generic names like "Component" or "Item"

```jsx
// ✅ Good
function  UserProfile()  {  }
function  ProductCard()  {  }
function  NavigationMenu()  {  }

// ❌ Bad
function  component()  {  }
function  card()  {  }
function  menu()  {  }

```

### Props Design

-   Use descriptive prop names
-   Provide default values when appropriate
-   Keep props simple and focused
-   Use TypeScript or PropTypes for type checking

```jsx
// ✅ Good
function  Button({ text, variant =  "primary", size =  "medium"  })  {  }

// ❌ Bad
function  Button({ t, v, s })  {  }

```

### File Organization

-   One component per file
-   Use descriptive file names
-   Group related components in folders
-   Keep components small and focused

```txt
src/
├── components/
│ ├── ui/
│ │ ├── Button.jsx
│ │ ├── Card.jsx
│ │ └── Input.jsx
│ ├── layout/
│ │ ├── Header.jsx
│ │ ├── Footer.jsx
│ │ └── Layout.jsx
│ └── features/
│ ├── UserProfile.jsx
│ └── ProductList.jsx

```

### JSX Best Practices

-   Use meaningful variable names
-   Extract complex logic into separate functions
-   Use conditional rendering appropriately
-   Keep JSX readable and well-formatted

```jsx
// ✅ Good
function  UserList({ users, showOnlineOnly })  {
const filteredUsers = showOnlineOnly
? users.filter(user  => user.isOnline)
: users;

return  (
<div className="user-list">
{filteredUsers.map(user  =>  (
<UserCard key={user.id} user={user}  />
))}
</div>
);
}

// ❌ Bad
function  UserList({ u, s })  {
return  (
<div>
{s ? u.filter(x  => x.o).map(x  =>  <div key={x.id}>{x.n}</div>)  : u.map(x  =>  <div key={x.id}>{x.n}</div>)}
</div>
);
}

```

Common Pitfalls
---------------

### 1. Forgetting to Export Components

```jsx
// ❌ Wrong - component not exported
function  MyComponent()  {
return  <div>Hello</div>;
}

// ✅ Correct - component exported
function  MyComponent()  {
return  <div>Hello</div>;
}
export  default MyComponent;

```

### 2. Using class instead of className

```jsx
// ❌ Wrong
<div class="container">

// ✅ Correct
<div className="container">

```

### 3. Not Providing Keys for Lists

```jsx
// ❌ Wrong - missing keys
{items.map(item  =>  <li>{item.name}</li>)}

// ✅ Correct - with keys
{items.map(item  =>  <li key={item.id}>{item.name}</li>)}

```

### 4. Mutating Props

```jsx
// ❌ Wrong - mutating props
function  UserCard({ user })  {
user.name =  "New Name";  // Don't do this!
return  <div>{user.name}</div>;
}

// ✅ Correct - props are read-only
function  UserCard({ user })  {
return  <div>{user.name}</div>;
}

```

### 5. Not Handling Missing Props

```jsx
// ❌ Wrong - could cause errors
function  UserCard({ user })  {
return  <div>{user.name.toUpperCase()}</div>;
}

// ✅ Correct - handle missing props
function  UserCard({ user })  {
if  (!user)  return  <div>No user data</div>;
return  <div>{user.name?.toUpperCase()}</div>;
}

```

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

-   State management with ```useState```
-   Event handling and user interactions
-   Side effects with ```useEffect```
-   Form handling and validation
-   Routing with React Router

Remember: Practice is key to mastering React. Build projects, experiment with different patterns, and don't be afraid to make mistakes. Each error is a learning opportunity!


## 2. useState & Event Handling
=========================

Introduction
------------

Welcome to the comprehensive tutorial on React state management and event handling! This tutorial will teach you how to create interactive, dynamic React components using the ```useState``` hook and proper event handling techniques. By the end of this tutorial, you'll understand how to build components that respond to user interactions and manage changing data.

What You'll Learn
-----------------

-   Understanding React state and its importance
-   Using the ```useState``` hook effectively
-   Handling user events in React
-   Building controlled components
-   Managing complex state updates
-   Best practices for state management

Concepts Overview
-----------------

### Understanding React State

State in React represents data that can change over time. When state changes, React automatically re-renders the component to reflect the new data. This is what makes React components interactive and dynamic.

Key Characteristics of State:

-   State is local to each component instance
-   State changes trigger re-renders
-   State is private to the component (unlike props)
-   State should be treated as immutable

### The useState Hook

The ```useState``` hook is React's way of adding state to functional components. It returns an array with two elements:

1.  The current state value
2.  A function to update that state

```jsx
const  [stateVariable, setStateFunction]  =  useState(initialValue);
```

### Event Handling in React

React uses synthetic events (wrapped native events) to handle user interactions. Event handlers are functions that respond to user actions like clicks, form submissions, and input changes.

Code Examples
-------------

### Basic useState Usage

```jsx
import React,  { useState }  from  'react';

function  Counter()  {
// Declare state variable and setter function
const  [count, setCount]  =  useState(0);

return  (
<div>
<p>Current count:  {count}</p>
<button onClick={()  =>  setCount(count +  1)}>
Increment
</button>
<button onClick={()  =>  setCount(count -  1)}>
Decrement
</button>
<button onClick={()  =>  setCount(0)}>
Reset
</button>
</div>
);
}

export  default Counter;

```

Explanation:

-   ```useState(0)``` initializes count to 0
-   ```count``` holds the current value
-   ```setCount``` is the function to update count
-   Each button uses ```setCount``` to modify the state

### Multiple State Variables

```jsx
import React,  { useState }  from  'react';

function  UserProfile()  {
// Multiple state variables
const  [name, setName]  =  useState('');
const  [email, setEmail]  =  useState('');
const  [age, setAge]  =  useState(0);
const  [isActive, setIsActive]  =  useState(false);

const  handleSubmit  =  (event)  =>  {
event.preventDefault();
console.log('User Profile:',  { name, email, age, isActive });
};

return  (
<form onSubmit={handleSubmit}>
<div>
<label>Name:</label>
<input
type="text"
value={name}
onChange={(e)  =>  setName(e.target.value)}
/>
</div>

<div>
<label>Email:</label>
<input
type="email"
value={email}
onChange={(e)  =>  setEmail(e.target.value)}
/>
</div>

<div>
<label>Age:</label>
<input
type="number"
value={age}
onChange={(e)  =>  setAge(parseInt(e.target.value)  ||  0)}
/>
</div>

<div>
<label>
<input
type="checkbox"
checked={isActive}
onChange={(e)  =>  setIsActive(e.target.checked)}
/>
Active User
</label>
</div>

<button type="submit">Save Profile</button>
</form>
);
}

export  default UserProfile;

```

Key Points:

-   Each piece of state is managed independently
-   Form inputs are controlled by state
-   Event handlers update the corresponding state

### Object State Management

```jsx
import React,  { useState }  from  'react';

function  TodoItem()  {
const  [todo, setTodo]  =  useState({
id:  1,
text:  'Learn React',
completed:  false,
priority:  'medium'
});

const  toggleComplete  =  ()  =>  {
setTodo(prevTodo  =>  ({
...prevTodo,
completed:  !prevTodo.completed
}));
};

const  updatePriority  =  (newPriority)  =>  {
setTodo(prevTodo  =>  ({
...prevTodo,
priority: newPriority
}));
};

return  (
<div style={{
padding:  '10px',
border:  '1px solid #ccc',
margin:  '10px 0',
backgroundColor: todo.completed ?  '#f0f0f0'  :  'white'
}}>
<h3
style={{
textDecoration: todo.completed ?  'line-through'  :  'none'
}}
onClick={toggleComplete}
>
{todo.text}
</h3>

<p>Priority:  {todo.priority}</p>

<div>
<button
onClick={()  =>  updatePriority('high')}
style={{
backgroundColor: todo.priority ===  'high'  ?  '#ff4444'  :  '#ccc',
color:  'white',
margin:  '2px',
padding:  '5px 10px',
border:  'none',
borderRadius:  '3px'
}}
>
High
</button>
<button
onClick={()  =>  updatePriority('medium')}
style={{
backgroundColor: todo.priority ===  'medium'  ?  '#ffaa00'  :  '#ccc',
color:  'white',
margin:  '2px',
padding:  '5px 10px',
border:  'none',
borderRadius:  '3px'
}}
>
Medium
</button>
<button
onClick={()  =>  updatePriority('low')}
style={{
backgroundColor: todo.priority ===  'low'  ?  '#44ff44'  :  '#ccc',
color:  'white',
margin:  '2px',
padding:  '5px 10px',
border:  'none',
borderRadius:  '3px'
}}
>
Low
</button>
</div>
</div>
);
}

export  default TodoItem;

```

Important Notes:

-   Always use the spread operator (```...```) when updating objects
-   Never mutate state directly
-   Create new objects/arrays when updating state

### Array State Management

```jsx
import React,  { useState }  from  'react';

function  ShoppingList()  {
const  [items, setItems]  =  useState([]);
const  [newItem, setNewItem]  =  useState('');

const  addItem  =  ()  =>  {
if  (newItem.trim())  {
setItems(prevItems  =>  [
...prevItems,
{
id: Date.now(),
name: newItem,
purchased:  false
}
]);
setNewItem('');
}
};

const  togglePurchased  =  (id)  =>  {
setItems(prevItems  =>
prevItems.map(item  =>
item.id === id
?  {  ...item,  purchased:  !item.purchased }
: item
)
);
};

const  removeItem  =  (id)  =>  {
setItems(prevItems  => prevItems.filter(item  => item.id !== id));
};

const  clearPurchased  =  ()  =>  {
setItems(prevItems  => prevItems.filter(item  =>  !item.purchased));
};

return  (
<div style={{  padding:  '20px',  maxWidth:  '500px'  }}>
<h2>Shopping List</h2>

<div style={{  marginBottom:  '20px'  }}>
<input
type="text"
value={newItem}
onChange={(e)  =>  setNewItem(e.target.value)}
placeholder="Add new item..."
style={{
padding:  '8px',
marginRight:  '10px',
width:  '300px',
border:  '1px solid #ccc',
borderRadius:  '4px'
}}
/>
<button
onClick={addItem}
style={{
padding:  '8px 16px',
backgroundColor:  '#007bff',
color:  'white',
border:  'none',
borderRadius:  '4px',
cursor:  'pointer'
}}
>
Add Item
</button>
</div>

<ul style={{  listStyle:  'none',  padding:  0  }}>
{items.map(item  =>  (
<li
key={item.id}
style={{
display:  'flex',
alignItems:  'center',
padding:  '8px',
margin:  '5px 0',
border:  '1px solid #ddd',
borderRadius:  '4px',
backgroundColor: item.purchased ?  '#f8f9fa'  :  'white'
}}
>
<input
type="checkbox"
checked={item.purchased}
onChange={()  =>  togglePurchased(item.id)}
style={{  marginRight:  '10px'  }}
/>
<span
style={{
flex:  1,
textDecoration: item.purchased ?  'line-through'  :  'none',
color: item.purchased ?  '#6c757d'  :  'black'
}}
>
{item.name}
</span>
<button
onClick={()  =>  removeItem(item.id)}
style={{
padding:  '4px 8px',
backgroundColor:  '#dc3545',
color:  'white',
border:  'none',
borderRadius:  '3px',
cursor:  'pointer'
}}
>
Remove
</button>
</li>
))}
</ul>

{items.length >  0  &&  (
<div style={{  marginTop:  '20px'  }}>
<p>
Total items:  {items.length}  |
Purchased:  {items.filter(item  => item.purchased).length}  |
Remaining:  {items.filter(item  =>  !item.purchased).length}
</p>
<button
onClick={clearPurchased}
style={{
padding:  '8px 16px',
backgroundColor:  '#6c757d',
color:  'white',
border:  'none',
borderRadius:  '4px',
cursor:  'pointer'
}}
>
Clear Purchased Items
</button>
</div>
)}
</div>
);
}

export  default ShoppingList;

```

Practical Exercises
-------------------

### Exercise 1: Simple Counter with Reset

Create a counter component that:

-   Starts at 0
-   Has increment and decrement buttons
-   Has a reset button
-   Shows the current count

### Exercise 2: Toggle Component

Build a component that:

-   Has a boolean state for visibility
-   Shows/hides content based on state
-   Button text changes based on current state

### Exercise 3: Form with Validation

Create a contact form with:

-   Name, email, and message fields
-   Basic validation (required fields)
-   Success message after submission
-   Form reset after successful submission

### Exercise 4: Todo List

Build a complete todo list with:

-   Add new todos
-   Mark todos as complete
-   Delete todos
-   Show count of remaining todos

Best Practices
--------------

### 1. State Structure

-   Keep state as simple as possible
-   Group related state into objects when appropriate
-   Avoid deeply nested state structures

```jsx
// Good: Simple, flat state
const  [name, setName]  =  useState('');
const  [email, setEmail]  =  useState('');

// Good: Related state grouped together
const  [user, setUser]  =  useState({
name:  '',
email:  '',
preferences:  {}
});

```

### 2. State Updates

-   Always use the setter function
-   Use functional updates when the new state depends on the previous state
-   Never mutate state directly

```jsx
// Good: Functional update
setCount(prevCount  => prevCount +  1);

// Good: Object update
setUser(prevUser  =>  ({
...prevUser,
name: newName
}));

// Bad: Direct mutation
user.name = newName;  // Don't do this!

```

### 3. Event Handling

-   Use descriptive function names
-   Extract complex logic into separate functions
-   Handle edge cases (empty inputs, validation)

```jsx
// Good: Descriptive names and error handling
const  handleNameChange  =  (event)  =>  {
const value = event.target.value.trim();
if  (value.length <=  50)  {
setName(value);
}
};

// Good: Extracted logic
const  validateEmail  =  (email)  =>  {
return email.includes('@')  && email.includes('.');
};

const  handleEmailChange  =  (event)  =>  {
const value = event.target.value;
setEmail(value);
setEmailValid(validateEmail(value));
};

```

### 4. Performance Considerations

-   Avoid creating objects/functions in render
-   Use useCallback for expensive event handlers
-   Consider useMemo for expensive calculations

```jsx
// Good: Memoized event handler
const handleClick =  useCallback(()  =>  {
// Expensive operation
},  [dependency]);

// Good: Memoized calculation
const expensiveValue =  useMemo(()  =>  {
return items.reduce((sum, item)  => sum + item.price,  0);
},  [items]);

```

Common Pitfalls
---------------

### 1. Mutating State Directly

```jsx
// Bad: Direct mutation
const  [items, setItems]  =  useState([]);
items.push(newItem);  // This won't trigger re-render!

// Good: Using setter function
setItems(prevItems  =>  [...prevItems, newItem]);

```

### 2. Stale State in Closures

```jsx
// Bad: Stale state
const  handleClick  =  ()  =>  {
setTimeout(()  =>  {
setCount(count +  1);  // Uses stale count value
},  1000);
};

// Good: Functional update
const  handleClick  =  ()  =>  {
setTimeout(()  =>  {
setCount(prevCount  => prevCount +  1);
},  1000);
};

```

### 3. Forgetting to Prevent Default

```jsx
// Bad: Form will submit and refresh page
const  handleSubmit  =  ()  =>  {
// Process form
};

// Good: Prevent default behavior
const  handleSubmit  =  (event)  =>  {
event.preventDefault();
// Process form
};

```

### 4. Missing Dependencies in useEffect

```jsx
// Bad: Missing dependency
useEffect(()  =>  {
fetchData(userId);
},  []);  // Missing userId dependency

// Good: Include all dependencies
useEffect(()  =>  {
fetchData(userId);
},  [userId]);

```

Advanced Patterns
-----------------

### Custom Hooks

```jsx
// Custom hook for form state
function  useForm(initialValues)  {
const  [values, setValues]  =  useState(initialValues);
const  [errors, setErrors]  =  useState({});

const  handleChange  =  (event)  =>  {
const  { name, value }  = event.target;
setValues(prev  =>  ({
...prev,
[name]: value
}));
};

const  handleSubmit  =  (onSubmit)  =>  (event)  =>  {
event.preventDefault();
onSubmit(values);
};

return  { values, errors, handleChange, handleSubmit };
}

// Usage
function  ContactForm()  {
const  { values, handleChange, handleSubmit }  =  useForm({
name:  '',
email:  '',
message:  ''
});

return  (
<form onSubmit={handleSubmit((data)  => console.log(data))}>
<input
name="name"
value={values.name}
onChange={handleChange}
placeholder="Name"
/>
{/* More inputs... */}
</form>
);
}

```

### State Reducer Pattern

```jsx
// For complex state logic
function  todoReducer(state, action)  {
switch  (action.type)  {
case  'ADD_TODO':
return  [...state, action.payload];
case  'TOGGLE_TODO':
return state.map(todo  =>
todo.id === action.payload
?  {  ...todo,  completed:  !todo.completed }
: todo
);
case  'DELETE_TODO':
return state.filter(todo  => todo.id !== action.payload);
default:
return state;
}
}

function  TodoApp()  {
const  [todos, dispatch]  =  useReducer(todoReducer,  []);

const  addTodo  =  (text)  =>  {
dispatch({
type:  'ADD_TODO',
payload:  {  id: Date.now(), text,  completed:  false  }
});
};

// More actions...
}

```

Additional Resources
--------------------

### Official Documentation

-   [React Hooks](https://reactjs.org/docs/hooks-intro.html)
-   [useState Hook](https://reactjs.org/docs/hooks-state.html)
-   [Event Handling](https://reactjs.org/docs/handling-events.html)

### Useful Tools

-   [React Developer Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)
-   [React Hook Form](https://react-hook-form.com/) - For complex forms
-   [Zustand](https://github.com/pmndrs/zustand) - Lightweight state management

### Practice Projects

1.  Calculator App - Basic arithmetic operations
2.  Weather Widget - Display weather data with state
3.  Chat Interface - Message list with input
4.  Shopping Cart - Product management with state
5.  Timer/Stopwatch - Time-based state management

Conclusion
----------

You've now learned the fundamentals of React state management and event handling! These concepts are crucial for building interactive React applications. Remember to:

-   Always use the setter function to update state
-   Keep state as simple as possible
-   Handle events properly with preventDefault when needed
-   Use functional updates for state that depends on previous state
-   Practice with real projects to solidify your understanding

In the next lesson, you'll learn about ```useEffect``` for handling side effects and API integration. Keep practicing with state and events - they're the foundation of interactive React applications!


## 3. Tutorial: useEffect & API Integration
=====================================

* * * * *

Introduction to Side Effects
----------------------------

### What are Side Effects?

In React, side effects are operations that affect something outside the scope of the current function being executed. These are operations that:

-   Fetch data from an API
-   Set up subscriptions or timers
-   Manually change the DOM
-   Log to the console
-   Set up event listeners

### Why Side Effects Need Special Handling

React components should be pure functions - given the same inputs (props and state), they should always return the same output. Side effects break this rule because they can cause:

-   Infinite re-renders: If you call an API in the component body, it runs on every render
-   Inconsistent behavior: The component might behave differently on different renders
-   Performance issues: Unnecessary API calls and operations

### Example: The Problem

```jsx
// WRONG - This will cause infinite re-renders
function  UserProfile({ userId })  {
const  [user, setUser]  =  useState(null);

// This runs on EVERY render!
fetch(```/api/users/${userId}```)
.then(res  => res.json())
.then(data  =>  setUser(data));

return  <div>{user?.name ||  'Loading...'}</div>;
}

```

Problems:

1.  API call runs on every render
2.  ```setUser``` triggers a re-render
3.  Re-render triggers another API call
4.  Infinite loop!

* * * * *

React Component Lifecycle Basics
--------------------------------

### Understanding Component Lifecycle

React components go through different phases during their lifetime. Understanding these phases is crucial for knowing when to run side effects and how useEffect fits into the component lifecycle.

### The Three Main Lifecycle Phases

#### 1. Mounting Phase

-   Component is created and added to the DOM
-   Initial state is set with ```useState```
-   Component renders for the first time
-   ```useEffect``` with empty dependencies ```[]``` runs

#### 2. Updating Phase

-   State or props change
-   Component re-renders
-   ```useEffect``` with dependencies runs (if dependencies changed)
-   ```useEffect``` with no dependencies runs after every render

#### 3. Unmounting Phase

-   Component is about to be removed from DOM
-   Cleanup functions from ```useEffect``` run
-   Component is removed from DOM

### Visual Representation

```
Component Lifecycle:
┌─────────────┐ ┌─────────────┐ ┌─────────────┐
│ Mount │───▶│ Update │───▶│ Unmount │
│ │ │ │ │ │
│ - useState │ │ - Re-render │ │ - Cleanup │
│ - useEffect │ │ - useEffect │ │ - Remove │
│ - Render │ │ - Render │ │ │
└─────────────┘ └─────────────┘ └─────────────┘

```

### Lifecycle Demo Component

```jsx
import  { useState, useEffect }  from  'react';

function  LifecycleDemo()  {
const  [count, setCount]  =  useState(0);
const  [isVisible, setIsVisible]  =  useState(true);

// This runs on every render (including initial render)
console.log('Component is rendering...');

// This runs after every render
useEffect(()  =>  {
console.log('Component rendered (useEffect with no dependencies)');
});

// This runs only on mount
useEffect(()  =>  {
console.log('Component mounted (useEffect with empty dependencies)');

// This runs on unmount
return  ()  =>  {
console.log('Component unmounted (cleanup function)');
};
},  []);

// This runs when count changes
useEffect(()  =>  {
console.log('Count changed to:', count);
},  [count]);

return  (
<div>
<h2>Lifecycle Demo</h2>
<p>Count:  {count}</p>
<button onClick={()  =>  setCount(count +  1)}>Increment</button>
<button onClick={()  =>  setIsVisible(!isVisible)}>
{isVisible ?  'Hide'  :  'Show'} Component
</button>

{isVisible &&  (
<div>
<h3>This component is visible</h3>
<p>Check the console to see lifecycle logs!</p>
</div>
)}
</div>
);
}

```

### Key Lifecycle Concepts

#### Mounting

-   When: Component first appears in the DOM
-   What happens:
-   -   Initial state is set
    -   Component renders
    -   ```useEffect``` with ```[]``` dependencies runs
-   Use cases: Setting up subscriptions, initial API calls, setting document title

#### Updating

-   When: State or props change
-   What happens:
-   -   Component re-renders
    -   ```useEffect``` with dependencies runs (if they changed)
    -   ```useEffect``` with no dependencies runs after every render
-   Use cases: Responding to prop changes, updating data based on state

#### Unmounting

-   When: Component is removed from DOM
-   What happens:
-   -   Cleanup functions from ```useEffect``` run
    -   Component is removed
-   Use cases: Cleaning up timers, canceling API requests, removing event listeners

### Why Understanding Lifecycle Matters

1.  Timing Control: Know when your side effects will run
2.  Performance: Avoid unnecessary operations
3.  Memory Management: Clean up resources properly
4.  Debugging: Understand why effects run when they do

### Common Lifecycle Patterns

#### Run Once on Mount

```jsx
useEffect(()  =>  {
// This runs only once when component mounts
console.log('Component mounted');
fetchInitialData();
},  []);  // Empty dependency array

```

#### Run on Every Update

```jsx
useEffect(()  =>  {
// This runs after every render
console.log('Component updated');
updateDocumentTitle();
});  // No dependency array

```

#### Run When Specific Values Change

```jsx
useEffect(()  =>  {
// This runs when userId or isActive changes
fetchUserData(userId, isActive);
},  [userId, isActive]);  // Specific dependencies

```

#### Cleanup on Unmount

```jsx
useEffect(()  =>  {
const timer =  setInterval(()  =>  {
console.log('Timer tick');
},  1000);

// Cleanup function runs on unmount
return  ()  =>  {
clearInterval(timer);
};
},  []);  // Empty array - only run on mount/unmount

```

### Lifecycle and Side Effects

Understanding the component lifecycle helps you:

-   Choose the right dependency array for your ```useEffect```
-   Know when effects will run and why
-   Debug timing issues with side effects
-   Optimize performance by running effects only when needed
-   Prevent memory leaks with proper cleanup

### Common Questions

Q: When does my component mount?
A: When it first appears in the DOM (usually when parent renders it)

Q: Why does my effect run multiple times?
A: Check your dependency array - effects run when dependencies change

Q: When should I clean up?
A: Always clean up subscriptions, timers, and event listeners to prevent memory leaks

Q: How do I know what to put in the dependency array?
A: Include all values from component scope that are used inside the effect

* * * * *

Understanding useEffect
-----------------------

### Basic Syntax

```jsx
import  { useEffect }  from  'react';

useEffect(()  =>  {
// Side effect code here
},  [dependencies]);  // Optional dependency array

```

### The Three Main Use Cases

#### 1. Run on Every Render (No Dependency Array)

```jsx
useEffect(()  =>  {
console.log('Component rendered');
// This runs after every render
});

```

#### 2. Run Only on Mount (Empty Dependency Array)

```jsx
useEffect(()  =>  {
console.log('Component mounted');
// This runs only once when component mounts
},  []);  // Empty array

```

#### 3. Run When Dependencies Change

```jsx
useEffect(()  =>  {
console.log('Count changed:', count);
// This runs when 'count' changes
},  [count]);  // 'count' in dependency array

```

### Complete Example

```jsx
import  { useState, useEffect }  from  'react';

function  Counter()  {
const  [count, setCount]  =  useState(0);
const  [name, setName]  =  useState('');

// Runs after every render
useEffect(()  =>  {
console.log('Component rendered');
});

// Runs only on mount
useEffect(()  =>  {
console.log('Component mounted');
document.title =  'Counter App';
},  []);

// Runs when count changes
useEffect(()  =>  {
console.log('Count is now:', count);
if  (count >  10)  {
alert('Count is getting high!');
}
},  [count]);

// Runs when name changes
useEffect(()  =>  {
console.log('Name changed to:', name);
},  [name]);

return  (
<div>
<h2>Count:  {count}</h2>
<input
value={name}
onChange={(e)  =>  setName(e.target.value)}
placeholder="Enter your name"
/>
<button onClick={()  =>  setCount(count +  1)}>
Increment
</button>
</div>
);
}

```

### Understanding the Dependency Array

The dependency array tells React when to run the effect:

-   No array: Run after every render
-   Empty array ```[]```: Run only on mount and unmount
-   Array with values ```[a, b]```: Run when any of the values change

```jsx
// Example with multiple dependencies
useEffect(()  =>  {
// This runs when either userId OR isActive changes
fetchUserData(userId, isActive);
},  [userId, isActive]);

```

* * * * *

Data Fetching Patterns
----------------------

### Basic Data Fetching

```jsx
import  { useState, useEffect }  from  'react';

function  UserList()  {
const  [users, setUsers]  =  useState([]);
const  [loading, setLoading]  =  useState(true);
const  [error, setError]  =  useState(null);

useEffect(()  =>  {
async  function  fetchUsers()  {
try  {
setLoading(true);
setError(null);

const response =  await  fetch('https://jsonplaceholder.typicode.com/users');

if  (!response.ok)  {
throw  new  Error(```HTTP ${response.status}: ${response.statusText}```);
}

const data =  await response.json();
setUsers(data);
}  catch  (err)  {
setError(err.message);
}  finally  {
setLoading(false);
}
}

fetchUsers();
},  []);  // Empty array - fetch once on mount

if  (loading)  return  <div>Loading users...</div>;
if  (error)  return  <div>Error:  {error}</div>;

return  (
<ul>
{users.map(user  =>  (
<li key={user.id}>
<strong>{user.name}</strong>  -  {user.email}
</li>
))}
</ul>
);
}

```

### Data Fetching with Parameters

```jsx
function  UserProfile({ userId })  {
const  [user, setUser]  =  useState(null);
const  [loading, setLoading]  =  useState(false);
const  [error, setError]  =  useState(null);

useEffect(()  =>  {
async  function  fetchUser()  {
if  (!userId)  return;  // Don't fetch if no userId

try  {
setLoading(true);
setError(null);

const response =  await  fetch(```/api/users/${userId}```);

if  (!response.ok)  {
throw  new  Error('User not found');
}

const userData =  await response.json();
setUser(userData);
}  catch  (err)  {
setError(err.message);
}  finally  {
setLoading(false);
}
}

fetchUser();
},  [userId]);  // Re-fetch when userId changes

if  (loading)  return  <div>Loading user...</div>;
if  (error)  return  <div>Error:  {error}</div>;
if  (!user)  return  <div>No user selected</div>;

return  (
<div>
<h2>{user.name}</h2>
<p>Email:  {user.email}</p>
<p>Phone:  {user.phone}</p>
</div>
);
}

```

### Search with Debouncing

```jsx
import  { useState, useEffect, useCallback }  from  'react';

function  SearchableUserList()  {
const  [searchTerm, setSearchTerm]  =  useState('');
const  [users, setUsers]  =  useState([]);
const  [loading, setLoading]  =  useState(false);
const  [error, setError]  =  useState(null);

// Debounced search function
const debouncedSearch =  useCallback(
debounce(async  (term)  =>  {
if  (!term.trim())  {
setUsers([]);
return;
}

try  {
setLoading(true);
setError(null);

const response =  await  fetch('/api/users/search?q=${encodeURIComponent(term)}'');

if  (!response.ok)  {
throw  new  Error('Search failed');
}

const data =  await response.json();
setUsers(data);
}  catch  (err)  {
setError(err.message);
}  finally  {
setLoading(false);
}
},  300),  // 300ms delay
[]
);

useEffect(()  =>  {
debouncedSearch(searchTerm);
},  [searchTerm, debouncedSearch]);

return  (
<div>
<input
type="text"
value={searchTerm}
onChange={(e)  =>  setSearchTerm(e.target.value)}
placeholder="Search users..."
/>

{loading &&  <div>Searching...</div>}
{error &&  <div>Error:  {error}</div>}

<ul>
{users.map(user  =>  (
<li key={user.id}>{user.name}</li>
))}
</ul>
</div>
);
}

// Simple debounce function
function  debounce(func, wait)  {
let timeout;
return  function  executedFunction(...args)  {
const  later  =  ()  =>  {
clearTimeout(timeout);
func(...args);
};
clearTimeout(timeout);
timeout =  setTimeout(later, wait);
};
}

```

* * * * *

Error Handling & Loading States
-------------------------------

### Comprehensive Error Handling

```jsx
function  DataComponent()  {
const  [data, setData]  =  useState(null);
const  [loading, setLoading]  =  useState(false);
const  [error, setError]  =  useState(null);
const  [retryCount, setRetryCount]  =  useState(0);

const  fetchData  =  async  (retry =  false)  =>  {
if  (!retry)  {
setLoading(true);
setError(null);
}

try  {
const response =  await  fetch('/api/data');

if  (!response.ok)  {
// Handle different HTTP status codes
switch  (response.status)  {
case  404:
throw  new  Error('Data not found');
case  500:
throw  new  Error('Server error. Please try again later.');
case  403:
throw  new  Error('Access denied');
default:
throw  new  Error(```HTTP ${response.status}: ${response.statusText}```);
}
}

const result =  await response.json();
setData(result);
setError(null);
setRetryCount(0);
}  catch  (err)  {
setError(err.message);
console.error('Fetch error:', err);
}  finally  {
setLoading(false);
}
};

useEffect(()  =>  {
fetchData();
},  []);

const  handleRetry  =  ()  =>  {
setRetryCount(prev  => prev +  1);
fetchData(true);
};

if  (loading)  {
return  (
<div className="loading-container">
<div className="spinner"></div>
<p>Loading data...</p>
</div>
);
}

if  (error)  {
return  (
<div className="error-container">
<h3>Something went wrong</h3>
<p>{error}</p>
<button onClick={handleRetry}>
Retry {retryCount >  0  &&  ```(${retryCount})```}
</button>
{retryCount >  3  &&  (
<p>Having trouble? Please contact support.</p>
)}
</div>
);
}

return  (
<div>
<h2>Data Loaded Successfully</h2>
<pre>{JSON.stringify(data,  null,  2)}</pre>
</div>
);
}

```

### Loading States with Different Types

```jsx
function  LoadingExample()  {
const  [loading, setLoading]  =  useState(false);
const  [loadingType, setLoadingType]  =  useState('');

const  handleAction  =  async  (type)  =>  {
setLoadingType(type);
setLoading(true);

try  {
// Simulate different loading times
const delay = type ===  'quick'  ?  1000  : type ===  'slow'  ?  3000  :  2000;
await  new  Promise(resolve  =>  setTimeout(resolve, delay));

// Your actual API call here
console.log(```${type} action completed```);
}  finally  {
setLoading(false);
setLoadingType('');
}
};

return  (
<div>
<button
onClick={()  =>  handleAction('quick')}
disabled={loading}
>
Quick Action
</button>

<button
onClick={()  =>  handleAction('normal')}
disabled={loading}
>
Normal Action
</button>

<button
onClick={()  =>  handleAction('slow')}
disabled={loading}
>
Slow Action
</button>

{loading &&  (
<div className="loading">
<div className="spinner"></div>
<p>
{loadingType ===  'quick'  &&  'Quick action in progress...'}
{loadingType ===  'normal'  &&  'Processing...'}
{loadingType ===  'slow'  &&  'This might take a while...'}
</p>
</div>
)}
</div>
);
}

```

* * * * *

Cleanup Functions
-----------------

### Why Cleanup is Important

Cleanup functions prevent:

-   Memory leaks: Timers and subscriptions continue running
-   State updates on unmounted components: Causes React warnings
-   Resource waste: Unnecessary API calls and operations

### Timer Cleanup

```jsx
function  Timer()  {
const  [seconds, setSeconds]  =  useState(0);
const  [isRunning, setIsRunning]  =  useState(false);

useEffect(()  =>  {
let interval;

if  (isRunning)  {
interval =  setInterval(()  =>  {
setSeconds(prev  => prev +  1);
},  1000);
}

// Cleanup function
return  ()  =>  {
if  (interval)  {
clearInterval(interval);
}
};
},  [isRunning]);  // Re-run when isRunning changes

return  (
<div>
<h2>Timer:  {seconds} seconds</h2>
<button onClick={()  =>  setIsRunning(!isRunning)}>
{isRunning ?  'Stop'  :  'Start'}
</button>
<button onClick={()  =>  setSeconds(0)}>Reset</button>
</div>
);
}

```

### Subscription Cleanup

```jsx
function  ChatRoom({ roomId })  {
const  [messages, setMessages]  =  useState([]);
const  [connection, setConnection]  =  useState(null);

useEffect(()  =>  {
// Create WebSocket connection
const ws =  new  WebSocket(```ws://localhost:8080/rooms/${roomId}```);

ws.onopen  =  ()  =>  {
console.log('Connected to chat room');
setConnection(ws);
};

ws.onmessage  =  (event)  =>  {
const message =  JSON.parse(event.data);
setMessages(prev  =>  [...prev, message]);
};

ws.onerror  =  (error)  =>  {
console.error('WebSocket error:', error);
};

ws.onclose  =  ()  =>  {
console.log('Disconnected from chat room');
setConnection(null);
};

// Cleanup function
return  ()  =>  {
if  (ws.readyState === WebSocket.OPEN)  {
ws.close();
}
};
},  [roomId]);  // Re-run when roomId changes

const  sendMessage  =  (text)  =>  {
if  (connection && connection.readyState === WebSocket.OPEN)  {
connection.send(JSON.stringify({ text,  timestamp: Date.now()  }));
}
};

return  (
<div>
<h2>Chat Room:  {roomId}</h2>
<div className="messages">
{messages.map((msg, index)  =>  (
<div key={index} className="message">
<span className="timestamp">
{new  Date(msg.timestamp).toLocaleTimeString()}
</span>
<span className="text">{msg.text}</span>
</div>
))}
</div>
<input
type="text"
placeholder="Type a message..."
onKeyPress={(e)  =>  {
if  (e.key ===  'Enter')  {
sendMessage(e.target.value);
e.target.value =  '';
}
}}
/>
</div>
);
}

```

### API Request Cleanup with AbortController

```jsx
function  SearchableList()  {
const  [searchTerm, setSearchTerm]  =  useState('');
const  [results, setResults]  =  useState([]);
const  [loading, setLoading]  =  useState(false);

useEffect(()  =>  {
// Create AbortController for this request
const abortController =  new  AbortController();

const  fetchResults  =  async  ()  =>  {
if  (!searchTerm.trim())  {
setResults([]);
return;
}

try  {
setLoading(true);

const response =  await  fetch(
```/api/search?q=${encodeURIComponent(searchTerm)}```,
{  signal: abortController.signal }  // Pass abort signal
);

if  (!response.ok)  {
throw  new  Error('Search failed');
}

const data =  await response.json();
setResults(data);
}  catch  (error)  {
// Don't update state if request was aborted
if  (error.name !==  'AbortError')  {
console.error('Search error:', error);
setResults([]);
}
}  finally  {
setLoading(false);
}
};

fetchResults();

// Cleanup function - abort the request
return  ()  =>  {
abortController.abort();
};
},  [searchTerm]);

return  (
<div>
<input
type="text"
value={searchTerm}
onChange={(e)  =>  setSearchTerm(e.target.value)}
placeholder="Search..."
/>

{loading &&  <div>Searching...</div>}

<ul>
{results.map((item, index)  =>  (
<li key={index}>{item.name}</li>
))}
</ul>
</div>
);
}

```

* * * * *

Advanced Patterns
-----------------

### Custom Hook for Data Fetching

```jsx
// Custom hook: useApi
function  useApi(url, options =  {})  {
const  [data, setData]  =  useState(null);
const  [loading, setLoading]  =  useState(false);
const  [error, setError]  =  useState(null);

const fetchData =  useCallback(async  ()  =>  {
try  {
setLoading(true);
setError(null);

const response =  await  fetch(url, options);

if  (!response.ok)  {
throw  new  Error(```HTTP ${response.status}: ${response.statusText}```);
}

const result =  await response.json();
setData(result);
}  catch  (err)  {
setError(err.message);
}  finally  {
setLoading(false);
}
},  [url,  JSON.stringify(options)]);

useEffect(()  =>  {
fetchData();
},  [fetchData]);

return  { data, loading, error,  refetch: fetchData };
}

// Using the custom hook
function  UserProfile({ userId })  {
const  {  data: user, loading, error, refetch }  =  useApi(```/api/users/${userId}```);

if  (loading)  return  <div>Loading user...</div>;
if  (error)  return  <div>Error:  {error}</div>;
if  (!user)  return  <div>No user found</div>;

return  (
<div>
<h2>{user.name}</h2>
<p>Email:  {user.email}</p>
<button onClick={refetch}>Refresh</button>
</div>
);
}

```

### Multiple API Calls

```jsx
function  Dashboard()  {
const  [user, setUser]  =  useState(null);
const  [posts, setPosts]  =  useState([]);
const  [loading, setLoading]  =  useState(true);
const  [error, setError]  =  useState(null);

useEffect(()  =>  {
async  function  fetchDashboardData()  {
try  {
setLoading(true);
setError(null);

// Fetch multiple resources in parallel
const  [userResponse, postsResponse]  =  await Promise.all([
fetch('/api/user'),
fetch('/api/posts')
]);

if  (!userResponse.ok ||  !postsResponse.ok)  {
throw  new  Error('Failed to fetch dashboard data');
}

const  [userData, postsData]  =  await Promise.all([
userResponse.json(),
postsResponse.json()
]);

setUser(userData);
setPosts(postsData);
}  catch  (err)  {
setError(err.message);
}  finally  {
setLoading(false);
}
}

fetchDashboardData();
},  []);

if  (loading)  return  <div>Loading dashboard...</div>;
if  (error)  return  <div>Error:  {error}</div>;

return  (
<div>
<h1>Welcome,  {user?.name}!</h1>
<h2>Your Posts</h2>
<ul>
{posts.map(post  =>  (
<li key={post.id}>{post.title}</li>
))}
</ul>
</div>
);
}

```

### Conditional Effects

```jsx
function  ConditionalDataFetch({ userId, shouldFetch })  {
const  [user, setUser]  =  useState(null);
const  [loading, setLoading]  =  useState(false);

useEffect(()  =>  {
// Only fetch if conditions are met
if  (!shouldFetch ||  !userId)  {
return;  // Early return - no effect
}

async  function  fetchUser()  {
try  {
setLoading(true);
const response =  await  fetch(```/api/users/${userId}```);
const userData =  await response.json();
setUser(userData);
}  catch  (error)  {
console.error('Error fetching user:', error);
}  finally  {
setLoading(false);
}
}

fetchUser();
},  [userId, shouldFetch]);  // Dependencies include the condition

if  (!shouldFetch)  {
return  <div>Fetching is disabled</div>;
}

if  (loading)  return  <div>Loading user...</div>;
if  (!user)  return  <div>No user data</div>;

return  <div>User:  {user.name}</div>;
}

```

* * * * *

Best Practices
--------------

### 1. Always Handle Loading and Error States

```jsx
// GOOD
function  DataComponent()  {
const  [data, setData]  =  useState(null);
const  [loading, setLoading]  =  useState(false);
const  [error, setError]  =  useState(null);

useEffect(()  =>  {
async  function  fetchData()  {
try  {
setLoading(true);
setError(null);
const response =  await  fetch('/api/data');
const result =  await response.json();
setData(result);
}  catch  (err)  {
setError(err.message);
}  finally  {
setLoading(false);
}
}
fetchData();
},  []);

if  (loading)  return  <div>Loading...</div>;
if  (error)  return  <div>Error:  {error}</div>;
return  <div>{JSON.stringify(data)}</div>;
}

```

### 2. Use Proper Dependency Arrays

```jsx
// GOOD - includes all dependencies
useEffect(()  =>  {
fetchUserData(userId, isActive);
},  [userId, isActive]);

// BAD - missing dependencies
useEffect(()  =>  {
fetchUserData(userId, isActive);
},  [userId]);  // Missing isActive

```

### 3. Clean Up Side Effects

```jsx
// GOOD - cleans up timer
useEffect(()  =>  {
const timer =  setInterval(()  =>  {
console.log('Timer tick');
},  1000);

return  ()  =>  clearInterval(timer);
},  []);

// BAD - no cleanup
useEffect(()  =>  {
setInterval(()  =>  {
console.log('Timer tick');
},  1000);
},  []);

```

### 4. Avoid Infinite Loops

```jsx
// GOOD - stable dependency
const  [count, setCount]  =  useState(0);

useEffect(()  =>  {
if  (count <  10)  {
setCount(prev  => prev +  1);
}
},  [count]);

// BAD - infinite loop
useEffect(()  =>  {
setCount(count +  1);
},  [count]);  // count changes, triggers effect, changes count again

```

### 5. Use AbortController for API Requests

```jsx
// GOOD - cancels previous requests
useEffect(()  =>  {
const abortController =  new  AbortController();

fetch('/api/data',  {  signal: abortController.signal })
.then(res  => res.json())
.then(setData);

return  ()  => abortController.abort();
},  []);

```

* * * * *

Common Pitfalls
---------------

### 1. Missing Dependency Array

```jsx
// WRONG - runs on every render
useEffect(()  =>  {
fetchData();
});

// CORRECT - runs only on mount
useEffect(()  =>  {
fetchData();
},  []);

```

### 2. Stale Closures

```jsx
// WRONG - uses stale count value
useEffect(()  =>  {
const timer =  setInterval(()  =>  {
console.log(count);  // Always logs initial value
},  1000);

return  ()  =>  clearInterval(timer);
},  []);

// CORRECT - uses current count value
useEffect(()  =>  {
const timer =  setInterval(()  =>  {
setCount(prev  =>  {
console.log(prev);  // Logs current value
return prev +  1;
});
},  1000);

return  ()  =>  clearInterval(timer);
},  []);

```

### 3. Forgetting to Clean Up

```jsx
// WRONG - memory leak
useEffect(()  =>  {
const subscription =  subscribeToUpdates();
// No cleanup!
},  []);

// CORRECT - proper cleanup
useEffect(()  =>  {
const subscription =  subscribeToUpdates();

return  ()  =>  {
subscription.unsubscribe();
};
},  []);

```

### 4. Incorrect Dependency Arrays

```jsx
// WRONG - missing dependencies
function  Component({ userId, filters })  {
useEffect(()  =>  {
fetchUserData(userId, filters);
},  [userId]);  // Missing filters dependency

return  <div>...</div>;
}

// CORRECT - includes all dependencies
function  Component({ userId, filters })  {
useEffect(()  =>  {
fetchUserData(userId, filters);
},  [userId, filters]);

return  <div>...</div>;
}

```

### 5. Async Functions in useEffect

```jsx
// WRONG - async function directly in useEffect
useEffect(async  ()  =>  {
const data =  await  fetchData();
setData(data);
},  []);

// CORRECT - define async function inside useEffect
useEffect(()  =>  {
async  function  fetchData()  {
const data =  await  fetchData();
setData(data);
}

fetchData();
},  []);

```

* * * * *

Summary
-------

useEffect is a powerful hook for handling side effects in React. Remember:

1.  Use it for side effects: API calls, timers, subscriptions, DOM manipulation
2.  Handle all states: loading, success, error
3.  Clean up properly: prevent memory leaks and unnecessary operations
4.  Use correct dependencies: include all values used inside the effect
5.  Avoid infinite loops: be careful with state updates in effects

With these patterns and best practices, you'll be able to build robust React applications that handle side effects properly and provide a great user experience.

* * * * *

Practice Exercises
------------------

1.  Basic Timer: Create a stopwatch that starts, stops, and resets
2.  Weather App: Fetch weather data for a city and display it
3.  Search with Debouncing: Implement a search that waits 300ms after user stops typing
4.  Data Dashboard: Fetch multiple API endpoints and display the data
5.  Real-time Updates: Use WebSocket or polling to show live data updates

Try building these examples to solidify your understanding of useEffect and API integration!

## 4. Forms & Controlled Components Tutorial
======================================

Introduction
------------

This comprehensive tutorial covers React form handling patterns, from basic controlled components to advanced validation and dynamic forms. Use this as a reference guide for building robust, user-friendly forms.

Core Concepts
-------------

### Controlled vs Uncontrolled Components

Controlled Components: Form data controlled by React state

```jsx
function  ControlledInput()  {
const  [value, setValue]  =  useState('');
return  <input value={value} onChange={(e)  =>  setValue(e.target.value)}  />;
}

```

Uncontrolled Components: Form data handled by DOM

```jsx
function  UncontrolledInput()  {
return  <input defaultValue="initial value"  />;
}

```

When to use: Controlled for most cases, uncontrolled for simple forms or non-React integrations.

### Form State Management

#### Single Field

```jsx
const  [email, setEmail]  =  useState('');
<input value={email} onChange={(e)  =>  setEmail(e.target.value)}  />

```

#### Multiple Fields (Object State)

```jsx
const  [formData, setFormData]  =  useState({
firstName:  '',
lastName:  '',
email:  ''
});

const  handleChange  =  (event)  =>  {
const  { name, value }  = event.target;
setFormData(prevData  =>  ({  ...prevData,  [name]: value }));
};

```

### Validation Patterns

#### Real-time Validation

```jsx
const  handleChange  =  (event)  =>  {
const  { name, value }  = event.target;
setFormData(prev  =>  ({  ...prev,  [name]: value }));

// Validate field
const error =  validateField(name, value);
setErrors(prev  =>  ({  ...prev,  [name]: error }));
};

```

#### Submit-time Validation

```jsx
const  validateForm  =  ()  =>  {
const newErrors =  {};
Object.keys(formData).forEach(key  =>  {
const error =  validateField(key, formData[key]);
if  (error) newErrors[key]  = error;
});
setErrors(newErrors);
return Object.keys(newErrors).length ===  0;
};

```

Code Examples
-------------

### Basic Contact Form

```jsx
function  ContactForm()  {
const  [formData, setFormData]  =  useState({
name:  '',
email:  '',
message:  ''
});

const  handleChange  =  (event)  =>  {
const  { name, value }  = event.target;
setFormData(prevData  =>  ({  ...prevData,  [name]: value }));
};

const  handleSubmit  =  (event)  =>  {
event.preventDefault();
console.log('Form submitted:', formData);
};

return  (
<form onSubmit={handleSubmit}>
<input
type="text"
name="name"
value={formData.name}
onChange={handleChange}
placeholder="Name"
required
/>
<input
type="email"
name="email"
value={formData.email}
onChange={handleChange}
placeholder="Email"
required
/>
<textarea
name="message"
value={formData.message}
onChange={handleChange}
placeholder="Message"
required
/>
<button type="submit">Send Message</button>
</form>
);
}

```

### Form with Validation

```jsx
function  ValidatedForm()  {
const  [formData, setFormData]  =  useState({  email:  '',  password:  ''  });
const  [errors, setErrors]  =  useState({});

const  validateField  =  (name, value)  =>  {
switch  (name)  {
case  'email':
return  /S+@S+.S+/.test(value)  ?  ''  :  'Invalid email';
case  'password':
return value.length >=  8  ?  ''  :  'Password must be 8+ characters';
default:
return  '';
}
};

const  handleChange  =  (event)  =>  {
const  { name, value }  = event.target;
setFormData(prev  =>  ({  ...prev,  [name]: value }));

const error =  validateField(name, value);
setErrors(prev  =>  ({  ...prev,  [name]: error }));
};

return  (
<form>
<input
type="email"
name="email"
value={formData.email}
onChange={handleChange}
className={errors.email ?  'error'  :  ''}
/>
{errors.email &&  <span>{errors.email}</span>}

<input
type="password"
name="password"
value={formData.password}
onChange={handleChange}
className={errors.password ?  'error'  :  ''}
/>
{errors.password &&  <span>{errors.password}</span>}
</form>
);
}

```

### Dynamic Form Fields

```jsx
function  DynamicForm()  {
const  [formData, setFormData]  =  useState({
name:  '',
skills:  [{  skill:  '',  level:  'beginner'  }]
});

const  addSkill  =  ()  =>  {
setFormData(prev  =>  ({
...prev,
skills:  [...prev.skills,  {  skill:  '',  level:  'beginner'  }]
}));
};

const  removeSkill  =  (index)  =>  {
setFormData(prev  =>  ({
...prev,
skills: prev.skills.filter((_, i)  => i !== index)
}));
};

const  updateSkill  =  (index, field, value)  =>  {
setFormData(prev  =>  ({
...prev,
skills: prev.skills.map((skill, i)  =>
i === index ?  {  ...skill,  [field]: value }  : skill
)
}));
};

return  (
<form>
<input
type="text"
name="name"
value={formData.name}
onChange={(e)  =>  setFormData(prev  =>  ({  ...prev,  name: e.target.value }))}
/>

{formData.skills.map((skill, index)  =>  (
<div key={index}>
<input
type="text"
value={skill.skill}
onChange={(e)  =>  updateSkill(index,  'skill', e.target.value)}
/>
<select
value={skill.level}
onChange={(e)  =>  updateSkill(index,  'level', e.target.value)}
>
<option value="beginner">Beginner</option>
<option value="intermediate">Intermediate</option>
<option value="advanced">Advanced</option>
</select>
<button type="button" onClick={()  =>  removeSkill(index)}>
Remove
</button>
</div>
))}

<button type="button" onClick={addSkill}>Add Skill</button>
</form>
);
}

```

Best Practices
--------------

### 1. Use Controlled Components

```jsx
// Good
<input value={value} onChange={handleChange}  />

// Avoid
<input defaultValue={value}  />

```

### 2. Proper Form Structure

```html
<form onSubmit={handleSubmit}>
<div className="form-group">
<label htmlFor="email">Email:</label>
<input
type="email"
id="email"
name="email"
value={formData.email}
onChange={handleChange}
required
/>
{errors.email &&  <span className="error-message">{errors.email}</span>}
</div>
</form>

```

### 3. Efficient State Updates

```jsx
// Good - prevents stale closures
setFormData(prevData  =>  ({  ...prevData,  [name]: value }));

// Avoid - can cause stale closures
setFormData({  ...formData,  [name]: value });

```

### 4. Error Handling

```jsx
const  handleSubmit  =  async  (event)  =>  {
event.preventDefault();

if  (!validateForm())  return;

setIsSubmitting(true);
try  {
await  submitForm(formData);
setIsSubmitted(true);
}  catch  (error)  {
setSubmissionError(error.message);
}  finally  {
setIsSubmitting(false);
}
};

```

Common Pitfalls
---------------

### 1. Forgetting preventDefault()

```jsx
const  handleSubmit  =  (event)  =>  {
event.preventDefault();  // Always include this!
// Handle form submission
};

```

### 2. Stale Closure Issues

```jsx
// Problematic
const  handleChange  =  (event)  =>  {
setFormData({  ...formData,  [event.target.name]: event.target.value });
};

// Better
const  handleChange  =  (event)  =>  {
setFormData(prevData  =>  ({  ...prevData,  [event.target.name]: event.target.value }));
};

```

### 3. Missing Loading States

```jsx
<button type="submit" disabled={isSubmitting}>
{isSubmitting ?  'Submitting...'  :  'Submit'}
</button>

```

Additional Resources
--------------------

### Documentation

-   [React Forms Documentation](https://reactjs.org/docs/forms.html)
-   [MDN Form Validation](https://developer.mozilla.org/en-US/docs/Learn/Forms/Form_validation)

### Libraries

-   [Formik](https://formik.org/) - Form library for React
-   [React Hook Form](https://react-hook-form.com/) - Performant forms with easy validation
-   [Yup](https://github.com/jquense/yup) - JavaScript schema validation

### Tools

-   [React Developer Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)
-   [Lighthouse](https://developers.google.com/web/tools/lighthouse) - Accessibility audit
-   

## 5. React Router & Navigation Tutorial
==================================

Introduction
------------

React Router is the standard routing library for React applications. It enables you to build single-page applications (SPAs) with multiple views that can be navigated without refreshing the page. This tutorial covers everything you need to know about React Router, from basic setup to advanced patterns.

What You'll Learn
-----------------

-   Single Page Application (SPA) concepts
-   React Router setup and configuration
-   Navigation components and patterns
-   Dynamic routing with parameters
-   Route protection and authentication
-   Nested routes and layouts
-   Performance optimization techniques

Why React Router Matters
------------------------

In traditional web applications, each page is a separate HTML file. When you click a link, the browser makes a new request to the server, loads a new page, and refreshes the entire content. This approach works but has several drawbacks:

-   Slower navigation: Each page load requires a full server round-trip
-   Loss of state: JavaScript state is lost between page loads
-   Poor user experience: Full page refreshes feel clunky
-   Increased server load: More requests to the server

React Router solves these problems by enabling client-side routing, where navigation happens entirely in the browser without server requests.

Core Concepts
-------------

### Single Page Applications (SPAs)

A Single Page Application loads once and then dynamically updates the content as users navigate. The URL changes, but the page doesn't refresh.

```
// Traditional multi-page app
// Page 1: /about.html
// Page 2: /contact.html
// Each click = new server request + full page reload

// SPA with React Router
// All navigation happens in JavaScript
// URL changes but no page refresh
// State is preserved between navigations

```

### Client-Side Routing

Client-side routing intercepts navigation attempts and renders the appropriate component based on the URL, all without making server requests.

```
// When user clicks a link or types a URL:
// 1. React Router intercepts the navigation
// 2. Determines which component to render
// 3. Updates the URL in the browser
// 4. Renders the new component
// 5. No server request needed!

```

Getting Started
---------------

### Installation

```bash
npm install react-router-dom
```

### Basic Setup

```jsx
// main.jsx
import React from  'react'
import ReactDOM from  'react-dom/client'
import  { BrowserRouter }  from  'react-router-dom'
import App from  './App.jsx'

ReactDOM.createRoot(document.getElementById('root')).render(
<React.StrictMode>
<BrowserRouter>
<App />
</BrowserRouter>
</React.StrictMode>,
)
```

```jsx
// App.jsx
import  { Routes, Route }  from  'react-router-dom'
import Home from  './pages/Home'
import About from  './pages/About'
import Contact from  './pages/Contact'

function  App()  {
return  (
<Routes>
<Route path="/" element={<Home />}  />
<Route path="/about" element={<About />}  />
<Route path="/contact" element={<Contact />}  />
</Routes>
)
}

export  default App

```

Navigation Components
---------------------

### Link Component

The ```Link``` component creates navigation links that don't cause a full page reload.

```jsx
import  { Link }  from  'react-router-dom'

function  Navigation()  {
return  (
<nav>
<Link to="/">Home</Link>
<Link to="/about">About</Link>
<Link to="/contact">Contact</Link>
</nav>
)
}

```

### NavLink Component

```NavLink``` is like ```Link``` but provides additional props for styling active links.

```jsx
import  { NavLink }  from  'react-router-dom'

function  Navigation()  {
return  (
<nav>
<NavLink
to="/"
className={({ isActive })  =>
isActive ?  'active-link'  :  'normal-link'
}
>
Home
</NavLink>
<NavLink
to="/about"
style={({ isActive })  =>  ({
fontWeight: isActive ?  'bold'  :  'normal'
})}
>
About
</NavLink>
</nav>
)
}

```

### useNavigate Hook

For programmatic navigation (like after form submission or button clicks).

```jsx
import  { useNavigate }  from  'react-router-dom'

function  LoginForm()  {
const navigate =  useNavigate()

const  handleSubmit  =  (event)  =>  {
event.preventDefault()
// Handle login logic
navigate('/dashboard')  // Navigate programmatically
}

return  (
<form onSubmit={handleSubmit}>
{/* form fields */}
<button type="submit">Login</button>
</form>
)
}

```

Dynamic Routing
---------------

### URL Parameters

Use ```:``` to define dynamic segments in your routes.

```jsx
// App.jsx
<Routes>
<Route path="/users/:id" element={<UserProfile />}  />
<Route path="/posts/:slug" element={<PostDetail />}  />
</Routes>

``````// UserProfile.jsx
import  { useParams }  from  'react-router-dom'

function  UserProfile()  {
const  { id }  =  useParams()

return  (
<div>
<h1>User Profile</h1>
<p>User ID:  {id}</p>
</div>
)
}

```

### Query Parameters

Access query string parameters using ```useSearchParams```.

```jsx
import  { useSearchParams }  from  'react-router-dom'

function  ProductList()  {
const  [searchParams, setSearchParams]  =  useSearchParams()
const category = searchParams.get('category')
const sort = searchParams.get('sort')

const  handleFilterChange  =  (newCategory)  =>  {
setSearchParams({  category: newCategory,  sort: sort ||  'name'  })
}

return  (
<div>
<h1>Products</h1>
{category &&  <p>Filtered by:  {category}</p>}
<button onClick={()  =>  handleFilterChange('electronics')}>
Electronics
</button>
</div>
)
}

```

Nested Routes
-------------

Nested routes allow you to create complex layouts with shared components.

```jsx
// App.jsx
import  { Routes, Route }  from  'react-router-dom'
import Layout from  './components/Layout'

function  App()  {
return  (
<Routes>
<Route path="/" element={<Layout />}>
<Route index element={<Home />}  />
<Route path="about" element={<About />}  />
<Route path="contact" element={<Contact />}  />
<Route path="blog" element={<Blog />}>
<Route index element={<BlogList />}  />
<Route path=":slug" element={<BlogPost />}  />
</Route>
</Route>
</Routes>
)
}

```

```jsx
// Layout.jsx
import  { Outlet }  from  'react-router-dom'
import Navigation from  './Navigation'

function  Layout()  {
return  (
<div>
<Navigation />
<main>
<Outlet />  {/* Child routes render here */}
</main>
<footer>Footer content</footer>
</div>
)
}

```

Route Protection
----------------

### Protected Routes

Create components that require authentication or specific permissions.

```jsx
// ProtectedRoute.jsx
import  { Navigate }  from  'react-router-dom'

function  ProtectedRoute({ children, isAuthenticated })  {
return isAuthenticated ? children :  <Navigate to="/login"  />
}

// Usage in App.jsx
<Route
path="/dashboard"
element={
<ProtectedRoute isAuthenticated={user.isLoggedIn}>
<Dashboard />
</ProtectedRoute>
}
/>

```

### Role-Based Access

```jsx
// RoleProtectedRoute.jsx
import  { Navigate }  from  'react-router-dom'

function  RoleProtectedRoute({ children, userRole, requiredRole })  {
return userRole === requiredRole ? children :  <Navigate to="/unauthorized"  />
}

// Usage
<Route
path="/admin"
element={
<RoleProtectedRoute userRole={user.role} requiredRole="admin">
<AdminPanel />
</RoleProtectedRoute>
}
/>

```

Advanced Patterns
-----------------

### Route Guards with Redirects

```jsx
// AuthGuard.jsx
import  { Navigate, useLocation }  from  'react-router-dom'

function  AuthGuard({ children })  {
const location =  useLocation()
const isAuthenticated =  checkAuthStatus()

if  (!isAuthenticated)  {
// Redirect to login with return URL
return  <Navigate to="/login" state={{  from: location }} replace />
}

return children
}

```

### Lazy Loading Routes

```jsx
// LazyRoute.jsx
import  { lazy, Suspense }  from  'react'

const LazyComponent =  lazy(()  =>  import('./HeavyComponent'))

function  LazyRoute()  {
return  (
<Suspense fallback={<div>Loading...</div>}>
<LazyComponent />
</Suspense>
)
}

// Usage in routes
<Route path="/heavy" element={<LazyRoute />}  />

```

### Custom Hooks for Navigation

```jsx
// useNavigation.jsx
import  { useNavigate, useLocation }  from  'react-router-dom'

function  useAppNavigation()  {
const navigate =  useNavigate()
const location =  useLocation()

const  goBack  =  ()  =>  navigate(-1)
const  goForward  =  ()  =>  navigate(1)
const  goHome  =  ()  =>  navigate('/')
const  goToProfile  =  (userId)  =>  navigate(```/users/${userId}```)

const  isCurrentPath  =  (path)  => location.pathname === path

return  {
goBack,
goForward,
goHome,
goToProfile,
isCurrentPath,
currentPath: location.pathname
}
}

```

Error Handling
--------------

### 404 Not Found

```jsx
// NotFound.jsx
import  { Link }  from  'react-router-dom'

function  NotFound()  {
return  (
<div>
<h1>404  - Page Not Found</h1>
<p>The page you're looking for doesn't exist.</p>
<Link to="/">Go Home</Link>
</div>
)
}

// Add to routes
<Route path="*" element={<NotFound />}  />

```

### Error Boundaries

```jsx
// ErrorBoundary.jsx
import  { Component }  from  'react'
import  { Link }  from  'react-router-dom'

class  ErrorBoundary  extends  Component  {
constructor(props)  {
super(props)
this.state =  {  hasError:  false  }
}

static  getDerivedStateFromError(error)  {
return  {  hasError:  true  }
}

render()  {
if  (this.state.hasError)  {
return  (
<div>
<h1>Something went wrong</h1>
<Link to="/">Go Home</Link>
</div>
)
}

return  this.props.children
}
}

```

Performance Optimization
------------------------

### Code Splitting

```jsx
// LazyRoute.jsx
import  { lazy, Suspense }  from  'react'

const Home =  lazy(()  =>  import('./pages/Home'))
const About =  lazy(()  =>  import('./pages/About'))

function  App()  {
return  (
<Suspense fallback={<div>Loading...</div>}>
<Routes>
<Route path="/" element={<Home />}  />
<Route path="/about" element={<About />}  />
</Routes>
</Suspense>
)
}

```

### Route-Based Data Fetching

```jsx
// PostDetail.jsx
import  { useParams, useNavigate }  from  'react-router-dom'
import  { useEffect, useState }  from  'react'

function  PostDetail()  {
const  { id }  =  useParams()
const navigate =  useNavigate()
const  [post, setPost]  =  useState(null)
const  [loading, setLoading]  =  useState(true)

useEffect(()  =>  {
async  function  fetchPost()  {
try  {
const response =  await  fetch(```/api/posts/${id}```)
if  (!response.ok)  {
navigate('/404')
return
}
const data =  await response.json()
setPost(data)
}  catch  (error)  {
navigate('/error')
}  finally  {
setLoading(false)
}
}

fetchPost()
},  [id, navigate])

if  (loading)  return  <div>Loading...</div>
if  (!post)  return  <div>Post not found</div>

return  (
<article>
<h1>{post.title}</h1>
<p>{post.content}</p>
</article>
)
}

```

Best Practices
--------------

### 1. Route Organization

```jsx
// Organize routes by feature
const routes =  [
{
path:  '/',
element:  <Layout />,
children:  [
{  index:  true,  element:  <Home />  },
{  path:  'about',  element:  <About />  },
{  path:  'contact',  element:  <Contact />  },
{
path:  'blog',
element:  <BlogLayout />,
children:  [
{  index:  true,  element:  <BlogList />  },
{  path:  ':slug',  element:  <BlogPost />  }
]
}
]
}
]

```

### 2. Consistent Navigation

```jsx
// Create a centralized navigation configuration
const navigationItems =  [
{  path:  '/',  label:  'Home'  },
{  path:  '/about',  label:  'About'  },
{  path:  '/contact',  label:  'Contact'  },
{  path:  '/blog',  label:  'Blog'  }
]

function  Navigation()  {
return  (
<nav>
{navigationItems.map(item  =>  (
<NavLink key={item.path} to={item.path}>
{item.label}
</NavLink>
))}
</nav>
)
}

```

### 3. URL State Management

```jsx
// Use URL state for filterable data
function  ProductList()  {
const  [searchParams, setSearchParams]  =  useSearchParams()
const  [products, setProducts]  =  useState([])

const category = searchParams.get('category')
const sort = searchParams.get('sort')

useEffect(()  =>  {
// Fetch products based on URL parameters
fetchProducts({ category, sort }).then(setProducts)
},  [category, sort])

const  updateFilters  =  (newFilters)  =>  {
setSearchParams(prev  =>  ({  ...prev,  ...newFilters }))
}

return  (
<div>
<FilterControls onFilterChange={updateFilters}  />
<ProductGrid products={products}  />
</div>
)
}

```

Common Pitfalls
---------------

### 1. Forgetting BrowserRouter

```jsx
// ❌ Wrong - Routes won't work
function  App()  {
return  (
<Routes>
<Route path="/" element={<Home />}  />
</Routes>
)
}

// ✅ Correct - Wrap with BrowserRouter
function  App()  {
return  (
<BrowserRouter>
<Routes>
<Route path="/" element={<Home />}  />
</Routes>
</BrowserRouter>
)
}

```

### 2. Using Anchor Tags Instead of Link

```jsx
// ❌ Wrong - Causes full page reload
<a href="/about">About</a>

// ✅ Correct - Uses client-side routing
<Link to="/about">About</Link>

```

### 3. Not Handling Route Parameters

```jsx
// ❌ Wrong - No error handling
function  UserProfile()  {
const  { id }  =  useParams()
const user = users.find(u  => u.id === id)  // Could be undefined

return  <h1>{user.name}</h1>  // Error if user not found
}

// ✅ Correct - Handle missing data
function  UserProfile()  {
const  { id }  =  useParams()
const user = users.find(u  => u.id === id)

if  (!user)  {
return  <div>User not found</div>
}

return  <h1>{user.name}</h1>
}

```

### 4. Stale Closures in Navigation

```jsx
// ❌ Wrong - Stale closure
function  SearchForm()  {
const  [query, setQuery]  =  useState('')
const navigate =  useNavigate()

const  handleSubmit  =  ()  =>  {
// query might be stale
navigate(```/search?q=${query}```)
}

return  (
<form onSubmit={handleSubmit}>
<input value={query} onChange={e  =>  setQuery(e.target.value)}  />
</form>
)
}

// ✅ Correct - Use current value
function  SearchForm()  {
const  [query, setQuery]  =  useState('')
const navigate =  useNavigate()

const  handleSubmit  =  (e)  =>  {
e.preventDefault()
navigate(```/search?q=${query}```)
}

return  (
<form onSubmit={handleSubmit}>
<input value={query} onChange={e  =>  setQuery(e.target.value)}  />
</form>
)
}

```

Testing React Router
--------------------

### Testing Routes

```jsx
// Route.test.jsx
import  { render, screen }  from  '@testing-library/react'
import  { BrowserRouter }  from  'react-router-dom'
import App from  './App'

test('renders home page',  ()  =>  {
render(
<BrowserRouter>
<App />
</BrowserRouter>
)

expect(screen.getByText('Home Page')).toBeInTheDocument()
})

```

### Testing Navigation

```jsx
// Navigation.test.jsx
import  { render, screen }  from  '@testing-library/react'
import userEvent from  '@testing-library/user-event'
import  { BrowserRouter }  from  'react-router-dom'
import Navigation from  './Navigation'

test('navigates to about page',  async  ()  =>  {
const user = userEvent.setup()

render(
<BrowserRouter>
<Navigation />
</BrowserRouter>
)

await user.click(screen.getByText('About'))
expect(window.location.pathname).toBe('/about')
})

```

Additional Resources
--------------------

### Documentation

-   [React Router Documentation](https://reactrouter.com/)
-   [React Router v6 Migration Guide](https://reactrouter.com/en/main/upgrading/v5)
-   [MDN History API](https://developer.mozilla.org/en-US/docs/Web/API/History_API)

### Advanced Topics

-   [Route-based code splitting](https://reactrouter.com/en/main/route/route#lazy)
-   [Data loading patterns](https://reactrouter.com/en/main/start/tutorial#loading-data)
-   [Error handling strategies](https://reactrouter.com/en/main/route/error-element)

### Tools and Libraries

-   [React Router DevTools](https://github.com/remix-run/react-router/tree/main/packages/react-router-devtools)
-   [React Router Examples](https://github.com/remix-run/react-router/tree/main/examples)

Summary
-------

React Router is essential for building modern React applications. Key takeaways:

1.  SPAs provide better user experience than traditional multi-page apps
2.  Client-side routing enables fast navigation without server requests
3.  Dynamic routes allow for parameterized URLs and flexible navigation
4.  Route protection enables authentication and authorization patterns
5.  Nested routes create complex layouts with shared components
6.  Performance optimization through code splitting and lazy loading

Master these concepts and you'll be able to build sophisticated, navigable React applications that provide excellent user experiences.

## 6. Context API & State Management Tutorial
**Introduction**
In this tutorial, you'll learn how to use React's Context API for global state management and how to integrate it with Material-UI (MUI) theming. The Context API is React's built-in solution for sharing state across multiple components without prop drilling, making it perfect for managing global application state like themes, user authentication, and shopping carts.

**Concepts Overview**
What is the Context API?
The Context API is a React feature that allows you to share data across multiple components without having to pass props down through every level of the component tree. This solves the "prop drilling" problem where you need to pass data through components that don't actually use it.

**When to Use Context**
Use Context when you have:

Global state that multiple components need access to
Theme data that affects the entire application
User authentication information
Shopping cart or other application-wide state
Language preferences or other user settings
When NOT to Use Context
Don't use Context for:

Local component state - use useState instead
Frequently changing data - can cause performance issues
Simple parent-child communication - props are more appropriate
Code Examples
Basic Context Setup
Let's start with a simple theme context:
```jsx
// ThemeContext.js
import React, { createContext, useContext, useState } from 'react';
```
```jsx
// 1. Create the context with a default value
const ThemeContext = createContext();
```
```jsx
// 2. Create a custom hook for using the context
export const useTheme = () => {
  const context = useContext(ThemeContext);
  if (!context) {
    throw new Error('useTheme must be used within a ThemeProvider');
  }
  return context;
};
```
```jsx
// 3. Create the provider component
export const ThemeProvider = ({ children }) => {
  const [isDarkMode, setIsDarkMode] = useState(false);
  
  const toggleTheme = () => {
    setIsDarkMode(prev => !prev);
  };

  // 4. Define the context value
  const value = {
    isDarkMode,
    toggleTheme,
    theme: isDarkMode ? 'dark' : 'light'
  };

  return (
    <ThemeContext.Provider value={value}>
      {children}
    </ThemeContext.Provider>
  );
};
```
Using Context in Components
```jsx
// Header.jsx
import React from 'react';
import { useTheme } from './contexts/ThemeContext';

const Header = () => {
  const { isDarkMode, toggleTheme } = useTheme();

  return (
    <header style={{ 
      backgroundColor: isDarkMode ? '#333' : '#fff',
      color: isDarkMode ? '#fff' : '#333'
    }}>
      <h1>My App</h1>
      <button onClick={toggleTheme}>
        Switch to {isDarkMode ? 'light' : 'dark'} mode
      </button>
    </header>
  );
};

export default Header;
```
MUI Theme Integration
Material-UI provides its own theming system that integrates beautifully with React Context:
```jsx
// ThemeProvider.js
import React, { createContext, useContext, useState } from 'react';
import { ThemeProvider as MuiThemeProvider, createTheme } from '@mui/material/styles';
import CssBaseline from '@mui/material/CssBaseline';

const CustomThemeContext = createContext();

export const useCustomTheme = () => {
  const context = useContext(CustomThemeContext);
  if (!context) {
    throw new Error('useCustomTheme must be used within a CustomThemeProvider');
  }
  return context;
};

export const CustomThemeProvider = ({ children }) => {
  const [isDarkMode, setIsDarkMode] = useState(false);

  const toggleTheme = () => {
    setIsDarkMode(prev => !prev);
  };

  // Create MUI theme with custom colors and typography
  const theme = createTheme({
    palette: {
      mode: isDarkMode ? 'dark' : 'light',
      primary: {
        main: isDarkMode ? '#90caf9' : '#1976d2',
        light: isDarkMode ? '#e3f2fd' : '#42a5f5',
        dark: isDarkMode ? '#1565c0' : '#0d47a1',
      },
      secondary: {
        main: isDarkMode ? '#f48fb1' : '#dc004e',
      },
      background: {
        default: isDarkMode ? '#121212' : '#ffffff',
        paper: isDarkMode ? '#1e1e1e' : '#ffffff',
      },
    },
    typography: {
      fontFamily: '"Roboto", "Helvetica", "Arial", sans-serif',
      h1: {
        fontSize: '2.5rem',
        fontWeight: 500,
      },
      h2: {
        fontSize: '2rem',
        fontWeight: 500,
      },
    },
    spacing: 8, // 8px spacing unit
    shape: {
      borderRadius: 8,
    },
  });

  const value = {
    isDarkMode,
    toggleTheme,
    theme
  };

  return (
    <CustomThemeContext.Provider value={value}>
      <MuiThemeProvider theme={theme}>
        <CssBaseline />
        {children}
      </MuiThemeProvider>
    </CustomThemeContext.Provider>
  );
};
```
Complex State Management with useReducer
For complex state that involves multiple actions, useReducer is often better than useState:
```jsx
// CartContext.js
import React, { createContext, useContext, useReducer, useEffect } from 'react';

const CartContext = createContext();

export const useCart = () => {
  const context = useContext(CartContext);
  if (!context) {
    throw new Error('useCart must be used within a CartProvider');
  }
  return context;
};

// Define action types as constants
const CART_ACTIONS = {
  ADD_ITEM: 'ADD_ITEM',
  REMOVE_ITEM: 'REMOVE_ITEM',
  UPDATE_QUANTITY: 'UPDATE_QUANTITY',
  CLEAR_CART: 'CLEAR_CART',
  LOAD_CART: 'LOAD_CART'
};

// Reducer function to handle state updates
const cartReducer = (state, action) => {
  switch (action.type) {
    case CART_ACTIONS.ADD_ITEM:
      const existingItem = state.items.find(item => item.id === action.payload.id);
      if (existingItem) {
        return {
          ...state,
          items: state.items.map(item =>
            item.id === action.payload.id
              ? { ...item, quantity: item.quantity + 1 }
              : item
          )
        };
      }
      return {
        ...state,
        items: [...state.items, { ...action.payload, quantity: 1 }]
      };

    case CART_ACTIONS.REMOVE_ITEM:
      return {
        ...state,
        items: state.items.filter(item => item.id !== action.payload)
      };

    case CART_ACTIONS.UPDATE_QUANTITY:
      return {
        ...state,
        items: state.items.map(item =>
          item.id === action.payload.id
            ? { ...item, quantity: action.payload.quantity }
            : item
        ).filter(item => item.quantity > 0)
      };

    case CART_ACTIONS.CLEAR_CART:
      return {
        ...state,
        items: []
      };

    case CART_ACTIONS.LOAD_CART:
      return {
        ...state,
        items: action.payload || []
      };

    default:
      return state;
  }
};

export const CartProvider = ({ children }) => {
  const [state, dispatch] = useReducer(cartReducer, {
    items: []
  });

  // Load cart from localStorage on mount
  useEffect(() => {
    const savedCart = localStorage.getItem('cart');
    if (savedCart) {
      try {
        const cartData = JSON.parse(savedCart);
        dispatch({ type: CART_ACTIONS.LOAD_CART, payload: cartData });
      } catch (error) {
        console.error('Error loading cart from localStorage:', error);
      }
    }
  }, []);

  // Save cart to localStorage whenever it changes
  useEffect(() => {
    localStorage.setItem('cart', JSON.stringify(state.items));
  }, [state.items]);

  // Action creators
  const addItem = (item) => {
    dispatch({ type: CART_ACTIONS.ADD_ITEM, payload: item });
  };

  const removeItem = (itemId) => {
    dispatch({ type: CART_ACTIONS.REMOVE_ITEM, payload: itemId });
  };

  const updateQuantity = (itemId, quantity) => {
    dispatch({ type: CART_ACTIONS.UPDATE_QUANTITY, payload: { id: itemId, quantity } });
  };

  const clearCart = () => {
    dispatch({ type: CART_ACTIONS.CLEAR_CART });
  };

  // Computed values
  const getTotalPrice = () => {
    return state.items.reduce((total, item) => total + (item.price * item.quantity), 0);
  };

  const getTotalItems = () => {
    return state.items.reduce((total, item) => total + item.quantity, 0);
  };

  const getItemQuantity = (itemId) => {
    const item = state.items.find(item => item.id === itemId);
    return item ? item.quantity : 0;
  };

  const value = {
    items: state.items,
    addItem,
    removeItem,
    updateQuantity,
    clearCart,
    getTotalPrice,
    getTotalItems,
    getItemQuantity
  };

  return (
    <CartContext.Provider value={value}>
      {children}
    </CartContext.Provider>
  );
};
```
Authentication Context Example
Here's how to create an authentication context:
```jsx
// AuthContext.js
import React, { createContext, useContext, useState, useEffect } from 'react';

const AuthContext = createContext();

export const useAuth = () => {
  const context = useContext(AuthContext);
  if (!context) {
    throw new Error('useAuth must be used within an AuthProvider');
  }
  return context;
};

export const AuthProvider = ({ children }) => {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    // Check for stored auth token on app load
    const token = localStorage.getItem('authToken');
    if (token) {
      validateToken(token);
    } else {
      setLoading(false);
    }
  }, []);

  const validateToken = async (token) => {
    try {
      const response = await fetch('/api/validate-token', {
        headers: { 
          'Authorization': ```Bearer ${token}```,
          'Content-Type': 'application/json'
        }
      });
      
      if (response.ok) {
        const userData = await response.json();
        setUser(userData);
      } else {
        // Token is invalid, remove it
        localStorage.removeItem('authToken');
        setUser(null);
      }
    } catch (error) {
      console.error('Token validation failed:', error);
      localStorage.removeItem('authToken');
      setUser(null);
    } finally {
      setLoading(false);
    }
  };

  const login = async (email, password) => {
    try {
      const response = await fetch('/api/login', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ email, password })
      });

      if (response.ok) {
        const { user: userData, token } = await response.json();
        localStorage.setItem('authToken', token);
        setUser(userData);
        return { success: true };
      } else {
        const errorData = await response.json();
        return { success: false, error: errorData.message || 'Login failed' };
      }
    } catch (error) {
      return { success: false, error: 'Network error' };
    }
  };

  const logout = () => {
    localStorage.removeItem('authToken');
    setUser(null);
  };

  const register = async (userData) => {
    try {
      const response = await fetch('/api/register', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(userData)
      });

      if (response.ok) {
        const { user: newUser, token } = await response.json();
        localStorage.setItem('authToken', token);
        setUser(newUser);
        return { success: true };
      } else {
        const errorData = await response.json();
        return { success: false, error: errorData.message || 'Registration failed' };
      }
    } catch (error) {
      return { success: false, error: 'Network error' };
    }
  };

  const value = {
    user,
    loading,
    login,
    logout,
    register,
    isAuthenticated: !!user
  };

  return (
    <AuthContext.Provider value={value}>
      {children}
    </AuthContext.Provider>
  );
};
```
### Practical Exercises
**Exercise 1: Basic Theme Context**
Create a simple theme context and implement it in a basic app:

// 1. Create ThemeContext.js with light/dark mode
// 2. Create a Header component that uses the theme
// 3. Create a Main component that displays content
// 4. Wrap your app with ThemeProvider
// 5. Test theme switching functionality

**Exercise 2: MUI Theme Integration**
Integrate your theme context with MUI:

// 1. Install MUI: npm install @mui/material @emotion/react @emotion/styled
// 2. Update your ThemeProvider to use MuiThemeProvider
// 3. Create custom theme colors and typography
// 4. Use MUI components in your app
// 5. Test responsive design and dark mode

**Exercise 3: Shopping Cart Context**
Build a shopping cart using Context and useReducer:

// 1. Create CartContext with useReducer
// 2. Implement add, remove, update quantity actions
// 3. Add localStorage persistence
// 4. Create cart display components
// 5. Test cart functionality

**Exercise 4: Multiple Contexts**
Combine multiple contexts in one application:

// 1. Create both ThemeContext and CartContext
// 2. Create AuthContext for user management
// 3. Show how to compose multiple providers
// 4. Create components that use multiple contexts
// 5. Test all functionality together

### Best Practices
**1. Context Organization**
```jsx
// Good: Separate contexts by concern
const ThemeContext = createContext();
const AuthContext = createContext();
const CartContext = createContext();

// Bad: One giant context for everything
const AppContext = createContext();
```
**2. Custom Hooks**
```jsx
// Good: Create custom hooks for context usage
export const useTheme = () => {
  const context = useContext(ThemeContext);
  if (!context) {
    throw new Error('useTheme must be used within a ThemeProvider');
  }
  return context;
};

// Bad: Using useContext directly in components
const theme = useContext(ThemeContext); // No error handling
```
**3. Performance Optimization**
```jsx
// Good: Split contexts to avoid unnecessary re-renders
const ThemeContext = createContext();
const UserContext = createContext();

// Bad: Putting frequently changing data with stable data
const AppContext = createContext(); // Contains both theme and user data
```
**4. Error Handling**
```jsx
// Good: Always check if context exists
export const useTheme = () => {
  const context = useContext(ThemeContext);
  if (!context) {
    throw new Error('useTheme must be used within a ThemeProvider');
  }
  return context;
};

// Bad: No error handling
export const useTheme = () => useContext(ThemeContext);
```
**5. Default Values**
```jsx
// Good: Provide meaningful default values
const ThemeContext = createContext({
  isDarkMode: false,
  toggleTheme: () => {},
  theme: 'light'
});

// Bad: No default value
const ThemeContext = createContext();
```
### Common Pitfalls
**1. Overusing Context**
```jsx
// Bad: Using context for local state
const LocalStateContext = createContext();

// Good: Use useState for local state
const [count, setCount] = useState(0);
```
**2. Creating Context in Render**
```jsx
// Bad: Creating context inside component
function MyComponent() {
  const MyContext = createContext(); // This creates a new context on every render!
  // ...
}

// Good: Create context outside component
const MyContext = createContext();

function MyComponent() {
  // ...
}
```
**3. Not Memoizing Context Value**
```jsx
// Bad: Creating new object on every render
function MyProvider({ children }) {
  const [state, setState] = useState({});
  
  return (
    <MyContext.Provider value={{ state, setState }}>
      {children}
    </MyContext.Provider>
  );
}

// Good: Memoize the context value
function MyProvider({ children }) {
  const [state, setState] = useState({});
  
  const value = useMemo(() => ({ state, setState }), [state]);
  
  return (
    <MyContext.Provider value={value}>
      {children}
    </MyContext.Provider>
  );
}
```
**4. Missing Provider**
```jsx
// Bad: Using context without provider
function MyComponent() {
  const theme = useTheme(); // Error: useTheme must be used within a ThemeProvider
  return <div>{theme}</div>;
}

// Good: Wrap with provider
function App() {
  return (
    <ThemeProvider>
      <MyComponent />
    </ThemeProvider>
  );
}
```
Additional Resources
Documentation
React Context API
MUI Theming
useReducer Hook
useContext Hook
Tools and Libraries
React DevTools - For debugging context
MUI Theme Builder - For creating custom themes
Redux DevTools - For debugging useReducer
Advanced Topics
Context Composition Patterns
Performance Optimization
Testing Context
Context vs Redux
Example Projects
E-commerce Cart with Context
Theme Switching App
Authentication with Context
Remember: Context API is a powerful tool for global state management, but use it judiciously. Start with local state (useState) and only move to Context when you need to share state across multiple components that don't have a direct parent-child relationship.

## 7. React Deploy on Vercel

Intro
=====

Hey there, future developers! Today, we're diving into the exciting world of deploying React applications with GitHub Actions and Vercel. Ever wondered how to seamlessly launch your creations into the digital space? Well, we've got you covered! We'll start by demystifying deployment, exploring different platforms, and then zooming in on the fantastic features of Vercel. Along the way, we'll get hands-on with configurations, GitHub repositories, Vercel CLI, and access tokens. Get ready to elevate your coding game as we embark on this journey to make your React projects shine online! Let's deploy and amaze the web!

* * * * *

Cloud Service Providers
=======================

Once you are done building your application you will need to host these apps, and that's where cloud service providers come into play; these are also known as hosting platforms or cloud platforms, are services that provide the infrastructure and tools necessary to deploy, host, and manage applications or websites on the internet. Here's a brief overview of three major providers:

![Untitled.png](https://cdn.disco.co/media/Untitled_5a3bcc4b-ca48-4e3b-82ec-b3a6b283b53a.png)

* * * * *

Amazon Web Services (AWS)
-------------------------

![Untitled.png](https://cdn.disco.co/media/Untitled_27199296-4e68-4b65-aac9-21ca1a376a4d.png)

-   Overview: AWS is a leading cloud platform offering a wide range of services, including compute, storage, databases, and more.
-   CD Tools: AWS CodePipeline, AWS CodeDeploy, AWS CodeBuild.
-   Benefits: Scalability, reliability, extensive service offerings, and strong community support.

Microsoft Azure
---------------

![Untitled.png](https://cdn.disco.co/media/Untitled_1f00c5ad-af80-4386-9d32-c8200811cc42.png)

-   Overview: Azure is Microsoft's cloud computing platform, providing services for building, deploying, and managing applications and services.
-   CD Tools: Azure DevOps, Azure Pipelines, Azure App Service.
-   Benefits: Seamless integration with Microsoft technologies, hybrid cloud capabilities, and enterprise-grade security features.

Google Cloud Platform (GCP)
---------------------------

![Untitled.png](https://cdn.disco.co/media/Untitled_b2287730-27a9-4b23-a9c1-bea69cbcd456.png)

-   Overview: GCP offers cloud computing services for building and deploying applications on Google's infrastructure.
-   CD Tools: Cloud Build, Cloud Deployment Manager, Google Kubernetes Engine (GKE).
-   Benefits: Advanced machine learning capabilities, global network infrastructure, and comprehensive data analytics tools.

Free Options to Deploy Services
-------------------------------

For developers and small businesses looking to deploy services without incurring significant costs, several free options are available:

-   AWS Free Tier: AWS offers a limited free tier with access to various services, allowing users to experiment and deploy applications at no cost for a certain period.
-   Azure Free Account: Microsoft Azure provides a free account with access to popular services and a credit to explore additional offerings.
-   Google Cloud Free Tier: GCP offers a free tier with access to core services, allowing users to run small workloads and learn about the platform.

These free options provide an excellent opportunity for beginners to get hands-on experience with cloud deployment while minimizing expenses.

* * * * *

Other Cloud Platforms for Deploying Services
============================================

![Untitled.png](https://cdn.disco.co/media/Untitled_34bb35a6-645a-4990-b802-f1c2b8592873.png)

In addition to the major cloud service providers like AWS, Azure, and GCP, there are several other platforms tailored to specific needs or preferences. Here are some notable ones:

### Heroku

![Untitled.png](https://cdn.disco.co/media/Untitled_c919ba9b-39c6-4f37-9d02-1bb57af4bcc9.png)

-   Overview: Heroku is a cloud platform that enables developers to build, deploy, and scale applications effortlessly. It is known for its simplicity and ease of use.
-   CD Tools: Heroku CI/CD, Heroku Pipelines.
-   Benefits: Quick deployment, support for multiple programming languages, and a wide range of add-ons and integrations.

### Render

![Untitled.png](https://cdn.disco.co/media/Untitled_61462d6d-7c18-4632-888b-6dd37c6a6034.png)

-   Overview: Render is a modern cloud platform that simplifies the deployment and scaling of web applications, databases, and static sites.
-   CD Tools: Native CI/CD, GitHub Actions.
-   Benefits: Fully managed infrastructure, automatic scaling, and a straightforward pricing model.

### Vercel (formerly Zeit)

![Untitled.png](https://cdn.disco.co/media/Untitled_eebf6609-9375-468f-adaf-540426c52cf9.png)

-   Overview: Vercel is a cloud platform optimized for deploying serverless functions, static websites, and front-end applications.
-   CD Tools: Vercel CLI, GitHub integration.
-   Benefits: Instant deployment, global CDN, and built-in support for Next.js.

### Netlify

![Untitled.png](https://cdn.disco.co/media/Untitled_fc1684b9-63d9-4bab-8bca-b78c38977979.png)

-   Overview: Netlify is a platform for modern web development, providing hosting, serverless functions, and continuous deployment.
-   CD Tools: Netlify CI/CD, GitHub/GitLab/Bitbucket integration.
-   Benefits: Seamless integration with Git, automatic SSL, and built-in form handling.

### Firebase

![Untitled.png](https://cdn.disco.co/media/Untitled_e2818ec0-eb7a-4d9f-95c7-d17a124e47ce.png)

-   Overview: Firebase is a mobile and web application development platform that provides hosting, real-time database, authentication, and more.
-   CD Tools: Firebase CLI, Firebase Hosting.
-   Benefits: Scalability, real-time updates, and a comprehensive suite of services for building and deploying applications.

### DigitalOcean App Platform

![Untitled.png](https://cdn.disco.co/media/Untitled_57289653-9eba-4fe2-9fc1-2e6b916764ad.png)

-   Overview: DigitalOcean's App Platform is a platform-as-a-service (PaaS) offering that simplifies the deployment and scaling of containerized applications.
-   CD Tools: Native CI/CD, GitHub/GitLab integration.
-   Benefits: Automatic scaling, managed infrastructure, and built-in database support.

* * * * *

Deploying React application in Vercel with GitHub Actions
=========================================================

Now, we'll walk you through deploying a React application in Vercel using GitHub Actions. This process is known as Continuous Deployment (CD), where changes made to your code are automatically deployed to your server.

Introduction to Vercel
----------------------

![Untitled.png](https://cdn.disco.co/media/Untitled_cde5c50f-e014-48fb-b66f-ed5d5e3a35bc.png)

Vercel provides a swift and uncomplicated method for deploying web projects, featuring automatic scaling and compatibility with contemporary web technologies such as serverless functions. The platform includes a global content delivery network (CDN) and automatic HTTPS, facilitating the seamless distribution of web content worldwide, and ensuring both security and dependability.

Moreover, Vercel boasts a user-friendly interface and seamless integrations with well-known development tools like GitHub, GitLab, and Bitbucket, streamlining the setup and management of your projects. Additionally, Vercel extends a generous free plan encompassing various features, making it an excellent choice for small-scale projects and personal usage.

💡 Learn more about Vercel here: [Resource
](https://vercel.com/)

* * * * *

Configurations for Vercel
-------------------------

First, we are going to need a Vercel Account.

-   Go here <https://vercel.com/>
-   Click on Sign Up in the upper right hand corner
-   Choose you're working on personal projects
-   Put in your name
-   Continue with GitHub
-   Authorize Vercel to do all the things
-   Skip the questions about the project

Now that we're in Vercel, we will need to create a new project there and transfer over an already existing GitHub repository into the new Vercel project.

NOTE: You can use any of the previous projects you've created and pushed to GitHub or you can use the ```vercel-trivia.zip``` project attached to this lesson.

READ: If you choose to use ```vercel-trivia.zip``` you will need to:

-   create a repository on GitHub
-   download and unzip the contents of ```vercel-trivia.zip```  into a folder
-   connect that folder with the newly created GitHub repository like you've done many times before
-   push the project up to GitHub

Once this is complete, then move on (:

Vercel
------

Now that we have our chosen GitHub repository/project, we can set it up in Vercel.

If you are currently on the Overview tab you will want to click on Add New... and choose Project or click on Import:

![image.png](https://cdn.disco.co/media/image_2c58d41b-0824-4082-af5a-ebf82a89e980.png)

That will take you to this screen (see below). Now click on the Install button with the GitHub Logo on it:

![image.png](https://cdn.disco.co/media/image_a977177b-4d7f-41a7-8bdf-157357dbaac7.png)

Sign into your GitHub account if it prompts you to do so (this should only happen if you're not already logged in):

![image.png](https://cdn.disco.co/media/image_4b3df081-f007-441c-87d4-9fd41f77a2a5.png)
If it asks you where to install it, choose the right account (this may or may not happen to you):

![image.png](https://cdn.disco.co/media/image_5bd69cc2-7c3b-47df-b5cf-23b8294e58d0.png)

Choose Only select repositories
Click on Select repositories
Choose your-github-username/vercel-trivia or the other repository you want to deploy to Vercel:

![image.png](https://cdn.disco.co/media/image_25b38d41-4c8f-464f-98c1-ad3f9a56e971.png)
Scroll further down and click on Install

![image.png](https://cdn.disco.co/media/image_fa190e7e-1762-454d-bcb9-9a3f72fd5e0e.png)

It will take you back to the main Vercel page
The chosen repository should show
Click on the Import button:

![image.png](https://cdn.disco.co/media/image_854d0409-00ae-494c-8192-0127cc47d712.png)

It will take you to another page where you can double check all the settings/selections
The Project Name will need to be unique from every other Vercel app on their platform
We shouldn't have to change anything else
Click on Deploy

![image.png](https://cdn.disco.co/media/image_7c9ad6cd-a859-4a1a-bae7-b957fe446c11.png)
Vercel automatically detects all the needed dependencies for deploying our app and installs/configures them for us

![Captura de pantalla 2024-02-28 a las 15.34.11.png](https://cdn.disco.co/media/Captura_de_pantalla_2024-02-28_a_las_15_34_11_1eff957e-61a7-428f-9e4c-d6f5f08b75cb.png)
Once it's done we should get a screen that looks like the image below:

Keep this window open

To view the live app, click on the image/screenshot of the application and it will take you to the URL of the deployed application

![image.png](https://cdn.disco.co/media/image_ab936dcd-46c5-4bae-b63f-218d2ffb59bf.png)
In our case it's <https://vercel-trivia.vercel.app/>

Yours will be different.

Here is what it will look like (your URL will be different):