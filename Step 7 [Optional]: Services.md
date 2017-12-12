### Creating a service which is how we can request data for our app to consume

First we need to add a service. Inside coffee-order-app/src/app we create a file called `coffee-types.service.ts` and then we export the class like this:
```
export class CoffeeTypesService {
  constructor() {}

  getCoffees() {
}
}

```
We then add this service to our app.module.ts

```
import { CoffeeTypesService } from './coffee-types.service';

...

providers: [
    CoffeeTypesService
  ],
```

We then go to our coffee-menu.component.ts and copy the array to add it to our coffee-type.service.ts we will add it in the getCoffees function like this:

```
  getCoffees() {

    return [
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
     }
```

We now go back to our coffee-types.component.ts, delete that array from there and we are going to start looking at dependency injection. 

Before moving forward we need to import the CoffeeTypesService into the coffee-menu.component.ts component:

```
import { CoffeeTypesService } from '.././coffee-types.service';
```

We will now add to our constructor the coffee array like this:

```
  coffees: Coffee[];
```
Inside our constructor we will call the CoffeeTypesService like this:
```
constructor (private coffeeService: CoffeeTypesService) {}
```
and on our ngOnInit lifecycle hook we will call our getCoffees method

```
 ngOnInit() {
    this.coffees = this.coffeeService.getCoffees();
  }

```

Finally to make this work we need to add our coffee-class.service.ts our Coffee class. We import it:
```
import { Coffee } from '../coffee-class/coffee-class';
```
