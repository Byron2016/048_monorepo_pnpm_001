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
Mohit Kumar Toshniwal's tutorial [Build a Monorepo using PNPM workspace, React, Vue, Node, Eslint, Prettier and Typescript](https://www.youtube.com/watch?v=pz4f9Q6VYZA)
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
