# Basic-Setting
`yarn create vite`
`프로젝트 명  작성:`
`REACT`
`typescript swc`
`yarn`
`yarn dev --port 3000 `
`code .`
`리액트 폴더에 들어가서 yarn dev —port 3000`
⇒ 프로젝트 설정 완료!
프리티어 설정 맞추기. (extension prettier 깔려있어야함)
yarn add prettier 할 수도 있지만 rc 설정 파일을 올리면 따로 설정해주지 않아도 최우선으로 본다.
.prttierrc (최상단 루트 폴더에)
**`{
"trailingComma": "none",`**
**//요소를 쓸때  name: 2, 엔터 칠때 마지막 프로퍼티 값에 찍어주면 all 아니면 none
`"tabWidth": 2,
"semi": true,
"singleQuote": true,
"arrowParens": "always",`**
// 매개변수 인자값이 하나여도 괄호를 씌울 것이냐
**`"printWidth": 80,`**
// 80자 이상이면 다음줄로
**`"quoteProps": "as-needed",
"jsxSingleQuote": false,
"bracketSpacing": true,
"jsxBracketSameLine": false,
"vueIndentScriptAndStyle": false,
"endOfLine": "auto"
}`**
cmd + p 하면 vs code 검색창 뜬다
>settings 에서 사용자 설정 JSON 파일 들어가서
가장 마지막 부분에, 추가하고 새로운 행에서
`"[typescriptreact]": { "editor.formatOnSave": true, "editor.defaultFormatter": "esbenp.prettier-vscode" }` // eslint 맞추지 않아도 자동으로 변환해준다.
```
{
  "compilerOptions": {
    "composite": true,
    "skipLibCheck": true,
    "module": "CommonJS",
    "allowSyntheticDefaultImports": true
  },
  "include": ["vite.config.ts"]
}
```
**tsconfig.json**
tsconfig 에서 아래 부분 바꿔준다. 우리문법은 es6 부터 바뀌었기때문에 원래의 설정처럼 해주면 그 이전의 브라우저들은 해석안돼, so 그걸 바꿔주는 부분
```json
"compilerOptions": {
    "target": "ES5",
    "lib": ["DOM", "DOM.Iterable", "ESNext"],
    "module": "CommonJS",
    "skipLibCheck": true,
  	"allowJs": true,
  	"esModuleInterop": true, // 이거해야 자체 모듈 허용 에러 사라짐
```
```json
"include": [".eslintrc.cjs","src"], // 우리가 eslintrc 수정해줄 파일
  "references": [{ "path": "./tsconfig.node.json" }]
```
"moduleResolution": "bundler", // 삭제하고 세이브 하면 오류 사라짐
**module.exports = {
env: { browser: true, es2020: true, node: true },
extends: [
'airbnb',
'airbnb-typescript',
'airbnb/hooks',
'plugin:react/recommended',
'plugin:@typescript-eslint/recommended',
'plugin:prettier/recommended'
],
parser: '@typescript-eslint/parser',
parserOptions: {
ecmaVersion: 'latest',
sourceType: 'module',
project: './tsconfig.json'
},
plugins: ['react', '@typescript-eslint', 'prettier'],
rules: {}
};**
**tsconfig.node.json**
```json
{
  "compilerOptions": {
    "composite": true,
    "skipLibCheck": true,
    "module": "CommonJS",
    "allowSyntheticDefaultImports": true
  },
  "include": ["vite.config.ts"]
}
```
**eslint 설정**
yarn add eslint-config-airbnb
yarn add eslint-config-airbnb-typescript
yarn add -D prettier eslint-config-prettier eslint-plugin-prettier
**.eslintrc.cjs**
```jsx
module.exports = {
env: { browser: true, es2020: true, node: true },
extends: [
'airbnb',
'airbnb-typescript',
'airbnb/hooks',
'plugin:react/recommended',
'plugin:@typescript-eslint/recommended',
'plugin:prettier/recommended'
],
parser: '@typescript-eslint/parser',
parserOptions: {
ecmaVersion: 'latest',
sourceType: 'module',
project: './tsconfig.json'
},
plugins: ['react', '@typescript-eslint', 'prettier'],
rules: {} // airbnb에서 끄고 싶은 옵션들을 끄면 됨!
rules: {'no-console': 'off',}..? 뭘 삭제해준다고? 해도 되고 안해도 됨
};
```
yarn add prettier -D
**tsconfig.json**
```json
{
  "name": "test-project",
  "private": true,
  "version": "0.0.0",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "tsc && vite build",
    "lint": "eslint src --ext ts,tsx --report-unused-disable-directives --max-warnings 0",
    "preview": "vite preview",
    "format": "prettier --cache --write ."//
  },
  "dependencies": {
    "eslint-config-airbnb": "^19.0.4",
    "eslint-config-airbnb-typescript": "^17.0.0",
    "react": "^18.2.0",
    "react-dom": "^18.2.0"
  },
  "devDependencies": {
    "@types/react": "^18.0.28",
    "@types/react-dom": "^18.0.11",
    "@typescript-eslint/eslint-plugin": "^5.57.1",
    "@typescript-eslint/parser": "^5.57.1",
    "@vitejs/plugin-react-swc": "^3.0.0",
    "eslint": "^8.38.0",
    "eslint-config-prettier": "^8.8.0",
    "eslint-plugin-prettier": "^4.2.1",
    "eslint-plugin-react-hooks": "^4.6.0",
    "eslint-plugin-react-refresh": "^0.3.4",
    "prettier": "^2.8.8",
    "typescript": "^5.0.2",
    "vite": "^4.3.2"
  }
}
```
## **Error Lens - 오류를 띄워주는 extention**
```json
{
  "compilerOptions": {
    "target": "ES5",
    "lib": ["DOM", "DOM.Iterable", "ESNext"],
    "module": "CommonJS",
    "skipLibCheck": true,
    "esModuleInterop": true, <<---------- *// 외부 모듈 추가해라?*
    /* Bundler mode */
    "allowImportingTsExtensions": true,
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react-jsx",
    /* Linting */
    "strict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noFallthroughCasesInSwitch": true
  },
  "include": [".eslintrc.cjs", "src"],
  "references": [{ "path": "./tsconfig.node.json" }]
}
```
**yarn add @types/node @types/react @types/react-dom @types/jest typescript**
