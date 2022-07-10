# PlumIcon

This component is a wrapper for svg icons

## How to add a new icon

Designers will give you compressed svgs that have prefixIds and no fill attribute.

Supported Icon names
- arrow

### Basic usage

### HTML Structure

```html
 <PlumIcon name="arrow" size="l" :rotation="180" />
```

## How to import new svg icon

To import a new icon, you have to rename it without uppercase and specials chars in `icons/`

## Inputs

| Name     | Required | Description                                                    | Values (default in bold) |
| -------- | -------- | -------------------------------------------------------------- | ------------------------ |
| name     | yes      | The icon name                                                  | -                        |
| size     | no       | the icon's width xs: 12, s: 18, m: 24, l: 30, xl: 42, xxl: 46, | **m**                    |
| rotation | no       | rotation on the icon                                           | **0**                    |
