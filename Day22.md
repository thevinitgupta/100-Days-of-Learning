# Adding an Animated Blob to Your Next.js App
Today, I took a break from my Backend development and decided to try something new on my Portfolio
### A blurry blob that follows my cursor.

In this guide, we'll walk you through the process of how I added the animated blob that follows the mouse cursor. 

> The blob will have a blur effect and remain visible on all screens.

## Step 1: Create a CSS Gradient
A simple blob would not look good, so use a Gradient generator like : [CSS Gradient](https://cssgradient.io/) to create a gradient background that you can add to your blob.

I used this one : 
![CSS Gradient IO](https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/54363f55-1c7b-4368-bcb1-09b51b9510e6)

Now that I had a gradient, I opened my [Portfolio Project](https://thevinitgupta.netlify.app) 👈 (How it works)

## Step 2: Create a Global JavaScript File
- Inside your project directory, create a folder named `public` if it doesn't exist.

- Inside the public folder, create a new JavaScript file named `global.js`.

- Open the `global.js` file and add the following code:

```javascript

    const blob = document.createElement('div');
    blob.className = 'blob';
    document.body.appendChild(blob);

    document.addEventListener('mousemove', (e) => {
      const x = e.clientX;
      const y = e.clientY;
      blob.style.transform = `translate(${x}px, ${y}px)`;
    });
```

## Step 3: Add Global Styles

 - Create a directory named `styles` in the root of your project if it doesn't exist.

 - Inside the styles directory, create a new CSS file named `globals.css`.

 - Open the `globals.css` file and add the following code:

```css
    .box{
  position: fixed;
  filter: blur(100px);
  z-index : -1;
  top : 50%;
  left : 50%;
  translate : -50% -50%;
  height : 100px;
  width : 100px;
  border-radius : 50%;
  background: rgb(158,60,207);
background: linear-gradient(90deg, rgba(158,60,207,1) 0%, rgba(29,71,253,1) 61%, rgba(69,252,225,1) 100%);
 animation : rotate 5s infinite;
}


@keyframes rotate {
  0% {
    rotate : 0deg;
  }
  50%{
    rotate : 180deg;
    transform : 1 1.3;
  }
  100%{
    rotate : 360deg;
  }
}
```
> 📌 The Animation function rotates the blob and in the middle of the rotation changes it's size.
> 
## Step 4: Include the Global JavaScript and Styles
- Open the  `_app.js` (or _app.tsx if you're using TypeScript) file inside the pages directory.

- Add the following lines at the top of the file:

```jsx
import '../styles/globals.css'; // Include global styles
import Script from 'next/script'; // Import Script component from Next.js
```

 - Modify the MyApp component to include the global JavaScript and styles using the Script component:

```jsx
    function MyApp({ Component, pageProps }) {
      return (
        <>
          {/* Include global JavaScript */}
          <Script src="/global.js" strategy="beforeInteractive" />
          <Component {...pageProps} />
        </>
      );
    }
```

## Step 5: Run Your Next.js Application

Start your Next.js development server using the following command:

```bash
    npm run dev
```
Open your web browser and visit `http://localhost:3000`. 
### You should see your Next.js application with the animated blob that follows your mouse cursor and has a blur effect something like this : 👇

https://github.com/thevinitgupta/100-Days-of-Learning/assets/65801700/24377ae8-c9e4-4640-967f-8e05d41eca31

Congratulations 🎉🥳! You've successfully added an animated blob with a blur effect that follows the mouse cursor to your Next.js application. 

Feel free to customize the styles and animation to match your preferences.
