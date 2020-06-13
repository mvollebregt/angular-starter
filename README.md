# Angular Starter

Starter project for Angular, adjusted to my own preferences. Those preferences are:

- Jest instead of Karma and Jasmine
- Cypress instead of Protractor (TODO)
- Leaner schematics (TODO)

You do not actually have to use this project as a starter project. To create this project, I followed the (easy)
steps below. You can easily follow the steps on your own project instead of starting with this project.

## Jest

### Adding the Jest schematic

Instead of Karma and Jasmine, I prefer to use Jest. In my experience, Jest is faster, and it has great [integration
with IntelliJ](https://www.jetbrains.com/help/idea/running-unit-tests-on-jest.html). Just open your spec file in
IntelliJ, click on the green arrows in the margin, and one or more tests will run within your IDE.

In the past I had some trouble setting up Jest with Angular, but now there is a great [jest schematic from 
briebug](https://github.com/briebug/jest-schematic), that makes installing Jest into your Angular project as easy
as typing

```shell script
ng add @briebug/jest-schematic
```

### Making ng test work

The above schematic requires you to run `npm run test` instead of `ng test`. To make `ng test` work, install
@angular/builders/jest and change your angular.json:

```shell script
npm i -D jest @types/jest @angular-builders/jest
```

In angular.json, look for `@angular-devkit/build-angular:karma` and change it to `@angular-builders/jest:run`.
