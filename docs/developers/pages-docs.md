# Character Studio Docs: Pages

[toc]

---

## Appearance

The `Appearance` component is a part of a larger React application. It's responsible for handling the appearance settings of a character in a 3D modeling or animation application. This component provides a user interface for loading and manipulating 3D models, animations, and textures.

In layman's terms, this component is like a control panel for a character in a video game or animation. It allows you to load different character models, animations, and textures, and provides buttons to perform various actions like moving to the next step, going back, randomizing the character's appearance, and entering debug mode.

**Import Statements**

The component begins with a series of import statements, which bring in various dependencies and other components that are used within the `Appearance` component.
Function Definition

The `Appearance` function is the main component function. It takes several props, which are parameters passed from a parent component. These props include various managers (`animationManager`, `blinkManager`, `lookatManager`, `effectManager`) and a `confirmDialog` function.

**Contexts**

The component uses several React Contexts, which are a way of passing data through the component tree without having to pass props down manually at every level. These contexts provide various pieces of data and functions that are used throughout the component.
State Variables

The component defines several state variables using the `useState` hook. These variables store the current state of the component and provide functions to update that state.
Event Listeners

The `useEffect` hook is used to add and remove event listeners to the `effectManager`. These listeners trigger a function when certain events occur.
Translation Hook

The `useContext(LanguageContext)` hook is used to provide a translation function `t` that can be used to display text in different languages.
File Handling Functions

There are several functions (`handleAnimationDrop`, `handleImageDrop`, `handleVRMDrop`, `handleFilesDrop`) that handle different types of files when they are dropped onto the component. These functions read the files, create URLs for them, and update the state variables accordingly.
Render

The `return` statement defines the JSX that will be rendered by the component. This includes a loading indicator, a title, a file drop component, an editor component, and several buttons. The buttons have various functions attached to their `onClick` events, which trigger when the buttons are clicked.

---

## Bio

**Summary**

The `BioPage` component is a part of a character creation process in a game or application. It allows users to customize their character's biography, including their name, voice, favorite color, greeting, and a description. It also includes three questions about the character's personality, relationships, and hobbies. The user's selections are stored in a local state and can be updated dynamically.

Think of this code as a form for creating a character in a video game. You can fill in details like the character's name, voice, favorite color, and a short biography. You can also answer some questions about the character's personality, hobbies, and relationships. As you fill in the form, your answers are saved so you can come back and change them later. There are also buttons to go back to the previous step or move on to the next step in the character creation process.


**Import Statements**

```jsx
import React, { useContext, useEffect } from "react"
import { voices } from "../constants/voices"
import { favouriteColors } from "../constants/favouriteColors"
import CustomButton from "../components/custom-button"
import { ViewContext, ViewMode } from "../context/ViewContext"
import styles from "./Bio.module.css"
import { local } from "../library/store"
import { LanguageContext } from "../context/LanguageContext"
import { SoundContext } from "../context/SoundContext"
import { AudioContext } from "../context/AudioContext"
import { SceneContext } from "../context/SceneContext"
```

**Helper Functions**

There are several helper functions defined in the file:

- `getBio`: This function generates a character's biography based on the base character data and personality.
- `getPersonalityQuestionsAndAnswers`, `getHobbyQuestionsAndAnswers`, `getRelationshipQuestionsAndAnswers`: These functions generate a random question and answer pair from the provided personality data.

```jsx!
export const getBio = (baseCharacterData, personality) => { ... }
export const getPersonalityQuestionsAndAnswers = (personality) => { ... }
export const getHobbyQuestionsAndAnswers = (personality) => { ... }
export const getRelationshipQuestionsAndAnswers = (personality) => { ... }
```

**BioPage Component**

The `BioPage` component is a functional component that uses several hooks to manage its state and side effects. It uses the useContext hook to access the necessary contexts, the `useState` hook to manage the character's full biography, and the useEffect hook to update the local storage whenever the biography changes.

```jsx!
function BioPage({ personality }) { ... }
```

Inside the component, there are several sections for different parts of the biography, each with its own label and input field. The user's input is stored in the `fullBio` state and can be updated dynamically.

```jsx!
<div className={styles.section}>
  <label className={styles.label} htmlFor="name">{t("labels.name")}</label>
  <input type="text" name="name" className={styles.input} defaultValue={fullBio.name} onChange={(e) => setFullBio({...fullBio, ...{name:e.target.value}})} />
</div>
```

