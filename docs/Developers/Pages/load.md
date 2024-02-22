# Load

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
