### Add an ngClass to add and remove CSS classes on an HTML element.

Once we have clicked done we want the button color to change to know which coffee we have already ordered. We do this by adding an ngClass to the button like this: 

```
<button mat-button (click)="onClick(i, order.value)" [class.checked]="coffee.quantity" >DONE</button>
```

We now need to add these classes to our coffee-menu.component.scss file like this:
```
.mat-button{
    background-color: rgba(255, 255, 255, 0.35);
    &.checked{
      background-color: #71dad1;
    }
    }
```
<a href="https://github.com/anacidre/AngularWorkshop/blob/master/Step%206%20%5BOptional%5D:%20Pipes.md">Next: Step 6 [Optional]</a>
