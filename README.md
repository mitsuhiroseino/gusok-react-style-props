# @gusok/react-style-props

**[日本語版READMEはこちら](./README-ja.md)**

`@gusok/react-style-props` is a package that moves style-related properties set in a component's props to standard React `style`, [Emotion](https://emotion.sh/docs/introduction) `css`, or similar properties.  
This functionality is designed to make it easier to set frequently used style-related properties.

## Installation

```sh
npm install @gusok/react-style-props
```

## Usage

### `applyStyleProps`

`applyStyleProps` applies style-related properties to `style`, `css`, `sx`, or other designated properties.

```tsx
import applyStyleProps from '@gusok/react-style-props';

const props = {
  xColor: 'red',
  xMargin: '10px',
  value: 'ABC',
};

const styledProps = applyStyleProps(props);
console.log(styledProps);
// Output: { style: { color: "red", margin: "10px" }, value: "ABC" }
```

### `withStyledProps`

You can use a Higher-Order Component (HOC) to add style-related property integration to a component.

```tsx
import { withStyledProps } from '@gusok/react-style-props';

const Box = (props: any) => <div {...props} />;
const StyledBox = withStyledProps(Box);

<StyledBox xWidth="100px" xHeight="200px" xBackgroundColor="red" />;
```

## Options

You can customize the behavior of `applyStyleProps` and `withStyledProps` by passing `StylePropsOptions`.

```tsx
// Maps the `cssWidth` prop to the `css` property’s `width` key and `cssHeight` to `height`
const options = {
  styleProp: 'css',
  propsMap: { cssWidth: 'width', cssHeight: 'height' },
};

// Using applyStyleProps
const newProps = applyStyleProps(props, options);

// Using withStyledProps
const Box = (props: any) => <div {...props} />;
const StyledBox = withStyledProps(Box, options);
```

### `styleProp`

- `style`, `css`, `sx`, or any other property
- Defines where the style-related properties should be assigned
- Default: `style`

### `styleApplyMode`

- `merge`, `append`
- Determines behavior when a value is already set for `styleProp`
  - `merge`: Merges with the existing object if it's an object
  - `append`: Appends to an array if the existing value is an array; otherwise, creates a new array
- Default behavior:
  - When `styleProp` is `style`: `merge`
  - When `styleProp` is `css`: `append`
  - When `styleProp` is `sx`: `append`
  - Otherwise: `merge`

### `propsMap`

- `Record<string, keyof CSSProperties>`
- A mapping between props and keys under the `styleProp`
- Default:

```js
const propsMap = {
  xBackground: 'background',
  xBackgroundColor: 'backgroundColor',
  xBorder: 'border',
  xBorderBottom: 'borderBottom',
  xBorderColor: 'borderColor',
  xBorderLeft: 'borderLeft',
  xBorderRadius: 'borderRadius',
  xBorderRight: 'borderRight',
  xBorderTop: 'borderTop',
  xBoxShadow: 'boxShadow',
  xColor: 'color',
  xOpacity: 'opacity',
  xVisibility: 'visibility',
  xAlignItems: 'alignItems',
  xFlexDirection: 'flexDirection',
  xFlexWrap: 'flexWrap',
  xJustifyContent: 'justifyContent',
  xGap: 'gap',
  xFlex: 'flex',
  xFlexBasis: 'flexBasis',
  xFlexGrow: 'flexGrow',
  xFlexShrink: 'flexShrink',
  xDisplay: 'display',
  xOverflow: 'overflow',
  xBottom: 'bottom',
  xLeft: 'left',
  xPosition: 'position',
  xRight: 'right',
  xTop: 'top',
  xZIndex: 'zIndex',
  xHeight: 'height',
  xMaxHeight: 'maxHeight',
  xMaxWidth: 'maxWidth',
  xMinHeight: 'minHeight',
  xMinWidth: 'minWidth',
  xWidth: 'width',
  xBoxSizing: 'boxSizing',
  xMargin: 'margin',
  xMarginBottom: 'marginBottom',
  xMarginLeft: 'marginLeft',
  xMarginRight: 'marginRight',
  xMarginTop: 'marginTop',
  xPadding: 'padding',
  xPaddingBottom: 'paddingBottom',
  xPaddingLeft: 'paddingLeft',
  xPaddingRight: 'paddingRight',
  xPaddingTop: 'paddingTop',
};
```

## License

MIT License
