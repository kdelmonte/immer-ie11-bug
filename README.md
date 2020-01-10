This repo shows an issue with immer when you pass `window.location` as the draft to its `produce` function.

```javascript
import produce from 'immer';

// Breaks IE 11
(produce((draft) => {
  return draft.hash = '#';
}, window.location))();
```

To reproduce:

* Install the [serve package](https://www.npmjs.com/package/serve)
* Run the following command `yarn build && serve -s build`
* Navigate to http://localhost:5000 using IE 11 and see how the app does not load
* Navigate to http://localhost:5000 using Chrome/FF and see how the app loads fine

To verify that the app loads fine in IE 11 without this bug:

* Comment out the lines 9-11 in the `src/index.js` file 
* Run `yarn build && serve -s build` once again