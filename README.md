

# Javascript/Typescript tips


## General guidelines

### **Never mutate data**
 never mutate data (and I mean it like never !) : always create a new object. Create object with spread operator like this 
 ```
 // keep all the old properties of the old object and append the new ones

 {...event, date: day.day, fetchId, start: event.from, end: event.to}
 ```

 ### **Always try to use spread operator when creating new object**

 ```
 {...event, date: day.day, fetchId, start: event.from, end: event.to}
 ```


 ### **Never use for loops**
Abstain from using for loops.
Never use for loops. Always try to to use `map`, `reduce`, `flatMap` 


### **useMemo when there is a setState and computation**

When there is a heavy computation needed that does should not happen on every re-render 
Wrap your function like this.
```
  const events = useMemo(() => {

        // when you have allEvents fetched return it.

        // make some computation on it like removing duplicates fx
        
        return allEvents;
    }, [allEvents, checked]);
```
In this specific case we shoudn't use callback

If we have a CountButtonList. In this case the child `CountButton` will only have to re-render when one of its props change.

```
const CountButton = React.memo(function CountButton({onClick, count}) {
  return <button onClick={onClick}>{count}</button>
})
```
But if the parent has to rerender due to its own internal state.
That's when we can useCallback. To not trigger a rerender of the whole Component. 

```
const [count1, setCount1] = React.useState(0)
  const increment1 = React.useCallback(() => setCount1(c => c + 1), [])
  const [count2, setCount2] = React.useState(0)
  const increment2 = React.useCallback(() => setCount2(c => c + 1), [])
  return (
    <>
      <CountButton count={count1} onClick={increment1} />
      <CountButton count={count2} onClick={increment2} />
    </>
  )
```


### **useEffect** hook, when to use it

 - data fetching
 - subscriptions
 - or manually changing the DOM


 ### **useReducer** when you got lots of useStates

 ```
function reducer(state, action) {
    switch (action.type) {
        CASE 'LAPSE': 
            return {
                ...state,
                lapse: action.now - action.startTime
            }
    }

}

const [state, dispatch] = useReducer(reducer, {
    running:false,
    lapse: 0
})

 ```

# Typescript things



