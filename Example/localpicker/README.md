# react-native-slidepicker

<h3><a href="https://github.com/lexguy/react-native-slidepicker/blob/main/CN.md">简中文档</a><h3>

<hr/>

<span> A react native picker component，used in time picker，address picker and other picker scenes. </span>

<img src="https://pic.downk.cc/item/5fca0ebf394ac52378391b0b.gif" width=360>

why：

- archived by JavaScript，run on Android and iOS.

- custom height,backgroundColor,fontSize,fontColor,or even picker header.

- support parallel data and cascade data.

- can be used in modal.

## Usage

install:

```javascript
npm install react-native-slidepicker
```

import:

```javascript
//Cascade data
import { CascadePicker } from "react-native-slidepicker";

//Parallel data
import { ParallelPicker } from "react-native-slidepicker";
```

## Example

```JSX
import {ParallelPicker} from 'react-native-slidepicker';
import ParaData from './one.json';
export default class PickerTest extends Component {
  ...
  onceChange = data => console.info('once', data);
  confirm = data => console.info('confirm', data);
  render() {
    return (
      <View style={{flex: 1}}>
        {/* <CascadePicker
          dataSource={CasCaData}
          onceChange={this.onceChange}
          confirm={this.confirm}
        /> */}
        <ParallelPicker
          dataSource={ParaData}
          onceChange={this.onceChange}
          confirm={this.confirm}
        />
      </View>
    );
  }
}

```

## props

- [`dataSource`](#dataSource)
- [`pickerDeep`](#deep)
- [`confirm`](#confirm)
- [`onceChange`](#oncechange)
- [`cancel`](#cancel)
- [`pickerStyle`](#pickerStyle)
- [`customHead`](#head)

<hr id="dataSource"></hr>

### `dataSource : array`

required. data source of the picker。

**for cascade data:**

```json
[
  {
    "name": "Asia",
    "id": 1,
    "list": [
      {
        "name": "China",
        "id": 100,
        "list": [
          {
            "name": "Beijing",
            "id": 1101
          }
        ]
      },
      {
        "name": "South Korea",
        "id": 200,
        "list": []
      }
    ]
  }
]
```

**for parallel data:**

```json
[
  [
    {
      "name": "2015",
      "id": 11
    }
  ],
  [
    {
      "name": "july",
      "id": 201
    },
    {
      "name": "August",
      "id": 202
    }
  ],
  [
    {
      "name": "1",
      "id": 2101
    }
  ]
]
```

<hr id="deep"></hr>

### `pickerDeep : number`

the num of sub pickers, required in CascadePicker Component.

<hr id="confirm"></hr>

### `confirm : (dataArray) => { }`

if you won't use the customeHead, this function is required.
called by confirm button, send the picker data back.

<hr id="oncechange"/>

### `onceChange : (dataArray) => { }`

(dataArray) => { } , function

not required.
once change the picker, it will be called and send current result back.

<hr id="cancel"/>

### `cancel : () => { } `

if you won't use the customeHead, this function is required.
called by cancel button, you should close the picker in this function.

<hr id="pickerStyle"/>

### `pickerStyle : object`

a custom style object, receives these props:

| Key             | Type            | Default Value | Description                                  |
| --------------- | --------------- | ------------- | -------------------------------------------- |
| itemHeight      | number          | 40            | item's height                                |
| visibleNum      | number          | 5             | Number of rows                               |
| activeBgColor   | string (color)  | "#ccc"        | Background color of selected item            |
| activeFontSize  | Number          | 18            | Font size of selected item                   |
| activeFontColor | string (color)  | "\#a00"       | Font color of selected item                  |
| normalBgColor   | string (color)  | "#fff"        | Unselected item background color             |
| normalBgOpacity | number (0-1)    | 0.4           | Background color opacity of unselected items |
| normalFontSize  | number          | 16            | Unselected item font color                   |
| normalFontColor | string：(color) | "#333"        | Unselected item font color                   |

<hr id="head"/>

### `customHead : view`

a rendered view, will replace the view that contains the [confirm]、[cancel] buttons.

you should bind the ref , and call `getResult` method to get the result of the picker.
[`getResult method`](#getresult)

## Method

if you custom the header,then you have to call `getResult` method by ref to get result.

<span id="getresult"></span>

### `getResult()`

unless you custom header，or you should use `confirm` method.
you can get the result by this function ,just like the following:

```JSX
export default class PickerTest extends Component {
  //...
  setPickerRef=(ref) => this.pickerRef = ref;

  getData=()=>{
    const data = this.pickerRef.getResult();
    console.info('data',data)
  }
  render() {
    const CustomHead = <View><Button onPress={this.getData}></Button></View>;
    return (
      <View style={{flex: 1}}>
        <ParallelPicker
          ref={this.setPickerRef}
          dataSource={ParaData}
          ...
        />
      </View>
    );
  }
}
```

## Illustration

This component does not deal with the logic of pop-up boxes, because the scheme of the pop-up layer may be different from the scheme adopted by each person. At present, it is difficult to find a solution that most people agree with. Therefore, the logic of this layer is left to the user. If there is a better scheme, welcome to issue

If you need to use it in the pop-up layer, you can use absolute positioning and z-Index or 'modal'.

example:

```jsx


//used in view with state

{this.state.isPicker &&
  <View>
    <CascadePicker {...props}>
  </View>}

```
