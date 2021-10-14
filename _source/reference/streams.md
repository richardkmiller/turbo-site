---
permalink: /reference/streams.html
order: 03
description: "A reference of everything you can do with Turbo Streams."
---

# Streams

## The seven actions

### Append

Appends the content within the template tag to the container designated by the target dom id.

```html
<turbo-stream action="append" target="dom_id">
  <template>
    Content to append to container designated with the dom_id.
  </template>
</turbo-stream>
```

### Prepend

Prepends the content within the template tag to the container designated by the target dom id.

```html
<turbo-stream action="prepend" target="dom_id">
  <template>
    Content to prepend to container designated with the dom_id.
  </template>
</turbo-stream>
```

### Replace

Replaces the element designated by the target dom id.

```html
<turbo-stream action="replace" target="dom_id">
  <template>
    Content to replace the element designated with the dom_id.
  </template>
</turbo-stream>
```

### Update

Updates the content within the template tag to the container designated by the target dom id.

```html
<turbo-stream action="update" target="dom_id">
  <template>
    Content to update to container designated with the dom_id.
  </template>
</turbo-stream>
```

### Remove

Removes the element designated by the target dom id.

```html
<turbo-stream action="remove" target="dom_id">
</turbo-stream>
```

### Before

Inserts the content within the template tag before the element designated by the target dom id.

```html
<turbo-stream action="before" target="dom_id">
  <template>
    Content to place before the element designated with the dom_id.
  </template>
</turbo-stream>
```

### After

Inserts the content within the template tag after the element designated by the target dom id.

```html
<turbo-stream action="after" target="dom_id">
  <template>
    Content to place after the element designated with the dom_id.
  </template>
</turbo-stream>
```

## Targeting Multiple Elements

To target multiple elements with a single action, use the `targets` attribute with a CSS query selector instead of the `target` attribute.

```html
<turbo-stream action="remove" targets=".elementsWithClass">
</turbo-stream>

<turbo-stream action="after" targets=".elementsWithClass">
  <template>
    Content to place after the elements designated with the css query.
  </template>
</turbo-stream>
```

## Processing Stream Elements

Turbo can connected to any form of stream to receive and process stream actions. A stream source must dispatch [MessageEvent](https://developer.mozilla.org/en-US/docs/Web/API/MessageEvent) messages that contain the stream action HTML in the `data` attribute of that event. It's then connected by `Turbo.session.connectStreamSource(source)` and disconnected via `Turbo.session.disconnectStreamSource(source)`. If you need to process stream actions from different source than something producing `MessageEvent`s, you can use `Turbo.session.streamObserver.receiveMessageHTML(streamActionHTML)` to do so.

A good way to wrap all this together is by using a custom element, like turbo-rails does with [TurboCableStreamSourceElement](https://github.com/hotwired/turbo-rails/blob/main/app/javascript/turbo/cable_stream_source_element.js).
