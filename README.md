# ionic-latest
Esqueleto de aplicación Ionic actualizado

Versiones:

Ionic 7.x
Angular 17.x
Capacitor 5.x

Actualizar Ionic CLI:
npm i -g @ionic/cli

Empezar un nuevo proyecto angular standalone con capacitor:
ionic start project blank --type=angular-standalone --capacitor --no-git


Migrar de karma/jasmine a jest

1. Quitar todas las dependencias de karma/jasmine del package.json
    - @types/jasmine
    - @typescript-eslint/eslint-plugin
    - jasmine-core
    - jasmine-spec-reporter
    - karma
    - karma-chrome-launcher
    - karma-coverage
    - karma-jasmine
    - karma-jasmine-html-reporter

2. Añadir las dependencias de jest
    - @types/jest
    - jest
    - jest-preset-angular

3. Borrar el nodo "test" del angular.json

4. Borrar el karma.conf.js y el test.ts

5. Añadir el fichero setup-jest.ts con el siguiente contenido:
    import 'jest-preset-angular/setup-jest';

6. Ejecutar npx jest --init. Esto creará el fichero jest.config.ts donde cambiaremos las siguientes propiedades:
    - preset: 'jest-preset-angular'
    - setupFilesAfterEnv: ['<rootDir>/setup-jest.ts']

7. Modificar el tsconfig.spec.json dejándolo así:
{
  "extends": "./tsconfig.json",
  "compilerOptions": {
    "outDir": "./out-tsc/spec",
    "types": [
      "jest"
    ],
    "esModuleInterop": true,
    "emitDecoratorMetadata": true
  },
  "include": [
    "src/**/*.spec.ts",
    "src/**/*.d.ts"
  ]
}

8. Adaptar el fichero app.component.spec.ts para que el test sea compatible con standalone

import { ComponentFixture, TestBed } from '@angular/core/testing';
import { provideRouter } from '@angular/router';
import { AppComponent } from './app.component';

describe('AppComponent', () => {
  let component: AppComponent;
  let fixture: ComponentFixture<AppComponent>;

  beforeEach(() => {
    TestBed.configureTestingModule({
      imports: [AppComponent],
      providers: [provideRouter([])],
    });

    fixture = TestBed.createComponent(AppComponent);
    component = fixture.componentInstance;
  });

  it('should create the app', () => {
    expect(component).toBeTruthy();
  });
});






