#personal #webdev

(also see [[Brief Pointers about NextJS]])
# Server and Client Side Rendering
NextJS components by default are all server side components which cannot handle user interaction or hooks. Client side components cannot perform server-side rendering but can handle user interaction and hooks.
# File Colocation
A route only becomes publicly accessible when we add the page.tsx file to it. The browser only gets what is returned by the page.tsx through a default exported component. This prevents components inside the app dir to accidently become routes themselves. It is recommended to keep components in a seperate Components dir in the src dir.

# Private Folders
Private folders contain internal code. They are excluded from the routing system. Private folders can be created by simply starting a dir name with _

# Route Groups
They are the only way in Next.js to share a layout between routes without affecting the URL. To create Route Groups, place the group folder name within parenthesis. This tells Nextjs to treat the folder is used only to organise routes without affecting the URL. Route groups can be nested.

# Layouts
They are used to share UI between multiple pages in the app. They can be implemented through route groups. Nextjs provides a layout by default as the Root Layout in the app folder and is not optional(to the point that Nextjs will auto generate the app on each reload). Nested layouts can be created for a specific group of pages as follows.

```
export default function ProductDetailsLayout({
	children,
}: {
	children: React.ReactNode;
    }){
	return(
	<>
		{children}
		/*
		Layout components
		*/
	</>
	)
}
```

==See "Multiple Route Layouts" under "Layouts" in [[Brief Pointers about NextJS]]==

# Search Engine Optimization with metadata
The metadata API lets us define metadata for each page which is used when the page is shared or indexed by a search engine.

In layout or page .tsx files we can either
1. export a static metadata object 
2. export a dynamic _generateMetadata_ function
==Layout metadata applies to all of its pages while page metadata is specific to that page. Metadata follows a top-down order, starting from root level. Page overrides layout metadata when applied on the same properties. Both static and dynamic metadata cannot be used in the same route segment==

==Metadata do not work in pages with 'use client' directive. To overcome this, seperate the client side logic as a seperate component==

## Title Metadata
It can be either set using a string or object. Its primary purpose is to set the title of the document.

In object, the default property will set the title for any child pages that dont define a title. The template property will add prefixes and suffixes to the title. Absolute will replace the default titles of the parent segment.

# Linking and Navigation
The `<Link` component extends the HTML anchor component for navigation. It is imported from "next/link"

## params and SearchParams
_params_ is a promise that resolves to an object containing the dynamic route parameters(like id).

_searchParams_ is a promise that resolves to an object containing the query parameters(like filters and sorting)

Since these are server components, we have to use the hook `use` to use them in client components.

`page.tsx` can access both of these values whereas `layout.tsx` can access only params.

## Navigating Programmatically
The `useRouter` component is a client component that is used to navigate programmatically.

## Templates
Layouts keep the common components intact and only mount the exclusive components when switching to different pages to increase performance. To change this, we use Template files as alternatives to layout files. The difference between templates and layouts is that templates generate new comopnents on each naviagation. A new template component instance is mounted, DOM elements recreated, states are cleared, effects are re-syncronized.

They can be used together with layouts. In this case, layouts are rendered first and then the children are replaced by template components.

## Loading Pages
They create loading states that appear instantly to let users know the page is active.

# Error Handling
skipped
# Parallel Routes
Parallel routes are implemented through a feature called **slots**. To create slots we use the `@folder` naming convention. Each defined slot automatically becomes a prop in its `layout.tsx`. These are not route segments. We get a 404. The children prop is an implicit slot.

They allow independent route handling(show loading states, errors etc).

It also allows sub-navigation, ie, independent interaction of the components.

## Unmatched Routes
We we navigate to different routes in the individual slots, the other slots become unmatched and their content do not change. If we reload the page with the slots, the `default.tsx` file in each unmatched slot act as the fallback, otherwise we see a 404. This happens because the active state of that slot could not be fetched. To fix this create `default.tsx` pages under each of the 4 slot route folders.

## Intercepting Routes
It allows for loading of a route from another part of the app while keeping the user in the current context and within the same layout(eg. login modal with /login url, enlarged photo modal with /photo/[id] url).

# Route Handlers
They enable custom request handlers for routes using RESTful endpoints without configuring a separate server using Node+Express.

They can make API requests that run server-side, hence ensuring that private keys stay secure. Next.js supports GET, POST, PUT, PATCH, DELETE, HEAD and OPTIONS. For unsupported methods, Next.js returns a 405 Method Not Allowed response.

Each route handler function gets a standard web request object as a parameter.

PATCH and DELETE requests require a dynamic segment like [id] in their endpoint.

## Headers
HTTP headers represent important metadata associated with an API request and response

**_Request Headers_** are sent by the client(eg web browser) to a server with information about the request such as "User-Agent" that identifiers the OS and the browser, "Accept" which indicates the type of data the client can process and "Authorization" used by the client to authenticate itself for resources. 

**_Response Headers_** are sent back from server to client and with information about the response such as "Content-Type" which indicates the type of response sent back('application/json' for JSON, 'text/html' for HTML documents etc)

## Cookies
They serve mainly 3 purposes: managing sessions, handling personalization, tracking.

## Caching
It is preferable to cache the data that rarely changes since otherwise each request results in a database query which is inefficient.

