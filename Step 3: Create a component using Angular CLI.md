## Creating our second component using Angular CLI

At the end of this section we should have developed a new component for the footer that shows the total price:

![picture](https://github.com/anacidre/AngularWorkshop/blob/master/assets/coffee-app-footer-selection.jpg)

For now, the price will be a static value, but in the next section will see how this value can be updated depending on the coffees purchased by the client.

This time the component will be generated using Angular CLI. So let's go to the Terminal and at coffee-order-app type:

```
ng generate component total-order
```
OR

```
ng g c total-order
```

This will create the necessary files for the component in the order folder and also import this component into app.module.ts.

You might notice that angular CLI has created an extra file called `total-order.component.spec.ts` we won't be working with this file it is for testing.

If we add the component at the end of the the coffee-menu.component.html page we can see our footer in the page:

```
...
</mat-grid-list>
</div>
<app-total-order></app-total-order>
```

Now let's change the component a little bit so it reflects the information that we want to show to our users.

First let's create an attribute that will contain the final price (order.component.ts).

```
  totalOrder: number = 0;
```
Our component should look like this:

```
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-total-order',
  templateUrl: './total-order.component.html',
  styleUrls: ['./total-order.component.scss']
})
export class TotalOrderComponent implements OnInit {
  totalOrder: number = 0;

  constructor() { }

  ngOnInit() {
  }

}

```
We need to modify the html for our order component:

```
<div class="footer">
  <h3>Price: {{totalOrder}}</h3>
</div>
```

Add finally change the styles in the order.component.scss:
```
.footer {
  background-color: #71dad1;
  position: absolute;
  left: 0;
  bottom: 0;
  height: 70px;
  width: 100%;
  overflow:hidden;
  h3{
    text-align: right;
    margin-right: 5em;
    color: #FFFFFF;
    font-size: 1.5em;
    font-family: sans-serif;
  }
}
```

<img src="https://github.com/anacidre/AngularWorkshop/blob/master/assets/mgc.gif">
