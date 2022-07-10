# PlumImage

This component displays an image.

### Basic usage

### HTML Structure

```html
<PlumImage
    src="https://plumguide-staging.freetls.fastly.net/listings/2591/hero/f29f49dc-7999-48d9-8a5a-da4bcde126ef.jpg"
    alt="Plum Guide Image"
    :lazyload="true" />
```

## Inputs

| Name     | Required | Description                                                    | Values (default in bold) |
| -------- | -------- | -------------------------------------------------------------- | ------------------------ |
| src      | yes      | images' path                                                   | -                        |
| alt      | no       | alt text                                                       | -                        |
| lazyload | no       | will change `src` to `data-src` based on visibility in viewport| **false**, true          |