Caching is not implemented in development mode and only for GET methods. It also does not work with dynamic functions like headers(), cookies() and while working with the _request_ object.

To re-validate cached data, we use "Incremental Static Regeneration". 

## Middleware
They allow for the interception and control flow of requests and responses throughout the app on a global level. They can significantly enhance redirects, URL rewrites, authentication, headers, cookies and more. 

To specify where the middleware will be active, we can use "Custom matcher config" or "Conditional statements".

# Rendering
Rendering refers to transforming the written code to user interfaces which can be interacted with. The important part is deciding when these transformations should occur.

Rendering in React initially was Client-Side Rendering(CSR) of Single Page Applications(SPAs). This had disadvantages with SEO since the intial html was just an empty div with a reference to `bundle.js`. It had low performance since user had to wait while the browser downloads and renders all the content. The bigger the `bundle.js` becomes, the longer is the wait. In Server-Side Rendering(SSR), the server renders the HTML once it gets the request. It then sends the content to the browser. However, the page cannot begin interaction until the request is sent, rendered and downloaded back, called hydration.
![[Pasted image 20260409111526.png]]

SS Solutions can be of type Static Site Generation(SSG). This occurs at build time and is suitable for content that does not change, eg blog posts. Server-Side Rendering(SSR) however, generates pages on-demand, mainly for personalized web pages like a home feed. SSR creates a "all or nothing" waterfall effect with the process of fetching, downloading JS and hydration which is very inefficient.

In Suspense SSR, we can utilize HTML streaming, which can fetch and display particular sections asynchronously. Furthermore, Selective Hydration allows asynchronous hydration of particular segments. React manages this automatically and further prioritizes portions related to user interactivity.

## React Server Components
In RSC, the Client Components primarily run on the client, but should also run once on the server for better optimization. They have access to the entire client environment.

The Server Components operate only on the server. This code is never downloaded and hence reduce the bundle size and skip the hydration step. They have direct access to server resources. It also has advantages like security, fetch optimization, caching, SEO etc.

In short, server components handle fetching and static rendering while client components handle interactivity.

The App Router in Next.js is build on the RSC architecture and all the corresponding benefits are built-in.

Note that a `console.log()` does not appear in the terminal unless we reload the page at which point the initial render occurs on the server, which displays the `console.log()` in the terminal.

## RSC Life cycle
![[Pasted image 20260409191427.png]]

![[Pasted image 20260409191530.png]]

## Types of Rendering
In Static Rendering, HTML pages are generated during build process. They can be cached by CDNs and served instantly to multiple users(blog posts, docs etc.). This is the default strategy in the app router.

All components are server components by default.Next.js also implements **prefetching** by which it automatically also preloads all links that appear in a particular page.

In dynamic rendering, routes are rendered uniquely for each user when they make a request. It is used for personalized feeds.

Next.js switches to dynamic rendering when it detects a "dynamic function" or a "dynamic API"(cookies(), headers(), connection(), draftMode(), searchParams prop, after()). 

In streaming, UI progressively loads and is streamed to the client as soon as they are ready without waiting for other elements that might have a slower load time.

## Server and Client Composition Patterns
**Server-only Code** is the code that runs exclusively on servers.

**Client-only code** include DOM manipulation, window object interactions and localStorage options which must strictly run on the client environment.

# Data Fetching
It is preferable to fetch data using server components because of security, lower bundle size to be downloaded and greater efficiency in fetching on server-side.

==User jsonPlaceholder for mock data==

React and therefore Next.js uses Request memoization where multiple same requests are de-duplicated and made only once.

## Loading and Error states
These are maintained through `loading.tsx` and `error.tsx` components on the server-side.

Error components need to be client components.

## Sequential fetching
They take longer loading times but are inevitable when request depend on each other.

## Parallel fetching
Requests are equally initiated and are awaited at the same time to reduce the load time.

## Fetching from a database
Fetching from database has advantages of making the DB operations seamless and various security advantages. SQLite is a file-based DB that doesnt require a server, accessed using Prisma.

## Data Mutations
For security reasons, the client side code cannot directly interact with the database. Therefore, we need to set up an API route to handle such requests.

## Server Actions
They are async functions executed on the server. They can be called in Server and Client components to handle form submissions and data mutations used when we need to perform secure database operations, reduct API boilerplate code, need progressive enhancement of forms or optimize performance.

## Pending State with useFormStatus
`useFormStatus` is a React hook that gives status about the last form submission.
`const status = useFormStatus()` has properties pending(currently submitting or not, boolean), data(submission data), method(HTTP verb, string), action(reference to the parent forms action function)
## Form Validation with useActionState
`useActionState()` is a react hook that allows the updation of state based on result of a form action, useful for forma validation and error messages.

## useAction vs useFormStatus in pending state
The pending state in useAction is a generic hook for all components whereas useFormStatus is specific to forms. It is recommended  to use `useFormStatus` over `useAction` while working with reusable form elements like buttons and spinners.

## Updating and Delete Server Actions
skipped

## useOptimistic hook
It provides a way to show users the expected results right away while an asynchronous action is under way.

## Form component
It is built on top of HTML forms and provides features like automatic prefetching loading UI, client-side navigation on form submission, progressive enhancement.

# Authentication
==clerk.com== is a powerful authentication library.