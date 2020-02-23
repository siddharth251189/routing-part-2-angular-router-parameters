# Router Parameters

## Passing Router Parameters
In the example we are passing two parameters to users route first is id and second is name in the routes configration.below is the example of url.

http://localhost:4200/users/1/max

### app.module.ts
```
const appRoutes:Routes=[
  {path:'',component:HomeComponent},
  {path:'users',component:UsersComponent},
  {path:'users/:id/:name',component:UserComponent},
  {path:'servers',component:ServersComponent}
]
```
## Fatching Router Parameters

In order to fatching URL we need to follow below steps:
1. import ActivatedRoute from @angular/router
2. Hold this ActivatedRoute in a private variable in constructor parameter
3. By Useing <b>snapshot.params</b> we can access the parameters

### Important syntax:
```
this.route.snapshot.params['id']
```

### user.component.ts
```
import { Component, OnInit } from '@angular/core';
import {ActivatedRoute} from '@angular/router'
@Component({
  selector: 'app-user',
  templateUrl: './user.component.html',
  styleUrls: ['./user.component.css']
})
export class UserComponent implements OnInit {
  user: {id: number, name: string};

  constructor(private route:ActivatedRoute) { }

  ngOnInit() {
    console.log(this.route.snapshot.params['id']);
    console.log(this.route.snapshot.params['name']);

    this.user={
      id:this.route.snapshot.params['id'],
      name:this.route.snapshot.params['name']
    }
  }

}

```
### user.component.html
```
<p>User with ID {{user.id}} loaded.</p>
<p>User name is {{user.name}}</p>

```

## Fatching Router Parameters Reactively(With Observable);
In some conditions screenshot method will not work. For example if we have a router link in user component like this:
```
<a [routerLink]="['/users',10,'Anna']">Load Anna</a>

```
If we will click on button it will update parameters in address bar(URL) but not on the view. so for prevent this issue we will have to use <b>params</b> observable.

### Important syntax:
```
this.route.params
    .subscribe((params:Params)=>{
     
    })
```
### user.component.ts

```
import { Component, OnInit } from '@angular/core';
import {ActivatedRoute, Params} from '@angular/router'
@Component({
  selector: 'app-user',
  templateUrl: './user.component.html',
  styleUrls: ['./user.component.css']
})
export class UserComponent implements OnInit {
  user: {id: number, name: string};

  constructor(private route:ActivatedRoute) { }

  ngOnInit() {
    console.log(this.route.snapshot.params['id']);
    console.log(this.route.snapshot.params['name']);

    this.user={
      id:this.route.snapshot.params['id'],
      name:this.route.snapshot.params['name']
    }
    
    this.route.params
    .subscribe((params:Params)=>{
      this.user.id=params['id'],
      this.user.id=params['name']
    })
  }

}

```


