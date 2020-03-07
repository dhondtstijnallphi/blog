# Creating a backend driven component.

## Introduction

Let' us set the scene. A customer has a need for an angular 2+ website where the view depends on information coming for the backend. When we say view we mean view not just the data but also how it is presented to the user. There are multiple ways to accomplish this but most people will use either an if or switch statements. But what if we used the "viewchild" to dynamically change the component on render. This is what this blogpost will try to show. 



## What we are going to create.

The image below gives you a design overview of what we will create.

​	![Finished screen](images\ALV.svg)

A webpage containing 3 section by using the css grid system.

Section 1: a header showing us the name of the title

Section 2: a side bar menu, with a filter system and a search system

Section 3: The log messages

We made 3 different card designs. 

1. Design 1: shows a big coloured square for the type
2. Design 2: Show an icon for the type
3. Design 3: Shows a text field for the type.

As you can see the pinnacle of good design. :)

## Tools used

Design tool : Figma

Coding tool Visual studio code

Extensions: Angular snippets (Version 9), Angular Language Service, angular2-switcher, auto rename tag, Bracket pair colorizer 2, material icon theme, path intellisense, Prettier - code formatter, vscode-angular-html

Framework : Angular 9, angular material design, CSS grid



## Start of the application

### setup angular project

We will begin by creating an empty angular 9 application.

Using your command line tool of choice let create the following application.

```bash
ng new alv --createApplication=false  --skipGit=true
```

This will create our empty project. Once this is generate go to the project folder.

```
cd alv 
```

Next lets generate the application that we are going to use for the base page and the default design.

```
ng g application alv --prefix=allphi --routing=false --style=scss
```

 As ui-toolkit we are going to use angular material designs. 

So let's run the following command to setup angular material design. 

```bash
ng add @angular/material
```

When prompted choose the theme, if you want global Typography and browser animations select yes for both.

We will also create a library project to hold two of the card-designs.

```bash
ng g library card-designs --prefix=cards
```

and one to hold our types.

```bash
ng g library alv-types --prefix=alv
```



For this article we are going to make another log viewer (alv) using Angular 9. 

The object we are trying to show is multiple logMessages. Because a normal grid is boring we are going to show a message as a card. Below the interface of a message.

```typescript
export interface message {
    id:string;
    type: string;
    description: string;
    longDescription: string;
    timestamp: date;
    location: string;
    application: string;
    version: string;
}
```

