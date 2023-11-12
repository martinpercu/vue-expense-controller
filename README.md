# expenses-vue

## Starting 
- Start a vue projects with vite.
```sh
npm init vite
```
- Then 
```sh
cd "folder name (same name of project)"
npm install
```
- From now .....
```sh
npm run dev
```
- Add fontawesome.
```sh
npm i --save @fortawesome/fontawesome-svg-core
```
```sh
npm i --save @fortawesome/free-solid-svg-icons
npm i --save @fortawesome/free-regular-svg-icons
npm i --save @fortawesome/free-brands-svg-icons
```
```sh
npm i --save @fortawesome/vue-fontawesome@latest-3
```
- Add FontAwesome in the src/main.js

## Splashscreen
- Create a component splashscreen.vue
- In splashscreen.vue some html to show as splashscreen.
- Add some style.
- IMPORTANT! ===> In App.vue import the Home component as an async Component with a setTimeout of 2500. The idea is to charge the component delayed.
- Then in App.vue use <Suspense> with <template #default> and <template #fallback> to show The splashscreen till the Home component be ready.

## Header and Content
- Create components Header.vue and Layout.vue (the layout will be for the content).
- In Header add the template with the logo and title "CashExpenses", also add a reload() for the icon. 
- In Layout call the template Header with class slot header.

## Layout
- Create components History.vue 
- Create a new folder "Resume" into the components folder. (here will be the main part of the app).
- Then In Resume folder create Index.vue. Add a template with the <main>
- In the Layout.vue add in template 2 divs. One for the Resume and other for the History. Add divs with classes to looks fine. Of course add styles.
- In the Layour.vue implement a onclick to show or not the history with v-show. ===> showHistory + boolean.

## Resume
- In Index.vue add 4 props 2 for label + 2 for amount. Also add 2 computed funtions (visualAmount() and visualLabel()) for this label and amount will be show in the template.
- Add in the template {{ visualAmount }} and {{ visualLabel }}.
- In Home send the 4 binding. ===>  label + date-label + amount + total-amount.
- In Home create add the needed const for date-label and initial amount.
- I left 2 sames const "initialAmount" one commented. Just to see how works the script.

## Money Format, Graphic and button action.
- In Home add 2 divs for chart + the button.
- In Index add new varible in the template to show the currency formated.
- Use the Intl.NumberFormat() constructor. ===> add a const to use it
- The create the new computhed method using the old visualAmount + the new const with Intl.NumberFormat.







This template should help get you started developing with Vue 3 in Vite.

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur) + [TypeScript Vue Plugin (Volar)](https://marketplace.visualstudio.com/items?itemName=Vue.vscode-typescript-vue-plugin).

## Customize configuration

See [Vite Configuration Reference](https://vitejs.dev/config/).

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```

### Lint with [ESLint](https://eslint.org/)

```sh
npm run lint
```
