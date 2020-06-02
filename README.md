[![Build Status](https://travis-ci.org/ngx-material-keyboard/core.svg?branch=master)](https://travis-ci.org/ngx-material-keyboard/core)

# ngx-material-keyboard
Onscreen virtual keyboard for [Angular] using [Angular Material].

![ngx-material-keyboard in action](https://cdn.rawgit.com/symplr-oss/ngx-material-keyboard-src/master/screenshots/ngxmk-2.gif)

## Demo

- `npm run build`
- Open `dist/demo/index.html`

## Docs

- `npm run build`
- Open `dist/docs/index.html`

## Getting started

### 1. Add the module to your project, e.g. `app.module.ts`:
```:typescript
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { BrowserModule } from '@angular/platform-browser';
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { MatButtonModule } from '@angular/material/button';
...
import { MatKeyboardModule } from '@ngx-material-keyboard/core';

@NgModule({
  imports: [
    // Angular modules
    BrowserModule,
    BrowserAnimationsModule,
    FormsModule,

    // Material modules
    MatButtonModule,
    MatKeyboardModule,
  ],
  ...
})
export class AppModule {}
```

### 2. Use the [`MatKeyboardDirective`] on your input elements or textareas and set the name or locale of the layout.
> If not provided the locale will be derieved from the `LOCALE_ID` or the browser.
```:angular2html
<input [matKeyboard]="'Azərbaycanca'">
```

## Providing custom layouts
Most of the base configurations are provided as [injection tokens][InjectionToken]. Please read [the documentation][InjectionToken] to 
understand how to handle it.

All layouts are based on (or directly inherited from) the [angular-virtual-keyboard][the-darc/angular-virtual-keyboard] which is based on
 [GreyWyvern VKI]. For details on how to structure a layout see the [comment derived from the original source code][VKI Readme].

> Note that this will most likely be changed in the near future. But for now a huge range of layouts is already usable because of the 
[great contribution][VKI Credits] back then.

But basicly you just provide the configuration of your new layout in your `AppModule`:
```:typescript
import { IKeyboardLayouts, keyboardLayouts, MAT_KEYBOARD_LAYOUTS, MatKeyboardModule } from '@ngx-material-keyboard/core';

const customLayouts: IKeyboardLayouts = {
  ...keyboardLayouts,
  'Tölles Läyout': {
    'name': 'Awesome layout',
    'keys': [
      [
        ['1', '!'],
        ['2', '@'],
        ['3', '#']
      ]
    ],
    'lang': ['de-CH']
  }
};

@NgModule({
  ...
  providers: [
    { provide: MAT_KEYBOARD_LAYOUTS, useValue: customLayouts }
  ],
  ...
})
export class AppModule {}
```

[Angular]: https://angular.io/
[Angular Material]: https://material.angular.io/
[the-darc/angular-virtual-keyboard]: https://github.com/the-darc/angular-virtual-keyboard
[GreyWyvern VKI]: http://www.greywyvern.com/code/javascript/keyboard

[InjectionToken]: https://angular.io/guide/dependency-injection-in-action#injectiontoken
[VKI Readme]: https://goo.gl/fCDExr
[VKI Credits]: https://goo.gl/NYqTwc

