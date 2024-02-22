# Landing

The `Landing` component is a part of a React application that serves as the landing page. It provides the user with options to create, optimize, or load a character. Each option is represented by a button, and clicking on these buttons triggers different actions. The component also interacts with various contexts to manage the application's state and play sounds based on user interactions.

Think of this code as the main menu of a video game. When you start the game, you see options to create a new character, optimize an existing one, or load a previously saved character. Each option is a button you can click. When you click a button, the game changes to the appropriate mode (create, optimize, or load), and a sound plays if the game's sound is turned on.

**Import Statements**

```jsx!
import React from "react"
import styles from "./Landing.module.css"
import { ViewMode, ViewContext } from "../context/ViewContext"
import { SoundContext } from "../context/SoundContext"
import { AudioContext } from "../context/AudioContext"
```

`React` is the base library. `styles` is a CSS module for styling the component. `ViewContext`, `SoundContext`, and `AudioContext` are React contexts used for managing the application's state.

**Function Definitions**

```jsx!
function Landing() {
  const { setViewMode } = React.useContext(ViewContext)
  const { playSound } = React.useContext(SoundContext)
  const { isMute } = React.useContext(AudioContext)

  const createCharacter = () => {
    setViewMode(ViewMode.CREATE)
    !isMute && playSound('backNextButton');
  }

  const optimizeCharacter = () => {
    setViewMode(ViewMode.OPTIMIZER)
    !isMute && playSound('backNextButton');
  }

  const loadCharacter = () => {
    setViewMode(ViewMode.LOAD)
    !isMute && playSound('backNextButton');
  }
  ...
}
```

The `Landing` function is the main component function. It uses the `useContext` hook to access the methods and values from the imported contexts. Three helper functions (`createCharacter`, `optimizeCharacter`, `loadCharacter`) are defined to handle button clicks. Each function sets a different view mode and plays a sound if the application is not muted.


**Render Method**

```jsx!
  return (
    <div className={styles.container}>
      <div className={styles.buttonContainer}>
        <button className={styles.button} onClick={createCharacter}>
          <img src="/assets/media/btn_create_character.png" />
        </button>
        <button className={styles.button} onClick={optimizeCharacter}>
          <img src="/assets/media/btn_optimize_character.png" />
        </button>
        {/*
        <button className={styles.button}
            onClick={
                loadCharacter
            }><img src='/assets/media/btn_load_character.png' /></button>
            */}
      </div>
    </div>
  )
```

The render method returns the JSX to be rendered. It includes a container `div` with two buttons for creating and optimizing characters. The button for loading a character is currently commented out.
