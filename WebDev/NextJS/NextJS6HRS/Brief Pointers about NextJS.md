#personal #webdev

# Setup
 - Create a NextJS project structure by using `npx create-next-app@latest`
 - run `npm run dev` to create a dev environment

# Routing
## Dynamic Routing
 -  Use `[page_name]` to define Dynamic Routing for those pages
 - Use destructuring on the route parameters  props as `params` 
 - The type of `params` is a *Promise* that resolves to an object containing the dynamic segments as key-value pairs
 - Use *async-await* to resolve the *Promise* 
![[Pasted image 20260322130945.png|461]]

## Nested Dynamic Routes
 - Simply take multiple prop ids
 ![[Pasted image 20260322131413.png|409]]
  - Catch-all Segments is another method of implementing dynamic routing in NextJS

## Catch-all Segments
 - These let us implement a large number of routing scenarios through a single file, thereby removing the complexity of highly nested folder structures
 - Create app -> docs -> [...slug] -> page.tsx (This path matches for any /docs/... path)
 - ![[Pasted image 20260322132139.png|376]]
 - This shows 404 for the page /docs. If we want a default page here we can do [ [... slugs ] ]
## Customising the 404 Page
 - Create  a file called `not-found.tsx` in app
 - Define a React component with custom styling within this .tsx page
 - The Not Found page can also be triggered by the `notFound()` function as follows
![[Pasted image 20260322132922.png|446]]
 - to create a specific Not Found page for the reviewid directory, create a new `not-found.tsx` page with specific to the review IDs.
 - The Not Found component is exported as `export default function NotFound()` and it does not accept props. To achieve this effect, we have the following
 ![[Pasted image 20260322133537.png|447]]
- The above gives a compile error without `"use client"` as react hooks only work in client components([[NextTheory]])

## Private Folders
Private folders can be created by simply starting a dir name with "\_". It is primarily used to keep UI logic seperate from routing logic. Alternatives to private folders are File Colocation and placing the logic outside app dir.

## Route Groups
To create Route Groups, place the group folder name within parenthesis.

## Layouts
To create a layout, default export a React component from a layout.tsx file. That component will take a children prop, which Nextjs will populate with the page content. Every layout component needs a children prop where the page content goes. The children component gets replace with the `page.tsx` content in each route.

### Nested Layouts
They allow for the creating of layouts that apply to only the set of pages within that dir.

### Multiple Root Layouts
In nested layouts, all the layouts above the nested layout will also be applied to the page. To exclude the root layout from certain pages, we use the **Multiple Root Layouts** with **Group Routing**. Simply create the required route groups and place the root page.tsx and layout.tsx files into one of the route groups.

# Metadata and Search Engine Optimization
static metadata
```
export const metadata = {
	title: "About page",
};
```

dynamic metadata
```
import {Metadata} from "next";

type Props = {
 params: Promise<{productId: string}>;
};

export const generateMetadata = async ({params}: Props): Promise<Metadata> =>{
	const id = (await params).productId;
	return {title: `Product ${id}`,};
}
```

## Title Metadata

String Title
```
export const metadat = {
	title: "About page,
};
```

Object Title
```
import {Metadata} from "next";
export const metadata: Metadata = {
	default: "Default title",
	template: "%s | MyBlog",
	absolute: "My Blog page",
};
```

# Linking and Navigation
## UI navigation
```
import Link from "next/link";

<Link href="/blog">Blog<Link>
<Link href="/">Home<Link>
```

## Dynamic Links
```
import Link from "next/link";

const productId = 199;

<Link href=`/products/${productId}` replace>Product1<Link>
```

In the above, the `replace` component will overwrite the history entry of the navigation.

## Active Links
```
"use client";

import {usePathname} from "next/navigation";

const pathname = usePathname();
```

Then use the condition
`pathname ===link.href || (pathname,startsWith(link.href) && link.href !== "/")`
for conditional styling of the active link

## params and SearchParams

```
 <Link href="/products/product1?colour=red></Link>
 <Link href="/products/product1?colour=blue></Link>
```

In the above, product1 is dynamic route parameter and colour is the query parameter.

