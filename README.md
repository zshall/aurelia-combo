# aurelia-combo ![CI](https://github.com/aurelia-contrib/aurelia-combo/workflows/CI/badge.svg)

An Aurelia plugin for easy keyboard combo short-cuts.

# Install Package

`npm i aurelia-combo` or `yarn add aurelia-combo`

> For aurelia-cli users, please make sure to use aurelia-cli version `1.0.0-beta.1` or above.

## Usage

In your main.js file

```js
aurelia.use.plugin(PLATFORM.moduleName('aurelia-combo'));
```

It uses [keymaster](https://github.com/madrobby/keymaster) underneath to support keyboard short-cut. Read it to understand the supported short-cut format.

```js
import {combo} from 'aurelia-combo';
export class MyVm {
  @combo('ctrl+f', 'command+f') // array of short-cuts
  findIt(e) {
    console.log('findIt');
  }

  @combo('ctrl+c, command+c') // or a string of all, keymaster understands
  copyIt(e) {
    console.log('copyIt');
  }
}
```

Take `findIt` as example, the above code is very similar to what you do manually:
```js
import key from 'keymaster';
export class MyVm {
  attached() {
    key('ctrl+f, command+f', e => {
      // return true if you want to skip preventDefault
      if (true !== this.findIt(e)) e.preventDefault();
    })
  }

  detached() {
    key.unbind('ctrl+f, command+f')
  }

  findIt(e) {
    console.log('findIt');
  }
}
```

## Notes

All short-cuts are attached globally to HTML document, the good practice is to use `@combo` on component loaded by router.

The unbind in detached removes all listeners for that short-cut. This means you don't want two components on screen handling same short-cut.


## This plugin is bootstrapped by aurelia-cli

https://aurelia.io/docs/plugins/write-new-plugin

