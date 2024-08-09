---
description: Breakdown of collection metadata CSV components
---

# In-depth Outline of collection metadata CSV

Follow details below to further understand how to format your .csv file correctly. The .csv file is where all your NFTs metadata will be stored, allowing you to add a further layer of uniqueness to each NFT.&#x20;

A quick note before you begin: You are not required to add **OR** fill your .csv file with any data; however, this will display your NFTs information as your collections default metadata.

The .csv file in your '**Artwork Folder**' can be formatted as shown below:

<table><thead><tr><th width="125" align="center">Name</th><th align="center">Description</th><th width="98" align="center">Media</th><th width="118" align="center">Thumbnail</th><th align="center">attribute [attribute name #1]</th><th align="center">attribute [attribute name #2]</th></tr></thead><tbody><tr><td align="center">NFT #1</td><td align="center"></td><td align="center">1.png</td><td align="center">1.png</td><td align="center"></td><td align="center"></td></tr><tr><td align="center">NFT #2</td><td align="center"></td><td align="center">2.png</td><td align="center">2.png</td><td align="center"></td><td align="center"></td></tr><tr><td align="center">NFT #3</td><td align="center"></td><td align="center">3.png</td><td align="center">3.png</td><td align="center"></td><td align="center"></td></tr><tr><td align="center">NFT #4</td><td align="center"></td><td align="center">4.png</td><td align="center">4.png</td><td align="center"></td><td align="center"></td></tr></tbody></table>

The components of your .csv document must be formatted correctly to ensure that your collection displays correctly.

1. **Name**: The name of your NFT. This will be displayed on your NFTs page.
   1. If the '**Name**' column does not exist, or if it is empty, the default name will be "\[Collection Name #TokenId]".
2. **Description**: The Description is where you can add any extra information that you would like to accompany your NFTs
   1. If the '**Description**' column does not exist, or if it is empty, the description of the collection will be used.
3. **Media**: The Media column allows you to manually link files to metadata using filenames, i.e. "image-001.png".
   1. If it exists, the content is mandatory and should be the filename in the 'media' folder. If it is empty or the file does not exist, a warning will be issued.
   2. If the content is not an image, there must be a 'thumbnails' column, and the content of the 'thumbnails' column should be in image format and there should be a corresponding file in the 'thumbnails' folder, otherwise a warning will be issued.
   3. If the content is an image, the content of the 'thumbnails' column does not matter.
   4.  If it does not exist, the files in the 'media' folder will be matched in order.

       If the number of tokens is greater than the number of files in 'media', a warning will be issued.
4. **Thumbnail**: The Thumbnail column can be created to attach images to non-image media. These images would come from your thumbnail folder.
5.  **Attributes**: Attributes will allow you to add metadata and properties to your individual NFTs. There is no limit to the number of attributes your NFT can have.

    If there is a column named 'attributes\[]', the content in the '\[]' is the attribute name. If the column content is empty, this attribute will not be saved.

## Other Essential Rules

There are a few essential rules that you **MUST** follow when creating your file:

1. The first row of the .csv MUST be used as a header for the titles of each column. When the file is read to display your collection information, it is read from row 2 onwards.
2. There can only be ONE .csv file in your artwork folder.

Your .csv file is now good to go! Place the .csv file into your artwork folder and continue with the creation of your collection.
