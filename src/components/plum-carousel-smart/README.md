# PlumCarouselSmart

This component displays a carousel.

### Basic usage

### HTML Structure

```html
    <PlumCarouselSmart
    :imageUrls="imageUrls"
    maxImages="30"
    :lazyload="true"
    :display-counter="true" />
```

## Inputs

| Name             | Required | Description                                                    | Values (default in bold) |
| ---------------- | -------- | -------------------------------------------------------------- | ------------------------ |
| imageUrls        | yes      | Array of image urls                                            | -                        |
| maxImages        | no       | number of slides/images to display                             | **30**                   |
| lazyload         | no       | will change `src` to `data-src` based on visibility in viewport| **false**, true          |
| display-counter  | no       | displays the current slide number out of total slides          | false, **true**          |
