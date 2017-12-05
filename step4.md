## Bindings

You can use Angular event bindings to respond to any DOM event.

Let's add a button to our coffee-menu component, the idea is that when the user clicks on that button the price of that coffee is updated to 0.00.

To do that, we'll add a button in our mat-trid-tile-footer and we'll specify the target when the button is clicked.

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
        <button mat-icon-button (click)="onClick(i)">FREE</button>
      </div>
    </mat-grid-tile>
  </mat-grid-list>
</div>
```

The target will be the method onClick that is defined in the coffee-menu.component.ts

```
onClick(index) {
  this.coffees[index].price = 0.00;
}
```

But that is not really what we want to do, we want to be able to specify how many coffees the user want to order.
To do so, let's add first the property quantity to the class Coffee.

```
export class Coffee {
  name: string;
  image: string;
  price: number;
  quantity: number;
}
```

Amend the file coffee-menu.component.html to add an input where the user can introduce the amount of coffees to order and change the button name.

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
        <input type=number max="10" #order>
        <button mat-icon-button (click)="onClick(i, order.value)">DONE</button>
      </div>
    </mat-grid-tile>
  </mat-grid-list>
</div>
<app-order></app-order>
```

Now we need to re-implement the behaviour when the user clicks on the DONE button:

```
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

And specify the value that we want to send in the coffee-menu.component.html:

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
