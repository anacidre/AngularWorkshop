## Setting up our coffee menu 

Now that we have set up our first Angular app, we will start making changes to develop the coffee app.

We will start developing our app, for now we will focus just on the menu that shows the different types of coffee that can be ordered from the store. 

At the end of this section we will have built the skeleton for the section highlighted in blue below:

<img src="https://github.com/anacidre/AngularWorkshop/blob/master/assets/coffee-app-menu-selection.jpg">

Apps are a representation of the data we can supply and send to our users, and our users can engage with our app to send us data back to a server, for example. 

1. Here’s the data set we’ll be using:

```
coffees: Coffee[] = [
    {
      name: 'Flat white',
      image: '/assets/images/flatWhite.png',
      price: 1.50
    },
    {
      name: 'Capuccino',
      image: '/assets/images/capuccino.png',
      price: 2.50
    },
    {
      name: 'CaramelMachiato',
      image: '/assets/images/caramelMachiato.png',
      price: 3.00
    },
    {
      name: 'Expresso',
      image: '/assets/images/expresso.png',
      price: 2.50
    }
  ];
```

We need to add this data to a component. But just before that let's create the Coffee interface:

Create a folder named 'coffee-interface' under the coffee-order-app/src/app/ folder:

```
cd src/app/
mkdir coffee-interface
cd coffee-interface
```

This folder will contain the definition of the Coffee class. We need to create the file coffee.model.ts inside that folder (we can do that in the IDE) and add the class:

```
export interface Coffee {
  name: string;
  image: string;
  price: number;
}
```

The menu page will have images which will represent the different types of coffee, so let's create the folder where we will put those images. Inside:

```
src/assets
```

We create a folder `images`.

And save (or move) the images there.
<a href="https://github.com/anacidre/AngularWorkshop/blob/master/assets/coffeeImages.zip">coffeeImages.zip </a>

Now we are ready to start with our coffee-menu component.

We can use angular CLI to help us generate an Angular component (which we will do later) but as this is the first time you are building a component we will do it from scratch to understand the structure properly.

First let's create the folder that will contain it. The folder name will match the component name and it should be located at coffee-order-app/src/app/:

```
cd coffee-order-app/src/app/
mkdir coffee-menu
cd coffee-menu
```

Inside of this folder we need to create three files (do this in the IDE):
* coffee-menu.component.ts: controller
* coffee-menu.component.html: template
* coffee-menu.component.scss: style


We now add our data to our coffee-menu.component.ts, to do so we need to import the component and OnInit interfaces from angular/core. We also need to import the coffee class that we just created:

```
import { Component, OnInit } from '@angular/core';

import { Coffee } from '../coffee-interface/coffee.model';

```
Underneath we need to add the component decorator to provide information for Angular to know what to do with the class.
```
@Component({
  selector: 'coffee-menu',
  templateUrl: './coffee-menu.component.html',
  styleUrls: ['./coffee-menu.component.scss']
})
```
Next we need to export the class in the same file which will implement the lifecycle hook OnInit (we will go deeper into this on step 7):

```
export class CoffeeMenuComponent implements OnInit {

  coffees: Coffee[] = [
    {
      name: 'Flat white',
      image: '/assets/images/flatWhite.png',
      price: 1.50
    },
    {
      name: 'Capuccino',
      image: '/assets/images/capuccino.png',
      price: 2.50
    },
    {
      name: 'CaramelMachiato',
      image: '/assets/images/caramelMachiato.png',
      price: 3.00
    },
    {
      name: 'Expresso',
      image: '/assets/images/expresso.png',
      price: 2.50
    }
  ];

  constructor() { }

  ngOnInit() { }
}
```

So the coffee-menu.component.ts should look like this:

```
import { Component, OnInit } from '@angular/core';

import { Coffee } from '../coffee-interface/coffee.model';


@Component({
  selector: 'coffee-menu',
  templateUrl: './coffee-menu.component.html',
  styleUrls: ['./coffee-menu.component.scss']
})

export class CoffeeMenuComponent implements OnInit {

  coffees: Coffee[] = [
    {
      name: 'Flat white',
      image: '/assets/images/flatWhite.png',
      price: 1.50
    },
    {
      name: 'Capuccino',
      image: '/assets/images/capuccino.png',
      price: 2.50
    },
    {
      name: 'CaramelMachiato',
      image: '/assets/images/caramelMachiato.png',
      price: 3.00
    },
    {
      name: 'Expresso',
      image: '/assets/images/expresso.png',
      price: 2.50
    }
  ];

  constructor() { }

  ngOnInit() { }
}
```
We now add this component to our module. Go to coffee-app/src/app/ app.module.ts and import the coffeMenuComponent:
```
import { CoffeeMenuComponent } from './coffee-menu/coffee-menu.component';

```
And add it to declarations:
```
 declarations: [
    AppComponent,
    CoffeeMenuComponent
  ],
```
In our template we'll be using angular material, it needs to be installed using the command specified below:

