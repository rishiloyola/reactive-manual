{"bigh3": true}

## SingleRange

![Image to be displayed](https://i.imgur.com/55jFax6.png)

A `SingleRange` sensor component creates a numeric range selector UI widget. It is like a list widget, but for numeric data.

Example uses:
* filtering search results by prices in an e-commerce or food delivery experience.
* browsing movies by a ratings filter.

### Usage

```js
<SingleRange
  componentId="PriceSensor"
  appbaseField="price"
  title="SingleRange Component"
  data={
    [{"start": 0, "end": 10, "label": "Cheap"},
     {"start": 11, "end": 20, "label": "Moderate"},
     {"start": 21, "end": 50, "label": "Pricey"},
     {"start": 51, "end": 1000, "label": "First Date"}]
  }
  defaultSelected="Cheap"
/>
```

### Props

- **componentId** `String`  
    unique id of the sensor, can be referenced in an actuator's `react` prop.
- **appbaseField** `String`  
    data field to be mapped with the component's UI view. The range items are filtered by a database query on this field.
- **title** `String or HTML` [optional]  
    title of the component to be shown in the UI.
- **data** `Object Array`  
    collection of UI `labels` with associated `start` and `end` range values.
- **defaultSelected** `String` [optional]  
    pre-select a label from the `data` array.

### CSS Styles

All reactivebase components are `rbc` namespaced.

![Annotated image](https://i.imgur.com/CIOLTQo.png)

```html
<div class="rbc rbc-singlerange col s12 col-xs-12 card thumbnail rbc-title-active">
  <div class="row">
    <h4 class="rbc-title col s12 col-xs-12">Price</h4>
    <div class="col s12 col-xs-12 rbc-list-container">
      <div class="rbc-list-item row">
        <input type="radio" class="rbc-radio-item" value="Cheap">
        <label class="rbc-label">Cheap</label>
      </div>
      <div class="rbc-list-item row">
        <input type="radio" class="rbc-radio-item" value="Moderate">
        <label class="rbc-label">Moderate</label>
      </div>
      <div class="rbc-list-item row">
        <input type="radio" class="rbc-radio-item" value="Pricey">
        <label class="rbc-label">Pricey</label>
      </div>
      <div class="rbc-list-item row">
        <input type="radio" class="rbc-radio-item" value="First Date">
        <label class="rbc-label">First Date</label>
      </div>
    </div>
  </div>
</div>
```

* SingleRange component's class name is `rbc-singlerange`. Additionally, depending on the presence / absence of the `title` prop, a `rbc-title-active` or `rbc-title-inactive` class is respectively applied.
* the title element has a class name of `rbc-title`.
* the radio inputs are encapsulated inside a `rbc-list-container` class with each element having class name of `rbc-list-item`.
* the input radio element has a class name of `rbc-radio-item`.
* the label element has a class name of `rbc-label`.

### Extending

`SingleRange` component can be extended to
1. customize the look and feel with `componentStyle`,
2. update the underlying DB query with `customQuery`,
3. connect with external interfaces using `onValueChange`.

```
<SingleRange
  ...
  componentStyle={{"paddingBottom": "10px"}}
  customQuery={
    function(value) {
      return {
        query: {
          match: {
            data_field: "this is a test"
          }
        }
      }
    }
  }
  onValueChange={
    function(value) {
      console.log("current value: ", value)
      // set the state
      // use the value with other js code
    }
  }
/>
```

- **componentStyle** `Object`
    CSS styles to be applied to the **SingleRange** component.
- **customQuery** `Function`
    takes **value** as a parameter and **returns** the data query to be applied to the component, as defined in Elasticsearch v2.4 Query DSL.
    `Note:` customQuery is called on value changes in the **SingleRange** component as long as the component is a part of `react` dependency of at least one other component.
- **onValueChange** `Function`
    is called every time the component's **value** changes and is passed in as a parameter to the function. This can be used for updating other UI components when **SingleRange's** value changes.

### Examples

1. [Range with all the default props](../playground/?selectedKind=SingleRange&selectedStory=Basic&full=0&down=1&left=1&panelRight=0&downPanel=kadirahq%2Fstorybook-addon-knobs&filterBy=ReactiveMaps)

2. [Range with pre-selected items](../playground/?selectedKind=SingleRange&selectedStory=With%20Default%20Selected&full=0&down=1&left=1&panelRight=0&downPanel=kadirahq%2Fstorybook-addon-knobs&filterBy=ReactiveMaps)

4. [Playground (with all knob actions)](../playground/?knob-title=SingleRange%3A%20Price%20Filter&knob-defaultSelected=Cheap&selectedKind=SingleRange&selectedStory=Playground&full=0&down=1&left=1&panelRight=0&downPanel=kadirahq%2Fstorybook-addon-knobs&filterBy=ReactiveMaps)