At the bottom of the component, there are two buttons for navigating back and forth in the character creation process. The `back` and `next` functions are defined at the beginning of the component and update the view mode accordingly.


```jsx!
<CustomButton theme="light" text={t('callToAction.back')} size={14} className={styles.buttonLeft} onClick={back} />
<CustomButton theme="light" text={t('callToAction.next')} size={14} className={styles.buttonRight} onClick={next} />
```

---

## Create



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

---



## Landing

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

---

## Load

The `Load` component is a part of a React application that interacts with the Ethereum blockchain. It allows users to connect their Ethereum wallet, fetches the NFTs (Non-Fungible Tokens) owned by the user, and displays them. The user can then select a character (NFT) to load. The component also provides audio feedback based on the user's actions and allows the user to navigate back to the landing page.

In simpler terms, this component is like a personal locker for users where they can see all the unique digital assets (NFTs) they own. They can connect their digital wallet, see their assets, and choose one to interact with.

**Imports**

```jsx!
import React, { useEffect, useState } from 'react';
import styles from './Load.module.css';
import { ethers } from 'ethers';
import { useWeb3React } from '@web3-react/core';
import { InjectedConnector } from "@web3-react/injected-connector"
import { ViewContext, ViewMode } from '../context/ViewContext';
import { SoundContext } from "../context/SoundContext"
import { AudioContext } from "../context/AudioContext"
```

The component imports necessary libraries and contexts. `ethers` is a library to interact with Ethereum blockchain. `useWeb3React` and `InjectedConnector` are used to connect to the user's Ethereum wallet. `ViewContext`, `SoundContext`, and `AudioContext` are React contexts used to manage global state related to view mode, sound, and audio settings.


**Component State and Contexts**

```jsx!
function Load() {
    const { account, library, activate } = useWeb3React();
    const [characters, setCharacters] = useState([]);
    const { setViewMode } = React.useContext(ViewContext);
    const { playSound } = React.useContext(SoundContext)
    const { isMute } = React.useContext(AudioContext)
    ...
}
```

The component uses `useWeb3React` to get the user's Ethereum account, the Ethereum library instance, and the `activate` function to connect the wallet. It also uses `useState` to manage a local state `characters` which stores the NFTs owned by the user. It uses `useContext` to get the necessary functions and values from the global state.

**Fetching NFTs**

```jsx
useEffect(() => {
    ...
}, [account, library]);
```

The `useEffect` hook is used to fetch the NFTs owned by the user whenever the `account` or `library` changes. It interacts with a smart contract on the Ethereum blockchain to get the balance and details of each NFT.

**Wallet Connection and Character Loading**

```jsx!
const connectWallet = () => {
    activate(injectedConnector)
}

const loadCharacter = (character) => {
    !isMute && playSound('backNextButton');
    setViewMode(ViewMode.APPEARANCE)
}
```

The `connectWallet` function is used to connect the user's Ethereum wallet. The `loadCharacter` function is used to load a selected character (NFT), play a sound if not muted, and change the view mode to `APPEARANCE`.

**Rendering**

```jsx!
return (
    ...
);
```

The component renders a message to connect the wallet if not connected, a list of characters (NFTs) owned by the user, and a back button to navigate back to the landing page. The styles are applied using CSS modules.

---

## Mint

The `MintComponent` is a React component that provides the functionality for minting a digital asset. In layman's terms, it's like a factory machine interface where you can create your own unique digital item (like a character in a game). This component handles the process of creating the item, showing the status of the creation process, and providing buttons to navigate to other parts of the application.

**Imports**

The component imports several dependencies, including styles, contexts, a custom button component, and a utility function for minting assets.

```jsx!
import React from "react"
import styles from "./Mint.module.scss"
import { ViewMode, ViewContext } from "../context/ViewContext"
import { SceneContext } from "../context/SceneContext"
import CustomButton from "../components/custom-button"
import { SoundContext } from "../context/SoundContext"
import { AudioContext } from "../context/AudioContext"
import { mintAsset } from "../library/mint-utils"
```

**Component Definition**

The `MintComponent` is a functional component that takes a `getFaceScreenshot` prop. It uses several contexts to get and set various application states.


