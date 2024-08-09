## Lightrun for Koa

**To use Lightrun with a Koa application:**

1. In your project's folder, install the node agent by running `npm install lightrun`.

2. Import Lightrun at the start of your application file (for example, `app.js`) by adding the following code:

     ```javascript
     require('lightrun').start({
          lightrunSecret: '<LIGHTRUN_SECRET>'
     });
     ```

3. Run the application, e.g., `node index.js` or `npm start`.

!!! info "Getting Company Details"
    To get your `<LIGHTRUN_SECRET>` key, log into the [Management Portal](https://app.lightrun.com) and inspect the **Set Up An Agent** section, under **Getting Started**.

--8<-- "ux-reference/node-typescript.md"
