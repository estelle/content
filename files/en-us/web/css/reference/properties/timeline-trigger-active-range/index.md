---
title: timeline-trigger-active-range CSS property
short-title: timeline-trigger-active-range
slug: Web/CSS/Reference/Properties/timeline-trigger-active-range
page-type: css-shorthand-property
status:
  - experimental
browser-compat: css.properties.timeline-trigger-active-range
sidebar: cssref
---

{{SeeCompatTable}}

The **`timeline-trigger-active-range`** [CSS](/en-US/docs/Web/CSS) [shorthand property](/en-US/docs/Web/CSS/Guides/Cascade/Shorthand_properties) specifies a [scroll-triggered animation](/en-US/docs/Web/CSS/Guides/Animation_triggers/Using_scroll-triggered_animations) trigger's active range.

## Constituent properties

This property is a shorthand for the following CSS properties:

- {{cssxref("timeline-trigger-active-range-start")}}
- {{cssxref("timeline-trigger-active-range-end")}}

## Syntax

```css
/* Keywords */
timeline-trigger-active-range: normal;
timeline-trigger-active-range: auto;

/* Range start only */
timeline-trigger-active-range: 0%;
timeline-trigger-active-range: 10px;
timeline-trigger-active-range: cover;
timeline-trigger-active-range: exit 10%;
timeline-trigger-active-range: contain 50px;

/* Range start and end */
timeline-trigger-active-range: 5% 95%;
timeline-trigger-active-range: entry exit;
timeline-trigger-active-range: auto 10%;
timeline-trigger-active-range: 10% normal;
timeline-trigger-active-range: contain contain 90%;
timeline-trigger-active-range: 200px exit 600px;
timeline-trigger-active-range: entry 10% 90%;
timeline-trigger-active-range: entry 0% exit 50%;
timeline-trigger-active-range: contain 100px contain 90%;

/* Multiple values */
timeline-trigger-active-range:
  cover,
  entry 0% exit 50%;

/* Global values */
timeline-trigger-active-range: inherit;
timeline-trigger-active-range: initial;
timeline-trigger-active-range: revert;
timeline-trigger-active-range: revert-layer;
timeline-trigger-active-range: unset;
```

### Values

This property is specified as a comma-separated list of animation ranges. Each animation range is specified as one to four space separated values composed of a {{cssxref("timeline-trigger-active-range-start")}} value and, optionally, a {{cssxref("timeline-trigger-active-range-end")}} value.

- `<'{{cssxref("timeline-trigger-active-range-start")}}'>`
  - : The keyword `normal` or `auto`, a {{cssxref("length-percentage")}}, a {{cssxref("timeline-range-name")}}, or both a `<timeline-range-name>` and `<length-percentage>`, in that order, separated by a space.
- `<'{{cssxref("timeline-trigger-active-range-end")}}'>`
  - : The keyword `normal` or `auto`, a `<length-percentage>`, a `<timeline-range-name>`, or or both a `<timeline-range-name>` and `<length-percentage>`, in that order, separated by a space.

Percentage values are relative to the length of the named timeline range, if specified, or the `normal` timeline if not.

## Description

The `timeline-trigger-active-range` property can be used to create a trigger active range that is the same size or longer than it's activation range. The property specifies the start and end of a trigger's active range, which defines how long a trigger will stay active once activated when creating [CSS scroll-triggered animations](/en-US/docs/Web/CSS/Guides/Animation_triggers/Using_scroll-triggered_animations).

Only when a tracked element moves out of the active range does the trigger become inactive, becoming active again when it re-enters the [activation range](/en-US/docs/Web/CSS/Reference/Properties/timeline-trigger-activation-range).

The _active range_ is the range within which a trigger remains activated once activation occurs. By default, the active range starts where the activation range starts and ends with the active range ends. Activation occurs when a tracked element _enters an activation range_, and deactivates when it _leaves the active range_. By default, the active range is the same as the activation range; but this property enables expanding the active range beyond the borders of the activation range, creating a buffer zone that prevents premature deactivations when a user scrolls back and forth across activation endpoints. Active ranges that are longer than activation ranges are useful when you want an animation to be triggered in a small activation range and to stay active within a larger range. The trigger becomes active whenever it enters (or re-enters) the activation range, but only deactivate when it leaves the larger active range.

