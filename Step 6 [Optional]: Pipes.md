### Adding pipes

We add pipes to tranform what we display within the html code.

Angular has some pre built-in pipes which you can find <a href="https://angular.io/guide/pipes#built-in-pipes" targer="_blank">here</a>

We will try out the uppercase pipe to put the titles of the coffees in uppercase. We can add the pipe directly to an interpolation:

```
 <h2 mat-line>{{coffee.name | uppercase}}</h2>
```

