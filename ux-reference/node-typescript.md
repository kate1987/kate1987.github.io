### Running the agent in TypeScript applications

!!! important
    As part of Lightrun’s commitment to align with industry standards, we strongly advise using the TypeScript Compiler (`tsc`) and not `ts-node` in production environments. 
    This choice not only ensures a more efficient memory footprint but also avoids generating unnecessary type information.
    
    It's essential to note that when utilizing Lightrun for TypeScript in a production setting, you must include 
    [sourcemap](https://www.typescriptlang.org/tsconfig#sourceMap) files on the server where your production software is deployed. This step is crucial for seamless debugging and troubleshooting.


**Instructions**

1. Insert the following code at the start of your application file (for example, `index.ts` or `app.ts`).

    ```javascript
    import * as lightrun from 'lightrun';

    lightrun.start({
        lightrunSecret: '<LIGHTRUN_SECRET>',
        filename: <full_path_to_metadata_file>
    });
    ```

  !!! info
       The `filename` parameter is optional. See [here](/node/metadata-and-tagging){:target="_blank"} for details on constructing the metadata file.

2. In the [```compilerOptions```](https://www.typescriptlang.org/tsconfig#compilerOptions){:target="_blank"} section of  the [```tsconfig.json```](https://www.typescriptlang.org/tsconfig#){:target="_blank"} file, set the parameter [`"sourceMap"`](https://www.typescriptlang.org/tsconfig#sourceMap){:target="_blank"} to `"true"`.

3. From a terminal, run the application.

   ```bash
   node index.js
   ```
