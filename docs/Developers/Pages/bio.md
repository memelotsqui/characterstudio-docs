# Bio

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