```
npm install @angular/material@latest --save
npm install @angular/cdk@latest --save
```
We now need to add Angular material to our module. So just where we were in app.module.ts we need to import: 
```
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { MatGridListModule } from '@angular/material/grid-list';
import { MatButtonModule } from '@angular/material/button';
import { MatInputModule } from '@angular/material/input';
import { MatFormFieldModule } from '@angular/material/form-field';
```
and add these to imports:

```
 imports: [
    BrowserModule,
    MatGridListModule,
    BrowserAnimationsModule,
    MatButtonModule,
    MatInputModule,
    MatFormFieldModule
  ],
  
```

You app.module.ts file should look like this:

```
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { MatGridListModule } from '@angular/material/grid-list';
import { MatButtonModule } from '@angular/material/button';
import { MatInputModule } from '@angular/material/input';
import { MatFormFieldModule } from '@angular/material/form-field';

import { AppComponent } from './app.component';
import { CoffeeMenuComponent } from './coffee-menu/coffee-menu.component';


@NgModule({
  declarations: [
    AppComponent,
    CoffeeMenuComponent,
  ],
  imports: [
    BrowserModule,
    MatGridListModule,
    BrowserAnimationsModule,
    MatButtonModule,
    MatInputModule,
    MatFormFieldModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```
So what are all these Modules we just added? Check them out in <a href="https://material.angular.io/">Angular Material</a>.


Now in the coffee-menu.component.html we will add a grid list and most importantly a ngFor which is the Angular "repeater" directive. Anything you see in double curly braces {{coffee.name}} are called Interpolations. They are property bindings, which allow us to access the string value of the corresponding component property.

```
<div class="coffee-menu">
  <mat-grid-list cols="2" rowHeight="2:1" gutterSize="20px">
    <mat-grid-tile class="coffee-tile" *ngFor="let coffee of coffees">
      <div class="coffee-image">
        <img src={{coffee.image}} alt={{coffee.name}}>
      </div>
      <div class="coffee-text">
        <h2 mat-line>{{coffee.name}}</h2>
        <span mat-line>Price: {{coffee.price}}</span>
      </div>
    </mat-grid-tile>
  </mat-grid-list>
</div>
```

Inside coffee-menu.component.scss we will add the necessary styles for this part of the guide.

```
.coffee-menu {
  margin: 5% 10%;
  .coffee-tile {
    background-color: rgba(208,79,2,1);
    border-radius: 1em;
  }
  .coffee-image {
    padding: 1em;
    justify-content: flex-start;
    img{
      width: 100%;
      float: left;
    }
  }
  .coffee-text {
    order: 1;
    color: #ffffff;
    font-family: Verdana, sans-serif;
    h2{
      font-family: Pacifico, sans-serif;
      font-size: 2em;
      text-align: left;
      font-weight: 400;
      -webkit-font-smoothing: antialiased;
      -moz-osx-font-smoothing: grayscale;
      margin: 0 0 0.4em 0;
    }
  }
}

```

Finally let's modify the file app.component.html to reference the coffee-menu component (we can delete everything that is in there):

```
<coffee-menu></coffee-menu>
```

Let's see where we are with our app and serve it.

GREAT! Let's add some finishing touches:

Add a background colour, an angular material theme and the Google Fonts that we will be using to the app in `app/styles.scss`. We are also going to prepare the app for the footer:
```
@import '~@angular/material/prebuilt-themes/pink-bluegrey.css';
@import url('https://fonts.googleapis.com/css?family=Pacifico');

html {
  position: relative;
  min-height: 100%;
}
body {
  background-color: rgba(252, 235, 182, 0.28);
  margin: 0 0 70px; /* bottom = footer height */
}

```
<a href="https://github.com/anacidre/AngularWorkshop/blob/master/Step%203:%20Create%20a%20component%20using%20Angular%20CLI.md">Next: Step 3</a>
