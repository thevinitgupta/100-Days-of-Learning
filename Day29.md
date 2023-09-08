# Building Lynkit 🔗 - Adding Routers and the 404 Page(It looks really cool)
For adding new pages, routing is really important. `react-router-dom` is an amazing library that provides this functionality in React easily.


And the best part is 👉 : **Setting up routing in your React application is easier than making a cup of coffee** (well, almost). Let's dive into it : 
## Step 1: Configuring The Router

This is where the magic begins. First, import the router you need - `BrowserRouter` for web. Then, wrap your entire app in this router. It's like giving your app a GPS!

```jsx
import React from "react"
import ReactDOM from "react-dom/client"
import App from "./App"
import { BrowserRouter } from "react-router-dom"

const root = ReactDOM.createRoot(document.getElementById("root"))
root.render(
  <React.StrictMode>
    <BrowserRouter>
      <App />
    </BrowserRouter>
  </React.StrictMode>
)
```

Normally, you'll do this in your `index.tsx` file or the `main.tsx` file in Vite⚡ apps. 

> The router acts like a friendly context provider, giving your app all the routing superpowers it needs.

## Step 2: Defining Routes

Now, let's tell our router where to send our users. Define your routes at the top level of your app, usually in the `App` component, but you can get creative if you want!

```jsx
import "./App.css";
import Landing from "./pages/Landing";
import { Route, Routes } from "react-router-dom";
import Auth from "./pages/Auth";
import Navbar from "./components/Navbar";
import NotFound from "./pages/NotFound";

function App() {
  return (
    <div className={`h-screen w-screen`}>
      <Navbar/>
      {/* <img id='background-image' alt="background gradient"/> */}
      <Routes>
      <Route path="/" element={<Landing />}/>
        
      <Route path="/auth" element={<Auth />} />
      <Route path="*" element={<NotFound/>}/>
      </Routes>
    </div>
  );
}

export default App;
```

It's as easy as creating a route for each destination and wrapping them in a `Routes` component. When your URL changes, React Router will handle the rest.

### Note : The * path is use to specify the URLs that are not defined, so we create a NotFound component and render it. React router is intelligent enough to detect which routes are not defined and then render the Not Found element accordingly.


## Step 3: Handling Navigation

Time to make our app interactive! Instead of regular anchor tags, we use React Router's super-smooth `Link` component for navigation.
> ![NOTE]
> I have defined the Navbar outside the Routes section for smooth transition between the pages.

```jsx

// Navbar Component
<ul aria-label='menu' className={`flex flex-1 justify-center gap-8 md:gap-20 items-center font-heading text-md md:text-lg`}>
        <Link  to="/trending" className={``}>
                <span className={`hidden md:inline-block`}>Trending</span>
                <FaArrowTrendUp className={`inline-block md:hidden`}/>
              </Link>
              <Link  to="https://github.com/thevinitgupta" className={``}>
                <span className={`hidden md:inline-block`}>Code</span>
                <FaGithub className={`inline-block md:hidden`}/>
              </Link>
              <Link  to="/auth" className={``}>
                <span className={`hidden md:inline-block`}>Profile</span>
                <BsPersonFill className={`inline-block md:hidden`}/>
              </Link>
 </ul>

```

We've spiced things up with a navigation menu, and notice we use the `to` prop instead of `href`. This keeps everything snappy and smooth.
    
## And the cool 404 page : 


https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/aa7b2dba-efe8-4e5e-8997-ed1b7ccd617e




And voila! You're now ready to explore the wonderful world of routing in your React app. Go ahead, have fun navigating different pages while your app stays snappy and responsive. Happy coding! 🚀