As noted, by default, the `timeline-trigger-active-range` value is the same as the {{cssxref("timeline-trigger-activation-range")}}. This can be explicitly set by specifying `auto`.

A value of `normal` sets the active range to the default named range. The default named range depends on the {{cssxref("timeline-trigger-source")}}: it is equivalent to `cover` for a [view progress timeline](/en-US/docs/Web/CSS/Guides/Scroll-driven_animations/Timelines#view_progress_timelines) and `scroll` for a [scroll progress timeline](/en-US/docs/Web/CSS/Guides/Scroll-driven_animations/Timelines#scroll_progress_timelines). The default offset values are `0%` for the range start and `100%` for the range end. Therefore, setting `normal`, with no offset, resolves to either `cover 0% cover 100%` or `scroll 0% scroll 100%`.

The `timeline-trigger-active-range` property can be used to set:

- Start and end offsets from the `normal` range
  - : A `<length>` or `<percentage>` value, without a named range, specifies offsets from the beginning of the `normal` timeline, which again defaults to [`cover`](/en-US/docs/Web/CSS/Reference/Values/timeline-range-name#cover) for a view progress timeline source, and [`scroll`](/en-US/docs/Web/CSS/Reference/Values/timeline-range-name#scroll) for a scroll progress timeline source. Negative values outset the start and end, resulting in an active range that is longer than the normal range. Positive values inset the start and end of the active range, specifying an active range that it shorter that the normal range (but still as long, or longer, than the activation range).
- Specific named ranges
  - : Setting a `<timeline-range-name>` value of `cover`, `contain`, `entry`, `exit`, `entry-crossing`, `exit-crossing`, or `scroll`, without an offset defaults to `0%` as the offset for the active-range starting value and `100%` for the end offsets along the named timeline ranges. See [Understanding timeline range names](/en-US/docs/Web/CSS/Guides/Scroll-driven_animations/Timeline_range_names).
- Offset from specific named ranges
  - : When both a `<timeline-range-name>` and `<length>` or `<percentage>` value are specified for the start or end value, the named range is offset by the distances specified, from the start of the named range. Percentage values are relative to the range specified. See [Setting insets using percentages](/en-US/docs/Web/CSS/Guides/Scroll-driven_animations/Timeline_insets#setting_insets_using_percentages)

The `timeline-trigger-active-range` property, along with the {{cssxref("timeline-trigger-name")}}, {{cssxref("timeline-trigger-source")}}, and {{cssxref("timeline-trigger-activation-range")}} properties, can also be set using the {{cssxref("timeline-trigger")}} shorthand.

### Property value order

The value of each property is the the keyword `normal` or `auto`, a `<length-percentage>`, a `<timeline-range-name>`, or or both a `<timeline-range-name>` and `<length-percentage>`, in that order, separated by a space. If a `<timeline-range-name>` is set without a `<length-percentage>`, it defaults to `0%` for the start value and `100%` for the end value.

If the value is only one keyword, one `<length-percentage>`, one named timeline range, or one named-range followed by a single `<length-percentage>`, that defines the value of the `timeline-trigger-active-range-start` component. If two or more values are included in your `animation-range` declaration and the values are anything other than a `<timeline-range-name>` followed by a `<length-percentage>`, both [constituent property](#constituent_properties) values are explicitly set.

When only the value of the `timeline-trigger-active-range-start` component is specified, the computed value of the `timeline-trigger-active-range-end` property follows specific rules:

- If the start value is a single `<length-percentage>` or the keyword `normal`, the end value is implicitly set to `normal`.
- If the start value is a single {{cssxref("timeline-range-name")}}, without a `<length-percentage>`, the active range is the full length of that named timeline.
- If the start value includes both a named timeline and an offset, the named timeline is applied to both the start and end values, and the end offset is set to `100%`.

When you include two values and the first value is the keyword `normal` or a `<length-percentage>`, that first value defines the `timeline-trigger-active-range-start` component and the second value defines the `timeline-trigger-active-range-end` component.

Other than `timeline-trigger-active-range` supporting the `auto` keyword, it works in exactly the same way as the {{cssxref("animation-range")}} property. See the following for more information:

- [Explicitly defining both range start and range end with two values](/en-US/docs/Web/CSS/Reference/Properties/animation-range#explicitly_defining_both_range_start_and_range_end_with_two_values)
- [Defining range start and defaulting range end](/en-US/docs/Web/CSS/Reference/Properties/animation-range#defining_range_start_and_defaulting_range_end)

### Specifying multiple ranges

If multiple `timeline-trigger-name` values are set, but only a single `timeline-trigger-active-range` value is set, the `timeline-trigger-active-range` will apply to all the `timeline-trigger-name`s. To set multiple `timeline-trigger-active-range` values, comma-separate them.

When you specify multiple comma-separated values in a single `timeline-trigger-active-range` declaration, they apply to the timeline triggers in the order in which they appear in the {{cssxref("timeline-trigger-name")}} property. When the number of triggers and `timeline-trigger-active-range` property values do not match, they are applied in the same way as [multiple animation property values](/en-US/docs/Web/CSS/Guides/Animations/Using#setting_multiple_animation_property_values).

When multiple `timeline-trigger-active-range` and `timeline-trigger-name` values are set, each name gets applied a range, cycling through the list of ranges, until every timeline trigger has a `timeline-trigger-active-range` value set.

Consider these declarations:

```css
timeline-trigger-name:
  --trigger1, --trigger2, --trigger3, --trigger4, --trigger5;
timeline-trigger-active-range:
  cover,
  contain 100px contain 90%;
```

In this case, as there are five names but only two ranges, the ranges are cycled, with every odd trigger using the `cover` range and every even numbered trigger using the `contain 100px contain 90%` range.

## Formal definition

{{cssinfo}}

## Formal syntax

{{csssyntax}}

## Examples

### Basic usages

### Basic usage

In this example, we demonstrate the effect of extending a trigger's active range by creating two identical triggered animations, and use the `timeline-trigger-active-range` property to extend both the start and end of one of the animation trigger's active range to be beyond the start and end of the activation range.

#### HTML

Our markup contains four {{htmlelement("div")}} elements — two to animate and two to create a trigger on — plus some basic text content to cause the page to scroll. We have hidden the text content for brevity.

```html
<div class="animated">I am animated</div>
<div class="animated longer">I am animated longer</div>

...
<section>
  <div class="trigger">I create the trigger</div>
  <div class="trigger longer">I create a longer trigger</div>
</section>
...
```

```html hidden live-sample___basic-example
<div class="animated">I am animated</div>
<div class="animated longer">I am animated longer</div>
<p>
  Fusce dictum ex quis ipsum consectetur placerat. Cras sed lectus ex. Quisque
  purus dolor, vulputate ac mi eget, commodo varius odio. Suspendisse faucibus
  ipsum vel libero finibus, in placerat nibh congue. Sed iaculis, metus et
  euismod posuere, mi diam vestibulum felis, ac vulputate eros ipsum id justo.
  Etiam a tincidunt purus. Maecenas semper sed enim at blandit. Aenean ut
  sagittis lorem, eget gravida purus. Phasellus eleifend, lectus nec pulvinar
  facilisis, dui dolor feugiat odio, iaculis tempor felis est non tortor. In
  suscipit lorem efficitur molestie tempus. Integer sit amet neque et risus
  iaculis sodales sed eget diam. Quisque sodales nunc sapien, vitae lacinia ex
  luctus quis. Maecenas scelerisque scelerisque elit eu consequat. Etiam ac
  tristique tellus, sed tincidunt velit.
</p>

<p>
  Fusce dictum ex quis ipsum consectetur placerat. Cras sed lectus ex. Quisque
  purus dolor, vulputate ac mi eget, commodo varius odio. Suspendisse faucibus
  ipsum vel libero finibus, in placerat nibh congue. Sed iaculis, metus et
  euismod posuere, mi diam vestibulum felis, ac vulputate eros ipsum id justo.
  Etiam a tincidunt purus. Maecenas semper sed enim at blandit. Aenean ut
  sagittis lorem, eget gravida purus. Phasellus eleifend, lectus nec pulvinar
  facilisis, dui dolor feugiat odio, iaculis tempor felis est non tortor. In
  suscipit lorem efficitur molestie tempus. Integer sit amet neque et risus
  iaculis sodales sed eget diam. Quisque sodales nunc sapien, vitae lacinia ex
  luctus quis. Maecenas scelerisque scelerisque elit eu consequat. Etiam ac
  tristique tellus, sed tincidunt velit.
</p>

<section>
  <div class="trigger">I create the trigger</div>
  <div class="trigger longer">I create a longer trigger</div>
</section>

<p>
  Fusce dictum ex quis ipsum consectetur placerat. Cras sed lectus ex. Quisque
  purus dolor, vulputate ac mi eget, commodo varius odio. Suspendisse faucibus
  ipsum vel libero finibus, in placerat nibh congue. Sed iaculis, metus et
  euismod posuere, mi diam vestibulum felis, ac vulputate eros ipsum id justo.
  Etiam a tincidunt purus. Maecenas semper sed enim at blandit. Aenean ut
  sagittis lorem, eget gravida purus. Phasellus eleifend, lectus nec pulvinar
  facilisis, dui dolor feugiat odio, iaculis tempor felis est non tortor. In
  suscipit lorem efficitur molestie tempus. Integer sit amet neque et risus
  iaculis sodales sed eget diam. Quisque sodales nunc sapien, vitae lacinia ex
  luctus quis. Maecenas scelerisque scelerisque elit eu consequat. Etiam ac
  tristique tellus, sed tincidunt velit.
</p>

<p>
  Fusce dictum ex quis ipsum consectetur placerat. Cras sed lectus ex. Quisque
  purus dolor, vulputate ac mi eget, commodo varius odio. Suspendisse faucibus
  ipsum vel libero finibus, in placerat nibh congue. Sed iaculis, metus et
  euismod posuere, mi diam vestibulum felis, ac vulputate eros ipsum id justo.
  Etiam a tincidunt purus. Maecenas semper sed enim at blandit. Aenean ut
  sagittis lorem, eget gravida purus. Phasellus eleifend, lectus nec pulvinar
  facilisis, dui dolor feugiat odio, iaculis tempor felis est non tortor. In
  suscipit lorem efficitur molestie tempus. Integer sit amet neque et risus
  iaculis sodales sed eget diam. Quisque sodales nunc sapien, vitae lacinia ex
  luctus quis. Maecenas scelerisque scelerisque elit eu consequat. Etiam ac
  tristique tellus, sed tincidunt velit.
</p>
```

#### CSS

The `.animated` elements' {{cssxref("position")}} is set to `fixed`, positioning them near the top-left of the scrollport to enable us to see when their animations start and stop.

```css hidden live-sample___basic-example
body {
  width: 80%;
  margin: 0 auto;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 1.3rem;
}

div {
  height: 100px;
  border: 5px solid black;
}

.animated {
  width: 100px;
  background: orange;
}

.trigger {
  background: wheat;
}
```

```css live-sample___basic-example
.animated {
  position: fixed;
  top: 25px;
  left: 25px;
}
.animated.longer {
  left: 150px;
}
section {
  display: flex;
  gap: 20px;
}
```

Next, we define the {{cssxref("@keyframes")}} for a `rotate` animation:

```css live-sample___basic-example
@keyframes rotate {
  from {
    rotate: 0deg;
  }

  to {
    rotate: 360deg;
  }
}
```

Using the {{cssxref("animation")}} shorthand, the `rotate` animation is applied to the `.animated` elements. The values reference a `timeline-trigger-name` of `--t` and `--longerT`, respectively, and define two `<animation-action>` values — `play` and `pause` — which specify that the animations will play on activation and pause on deactivation.

```css live-sample___basic-example
.animated {
  animation: rotate 3s infinite linear;
  animation-trigger: --t play pause;
}
.animated.longer {
  animation-trigger: --longerT play pause;
}
```

The `.trigger` elements create the `.animated` elements' triggers via the following properties:

- A {{cssxref("timeline-trigger-name")}} with value `--t`, which is equal to the identifier referenced in the `.animated` elements' `animation-trigger` property value, associating them together.
- A {{cssxref("timeline-trigger-source")}} with value [`view()`](/en-US/docs/Web/CSS/Reference/Properties/animation-timeline/view), which sets the timeline trigger as a view progress timeline, and the element providing the timeline trigger as the nearest scrolling ancestor element.
- A {{cssxref("timeline-trigger-activation-range")}} of `contain 40% 60%`. The `contain` range spans from when the trigger element has completely entered the viewport to when it starts to leave. This value sets the trigger's activation range to start `40%` of the way through the range and end `60%` through it, meaning activation range start right before the trigger is vertically centered in the scrollport and ends right after it has scrolled past this midpoint.

The `.trigger.longer` element creates the `.animated.longer` element's trigger via the following properties:

- A {{cssxref("timeline-trigger-name")}} with value `--longerT` (overriding the `--t`), which is equal to the identifier referenced in the `.animated.longer` element's `animation-trigger` property value, associating the two together.

- A `timeline-trigger-active-range` of `contain -50px cover 100%`. The `contain -50px` means the `timeline-trigger-active-range` occurs when the bottom edge of the trigger is `50px` from the bottom edge of the scrollport and `timeline-trigger-active-range-end` occurs when the bottom edge of the trigger has just crossed the top edge of the scrollport.

```css live-sample___basic-example
.trigger {
  timeline-trigger-name: --t;
  timeline-trigger-source: view();
  timeline-trigger-activation-range: contain 40% 60%;
}
.trigger.longer {
  timeline-trigger-name: --longerT;
  timeline-trigger-active-range: contain -50px cover 100%;
}
```

```css hidden live-sample___basic-example
@supports not (timeline-trigger-active-range: contain -50px cover 100%) {
  body::before {
    content: "Your browser does not support the timeline-trigger-active-range property.";
    background-color: wheat;
    text-align: center;
    padding: 1rem 0;

    z-index: 1;
    position: fixed;
    inset: 40% 0 auto;
  }
}
```

#### Result

{{EmbedLiveSample("basic-example", "100%", "240")}}

Try scrolling the content up. Both animations start playing at `40%`, right before the tracked `.trigger` elements are vertically centered in the scrollport. The animation of one element pauses when the trigger is at `60%` of the `contain` timeline, which occurs when the triggers are just past the vertical center of the scrollport. The `.animated.longer` element pauses only when the trigger has fully exited the viewport.

After both animations have paused, scroll downward again. The animations both restart playing when the trigger elements reach the `60%` point, just before they are vertically centered in the scrollport. This is because the active range can extend how long the trigger remains active, but has no effect where activation and deactivation occur. As you continue scrolling down, the animation of one element pauses just after is crosses the center of the scrollport, while the other remains active until the trigger is halfway past the bottom edge of the scrollport.

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- {{cssxref("timeline-trigger-active-range-end")}}, {{cssxref("timeline-trigger-active-range-start")}}
- {{cssxref("animation-trigger")}}
- {{cssxref("timeline-trigger-name")}}, {{cssxref("timeline-trigger-source")}}, and {{cssxref("timeline-trigger-activation-range")}}
- {{cssxref("timeline-trigger")}} shorthand property
- {{cssxref("trigger-scope")}}
- {{cssxref("animation-action")}} type
- [Using CSS scroll-triggered animations](/en-US/docs/Web/CSS/Guides/Animation_triggers/Using_scroll-triggered_animations)
- [CSS animation triggers](/en-US/docs/Web/CSS/Guides/Animation_triggers/) module
- [CSS animations](/en-US/docs/Web/CSS/Guides/Animations) module
