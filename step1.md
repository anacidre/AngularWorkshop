## First Angular App

First of all we need to install angular-cli, the command line tool for scaffolding Angular applications.

```
npm install -g @angular/cli
```

Now we can generate our fist Angular Project using Angular-CLI.
Fist let's create a folder where we'll keep the examples that will be developed at this workshop. So choose your favorite location and type:

```
mkdir angular-workshop
cd angular-workshop
```

Then type the following at the prompt to create your first Angular application:

```
ng new coffee-order-app --style=scss
```

Now there will be a folder named coffee-order-app at your angular-workshop folder.
Move to coffee-order-app and start serving your app:

```
cd coffee-order-app
ng serve --open
```
