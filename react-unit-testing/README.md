1 - Instalation and configuration the Jest and Testing Library

 - Add Jest as a dev depedency:
    ```console
    npm i jest -D
    ```

    Install the types as a development dependency if using TypeScript:
    ```console
    npm i @types/jest -D
    ```

 - Initialize the Jest:
    ```console
    npx jest --init
    ```
    Select this configurations:
    ```console
    √ Would you like to use Jest when running "test" script in "package.json"? ... yes    
    √ Would you like to use Typescript for the configuration file? ... yes
    √ Choose the test environment that will be used for testing » jsdom (browser-like)
    √ Do you want Jest to add coverage reports? ... no
    √ Which provider should be used to instrument code for coverage? » v8
    √ Automatically clear mock calls, instances, contexts and results before every test? ... yes
    ```

 - Add **transform** in `jest.config.ts`
   ```ts
   export default {
      //...othes configurations
      transform: {
         "^.+\\.(t|j)sx?$": [
            "@swc/jest",
            {
            jsc: {
               parser: {
                  syntax: "typescript",
                  tsx: true,
                  decorators: true,
               },
               keepClassNames: true,
               transform: {
                  legacyDecorator: true,
                  decoratorMetadata: true,
                  react: {
                  runtime: "automatic",
                  },
               },
            },
            module: {
               type: "es6",
               noInterop: false,
            },
            },
         ],
      },
   }
   
   ```

 - Install ts-node as a development dependency if using TypeScript 
    ```console
    npm i ts-node -D
    ```
 - Install the SWC (stands for Speedy Web Compiler) as a dev depedency
    ```console
    npm i @swc/core @swc/jest -D
    ```
 - Install the Testing Library as a dev depedency
    ```console
    npm i @testing-library/react @testing-library/jest-dom @testing-library/user-event -D
    ```

  - To run the tests, use:
    ```console
    npm test
    ```
    To run all tests every time you save the file, change this in `package.json`:

    from: 
    ```json
    "scripts": {
      //...othes scripts
     "test": "jest"
    },
    ```
    to: 
    ```json
    "scripts": {
      //...
     "test": "jest --watchAll"
    },
    ```

  - Error if using react 18
    ```console
    ● Validation Error:
    nt configuration option points to an existing node module.
    
    Configuration Documentation:
    https://jestjs.io/docs/configuration
    
    As of Jest 28 "jest-environment-jsdom" is no longer shipped by default, make sure to install it separately.
    ```
    To fix it, do this:
    ```console
    npm i -D jest-environment-jsdom
    ```