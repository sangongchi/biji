> ```js
> for (var i = 0; i < 5; i++) {
> setTimeout(function() {
>  console.log(i);
> }, 0);
> }
> ```
> ```js
> for (let i = 0; i < 5; i++) {
> setTimeout(function() {
>  console.log(i);
> }, 0);
> }
> ```
> ```js
> for (let i = 0; i < 5; i++) {
> setTimeout(() => {
>  console.log(i);
> }, 0);
> }
> ```
> 
>
> ```js
> for (var i = 0; i < 5; i++) {
> (function(j) {
>  setTimeout(function() {
>    console.log(j);
>  });
> })(i);
> }
> //等价于
> var output = function(i) {
> setTimeout(function() {
>  console.log(i);
> }, 0);
> };
> for (var i = 0; i < 5; i++) {
> output(i);
> }
> 
> ```
>
> 