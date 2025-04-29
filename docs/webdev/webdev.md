## react

- JS library used to for building UIs
- component based architecture
- JS + UML like syntax

### starting up
- need to do some research on vite but from what i understand it's just faster
- `npx create-react-app my-app`

### useStateHook
- `const [count, setCount] = useState(0);`
- count is current val, setCount is function used to change it

### useEffect Hook
```
useEffect( () => {
  console.log("component mounted");
}, []);
```
- can fetch data, subscribe to events, update the DOM

### conditional rendering
- `{isOnline ? "Online" : "Offline"}`
- show hide stuff

### list and keys:
```
{items.map((item, index) => (
  <li key={index}> {item} </li>
))}
```
- used to render dynamic lists and helps track each item for updates
- 