```
export default async function ProductDesc({params, searchParams}: {
	params: Promise<{productId: string}>;
	searchParams: Promise<{colour?: "red" | "blue"}>;
}) {
		const {productId} = await params;
		const {colour = "red"} = await searchParams;	
}
```
The above is how to access the route and query parameters. We can use async and await here since these parameters are server components. Below is how:

```
import {use} from "react";

export default function ProductDesc({params, searchParams}: {
	params: Promise<{productId: string}>;
	searchParams: Promise<{colour?: "red" | "blue"}>;
}) {
		const {productId} = use(params);
		const {colour = "red"} = use(searchParams);	
}
```

## Navigating Programmatically
```
"use client";

import {useRouter} from "next/navigation";

export default function OrderProduct(){
	const router = useRouter();
}

const handleClick = () {
	console.log("Placing your order");
	router.push("/");
}
```

==Other router function include `replace`, `back` etc==

==We can also use `redirect` from "next/navigation" to redirect to a particular route==

## Templates
Simply rename `layout.tsx` to `template.tsx`

## Loading Pages
Create `loading.tsx`

```
export default function Loading() {
	return <h1>Loading</h2>;
}
```

# Error Handling
skipped
# Parallel Routes
Parallel routes are implemented through a feature called **slots**. To create slots we use the `@folder` naming convention. Each defined slot automatically becomes a prop in its `layout.tsx`. These are not route segments. We get a 404.

In `layout.tsx`
```
export default function ComplexDashboard({
	children,
	users,
	revenue,
	notifications,
}: {
	children: React.ReactNode;
	users: React.ReactNode;
	revenue: React.ReactNode;
	notifications: React.ReactNode;
	}
})
```
The above therefore, has 4 slots.

## Unmatched Routes
To fix the 404 on page reload, create `default.tsx` pages under each of the 4 slot route folders.

## Conditional Routes
Simply return the slot as a conditional render to some boolean variable
```
export default function Dashboard({login}: {login: React.ReactNode;}){

	isLoggedin ? (
	<div>Logged In</div>
	) : (
	login
	);
}
```

## Intercepting Routes
Use `(.)dirname` when intercepting a folder in the same level, `(..)dirname` when the folder is one level higher, `(..)(..)dirname` at two levels higher and `(...)dirname` at the route on root level.

==The dirname must match exactly with the target route dirname==

# Route Handlers
They MUST live inside the _app_ folder. Inside the `dirname` folder create a file `route.tsx` then
```
import { comments } from "./comments"

export async function GET(){
	return new Response('Hello World!')
	//OR return Response.json(comments)
}

export async function POST(request: Request){
	const comment = await request.json();
	const newComment = {
		id: comments.length + 1,
		text: comment
	};
	comments.push(newComment);
	return new Response(JSON.stringify(newComment), 
	{
		headers: {"Content-Type": "application/json"},
		status: 201,
	});
}
```


In a route, `route.tsx` has higher priority than `page.tsx`. To get over this, move all route handlers under `api` folder.

For PATCH and DELETE, define `route.tsx` under a dynamic route handler folder(eg `[id]`)

```
import {comments} from "./data";

export async function GET(_request: Request,
	{params}: {params:Promise<{id: string}>}
)
{
	const {id} = await params;
	const comment = comments.find((comment) => comment.id === parseInt(id));
	return Response.json(comment);
}

export async function PATCH(request: Request,
	{params}: {params:Promise<{id: string}>}
)
{
	const {id} = params;
	const body = await request.json();
	const {text} = body;
	
	const index = comments.findIndex((comment) => comment.id === parseInt(id));
	comments[index].text = text;
	return Response.json(comments[index]);
}

export async function DELETE(request: Request,
	{params}: {params:Promise<{id: string}>}
)
{
	const {id} = params;
	const index = comments.findIndex((comment) => comment.id === parseInt(id));
	const deletedComment = comments[index];
	comments.splice(index, 1);
	return Response.json(deletedComment);
}


```

## Query Parameters

Filtering responses by query parameters is done as follows
```
import {type NextRequest} from "next/server";
import {comments} from "./data";

export default async function GET(request: NextRequest){
	const searchParams = request.nextUrl.searchParams;
	const query = searchParams.get("query");
	
	const filteredComments = query ? comments.filter((comment) => comment.text.includes(query)) : comments;
	
	return new Response.json(fileredComments);
}
```

