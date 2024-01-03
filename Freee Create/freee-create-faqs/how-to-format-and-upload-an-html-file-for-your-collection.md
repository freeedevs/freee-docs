# How to format and upload an HTML file for your collection

A guide on how to upload and format your HTML collection on Freee.

HTML files are now supported by FREEE's creator toolkit, expanding the possibilities of what you can create. Follow along below to learn more about this tool and how to use it.

## How do I upload an HTML file to my collection?

When creating a collection with an HTML file, you must zip that file and all other media and files together and then upload that zipped file. You cannot just upload an HTML file.

\*You can also follow our in-depth guide below to go through the formatting and upload process.

## Can I have external files within my HTML?

**NO**, you cannot have external files. All intended media and files must be zipped together before uploading.

## Can I link to external scripts?

**NO**, you must ensure you don’t have any references to scripts on other servers. If you see something like this

```js
<script src="https://cdn.jsdelivr.net/npm/p5@1.6.0/lib/p5.js"></script>
```

You will need to download the p5.js file, include it in your zip, and change the link to

```js
<script src="./p5.js"></script>
```

## How to format and upload your HTML file

There are **two** essential requirements to consider before you upload your HTML file.

1. When creating your artwork, ensure that it is **reactive to display size**, as it will be viewed at different window sizes depending on the platform and screen size.
2. Your HTML file **MUST** be named "index.html"

Once your HTML file and other necessary files are ready to go:

1. Select all your files and zip/compress them together
   1. Do **NOT** zip a folder containing the files; only zip the files themselves.
2. Upload the zipped file to your collection
3. Now you can fill out all your collection details and settings. To learn more about how to create your collection, check out our guides below:
   1. [How to create a Edition](../how-to-create-a-edition/how-to-create-a-edition.md)
