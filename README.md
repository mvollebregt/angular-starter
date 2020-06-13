# AngularStarter

Starter project for Angular, adjusted to my own preferences. Those preferences are:

- Jest instead of Karma and Jasmine
- Cypress instead of Protractor (TODO)
- Leaner schematics (TODO)

## Jest

Instead of Karma and Jasmine, I prefer to use Jest. In my experience, Jest is faster, and it has great [integration
with IntelliJ](https://www.jetbrains.com/help/idea/running-unit-tests-on-jest.html). Just open your spec file in
IntelliJ, click on the green arrows in the margin, and one or more tests will run within your IDE.

In the past I had some trouble setting up Jest with Angular, but now there is a great [jest schematic from 
briebug](https://github.com/briebug/jest-schematic), that makes installing Jest into your Angular project as easy
as typing

```shell script
ng add @briebug/jest-schematic
```

### Note

To run your tests from the command line, you must type the following command:

```shell script
npm run test
```

ng test won't work anymore.
