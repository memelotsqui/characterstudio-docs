---
sidebar_position: 1
---

# Overview

The manifest files are essential if you want to mod Character Studio with your own assets and selection screens. They are found in various parts of the project, and basically are the main file other than art assets that you would need to modify to make an avatar builder program.



## Character Selection

This is for the select screen that loads up profiles for character bases models and their associated assets.

![Screenshot from 2024-02-16 02-27-37](https://hackmd.io/_uploads/HkU6ZQWhT.png)

<details>

character-select

</details>

---

## Manifest Files for Traits

Setting up this manifest will populate the asset trait section with your own traits that people can select from. It will also serve the character studio for cull trait model options (remove faces underneath) based on the layers, so the triangles disappear underneath the clothing for example.

![Screenshot from 2024-02-19 13-42-19](https://hackmd.io/_uploads/By1NZXbhT.jpg)



<details>

character-traits
    
</details>


---

## Manifest Files for LoRAs

This manifest is inspired by the [VRM to LoRA guide](https://hackmd.io/@reneil1337/avatar-lora) by [reneil1337](https://github.com/reneil1337) will generate training data that can be used for training LoRAs using tools such as [Kohya](https://github.com/bmaltais/kohya_ss).

![rendercombined](https://hackmd.io/_uploads/H1OJTfb36.jpg)

<details>
    
vrm-to-lora
    
</details>
    
---

## Personality.json

This is an experimental feature for prepopulating and customizing personalities for VRM avatars for AI chatbot application use cases. There's also an ongoing effort to standardize this type of metadata as a [gltf extension](https://github.com/omigroup/gltf-extensions/tree/main/extensions/2.0/OMI_personality) if interested.

![Screenshot from 2024-02-19 13-46-05](https://hackmd.io/_uploads/B11GGmZnT.jpg)


<details>

ai-personalities

</details>
    

---

## Generating Manifest Files

Some useful scripts to help with generating the manifest files

<details>

generating-manifest

</details>
