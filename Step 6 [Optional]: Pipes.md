### Adding pipes

We add pipes to tranform what we display within the html code.

Angular has some pre built-in pipes which you can find <a href="https://angular.io/guide/pipes#built-in-pipes" targer="_blank">here</a>

We will try out the uppercase pipe to put the titles of the coffees in uppercase. We can add the pipe directly to an interpolation:

```
 <h2 mat-line>{{coffee.name | uppercase}}</h2>
```

We'd like to show the currency for the price and total order price, to do so we can use the currency pipe:

```
<span mat-line>Price: {{coffee.price | currency:'EUR'}}</span>
```

```
<app-order [totalOrder]='total  | currency:"EUR"'></app-order>
```
<a href="https://github.com/anacidre/AngularWorkshop/blob/master/Step%207%20%5BOptional%5D:%20Services.md">Next: Step 7 [Optional]</a>
