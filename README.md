<div>
	<div>
		<img src=https://raw.githubusercontent.com/Byron2016/00_forImages/main/images/Logo_01_00.png align=left alt=MyLogo width=200>
	</div>
	&nbsp;
	<div>
		<h1>042_node_electron_react_001</h1>
	</div>
</div>

&nbsp;

# Table of contents

---

- [Table of contents](#table-of-contents)
- [Project Description](#project-description)
- [Technology stack](#technology-stack)
- [Technologies used](#technologies-used)
- [References](#references)
- [Steps](#steps)

[⏪(Back to top)](#table-of-contents)

# Project Description

**048_monorepo_pnpm_001"** is a practice to build a **PNPM Monorepo** following Youtube
Mohit Kumar Toshniwal's tutorial [Build a Monorepo using PNPM workspace, React, Vue, Node, Eslint, Prettier and Typescript](https://www.youtube.com/watch?v=pz4f9Q6VYZA) [Github](https://github.com/mohitkumartoshniwal/monorepo/tree/main)
and the other help that you can find into **Reference** section.

# Technology stack

We are going to use

- We are going to use **pnpm** to create a **monorepo**.
- We are going to use **TypeScript**.
- **Backend**: We are going to use **Nodejs** with **express**.
- **Frondend**: We are going to use **Reactjs** and **Vuejs**.
- **Library**: We are going to use a common library for banckend and fronend applicatons.

[⏪(Back to top)](#table-of-contents)
&nbsp;

# Technologies used

![PNPM](https://img.shields.io/badge/pnpm-%234a4a4a.svg?style=for-the-badge&logo=pnpm&logoColor=f69220)
![NodeJS](https://img.shields.io/badge/node.js-6DA55F?style=for-the-badge&logo=node.js&logoColor=white)
![Express.js](https://img.shields.io/badge/express.js-%23404d59.svg?style=for-the-badge&logo=express&logoColor=%2361DAFB)
![TypeScript](https://img.shields.io/badge/typescript-%23007ACC.svg?style=for-the-badge&logo=typescript&logoColor=white)
![React](https://img.shields.io/badge/react-%2320232a.svg?style=for-the-badge&logo=react&logoColor=%2361DAFB)
![Vue.js](https://img.shields.io/badge/vuejs-%2335495e.svg?style=for-the-badge&logo=vuedotjs&logoColor=%234FC08D)

[⏪(Back to top)](#table-of-contents)

# References

- Shields.io

  - [Shields.io](https://shields.io/)

  - [Github Ileriayo markdown-badges](https://github.com/Ileriayo/markdown-badges)

  - [Github Ileriayo markdown-badges WebSite](https://ileriayo.github.io/markdown-badges/)

[⏪(Back to top)](#table-of-contents)

# Steps

- Add package.json file

  ```bash
  pnpm init
  ```

- Prettier

  - Add prettier dev dependency

  ```bash
  pnpm add -D prettier
  ```

  - Add .prettierignore file

  ```bash
  touch .prettierignore
  echo "coverage
  public
  dist
  pnpm-workspace.yaml
  pnpm-lock.yaml" > .prettierignore
  ```

  - Add .prettierrc file

  ```bash
  touch .prettierrc
  echo "{
  \"semi\": true,
  \"singleQuote\": true
  }" > .prettierrc
  ```

  - Add package.json scrpts

  ```bash
  npm pkg set scripts.format="pnpm prettier --check"
  npm pkg set scripts.format:write="pnpm prettier --write"
  ```

- Add .vscode

  - Add and configure .vscode settings.json

  ```bash
  mkdir .vscode
  cd .vscode
  touch settings.json
  echo "{
  \"editor.formatOnSave\": true,
  \"editor.defaultFormatter\": \"esbenp.prettier-vscode\"
  }" > settings.json
  cd ..
  ```

  - Add esben.prettier-vscode extension to VSCode.

- ESLint

  - Add ESLint dev dependency

  ```bash
  pnpm create @eslint/config

  # ? How would you like to use ESLint?         · To check syntax only
  # How would you like to use ESLint?           · problems
  # What type of modules does your project use? · esm
  # Which framework does your project use?      · none
  # Does your project use TypeScript?           · typescript
  # Where does your code run?                   · browser
  # The config that you have selected requires the following dependencies:
  #  --> eslint, globals, @eslint/js, typescript-eslint
  # ? Would you like to install them now?       ·  Yes
  # Which package manager do you want to use?   · pnpm
  ```

  - Add eslint-config-prettier to aboit prettier and ESLint confligs

  ```bash
  pnpm i -D eslint-config-prettier
  ```

  ```javascript
  ....
  import eslintConfigPrettier from 'eslint-config-prettier';

  export default [
  	....
  	eslintConfigPrettier,
  ];
  ```

  - Add package.json scrpts

  ```bash
  npm pkg set scripts.lint:nofix="eslint ."
  npm pkg set scripts.lint="eslint . --fix"
  npm pkg set scripts.lint:inspect:write="eslint --inspect-config"
  ```

- Install husky and lint-staged

  - Add husky and lint-staged dev dependency

  ```bash
  pnpm add -D husky lint-staged
  ```

  ```bash
  npx husky init
  node --eval "fs.writeFileSync('.husky/pre-commit','pnpm exec lint-staged\n')"
  ```

  - Update package.json

  ```json
  {
    ....
    "lint-staged": {
      "**/*.{js,ts,tsx}": [
        "eslint --fix"
      ],
      "**/*": "prettier --write   --ignore-unknown"
    }
  }
  ```

- Worksapaces

  - Add workspaces definition file

  ```bash
    touch pnpm-workspace.yaml
    echo "packages:
  - 'apps/*'
  - 'libs/*'" > pnpm-workspace.yaml

  ```

  - Add apps and libs folders

  ```bash
    mkdir apps libs

  ```

  - Create a vite project

  ```bash
    cd libs
    pnpm create vite utils

  # ? Select a framework:         · Vanilla
  # ? Select a variant:           · TypeScript
  # What type of modules does your project use? · esm
  # Which framework does your project use?      · none
  # Does your project use TypeScript?           · typescript
  # Where does your code run?                   · browser
  # The config that you have selected requires the following dependencies:
  #  --> eslint, globals, @eslint/js, typescript-eslint
  # ? Would you like to install them now?       ·  Yes
  # Which package manager do you want to use?   · pnpm

    pnpm i
    cd ..

  ```

  - Delete files / folders

  ```bash
  cd libs/utils
  rm index.html
  rm -rf public
  cd src
  rm style.css typescript.svg counter.ts
  cd ../../..

  ```

  - Add utils/package.json scrpts

  ```bash
  cd libs/utils
  npm pkg set scripts.dev="pnpm run build --watch"
  npm pkg set scripts.dev:old="vite"
  cd ../..
  ```

  Note: dev script: so that any change in the code will rebuild automatically and reflect in the **web-app** in real-time

  - Update utils/src/main.ts

  ```javascript
  export const isEmpty = (data: unknown) => {
    if (data === null || data === undefined) {
      return 'It is Empty';
    }
    return 'It is not Empty';
  };
  ```

  - Add vite-plugin-dts dependency

  ```bash
  cd libs/utils
  pnpm i -D vite-plugin-dts
  pnpm i -D @types/node # to avoid errors in vite-config.ts "Cannot find module 'path' or its corresponding type declarations"
  cd ../..
  ```

  - Update libs/utils/package.json

  ```bash
  cd libs/utils
  npm pkg set main="./dist/utils.umd.cjs"
  npm pkg set module="./dist/utils.js"
  npm pkg set types="./dist/main.d.ts"
  cd ../..
  ```

  - Add libs/utils/vite.config.ts

  ```javascript
  import { resolve } from 'path';
  import { defineConfig } from 'vite';
  import dts from 'vite-plugin-dts';

  export default defineConfig({
    build: { lib: { entry: resolve(__dirname, 'src/main.ts'), name: 'utils' } },
    plugins: [dts()],
  });
  ```

  - backend (19.19)

    - Create backend folder

    ```bash
      cd apps && mkdir backend && cd backend
      pnpm init
      npm pkg set type="module"
      cd ../..

    ```

    - Add ./apps/backend/tsconfig.json file

    ```bash
      cd apps/backend
      npx tsc --init

    ```

    ```json
    {
      "compilerOptions": {
        "module": "ES2020",
        "moduleResolution": "Node16",
        "target": "ES2020",
        "sourceMap": true,
        "outDir": "dist",
        "esModuleInterop": true,
        "allowSyntheticDefaultImports": true,
        "strict": true
      },
      "include": ["src/**/*"]
    }
    ```

    - Add ./apps/backend/nodemon.json

    ```json
    {
      "execMap": {
        "ts": "ts-node-esm"
      }
    }
    ```

    - **Note:**:

      - ts-node
        - It is the same: "ts": "ts-node-esm" and "ts": "ts-node --esm"
        - To call "ts-node-esm" generates a error, solve it with
          - "tsOKa": "node --inspect --experimental-loader ts-node/esm",
            - [solve experimental-loader](https://github.com/TypeStrong/ts-node/issues/2100#issuecomment-2039564225)
          - Or use tsx
      - tsx
        - "ts": "tsx"

    - Add dependencies and dev dependencies

    ```bash
      cd apps/backend
      pnpm i express cors
      pnpm i -D @types/cors @types/express  @types/node ts-node
      pnpm i -D tsx # to solve ts-node problem.
      cd ../..

    ```

    - Add apps/backend/src/app.ts

    ```bash
      cd apps/backend
      mkdir apps && touch app.ts
      # cd ../..

    ```

    ```javascript
    import express from 'express';
    import cors from 'cors';
    import utils from 'utils';

    const PORT = process.env.PORT || 5000;

    const app = express();

    app.use(cors());

    app.get('/', (req, res) => {
      res.json({ message: utils.isEmpty('abc') });
    });

    app.listen(PORT, () => {
      console.log(`Server running on PORT ${PORT}`);
    });
    ```

    - Enable "libs/util" in apps/backend/package.json

    ```json
    {
      ....
      "dependencies" : {
        ....
        "utils": "workspace:*"
      }
    }

    ```

    - with code

    ```bash
      cd apps/backend
      npm pkg set scripts.dev="nodemon src/app.ts"
      pnpm i -D nodemon
      cd ../..

    ```

    - Update dependencies

    ```bash
      cd apps/backend
      pnpm i
      cd ../..

    ```

    - Add typescript dev dependency to monorepo root package.json

    ```bash
      pnpm i -D typescript -w

    ```

  - backend (28)

    - Create frontends' apps

      - react-frontend app

      ```bash
        cd apps
        pnpm create vite
        # Project name: react-frontend
        # Select a framework: React
        # Select a variant: Typescript
        cd react-frontend
        pnpm i
        pnpm run dev
        cd ../..

      ```

      - vue-frontend app

      ```bash
        cd apps
        pnpm create vite
        # Project name: vue-frontend
        # Select a framework: Vue
        # Select a variant: Typescript
        cd react-frontend
        pnpm i
        pnpm run dev
        cd ../..

      ```

    - Enable "libs/util"

      - in react-frontend app

      ````json
      {
        ....
        "dependencies" : {
          ....
          "utils": "workspace:*"
        }
      }


      ```bash
        cd apps/react-frontend
        pnpm i
        cd ../..
      ````

      - in vue-frontend app

      ```json
      {
        ....
        "dependencies" : {
          ....
          "utils": "workspace:*"
        }
      }

      ```

      ```bash
        cd apps/vue-frontend
        pnpm i
        cd ../..
      ```

    - Fetch backend app and libs/utils

      - from react-frontend app

      ```javascript
        // apps/react-frontend/src/App.tsx
        ....
        import { isEmpty } from 'utils';

        function App() {
          const [count, setCount] = useState(0);

          useEffect(() => {
            fetch('http://localhost:5000')
              .then((data) => data.json())
              .then((data) => console.log(data));
          }, []);

          return (
            <>
              ....
              <pre>{isEmpty('abc')}</pre>
              <pre>{isEmpty(null)}</pre>
            </>
          );
        }

        export default App;

      ```

      - from vue-frontend app

      ```javascript
        // apps/vue-frontend/src/App.vue

        <script setup lang="ts">
        ....
        import { onMounted } from 'vue';
        import { isEmpty } from 'utils';

        onMounted(() => {
          fetch('http://localhost:5000')
            .then((data) => data.json())
            .then((data) => console.log(data));
        });
        </script>

        <template>
          ....
          <HelloWorld msg="Vite + Vue" />

          <pre>{{ isEmpty('abc') }}</pre>
          <pre>{{ isEmpty(null) }}</pre>
        </template>

        <style scoped>
        ....
        </style>


      ```

    - Add script to run ./package.json

    ```json
    {
      ....
      "scripts" : {
        ....
        dev="pnpm --parallel --stream -r run dev"
      }
    }

    ```

    - with code

    ```bash
      cd .
      npm pkg set scripts.dev="pnpm --parallel --stream -r run dev"

    ```
