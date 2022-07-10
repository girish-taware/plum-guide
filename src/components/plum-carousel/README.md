# PlumCarousel

This component displays a carousel navigators and the content.

Exposes a variable currentSlide via v-slot="{ currentSlide }" which can be used to display the slide in the content.

### Basic usage

### HTML Structure

```html
<PlumCarousel
    v-slot="{ currentSlide }"
    :display-counter="true"
    total-slides="30"
    >
    <!-- Carousel content -->
</PlumCarousel>
```

## Inputs

| Name             | Required | Description                                                    | Values (default in bold) |
| ---------------- | -------- | -------------------------------------------------------------- | ------------------------ |
| display-counter  | no       | displays the current slide number out of total slides          | false, **true**          |
| total-slides     | no       | number of slides to display                                    | **0**                    |
