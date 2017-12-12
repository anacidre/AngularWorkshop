## Bindings

You can use Angular event bindings to respond to any DOM event.

Let's add a button to our coffee-menu component, the idea is that when the user clicks on that button the price of that coffee is updated to 0.00.

To do that, we'll add a button in our mat-grid-tile and we will specify the target when the button is clicked. We also need to add an index to our ngFor:

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

The target will be the onClick method that is defined in the coffee-menu.component.ts

```
onClick(index) {
  this.coffees[index].price = 0.00;
}
```

But that is not really what we want to do, we want to be able to specify how many coffees the user want to order.
To do so, let's first add the property quantity to the coffee-class.ts:

```
export class Coffee {
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


Amend the file coffee-menu.component.html to add an input where the user can introduce the amount of coffees to order and change the button name.

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
            <input matInput type=number max="10" title="quantity" placeholder="quantity" #order>
          </mat-form-field>
        </div>
        <button mat-button (click)="onClick(i, order.value)">DONE</button>
      </div>
    </mat-grid-tile>
  </mat-grid-list>
</div>
<app-total-order></app-total-order>
```

Now we need to add `[totalOrder]="total"` to our <app-total-order> component like this:

```
<app-total-order></app-total-order>
```
This is called one way data binding. One way data binding from data source to the view target means that values from the view are not passed back to the component, while any changes made to the expression in the component are reflected in the view - it is one way data binding from data source to the view.

Later on we will see two way data binding.

Now we need to re-implement the behaviour when the user clicks on the DONE button:

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

Open the console and you'll see how the value total value changes.
But the thing that we want to do is pass the order total from the coffee-menu component to the order component, to do so we need to use the decorator '@'Input:

```
import { Component, OnInit, Input } from '@angular/core';

@Component({
  selector: 'app-order',
  templateUrl: './order.component.html',
  styleUrls: ['./order.component.scss']
})
export class OrderComponent implements OnInit {
  @Input() totalOrder: number;

  constructor() { }

  ngOnInit() {
  }
}
```
What we have done here is one-way data binding. 
YOU'VE FINISHED

<img src="https://github.com/anacidre/AngularWorkshop/blob/master/assets/minions.gif">

but if you want to learn more check out steps <a href="https://github.com/anacidre/AngularWorkshop/blob/master/Step%205%20%5BOptional%5D:%20ngClass.md">5</a>, <a href="https://github.com/anacidre/AngularWorkshop/blob/master/Step%206%20%5BOptional%5D:%20Pipes.md">6</a> and <a href="https://github.com/anacidre/AngularWorkshop/blob/master/Step%207%20%5BOptional%5D:%20Services.md">7</a>.

