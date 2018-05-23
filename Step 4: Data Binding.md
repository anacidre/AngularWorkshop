## Data Bindings

You can use Angular data bindings to respond to any DOM event. There are four different types of data bindings, one which we have already seen:

- <b>Interpolation:</b> With interpolation you can display a component property. To do so, you put the property name in the view template,       enclosed in double curly braces: `{{coffee.price}}`

- <b>Property binding:</b> It flows a value in one direction, from a component's data property into a target element property. Which is what we are going to do next. We use square brackers to access the property name like this: `[totalOrder]="total"`

- <b>Event binding:</b> Users don't just stare at the screen. They enter text into input boxes. They pick items from lists. They click           buttons. Such user actions may result in a flow of data in the opposite direction: from an element to a component. To do this we use       the parenthesis `()` to access a DOM event name. You can see this here: `<button mat-button (click)="onClick(i)">FREE</button>`

- <b>Two-way binding:</b> You often want to both display a data property and update that property when the user makes changes.
       We can use `[(ngModel)]` or a `#`. We will go more into detail once we get there.

Let's add a button to our coffee-menu component, the idea is that when the user clicks on that button the price of that coffee is updated to 0.00.

### Interpolation and Event binding

We will add a button that uses event binding in our mat-grid-tile and we will specify the target when the button is clicked.

<img src="https://github.com/anacidre/AngularWorkshop/blob/master/assets/freeCoffee.png">

First we'll need to add an index to our ngFor:

```

    <mat-grid-tile class="coffee-tile" *ngFor="let coffee of coffees; let i=index">
      <div class="coffee-image">
       ...

        <span mat-line>Price: {{coffee.price}}</span>
        <button mat-button (click)="onClick(i)">FREE</button>
      </div>
     </mat-grid-list>
</div>
<app-total-order></app-total-order>
```
We can see that we are using interpolation ` {{coffee.price}}` to access the price of the coffee. We have seen interpolation in previous steps already.

The target will be the onClick method that is defined in the coffee-menu.component.ts. So let's add that before our constructor

```
onClick(index) {
  this.coffees[index].price = 0.00;
}
```
### Property binding

But that is not really what we want to do, we want to be able to specify how many coffees the user wants to order.
And to do so we will be using property binding. First let's make some changes in the coffee interface and our coffee array. Add the property quantity to the coffee.model.ts:

```
export interface Coffee {
  name: string;
  image: string;
  price: number;
  quantity: number;
}
```
We now need to add a quantity to our array of coffees in coffee-menu.component.ts:

```
 coffees: Coffee[] = [
    {
      name: 'Flat white',
      image: '/assets/images/flatWhite.png',
      price: 1.50,
      quantity: 0,
    },
    {
      name: 'Capuccino',
      image: '/assets/images/capuccino.png',
      price: 2.50,
      quantity: 0,
    },
    {
      name: 'Caramel Machiato',
      image: '/assets/images/caramelMachiato.png',
      price: 3.00,
      quantity: 0,
    },
    {
      name: 'Expresso',
      image: '/assets/images/expresso.png',
      price: 2.50,
      quantity: 0,
    }
  ];
```


Amend the file coffee-menu.component.html to add an input where the user can introduce the amount of coffees to order. Change the button name and value.

```
<div class="coffee-menu">
  <mat-grid-list cols="2" rowHeight="2:1" gutterSize="20px">
    <mat-grid-tile class="coffee-tile" *ngFor="let coffee of coffees; let i=index">
      <div class="coffee-image">
        <img src={{coffee.image}} alt={{coffee.name}}>
      </div>
      <div class="coffee-text">
        <h2 mat-line>{{coffee.name}}</h2>
        <span mat-line>Price: {{coffee.price}}</span>
        <div>
          <mat-form-field color="accent">
            <input matInput type=number max="10" min="0" title="quantity" placeholder="quantity" #order>
          </mat-form-field>
        </div>
        <button mat-button (click)="onClick(i, order.value)">DONE</button>
      </div>
    </mat-grid-tile>
  </mat-grid-list>
</div>
<app-total-order></app-total-order>
```

