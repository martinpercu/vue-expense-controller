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
- Use the Intl.NumberFormat() constructor. ===> add a const to use it.
- The create the new computhed method using the old visualAmount + the new const with Intl.NumberFormat.

## History Component
- Recact the History move it to new Folder History and change it as Index.vue inside History new folder. This is to have a clear order in the entire app.
- In new Index add the template needed. A title + a v-for for the list of expenses.
- In the script defineProps type array and default a functino returning a list. Then add toRefs to be reactive.
- In the Home in the template call the history expense
- In the script just create a list of expenses to use and show it.
- Add some styles.
- In folder history new file expense.vue. Here is the expense we will loop for in the Index. (Also is to get the app most modular as possible)
- In the Index import this component. Add the 

## History List
- In Index (history folder) improve the "Expense" component with "id description amount title".
- In Expense add this in the defineProps. Obviously ;)
- In Expense template add format to show description title amount + a trash button (show the id of the element ===> to delete it in the future.)
- In the Expense to use the trash defineEmit removeExpense(). 
- To receive this event in the Index template add ===> @removeThisExpense="removeThis". With this we get the ID of the expense to delete it.
- To change the color of the amount in the Expense template add a dynamic class ===> :class="[{  }]". 
- Add a boolean const with computed() to know if amount is positive. Use this const in the :class="[{ 'green': isPositive, 'red': !isPositive  }]".

## Add Expense Modal
- In folder component new file Action.vue. 
- In Action add a button with a click to change the status of showModal (true/false).
- Then add a teleport (to the #app) ==> the MODAL itself. With v-show. This will be show or not if showModal is in true or false.
- Then just add the const showModal with ref(false).
- In folder component new file Modal.vue.
- In Modal add the template with a header and a body. (the header just add title and an icon to close ===> @click="closeModal").
- Then add the function to closeModal with an emits.
- Then in Action listen the "closeModal" to chanche the showModal to false. This will close the modal.
- In Action import Modal!!!. Then us it in the <teleport>. 

## Expense Form
- In Action ==> Add the form with info needed for the expense. ( title + amount + description + expenseType(income or expense).
- Add submit. Just to close the modal. (in the future will use it to add new expense to list)
- Add the const in the script (title + amount + description + expenseType).
- Add some styles.

## SVG Graph
- In folder Resume create Graph.vue. (here will be the graphic to show the expenses evolution in time)
- In Graph add a template. Using <svg> create the example of what we need for this. On middle line (for the Zero value in money). A Polyline to show the fluctuation. and a cross line for show the position we want to see.
- Import the component to Home

## Graph Amount into Pixels
- In Graph.vue. We will change the points in the polyline to make them reactif.
- So add the v-bind in points ====> :points="points"
- Now we add some logic to get the values (amounts) to convert thats as coordinates for the graphics.
- In Home ===> <Graph :amounts="amounts" /> to send the amounts to Graph also.
- In Graph make the logic to get the amounts variable. Then add the functions needs to convert to coordinates.

## Graph Logic
- In the Graph we improve the funtions already had.
- The amountToPixels() ===> with this we send the "position heigh" of each amount.
- Important!! the html svg graph use use on top the "0" and increasing going down. This is the reason we stating getting the "abs" value and then subsctracting from the total heigh.
- We use the same function to get the zero value to draw the gray line in the graph.

## Graph touch interaction
- The vertical line will be follow the touch. So we will replace the x1 and x2 in the Graph template (attention the 3th line, NOT the ZERO one).
- In Graph. In the template in svg add: a v:show="lineShow" and the this 3 event: ===> "@touchstart + @touchmove + @touchend".
- In Graph. add the logic to ose the events to show or not the line.
- Create a const to get the position when @touchstart or @touchmove. Inside this function use console.log(target, touches) to see what returns when click. With this info continue with this funtion. ===> tapActive().
- Add a const lineShowedPosition = ref(0); Then put this const in the 3th line in the x values. ====> :x1="lineShowedPosition" + :x2="lineShowedPosition"
- In the function add the value getted to lineShowedPosition.
- Is possible to make something similar using mouse click. Just add @click="tapActiveClick" in the svg and create the tapActiveClick() function similar as the tapActive().

## Data Model
- In Home add amount to the "theExpenses" add amounts values + time (the moment user add the expense).
- Now the amounts should be the relation between each expense in order. Example if first expense is 50 and the secon expense is 12 the 2nd amounts shoud be 62. This will give us the good coordinates.
- So const amounts using a computed() ===> first get an array of amount from theExpenses. ===> last30DaysExpenses
- Then use slice the last30DaysExpenses and using reduce() return the array wantend.












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
