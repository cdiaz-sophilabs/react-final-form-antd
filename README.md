# redux-form-antd
This is  bindings for redux form and redux form antd.
This library should be compatible for both redux-form and react-final-form.
Stories for final form are welcome.

[![NPM Downloads](https://img.shields.io/npm/dm/react-final-form-antd.svg?style=flat)](https://www.npmjs.com/package/react-final-form-antd)
---
[`redux-form-antd`](https://github.com/zhdmitry/redux-form-antd) is a set of
wrappers to facilitate the use of antd components with
[`redux-form`](https://github.com/erikras/redux-form).
---

## [Live Demo](http://sophilabs-forks.github.io/react-final-form-antd/index.html) :eyes:


## Installation

Using yarn:

```bash
  $ yarn add react-final-form-antd
```

Using [npm](https://www.npmjs.org/):

```bash
  $ npm install --save react-final-form-antd
```

## Available Components

- Select
- Radio Buttons
- DatePicker
- MonthPicker
- NumberField
- TextField
## Usage

Rather than import your component class from `antd`, import it from `react-final-form-antd`
and then pass the component class directly to the `component` prop of `Field`.

```js
import { Form, Field } from 'react-final-form'
import {
  SelectField,
  TextField,
} from 'react-final-form-antd'

class MyForm extends Component {
  handleSubmit = (data) => {
    // Do something
  }
  render() {
    return (
      <Form 
        onSubmit={this.handleSubmit}
        render={({ handleSubmit, pristine, invalid }) => (
    	  <form>
            <Field name="username" component={TextField} hintText="Street"/>
          </form>
        )}
      />
    );
  }
}


export default MyForm
```
or you can check stories code [click](https://github.com/sophilabs-forks/react-final-form-antd/blob/master/stories/TextInput.js)

## Instance API

#### `getRenderedComponent()`

Returns a reference to the UI component that has been rendered. This is useful for
calling instance methods on the UI components. For example, if you wanted to focus on
the `username` element when your form mounts, you could do:

```js
componentWillMount() {
  this.refs.firstField
    .getRenderedComponent()
    .focus()
}
```

as long as you specified a `ref` and `withRef` on your `Field` component.

```js
render() {
  return (
    <form>
      ...
      <Field name="username" component={TextField} withRef ref={r=>(this.textField = r)}/>
      ...
    </form>
  )
}
```

## Custom component wrapper
You can use `createComponent` and `customMap` functions to wrap your custom component. 
Usage example:

```js
import { createComponent, customMap } from 'redux-form-antd';
import { InputPasswordViewableComponent } from './components/InputPasswordViewableComponent'; // Your custom component

function mapFunction(mapProps, { input: { onChange } }) {
  return {
    ...mapProps,
    onChange: event => onChange(event.nativeEvent.target.value)
  };
}
const textFieldMap = customMap(mapFunction);

export const InputPasswordViewable = createComponent(InputPasswordViewableComponent, textFieldMap);
```

* `createComponent` creates FormItem wrapper and attaches validate status handler.
* `customMap` maps redux-form [Field props](https://redux-form.com/7.2.3/docs/api/field.md/#props) 
to ant.design [form fields props](https://ant.design/components/form/#components-form-demo-validate-static).
You can omit customMap's attribute, in such case default mapping will be applied. 
If you specify a map function, then it should return an object with required 
properties for ant's FormItem and your component. The signature of map function 
is `(mapProps, props) => ({...mapProps})`, where `mapProps` - default mapping 
properties, `props` - redux-form's Field properties.

---
inspired by redux-form-material-ui by [erikras](https://github.com/erikras/redux-form-material-ui)
Forked from redux-form-antd by [zherebko dmitry](https://github.com/zhDmitry/redux-form-antd)