Now we need to add our one-way data binding `[totalOrder]="total"` to our `<app-total-order>` component like this:

```
<app-total-order [totalOrder]="total"></app-total-order>
```
One way data binding from a data source to the view target means that values from the view are not passed back to the component, while any changes made to the expression in the component are reflected in the view - it is one way data binding from data source to the view.

We then make the button more visible by adding the following to coffee-menu.component.scss:
```
.mat-button{
    background-color: rgba(255, 255, 255, 0.35);
    }
```

Now we need to re-implement the behaviour when the user clicks on the DONE button in the `coffee-menu.component.ts`:

```
total: number = 0;

onClick(index, order) {
  this.coffees[index].quantity = order;
  for (let coffee of this.coffees) {
    this.total += coffee.price * coffee.quantity;
  }
  console.log(this.total);
}
```

What we want to do now is pass the order total from the coffee-menu component to the order component, to do so we need to use the decorator `@Input`, that will be imported as well in the component:

```
import { Component, OnInit, Input } from '@angular/core';

@Component({
  selector: 'app-order',
  template: `total-order works!`,
  styleUrls: ['./total-order.component.scss']
})
export class TotalOrderComponent implements OnInit {
  @Input() totalOrder: number;

  constructor() { }

  ngOnInit() {
  }
}
```
### Two-way data binding

Let's welcome our users! We will add an input box where the user can add his or her name. To do this we will be using two-way data binding, like this:

<img src="https://github.com/anacidre/AngularWorkshop/blob/master/assets/welcome-nav.jpg">

We will be using the `[(ngModel)]` directive to implement this. The `[(ngModel)]` takes care of updating the underlying input DOM  element.


First we will create a component

```
ng g c welcome-nav  
```

We add the html to our `welcome-nav.component.ts` template:
```
<div class="welcome-nav">
  <mat-form-field color="accent" class="username-input">
    Enter your username: <input matInput [(ngModel)]="username" class="orange-underline">
  </mat-form-field>
  <div class="username"><span >Welcome {{ username }} !</span></div>
</div>
```

We need to import the `FormsModule` from `@angular/forms` and declare in imports in our app.module.ts:

```
import { FormsModule } from '@angular/forms';

...

imports: [
    BrowserModule,
    MatGridListModule,
    BrowserAnimationsModule,
    MatButtonModule,
    MatInputModule,
    MatFormFieldModule,
    FormsModule
  ],

```

We now have to add this component to our `app.component.ts`:
```
...
<app-welcome-nav></app-welcome-nav>
<coffee-menu></coffee-menu>

```

Now we make it look pretty in `welcome-nav.component.scss`;
```
.welcome-nav {
  padding: 0 0 0 20px;
  color: #d04f02;
  font-family: Pacifico, sans-serif;

  .username-input {
    text-align: left;
    width: 50%;
    /deep/ .mat-form-field-underline {
      background-color: #d04f02;
      width: 50%;
      .mat-form-field-ripple {
        background-color: #71dad1;
      }
    }

    .orange-underline {
      width: 25%;
    }
  }
  .username {
    font-size: 1.5em;
    line-height: 1.5em;
    text-align: center;
  }

  .username-input .username {
    display: inline-block;
  }

}

```

And remove some margin from the coffee-menu.component.scss:

```
.coffee-menu {
  margin: 1% 10%;
  }
```
YOU'VE FINISHED

but if you want to learn more check out steps <a href="https://github.com/anacidre/AngularWorkshop/blob/master/Step%205%20%5BOptional%5D:%20ngClass.md">5</a>, <a href="https://github.com/anacidre/AngularWorkshop/blob/master/Step%206%20%5BOptional%5D:%20Pipes.md">6</a> and <a href="https://github.com/anacidre/AngularWorkshop/blob/master/Step%207%20%5BOptional%5D:%20Services.md">7</a>.
