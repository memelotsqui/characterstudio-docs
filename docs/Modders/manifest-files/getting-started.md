---
sidebar_position: 1
---

# Getting Started with Manifest Files

This guide will help you set up your first character collection for Character Studio. We'll walk through creating a manifest file that tells the studio how to display and organize your 3D models, textures, and other assets.

## What is a Manifest File?

A manifest file is like a recipe that tells Character Studio:
- Where to find your 3D models and textures
- How to organize them into categories (like body, clothing, hair)
- How they should interact with each other (like clothes covering the body)
- What colors and textures can be applied

## Creating Your First Manifest File

### Step 1: Create a New Text File

1. Open your favorite text editor (like Notepad, TextEdit, or VS Code)
2. Create a new file
3. Save it as `manifest.json` (make sure to include the `.json` extension)

### Step 2: Basic Structure

Copy and paste this basic structure into your file:

```json
{
  "assetsLocation": "/character-assets",
  "traitsDirectory": "/your-collection/",
  "thumbnailsDirectory": "/your-collection/",
  "format": "vrm",
  "displayScale": 1.0,
  "traits": []
}
```

### Step 3: Organize Your Files

Create these folders in your project:
```
character-assets/
└── your-collection/
    ├── BODY/
    │   ├── female.vrm
    │   └── female.png
    ├── CLOTHING/
    │   ├── dress.vrm
    │   └── dress.png
    ├── HAIR/
    │   ├── long.vrm
    │   └── long.png
    └── icons/
        └── body.svg
```

### Step 4: Add Your First Trait

Let's add a body trait. Replace the empty `"traits": []` with:

```json
"traits": [
  {
    "trait": "BODY",
    "name": "Body",
    "iconSvg": "icons/body.svg",
    "cullingLayer": 0,
    "cameraTarget": {
      "distance": 0.75,
      "height": 1.35
    },
    "collection": [
      {
        "id": "FEMALE",
        "name": "Female",
        "directory": "BODY/female.vrm",
        "thumbnail": "BODY/female.png"
      }
    ]
  }
]
```

### Step 5: Add More Traits

Add clothing and hair traits following the same pattern:

```json
"traits": [
  {
    "trait": "BODY",
    "name": "Body",
    "iconSvg": "icons/body.svg",
    "cullingLayer": 0,
    "cameraTarget": {
      "distance": 0.75,
      "height": 1.35
    },
    "collection": [
      {
        "id": "FEMALE",
        "name": "Female",
        "directory": "BODY/female.vrm",
        "thumbnail": "BODY/female.png"
      }
    ]
  },
  {
    "trait": "CLOTHING",
    "name": "Clothing",
    "iconSvg": "icons/clothing.svg",
    "cullingLayer": 1,
    "cameraTarget": {
      "distance": 1.0,
      "height": 1.0
    },
    "collection": [
      {
        "id": "DRESS",
        "name": "Dress",
        "directory": "CLOTHING/dress.vrm",
        "thumbnail": "CLOTHING/dress.png"
      }
    ]
  },
  {
    "trait": "HAIR",
    "name": "Hair",
    "iconSvg": "icons/hair.svg",
    "cullingLayer": 2,
    "cameraTarget": {
      "distance": 0.5,
      "height": 1.5
    },
    "collection": [
      {
        "id": "LONG",
        "name": "Long",
        "directory": "HAIR/long.vrm",
        "thumbnail": "HAIR/long.png"
      }
    ]
  }
]
```

### Step 6: Add Colors and Textures

Add color options for hair and skin:

```json
"colorCollections": [
  {
    "trait": "HAIR_COLORS",
    "collection": [
      {
        "id": "BLACK",
        "name": "Black",
        "value": ["#000000"]
      },
      {
        "id": "BROWN",
        "name": "Brown",
        "value": ["#8B4513"]
      }
    ]
  }
],
"textureCollections": [
  {
    "trait": "SKIN_TONES",
    "collection": [
      {
        "id": "LIGHT",
        "name": "Light",
        "directory": "textures/skin_light.png",
        "thumbnail": "textures/skin_light_thumb.png"
      },
      {
        "id": "MEDIUM",
        "name": "Medium",
        "directory": "textures/skin_medium.png",
        "thumbnail": "textures/skin_medium_thumb.png"
      }
    ]
  }
]
```

### Step 7: Save and Test

1. Save your `manifest.json` file
2. Place it in your `character-assets` folder
3. Load it in Character Studio to test

## Tips for Artists

### File Organization
- Keep your files organized in clear folders
- Use descriptive names for your files
- Include thumbnails for all your 3D models
- Create simple SVG icons for each category

### 3D Models
- Export your models in VRM format
- Make sure your models are properly scaled
- Test your models in Character Studio before adding them to the manifest

### Textures and Colors
- Use PNG format for textures
- Keep texture sizes reasonable (2048x2048 is usually enough)
- Use web-safe colors for color options

### Culling Layers
- Base body should be layer 0
- Clothing should be layer 1
- Accessories should be layer 2 or higher
- Use -1 for things that shouldn't cull (like hair)

## Common Issues and Solutions

### My models don't show up
- Check if the file paths in the manifest match your folder structure
- Make sure your VRM files are properly exported
- Verify that the file names match exactly (including case)

### Textures look wrong
- Check if your texture files are in the correct format (PNG)
- Verify the texture paths in the manifest
- Make sure your UV maps are correct

### Colors don't apply
- Check if the color values are in the correct format (#RRGGBB)
- Verify that the trait IDs match between traits and color collections

## Next Steps

1. Test your manifest with a few basic traits
2. Add more options to each category
3. Experiment with different culling layers
4. Add more color and texture options

For more detailed information about each field, refer to the [Character Traits Documentation](./character-traits.md). 