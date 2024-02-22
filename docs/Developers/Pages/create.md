# Create



In layman's terms, this code defines a component in a React application that allows users to select a character class for a game. The component fetches a list of available classes from a context, displays them in a scrollable container, and allows the user to select a class. If the class is disabled, the user cannot select it. When a class is selected, the component fetches additional information about the class and transitions to a different view. The component also plays different sounds based on user interactions, if the sound is not muted.


**Import Statements**

The component imports necessary modules and contexts at the beginning. These include React hooks, CSS styles, and several contexts that provide shared state across the application.

```jsx!
import React, { useEffect, useState } from "react"
import styles from "./Create.module.css"
import { ViewMode, ViewContext } from "../context/ViewContext"
import CustomButton from "../components/custom-button"
import { LanguageContext } from "../context/LanguageContext"
import { useContext } from "react"
import { SceneContext } from "../context/SceneContext"
import { SoundContext } from "../context/SoundContext"
import { AudioContext } from "../context/AudioContext"
```

**Create Function Component**

The `Create` function component takes a `fetchCharacterManifest` function as a prop. This function is used to fetch additional information about a class when it is selected.

```jsx!
function Create({fetchCharacterManifest}) {
  ...
}
```

**State and Contexts**

The component uses several pieces of state and context. The `useState` hook is used to manage the `classes` state, which is an array of available classes. The `useContext` hook is used to access shared state from the `ViewContext`, `SoundContext`, `AudioContext`, and `SceneContext`.

```jsx!
const {t} = useContext(LanguageContext);
const { setViewMode } = React.useContext(ViewContext)
const { playSound } = React.useContext(SoundContext)
const { isMute } = React.useContext(AudioContext)
const { manifest } = React.useContext(SceneContext)
const [ classes, setClasses ] = useState([]) 
```

**useEffect Hook**

The `useEffect` hook is used to update the `classes` state whenever the `manifest` context changes. The `manifest` context contains information about the available classes.


```jsx!
useEffect(() => {
  if (manifest != null){
    const manifestClasses = manifest.map((c) => {
      return {
        name:c.name, 
        image:c.portrait, 
        description: c.description,
        manifest: c.manifest,
        icon:c.icon,
        format:c.format,
        disabled:false
      }
    })
    setClasses(manifestClasses);
  }
}, [manifest])
```

**Event Handlers**

The component defines several event handlers for user interactions. The `back` function is called when the user wants to go back to the previous view. The `selectClass` function is called when the user selects a class. The `hoverClass` function is called when the user hovers over a class.


```jsx!
const back = () => {
  setViewMode(ViewMode.LANDING)
  !isMute && playSound('backNextButton');
}

const selectClass = (index) => {
  fetchCharacterManifest(index).then(()=>{
      setViewMode(ViewMode.APPEARANCE)
  })
  !isMute && playSound('classSelect');
}
const hoverClass = () => {
  !isMute && playSound('classMouseOver');
}
```

**Render Method**

The render method returns the JSX that defines the component's UI. It maps over the `classes` state to create a list of class options. Each class option is a `div` that displays the class's image, icon, name, and description. If the class is disabled, it cannot be clicked or hovered over.

```jsx!
return (
  <div className={`${styles.container} horizontalScroll`}>
    ...
    <div className={styles.classContainer}>
      {classes.map((characterClass, i) => {
        return (
          <div
            key={i}
            className={
              !characterClass["disabled"]
                ? styles.class
                : styles.classdisabled
            }
            onClick={
              characterClass["disabled"]
                ? null
                : () => selectClass(i)
            }
            onMouseOver={
              characterClass["disabled"]
                ? null
                : () => hoverClass()
            }
          >
          ...
          </div>
        )
      })}
    </div>
    ...
  </div>
)
```