```jsx!
function MintComponent({getFaceScreenshot}) {
  const { templateInfo, model, avatar } = React.useContext(SceneContext)
  const { setViewMode } = React.useContext(ViewContext)
  const { playSound } = React.useContext(SoundContext)
  const { isMute } = React.useContext(AudioContext)
  ...
}
```


**State Variables**

The component uses two state variables: `status` to store the current status of the minting process, and `minting` to store whether the minting process is currently ongoing.

```jsx!
const [status, setStatus] = React.useState("")
const [minting, setMinting]= React.useState(false)
```

**Functions**

The component defines several functions:

- `back` and `next` are used to navigate to other views in the application.
- `MenuTitle` is a sub-component that renders the title of the menu.
- `Mint` is an asynchronous function that handles the minting process.

```jsx!
const back = () => {...}
const next = () => {...}
function MenuTitle() {...}
async function Mint(){...}
```

**Render**

The component returns a JSX structure that includes:

- A title for the section.
- A container for the minting process, which includes the `MenuTitle` sub-component, two `CustomButton` components for the minting options, and a status message.
- A container for navigation buttons.

```jsx!
return (
  <div className={styles.container}>
    ...
  </div>
)
```

**Export**

Finally, the `MintComponent` is exported for use in other parts of the application.

```jsx!
export default MintComponent
```

---

## Optimizer

The `Optimizer` component is a part of a React application that provides an interface for users to optimize their 3D character models. Users can drop their character files into the component, which then processes the file, optimizes it, and allows the user to download the optimized version. The component also provides options for merging and creating texture atlases, and displays information about the current model.

In layman's terms, this component is like a workshop for 3D character models. Users can bring their models in, tweak some settings, and then get a more optimized version of their model to use in their projects.

**Imports**

The component imports various hooks from React, styles, contexts, components, and utility functions from different modules.

```jsx!
import React, { useContext, useEffect, useState } from "react"
import styles from "./Optimizer.module.css"
import { ViewMode, ViewContext } from "../context/ViewContext"
import { SceneContext } from "../context/SceneContext"
import CustomButton from "../components/custom-button"
import { LanguageContext } from "../context/LanguageContext"
import { SoundContext } from "../context/SoundContext"
import { AudioContext } from "../context/AudioContext"
import FileDropComponent from "../components/FileDropComponent"
import { getFileNameWithoutExtension, disposeVRM, getAtlasSize } from "../library/utils"
import ModelInformation from "../components/ModelInformation"
import MergeOptions from "../components/MergeOptions"
import { local } from "../library/store"
```

**Component Definition**

The `Optimizer` component is defined as a functional, no props are required.

```jsx!
function Optimizer() {
  // Component body
}
```

**State and Context**

The component uses several pieces of state and context to manage its behavior and data.

```jsx!
const { 
    isLoading, 
    setViewMode 
} = React.useContext(ViewContext)
const {
    characterManager,
    animationManager,
    sceneElements,
    loraDataGenerator,
    spriteAtlasGenerator
} = React.useContext(SceneContext)
const { playSound } = React.useContext(SoundContext)
const { isMute } = React.useContext(AudioContext)

const [model, setModel] = useState(null);
const [nameVRM, setNameVRM] = useState("");
```
*characterManager* is the class that holds the logic to load/append vrm models and custom character manifests.

*animationManager* is the class that holds the logic to load animations to current loaded traits.

*sceneElements* all the elements within the scene that dont belong to the character traits.

*loraDataGenerator* is the class that holds the logic to create lora data from loaded vrm files.

*spriteAtlasGenerator* is the class that holds the logic to create 2d animated sprites and spritesheets from the currently loaded vrm files.




**Helper Functions**

Several helper functions are defined within the component to handle various tasks such as getting options, downloading the VRM, handling file drops, and more.

```jsx!
const back = () => { /* Function body */ }
const getOptions = () => { /* Function body */ }
const download = () => { /* Function body */ }
const handleAnimationDrop = async (file) => { /* Function body */ }
const handleVRMDrop = async (file) => { /* Function body */ }
const handleFilesDrop = async(files) => { /* Function body */ };
```

**useEffect Hook**

A `useEffect` hook is used to perform side effects when the `currentVRM` state changes.

```jsx!
useEffect(() => {
  const fetchData = async () => { /* Function body */ }
  fetchData();
}, [currentVRM])
```

**Render**

The component returns a JSX structure that includes a loading indicator, a section title, a `FileDropComponent`, a `MergeOptions` component, a `ModelInformation` component, and a set of `CustomButton` components.


