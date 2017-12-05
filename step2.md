## Setting up our coffee menu - Our first component

Now that we have set up our first Angular app, we will start making changes to develop our Hipster Coffee web.

We will start developing our app, for now we will focus just on the menu that shows the different types of coffee that can be ordered from the store. To do that we will create a new component from scratch.

At the end of this section we will have built the skeleton for the section highlighted in blue below:

![picture](https://github.com/Vero333/angularWorkshopGuide/blob/master/guideResources/images/coffe-order-app.jpg)


We can use angular CLI to help us to create an Angular component (which we will do that later) but as this is the first time you we are building a component we will do it from scratch to understand the structure properly.

But before that let's create the Coffee class:

Create a folder named shared under the coffee-order-app/src/app/ folder:

```
cd coffee-order-app/src/app/
mkdir shared
cd shared
```

This folder will contain the definition of the Coffee class. We create the file coffee-class.ts and add the class:

```
export class Coffee {
  name: string;
  image: string;
  price: number;
}
```

The menu page will have images which will represent the different types of coffee, so let's create the folder where we will put those images:

```
cd coffee-order-app/src/assets
mkdir images
```

And save the images there.
Markup :  [coffeImages.zip](https://github.com/Vero333/angularWorkshopGuide/raw/master/guideResources/images/coffeeImages.zip)

Now we are ready to start with our coffee-menu component.
First let's create the folder that will contain it. The folder name will match the component name and it should be located at coffee-order-app/src/app/:

```
cd coffee-order-app/src/app/
mkdir coffee-menu
cd coffee-menu
```

Inside of this folder we need to create three files:
* coffee-menu.component.ts: controller
* coffee-menu.component.html: template
* coffee-menu.component.scss: style


coffee-menu.component.ts:

```
import { Component, OnInit } from '@angular/core';

import { Coffee } from '../shared/coffee';

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

In our template we'll be using angular material, it needs to be installed using the command specified below:

```
npm install @angular/material@latest --save
npm install @angular/cdk@latest --save
```

coffee-menu.component.html

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

coffee-menu.component.scss

```
.coffee-menu {
  margin: 5% 10%;
  .coffee-tile {
    background-color: darkorange;
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
      font-size: 1.5em;
      text-align: left;
    }
  }
}

```

Now we need to modify the file app.module.ts

```
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { MatGridListModule } from '@angular/material/grid-list';

import { AppComponent } from './app.component';

import { CoffeeMenuComponent } from './coffee-menu/coffee-menu.component';

@NgModule({
  declarations: [
    AppComponent,
    CoffeeMenuComponent
  ],
  imports: [
    BrowserModule,
    BrowserAnimationsModule,
    MatGridListModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }

```

Finally let's modify the file app.component.html to reference the coffee-menu component:

```
<coffee-menu></coffee-menu>
```

