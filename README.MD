<h1 align="center">
 useRefsMap ( React hook )
</h1>
<p align="center">
<a href="https://www.npmjs.com/package/use-refs-map">
<img src="https://img.shields.io/npm/v/use-refs-map.svg" alt="NPM" /></a>
</p>

## What the purpose ?

useRefMap is a simple React Hook to keep the last values & objects references on a constant hashmap/object.

Ok, but what the purpose ?

When we define functions, the accessible variables are those that where present when the function was defined.<br/>
This force us to redefine functions on most redraw, or use complex state management & reducers.

This Hook, allow us to keep functions unique as they can access the last value throught the RefMap

## Code ( so simple )

```jsx
export default function useRefsMap( refs ) {
	const scope = React.useRef({}).current;
	
	Object.assign(scope, refs);
	
	return scope;
}
```

## Sample

```jsx
import useRefsMap from "use-refs-map";

export default ( {
	                 style,
	                 ...props
                 } ) => {
	const
		slideQuery                        = Hooks.useQuery(
			"Slides",
			{
				params: { orderBy: { _created: -1 } }
			}
		),
		[selectedIndex, setSelectedIndex] = React.useState(0),
		styles                            = React.useMemo(
			() => (
				{}
			),
			[]
		),
		locals                            = useRefsMap(
			{
				slideQuery,
				selectedIndex
			}
		),
		api                               = React.useMemo(
			() => (
				{
					doSomeStuff: () => {
						// locals.slideQuery is updated on any render
						// so functions in the api object does'nt need to be re-created
						// this avoid rerender / updating listeners 
					}
				}
			),
			[]
		);
	
	return <div className={"HomePage"}>
		{/*  */}
	</div>;
};
```
