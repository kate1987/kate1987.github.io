## Lightrun for Express

**To use Lightrun with a Express application:**

1. In your project's folder, install the node agent by running `npm install lightrun`.

1. Import Lightrun at the start of your application file (for example,  `app.js`) by adding the following code:

     ```javascript
     require('lightrun').start({
          lightrunSecret: '<LIGHTRUN_SECRET>'
     });
     ```

1. Run the application as you normally would; for example, `node index.js` or `npm start`.

!!! info "Getting Company Details"
    To get your `<LIGHTRUN_SECRET>` key, log into the [Management Portal](https://app.lightrun.com) and inspect the **Set Up An Agent** section, under **Getting Started**.

--8<-- "ux-reference/node-typescript.md"