```jsx!
return (
  <div className={styles.container}>
    {/* JSX structure */}
  </div>
)
```

**Export**

Finally, the `Optimizer` component is exported for use in other parts of the application.

```jsx
export default Optimizer
```

---

## Save

The `Save` component is a part of a React application that provides a user interface for saving a character. It includes buttons for going back, merging options, exporting, and minting. The component also interacts with several contexts to manage view modes, language, sound, and audio settings.

In layman's terms, this component is like a control panel for a character in a game or app. It allows the user to save their character, go back to previous steps, export their character's image, and perform a process called "minting". It also adjusts its behavior based on the user's language and sound settings. Here's a breakdown of what it doesn:


1. **Imports**: The component imports several dependencies at the top of the file. These include React itself, some CSS styles, other components (`ExportMenu`, `CustomButton`, `MergeOptions`), and several contexts (`ViewContext`, `LanguageContext`, `SoundContext`, `AudioContext`).

2. **Function Component**: The `Save` function is a React component that receives `getFaceScreenshot` as a prop.

3. **Contexts**: Inside the component, it uses the `useContext` hook to access the values from the imported contexts. These values include translation function (`t`), sound playing function (`playSound`), mute status (`isMute`), and a function to set the view mode (`setViewMode`).

4. **Functions**: It defines two functions, `back` and `mint`, which are used to change the view mode and play a sound if the audio is not muted.

5. **Render**: In the render return, it uses the imported components and contexts to create a user interface. This includes a title, two `CustomButton` components, a `MergeOptions` component, and an `ExportMenu` component. The `CustomButton` components have onClick handlers that trigger the `back` and `mint` functions when clicked.

6. **Export**: At the end of the file, it exports the `Save` component as a default export, so it can be imported and used in other parts of the application.


---

## View

The `View` component is a part of a React application that handles the user interface for a chat feature. It uses various contexts to manage state and behavior, such as view mode, sound, audio, and language settings. The component also controls a microphone feature and speech recognition. In layman's terms, this component is like the control center for a chat room where users can interact with each other, and it manages how the chat room looks, sounds, and behaves.

**Imports**

```jsx!
import React, { useContext } from "react"
import styles from "./View.module.css"
import { ViewMode, ViewContext } from "../context/ViewContext"
import Chat from "../components/Chat"
import CustomButton from "../components/custom-button"
import { LanguageContext } from "../context/LanguageContext"
import { SoundContext } from "../context/SoundContext"
import { AudioContext } from "../context/AudioContext"
```

The component imports necessary modules, styles, and contexts. `useContext` is a React hook that allows the component to access the state and functions provided by the imported contexts.

**Component Function**

```jsx!
function View({templateInfo}) {
  ...
}
```

The `View` component receives `templateInfo` as a prop.


**State and Context**


```jsx!
const { setViewMode } = React.useContext(ViewContext)
const [micEnabled, setMicEnabled] = React.useState(false)
const [speechRecognition, setSpeechRecognition] = React.useState(false)
const { playSound } = React.useContext(SoundContext)
const { isMute } = React.useContext(AudioContext)
const { t } = useContext(LanguageContext);
```

The component uses several pieces of state and context:

- `setViewMode`: A function from `ViewContext` to change the view mode.
- `micEnabled` and `setMicEnabled`: State variables to manage the microphone status.
- `speechRecognition` and `setSpeechRecognition`: State variables to manage the speech recognition status.
- `playSound`: A function from `SoundContext` to play a sound.
- `isMute`: A state variable from `AudioContext` to check if the audio is muted.
- `t`: A function from `LanguageContext` to translate text.

**Back Function**

```jsx!
const back = () => {
  setViewMode(ViewMode.SAVE)
  !isMute && playSound('backNextButton');
  if (speechRecognition)
    speechRecognition.stop()
  setMicEnabled(false)
}
```


The `back` function changes the view mode to `SAVE`, plays a sound if audio is not muted, stops speech recognition if it's active, and disables the microphone.

**Render**

```jsx
return (
  ...
)
```

The component renders a chat interface with a title, a `Chat` component, and a `CustomButton` component. The `Chat` component receives several props related to the microphone and speech recognition. The `CustomButton` component is configured to act as a back button.

**Export**

```jsx
export default View
```

The `View` component is exported for use in other parts of the application.