# Angular Starter

Starter project for Angular, adjusted to my own preferences. Those preferences are:

- Jest instead of Karma and Jasmine
- Cypress instead of Protractor
- Leaner schematics (TODO)

You do not actually have to use this project as a starter project. To create this project, I followed the (easy)
steps below. You can easily follow the steps on your own project instead of starting with this project.

By the way, I love the people from [briebug](https://github.com/briebug) for creating all those convenient schematics
I use below.

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
@angular-builders/jest and change your angular.json:

```shell script
npm i -D jest @types/jest @angular-builders/jest
```

In angular.json:

- look for `@angular-devkit/build-angular:karma` and 
- change it to `@angular-builders/jest:run`.

### [Use jest types instead of jasmine types](https://github.com/briebug/jest-schematic/issues/24)

Fix the types:

- Change types: `["jasmine", "node"]` to types: `["jest", "node"]` in tsconfig.spec.json

Do not remove @types/jasmine and @types/jasminewd2 from your package.json if you still want to be able to run 
protractor tests.

### Fix SyntaxError: Cannot use import statement outside a module
 
If you encounter this error, see the solution on 
[stackoverflow](https://stackoverflow.com/questions/55794280/jest-fails-with-unexpected-token-on-import-statement).

For example, add this to your package.json:

```json
{
  "transformIgnorePatterns": [
    "node_modules/(?!(@ionic-native)/)"
  ]
}
```

### Adding support for multi project setup

The @briebug/jest-schematic does not work well with an Angular CLI multi project setup. Use the [solutions described
here](https://github.com/briebug/jest-schematic/issues/22) to fix that.

## Cypress

### Adding the cypress schematic

In my experience, testing with protractor can be rather bumpy. Cypress gives a smoother experience. It now also has
[Firefox and Edge support](https://www.cypress.io/blog/2020/02/06/introducing-firefox-and-edge-support-in-cypress-4-0/).

For replacing Protractor with Cypress, simply use the [cypress schematic](https://github.com/briebug/cypress-schematic).

`ng add @briebug/cypress-schematic`

Opening the interactive Cypress UI is as easy as typing `ng e2e`. Or simultaneously run `ng test` and `npx cypress run`
to run Cypress in headless mode.

### Fixing lint settings

After adding the above schematic, ng lint will complain about e2e/tsconfig.json not existing. Open angular.json and
replace "e2e/tsconfig.json" by "cypress/tsconfig.json".

### Removing jasmine

You can remove all jasmine related packages from package.json (every line that contains the word 'jasmine').

## Leaner schematics (TODO)

If you generate your components with `ng generate component` and do not clean up, you will get lots of empty CSS files,
empty constructors and empty ngOnInit methods. That irritates me immensely. What I would like to do:

- remove the empty constructor from the default schematic
- remove the ngOnInit
- remove the CSS file

This is something I will look into at a later moment. For now I'll just remove them manually every time. To make that
a little bit easier, I changed the following in angular.json:

```json
{
  "schematics": {
    "@schematics/angular:component": {
      "inlineStyle": true
    }
  }
}
```

Now I just have to remove a single line in the TypeScript file, instead of a line in the TypeScript file and a separate
file. Note that if I want to add custom CSS to a component, I do NOT do that inline, but replace the inline style with
a separate SCSS file.
