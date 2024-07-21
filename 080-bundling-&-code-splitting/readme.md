# Bundling vs Code Splitting

## Bundling

**Bundling** is the process of taking multiple JavaScript, CSS, and other files and combining them into one or more bundles. The primary goal of bundling is to reduce the number of HTTP requests a web application needs to make to load its resources, which improves load times and performance.

#### How Bundling Works

- **Combining Files:** All JavaScript files, for example, are combined into a single file. Similarly, CSS files can be combined into a single stylesheet.
- **Tools:** Common bundling tools include Webpack, Rollup, and Parcel. These tools can also handle other tasks like minification and transpilation.
- **Optimization:** Bundlers often come with optimization techniques like tree shaking to remove unused code, leading to smaller bundle sizes.

## Code Splitting

**Code splitting** is a technique that allows you to split your code into smaller chunks which can be loaded on demand. This is particularly useful for improving the performance of large web applications by only loading the necessary code when it is needed.

#### How Code Splitting Works

- **Dynamic Imports:** Modern bundlers support dynamic `import()` statements which allow you to load modules dynamically.
- **Route-Based Splitting:** Split code by routes in a single-page application (SPA) so that each route only loads its necessary code.
- **Component-Based Splitting:** Split code by components so that large components or libraries are only loaded when they are actually used.

### Differences Between Bundling and Code Splitting

| Feature                | Bundling                                                       | Code Splitting                                      |
| ---------------------- | -------------------------------------------------------------- | --------------------------------------------------- |
| **Purpose**            | Combine multiple files into a single file or fewer files       | Split code into smaller, loadable chunks            |
| **Performance Impact** | Reduces HTTP requests but can lead to large initial file sizes | Reduces initial load size by loading code on demand |
| **Tools**              | Webpack, Rollup, Parcel                                        | Webpack, Rollup, React.lazy, React.Suspense         |
| **Use Cases**          | Small to medium-sized applications                             | Large applications, SPAs with multiple routes       |

### Combining Bundling and Code Splitting

In modern web development, it's common to use both bundling and code splitting together. Bundling is used to combine related files into optimized bundles, while code splitting ensures that the application only loads the necessary code when required.

#### Example: React Application with Code Splitting

```javascript
import React, { Suspense, lazy } from "react";
import ReactDOM from "react-dom";

const LazyComponent = lazy(() => import("./LazyComponent"));

function App() {
  return (
    <div>
      <Suspense fallback={<div>Loading...</div>}>
        <LazyComponent />
      </Suspense>
    </div>
  );
}

ReactDOM.render(<App />, document.getElementById("root"));
```

### Conclusion

- **Bundling** helps reduce the number of HTTP requests and optimizes the size of assets by combining them.
- **Code splitting** improves performance by loading code only when it is needed, thus reducing the initial load time of an application.
- Using both techniques together, developers can create highly performant and scalable web applications.