## Headers
```
import {type NextRequest} from "next/server";

export async function GET(request: NextRequest){
	const requestHeaders = new Headers(request.headers);
	console.log(requestHeaders.get("Authorization"));
}
```
OR
```
import {headers} from "next/headers";
import {type NextRequest} from "next/server";

export async function GET(request: NextRequest){
	const headersList = await headers();
	console.log(headersList.get("Authorization"));
	return new Response("Profile API data");
	//OR
	return new Response("Profile API data",
	{
		headers: {
			"Content-Type": "text/html",
		},
	});
}
```


## Cookies
```
import {headers} from "next/headers";
import {type NextRequest} from "next/server";

export async function GET(request: NextRequest){
	const headersList = await headers();
	console.log(headersList.get("Authorization"));
	return new Response("Profile API data");
	//OR
	return new Response("Profile API data",
	{
		headers: {
			"Content-Type": "text/html",
			"Set-Cookie": "theme=dark"
		},
	});
}
```
To read cookies
`const theme = request.cookies.get("theme")`

OR
```
import {headers, cookies} from "next/headers";
export async function GET(request: NextRequest){
	
	const cookieStore = await cookies();
	cookieStore.set("resultsPerPage", "20");
	cookieStore.get("resultsPerPage");
	
	return new Response("Profile API data",
	{
		headers: {
			"Content-Type": "text/html",
			"Set-Cookie": "theme=dark"
		},
	});
}

```

## Redirecting Route Handlers
Use `redirect(<endpoint>);` at the beginning of the handler function to redirect to a new url with the same logic

## Caching
Use `export const dynamic = 'force-static;` at the start of `route.tsx` to implement caching.

To use "Incremental Static Regeneration" after 10s,
`export const revalidate = 10;`

## Middleware

Add `middlware.ts` file in `src`
```
import {NextResponse} from "next/server";
import {type NextRequest} from "next/server";

export function middleware(request: NextRequest){
	return NextRequest.redirect(new URL("/", request.url));
}

export const config = {
	matcher: "/profile",
}
```

OR using conditional statements
```
import {NextResponse} from "next/server";
import {type NextRequest} from "next/server";

export function middleware(request: NextRequest){
	if(request.nextUrl.pathname === "/profile")
		return NextResponse.redirect(new URL("/", request.url));
		//OR use .rewrite()
}
```

# Rendering
All components are server components by default.

To create an optimized production build, use `npm run build`. The hollow circles along each page shows that it is statically rendered.

Dynamic routes show up with an 'f' in the terminal when we do `npm run build`. We wont find html files for these pages in .next folder since they will be generated at request time. To force a site to be dynamically rendered we can use `export const dynamic = 'force-dynamic'` at the top of the page. 

***generateStaticParams()*** is a function that lets us generate static routes for dynamic route segments(eg [id]) for a performance boost. 

```
export async function generateStaticParams(){
	return [{"id": "1"}, {"id": "2"}, {"id": "3"}];
}

export default async function ProductPage()...
```

These IDs appear with a filled circle in the terminal(SSG). These are generally used for popular dynamic segments.

For multiple dynamic segments we can include each dynamic part within the array element.

If we set `export const dynamicParams = false;` in the beginning of the page, the other dynamic segments will return a 404.

In streaming, we wrap the UI elements with suspense to implement progressive rendering.

```
import {Suspense} from "react";
export default function ProductReviews(){
return(

	<Suspense fallback = {<p>Loading products...</p>}>
		<Product />
	</Suspense>
)}
```

## Server and Client Compositions
### Server-only Code
1. We can use the **server-only package** to throw build-time error if someone imports server code into a Client Component. To use it: `npm i server-only` then `import "server-only";` at the top of the server fuction.

2. To use thrid-party packages that require client side features on the server-side, we can wrap them in client compoenents(eg react-slick).

```
"use client";
import <third-party package>

export const MyClientComponent = () =>{
<use of third-party package>
}

```
and then use MyClientComponent in the server-side code.

3. React Context providers live near the root of an application to share global state and logic(eg theme). These are not supported in Server Components and throw an error. Thus we create the context and render its provider inside a dedicated Client Component.
### Client-only Code
1. Use `npm i client-only` and then `import "client-only";`
2. **Client Component Placement** refers to the practice of placing client components lower on the component tree, because when we make a component a Client Component, all its children also become client components. Therefore, place all the components that require client-side features as the leaf nodes.
## Interleaving
We can have a:
1. Server component inside another server component.
2. Client component inside another client component.
3. Client component inside a server component.
We cannot have a Server component inside a client component because all children of client components are also client components.

