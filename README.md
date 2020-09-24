# React Settings

## Create TypeScript Project

1. プロジェクトの作成

    ```bash
    npx create-react-app my-app --template typescript
    cd my-app
    code .
    ```

1. build時に相対パスで処理できるようにpackage.jsonに`"homepage": ".",`を追加。

    ```json:package.json
    "homepage": ".",
    ```

1. `npm start` と `npm run build` で `homepage` を分ける場合

    [GitHubPages](#githubpages)を参照

## eslint + airbnb + prettier

1. `npm i -D eslint-config-airbnb eslint-config-react-app eslint-plugin-import eslint-plugin-react eslint-plugin-react-hooks eslint-plugin-jsx-a11y @typescript-eslint/parser @typescript-eslint/eslint-plugin eslint-config-prettier eslint-plugin-prettier prettier`
1. `npx eslint --init` 最後のインストールしますか？でNを選択。
1. package.josonから`"eslintConfig": { "extends": "react-app" }`を削除。
1. .eslintrc.jsonに以下を追加。

    ```json:.eslintrc.json
    "extends": [
      "plugin:react/recommended",
      "airbnb",
      "airbnb/hooks",
      "plugin:@typescript-eslint/recommended",
      "plugin:prettier/recommended",
      "prettier/react",
      "prettier/@typescript-eslint"
    ],
    "settings": {
      "import/resolver": {
        "node": {
          "extensions": [".js", ".jsx", ".ts", ".tsx"]
        }
      }
    },
    "rules": {
      "import/extensions": [
        "error",
        "ignorePackages",
        {
          "js": "never",
          "jsx": "never",
          "ts": "never",
          "tsx": "never"
        }
      ],
      "react/jsx-filename-extension": [1, { "extensions": [".ts", ".tsx"] }]
    }
    ```

1. .prettierrc.jsonを作成し以下を追加。

    ```json:.prettierrc.json
    {
      "singleQuote": true
    }
    ```

## [react-bootstrap](https://react-bootstrap.github.io/)

1. `npm i react-bootstrap bootstrap`
1. App.jsxなどでimportして使用する。

    ```javascipt:App.jsx
    import { Container, Row, Col, Form } from 'react-bootstrap';
    import 'bootstrap/dist/css/bootstrap.min.css';
    ```

## [Font Awesome](https://fontawesome.com/how-to-use/on-the-web/using-with/react)

1. `npm i @fortawesome/fontawesome-svg-core @fortawesome/free-solid-svg-icons @fortawesome/react-fontawesome`
1. コンポーネント毎に個別にインポートする

    ```javascript:App.jsx
    import ReactDOM from 'react-dom'
    import { FontAwesomeIcon } from '@fortawesome/react-fontawesome'
    import { faCoffee } from '@fortawesome/free-solid-svg-icons'

    const element = <FontAwesomeIcon icon={faCoffee} />

    ReactDOM.render(element, document.body)
    ```

1. グローバルにインポートしてコンポーネントから参照する

    1. 親コンポーネントにlibraryを利用してインポート

        ```javascript:App.jsx
        import ReactDOM from 'react-dom'
        import { library } from '@fortawesome/fontawesome-svg-core'
        import { fab } from '@fortawesome/free-brands-svg-icons'  // ブランドアイコンをまとめてインポート
        import { faCheckSquare, faCoffee } from '@fortawesome/free-solid-svg-icons'  // 個別にインポート

        library.add(fab, faCheckSquare, faCoffee)
        ```

    1. 子コンポーネントで使用

        ```javascript:children.jsx
        import React from 'react'
        import { FontAwesomeIcon } from '@fortawesome/react-fontawesome'

        export const Beverage = () => (
          <div>
            <FontAwesomeIcon icon="check-square" />
            Your <FontAwesomeIcon icon="coffee" /> is hot and ready!
          </div>
        )
        ```

## Deploy

### GitHub

1. GitHubにレポジトリ作成
1. `git remote add origin git@github.com:myname/my-app.git`
1. `git push -u origin master`

### GitHubPages

1. `npm i -D cross-env gh-pages`
1. package.jsonに以下を追加

    ```json:package.json
    "homepage": "https://myusername.github.io/my-app",
    "scripts": {
      "start": "cross-env PUBLIC_URL=. react-scripts start",
      "build": "react-scripts build",
      "deploy": "gh-pages -d build"
    }
    ```

1. `npm run build`
1. `npm run deploy`
