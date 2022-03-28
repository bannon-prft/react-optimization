# React Optimization

This is the optimization section from [React - The Complete Guide (incl Hooks, React Router, Redux)](https://www.udemy.com/course/react-the-complete-guide-incl-redux/)


## Key Concepts

- React determines how the component tree currently looks and what it should look like
- ReactDOM receives the differences and then manipulates the real DOM
- React components are re-evaluated when one of the following changes:
  - props (which only changes if a parent state changes)
  - state
  - context (which even uses some internal state)
  - **all comes down to state changes in the end**
- React executes component functions
- Changes to the real DOM are only made for differences between evaluations
- Child components are re-evaluated and re-executed when parent state changes because they are function calls within the parent function which is re-executing so in turn the children also have to re-execute

## React.memo()

- Takes a component as an argument
- Should look at props component gets, and check new value for all of those props, and only if the value changes to re-execute 
- Comes at a cost, has to store the previous prop values and also make the comparison between the previous and the new
- Greatly depends on the component you are applying it to
- Trade performance cost of re-evaluating component to re-comparing props
- Will not work on a component that has a function passed, because the JS never evaluates 2 functions to be equal even if they are the exact same

## useCallback()

- Allows us to store a function across component executions
- Saves function somewhere in React's internal storage and always uses that same function in memory
- Since JS functions are closures that are defined when the components are run, the values for the variables are also locked when the function is defined (when the component renders)
- See the App.js `toggleParagraphHandler` for example
  - Without the `allowToggle` dependency, the allowToggle value inside of the function would never change and the button wouldn't work