A workaround is passing the server component as a prop to a client component through a slot

serverComponentOne.tsx
```
<ClientComponentOne> 
	<ServerComponentOne/>
</ClientComponentOne>
```

clientComponentOne.tsx
```
export const ClientComponentOne({children}: {
	children: React.ReactNode
}) => {
	return(
		<>
			<p>Client ComponentOne</p>
			{children}
		</>
	)
}
```

# Data Fetching
## Client-side fetching
```
useEffect(() => {
	async function fetchUsers() {
		try{
			const response = await fetch(<endpoint>);
			if(!response.ok) throw new Error("Failure");
			const data = await response.json();
			setUsers(data);
		} catch(err){
			if(err instanceOf Error) s
				setError(err.message);
			else
				setError("unknown error");
		} finally setLoading(false);
	}
	fetchUsers();
}, []);
```

This should only be done when we need real time updates with client-interactions we cannot predict on the server-side.

## Server-side fetching
```
type User = {
	id: number;
	.
	.
	.
};

export default async function UsersServer(){
			//server components suppoer async functions
	const response = await fetch(<endpoint>);
	const users: User[] = await response.json();
	console.log(users);
}
```

## Loading and Error States
These are maintained through `loading.tsx` and `error.tsx` components on the server-side.

Error components need to be client components.
error.tsx
```
"use client";

export default function ErrorPage({error}: {error: Error})
{
	useEffect(() => {
		console.log(`${error}`);
	}, []);
}
```

## Sequential fetching
Requests in a component tree are dependent on each other. This is done by defining the sequence of fetches in their own components and then calling these components in the order they are to be fetched. The components can be wrapped in `Suspense` to fetch in the background to not block the UI.

## Parallel fetching
Requests are equally initiated and are awaited at the same time to reduce the load time. Define the async fetching functions outside the async component function.

```
async function getUserPosts(userId: string){
	const res = await fetch(<endpoint>);
	return res.json()l
};
...

export default async function UserProfile({
	params,
}: {
	params: Promise<{id: string}>;
})
{
	const {id} = await params;
	
	const postsData = getUserPosts();
	const albumsData = getAlbums(id);
	
	const [posts, albums] = await Promise.all(
	[postsData, albumsData]);
}

```
In the above, since awaited request block all requests below it, we initiated the requests before awaiting them at the same time.

## Fetching from a database
1. `npm install prism -D`
2. `npx prisma init --datasource-provider sqlite`
3. In schema.prisma, update `url = "file:app.db"` and add the file to `.gitignore`
4. `npx prisma migrate deb --name init` 
5. In src, create `prisma-db.ts`
6. Define operations in `prisma-db.ts`

## Data Mutations
They refer to the CRUD operations. 

## Server Actions
User `"user server"` directive at the top of an async function or at the top of a seperate file to mark all exports of that file as server actions.

```
export default function AddProductPage(){
	async function createProduct(formData: FormData){
		"use server";
		
		const title = formData.get("title") as string;
		const price = formData.get("price") as string;
		const description = formData.get("description") as string;
		addProduct(title, parseInt(price), description);
	
	}
	
	return(
		<form action={createProduct}>
		.
		.
		.
	)
}
```

## Pending status with useFormStatus
```
import {useFormStatus} from "react-dom";

export const Submit = () =>{
	const {pending} = useFormStatus();
	
	return(
		<button type="submit" disabled={pending}>
			Submit
		</button>
	)
}
```

## Form Validation with useActionState
```
"use client";
type Errors = {
	title?: string;
	price?: string;
	description?: string;
};

type FromState = {
	errors: Errors;
};

export default function AddProductPage() {
	const initialState: FormState = {
		errors: {},
	};
};

	const [state, formAction, isPending] = useActionState(createProduct, initialState);
	.
	.
	.
	
}
```
The above will give error if we have a server action function within the page. The workaround is below.

### Seperating Server Actions
Simply create a new .ts file for the server acton(s).
`export async function createProduct(prevState: FormState, formData: FormData){...}`.

==Note the `prevState`==
