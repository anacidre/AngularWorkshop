## Build your first Angular App

First of all we need to install angular-cli, the command line tool for scaffolding Angular applications.

```
npm install -g @angular/cli
```

Now we can generate our fist Angular Project using Angular-CLI.
First let's create a folder where we will keep the examples that will be developed at this workshop. So choose your favorite location create a directory and move into it:

```
mkdir angular-workshop
cd angular-workshop
```

Then type the following at the prompt to create your first Angular application (here we are adding the styling scss as the styles we will be using later in the workshop have the scss syntax):

```
ng new coffee-order-app --style=scss
```

Now there will be a folder named coffee-order-app in your angular-workshop folder.
Move to coffee-order-app and start serving your app:

```
cd coffee-order-app
ng serve --open
```
To stop serving use ctrl + c.

We now have to open up our app in our favourite IDE such as webstorm, VS Code, sublime text, ...
