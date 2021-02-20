# react-hooks

- Reative state
- Side on effects
- Grab elements

Basics Hooks
------------
- useState
- useEffect
- useContext

Additional Hooks
----------------
- useReducer
- useCallback
- useMemo
- useRef
- useImperativeHandle
- useLayoutEffect
- useDebugValue

componentDidMount() {
// initialized (on)
}

componentDidUpdate() {
// state updated (loop)
}

componentWillUnmount() {
// destroyed (off)
}


useState() => when data changes, re-render the UI

Function e.g.

function App() {

const [count, setCount] = useState(0);

return (
<button onClick={() => setCount(count+1)}>
{count}
</button>
);
}

Class Component e.g.

class Btn extends React.Component {
constructor(props) {
super(props);
this.state = {
  count: 0
};
}

render() {
return(
<button onClick={() => this.setState({ count: this.state.count + 1})
}>
{this.state.count}
);
}
}


useEffect() =>

Function e.g.

function Btn() {

const [count, setCount] = useState(0);
const [loaded, setLoaded] = useState(false);

useEffect(() => {
  alert('hello side effect!') // when state changes
  return () => alert('goodbye component!')
})

useEffect(() => {
  fetch('foo').then(() => setLoaded(true) )
}, 
[count] // when count changes
)

return (
<button onClick={() => setCount(count+1)}>
{count}
</button>
);
}


useContext() // share data without passing props

const moods = {
  happy: 'Hi',
  sad: 'Bye'
}

const MoodContext = createContext(moods);

function App(props) {
  return (
  <MoodContext.Provider value={moods.happy}></MoodContext.Provider>
  );
}

function MoodEmoji() {
  return <MoodContext.Consumer>
    { ({mood}) => <p>{mood}</p> }
  </MoodContext.Consumer>
}


useRef()

function App() {
  const count = useRef(0);

  return (
    <button onClick={() => count.current++ }>
	{count.current}
    </button>
  );
}


useReducer() // a differnt way to manage state redux = [ action, reducer, store ]

function reducer(state, action) {
 switch (action.type) {
  case 'increment':
    return state + 1;
  case 'decrement':
    return state - 1;
  default:
    throw new Error();
  }
}

function App() {
  const [state, dispatch] = useReducer(reducer, 0);
  return(
    <>
      Count: {state}
      <button onClick={() => dispatch({type: 'decrement'})}>-</button>	   
      <button onClick={() => dispatch({type: 'increment'})}>+</button>	   
    </>
  )
}


useMemo() // cache result of function call 
