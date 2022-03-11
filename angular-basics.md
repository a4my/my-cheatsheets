---
title: ANGULAT
category: ANGULAT Tutorial
updated: 2022-03-09

A closer look into Angular's basics
---

## What's Angular

Angular is an SPA (Single Pae Application) created in 2010 and maintained by Google. Angular is a Component Based Frontend Framework (like React and Vue.js)

Angular.js is the first version and Angular now refers to the version 2 and above.

It is an all-in-one solution (routing, http, etc) but mainly used for big applications. It uses TypeScript and ES6 and has a great CLI.

Angular uses concepts such as MVC, "modules", "services" or "observables" and ngrx for state management (equivalent of Redux in React).

## Angular npm config

`npm install -g @angular/cli` will generate an Angular app whenever and wherever on your computer
`ng --version` will show details about the Angular version installed on your computer.
`ng new appname` will create an Angular app called "appname"
`ng serve` will run the live server

## ngIf and ngFor directives

```js
@component({
  selector: 'listItems',
  template: `
        <div *ngIf="listItems.length > 0 ">
            <h1>List of items</h1>
        </div>    
        `
})
export class ListItemsComponent {
  listItems = ['item1', 'item2', 'item3']
}
```

```js
@component({
  selector: 'listItems',
  template: `
        <div *ngFor="let item of listItems">
            <h1>{{ item }}</h1>
        </div>    
        `
})
export class ListItemsComponent {
  listItems = ['item1', 'item2', 'item3']
}
```

## Angular CLI

`ng generate component components/Todos` or `ng g c components/Todos`will create a new component in a folder called Todos inside a folder called component
`ng generate pipe <name>` will create a custom pipe

## Pipes

ex:

```js
@Pipe({
  name: 'deleteSpace'
})
export class DeleteSpacePipe implements PipeTransform {
  transorm(value: string) {
    return value.replace(' ', '')
  }
}
```

⚠️ Add the pipe into the declarations in `app.module.ts` :

```js
  @NgModule({
    declarations: [
      AppComponent,
      DeleteSpacePipe
    ]
  })
```

then apply the pipe in the HTML:

```html
<td>{{ books.category | deleteSpace}}</td>
```

==> 'Big data' will become 'Bigdata'
