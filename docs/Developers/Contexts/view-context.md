# View Context

Allows navigation within the app and current active page. Viwmode just defines which page is currently active:

- `LANDING`: Iinitial Landing page with menu selection.

- `CREATE`: Character selection page.

- `CLAIM`: Type of batch downlaod selection page.

- `LOAD`: Load created character selection page.

- `APPEARANCE`: Character dress up and customization page.

- `BATCHDOWNLOAD`: Page to download with NFT json traits.

- `BATCHMANIFEST`: Page to download with manifest.

- `BIO`: Character Bio description page.

- `CHAT`: Chat with created character page.

- `OPTIMIZER`: Optimize existing VRM page.

- `WALLET`: Menu after connecting wallet Page.


**Functions**

- `setViewMode`: set the current view mode, access it with variable `viewMode`

- `setIsLoading`: toggle loading validation, access it with variable  `isLoading`

- `setMouseIsOverUI`: function to know if the user has the mouse inside ui, access it with variable  `mouseIsOverUI`

- `setCurrentCameraMode`: (wip) set camera type (`Normal`, `AR`, `AR_Front`, `VR`), access it with variable  `currentCameraMode`