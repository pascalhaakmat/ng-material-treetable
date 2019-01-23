# Angular Material TreeTable Component

[![Build Status](https://travis-ci.com/mlrv/ng-material-treetable.svg?branch=master)](https://travis-ci.com/mlrv/ng-material-tree-table)


![Gif Demo](https://media.giphy.com/media/64CInKKyLZZB31kKDc/giphy.gif)

[Live Demo](http://ng-material-treetable.surge.sh/)

[StackBlitz Demo](https://stackblitz.com/edit/angular-qnlruj)

## Installation

Simply install the package through `npm`

```
npm i ng-material-treetable --save
```

import the main module

```typescript
import { TreetableModule } from 'ng-material-treetable';

@NgModule({
    ...
  imports: [
    ...
    TreetableModule
  ],
  ...
})
export class AppModule { }
```

and use the component in your template

```html
<ng-treetable [tree]="yourTreeDataStructure"></ng-treetable>
```

Finally, make sure you import the required material icons font in your `styles.css`

```css
@import url( 'https://fonts.googleapis.com/css?family=Roboto:400,700|Material+Icons');
```

## Data Format

The tree object that's rendered by the component needs to satisfy a very simple `Node` interface

```typescript
import { Node } from 'ng-material-treetable';

interface Node<T> {
  value: T;
  children: Node<T>[];
}
```

Here's a simple example.


```javascript
{
  value: {
    name: 'Reports',
    owner: 'Eric',
    protected: true,
    backup: true
  },
  children: [
    {
      value: {
        name: 'Charts',
        owner: 'Stephanie',
        protected: false,
        backup: true
      },
      children: []
    },
    {
      value: {
        name: 'Sales',
        owner: 'Virginia',
        protected: false,
        backup: true
      },
      children: []
    },
    {
      value: {
        name: 'US',
        owner: 'Alison',
        protected: true,
        backup: false
      },
      children: [
        {
          value: {
            name: 'California',
            owner: 'Claire',
            protected: false,
            backup: false
          },
          children: []
        },
        {
          value: {
            name: 'Washington',
            owner: 'Colin',
            protected: false,
            backup: true
          },
          children: [
            {
              value: {
                name: 'Domestic',
                owner: 'Oliver',
                protected: true,
                backup: false
              },
              children: []
            },
            {
              value: {
                name: 'International',
                owner: 'Oliver',
                protected: true,
                backup: true
              },
              children: []
            }
          ]
        }
      ]
    }
  ]
}
```

## Options

> Work in Progress...

An `option` input property can be used to customise the component

```typescript
import { Node, Options } from 'ng-material-treetable';
```

---

```html
<ng-treetable
  [tree]="yourTreeDataStructure"
  [options]="yourOptions">
</ng-treetable>
```

| Name                  | Description                                                                                                                                                                                                                                                                                | Type      | Default |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|---------|
| `verticalSeparator`   | If `true`, separates table columns with  vertical lines.                                                                                                                                                                                                                                   | `boolean` | `true`  |
| `capitalisedHeader`   | If `true`, capitalise the first letter of each column header.                                                                                                                                                                                                                              | `boolean` | -       |
| `highlightRowOnHover` | If `true`, hovering the mouse over a row highlights its background.                                                                                                                                                                                                                        | `boolean` | `true`  |
| `customColumnOrder`   | By default, the columns are ordered following  the array generated by calling `Object.keys()` on the nodes of the tree object; this option  can be used to specify a custom order. Note that `customColumnOrder` needs to be an  array containing all the keys present in the node object. | `Array`   | -       |

### customColumnOrder example

Given a tree data type like

```typescript
interface Person {
  name: string;
  age: number;
  married: boolean;
}

const tree: Node<Person> = ...
```

a custom column order can be specified with the following `options` object

```typescript
const opts: Options<Person> = {
  customColumnOrder: ['married', 'age', 'name']
}
```

an incomplete or incorrect `customColumnOrder` value will result in an error

```typescript
customColumnOrder: ['married', 'age'] // 'name' missing
customColumnOrder: ['married', 'age', 'name', 'surname'] // 'surname' is not a valid key
```

## Events

> Work in Progress...

| Name          | Description                                                                              | Type      |
|---------------|------------------------------------------------------------------------------------------|-----------|
| `nodeClicked` | Whenever a node is expanded or collapsed, emits an event with the new status of the node | `Node<T>` |

### nodeClicked example

```html
<ng-treetable
  [tree]="yourTreeDataStructure"
  (nodeClicked)="logToggledNode($event)">
</ng-treetable>
```

---

```typescript
logToggledNode(node: Node<SomeNodeType>): void {
  console.log(node);
}
```