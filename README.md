Lovelace card to be used as a container for other cards which uses a CSS grid for layout.

**Note: When including this file in your `ui-lovelace.yaml` you must use `type: module`**

## Config

| Name | Type | Description | Default
| ---- | ---- | ----------- | -------
| type | string | `custom:grid-layout` | **Required**
| column_definitions | string | Grid columns definitions (see below) | **Required**
| row_definitions | string | Grid row definitions (see below) | **Required**
| cards | list | Card definitions (see below) | **Required**
| card_margin | integer | Space between cards | 0

### Column and Row Definitions
These can be any standard CSS Grid layout definitions and will be applied
as `grid-template-columns` and `grid-template-rows`. See [Columns](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-template-columns)
and [Rows](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-template-rows) for more information.

### Card Definitions
| Name | Type | Description | Default
| ---- | ---- | ----------- | -------
| type | string | Lovelace card type | **Required**
| column | object | Card column definition (see below) | None
| row | object | Card row definition (see below) | None
| config | Object | Specific card config options | None

### Card Column and Row Definition
Specifiy the placement and size of the card. This should be an object with
2 properties: the starting point and the size. For column the 2 properties are
`start` and `width`. For row the 2 properties are `start` and `height`.

```yaml
column:
  start: 2
  width: 3
row:
  start: 3
  height: 1
```

This will place the card in the third row and span 3 columns starting at the second

## Installation

### Step 1

Install `grid-layout` by copying `grid-layout.js`from this repo to `<config directory>/www/` on your Home Assistant instance.

### Step 2

Link `grid-layout` inside you `ui-lovelace.yaml`.

```yaml
resources:
  - url: /local/grid-layout.js?v=0
    type: module
```

### Step 3

Add a custom card or custom element in your `ui-lovelace.yaml` using `type: custom:grid-layout` and set `panel: true`

## Example
```yaml
- type: custom:grid-layout
  column_definitions: 150px 200px 300px 300px 1fr 1fr
  row_definitions: 180px 150px 150px 100px
  card_margin: 4
  cards:
    - type: glance
      column:
        start: 1
        width: 1
      row:
        start: 1
        height: 3
      config:
        entities:
          - climate.ecobee
          - cover.kitchen_window
          - switch.ac
          - climate.heatpump
        column_width: 100%
    - type: picture-entity
      column:
        start: 5
        width: 2
      row:
        start: 1
        height: 2
      config:
        image: https://images.unsplash.com/photo-1505773278895-5efa7b11679a?ixlib=rb-0.3.5&ixid=eyJhcHBfaWQiOjEyMDd9&s=0bcc9d09bd4d332b2f25603ee03fa60e&auto=format&fit=crop&w=1436&q=80
        title: Bedroom Light
        entity: light.bed_light
        tap_action: toggle
    - type: map
      column:
        start: 4
        width: 1
      row:
        start: 2
        height: 2
      config:
        entities:
          - device_tracker.demo_paulus
          - device_tracker.demo_home_boy
    - type: entities
      column:
        start: 2
        width: 2
      row:
        start: 2
        height: 2
      config:
        entities:
          - climate.ecobee
          - entity: input_number.noise_allowance
          - input_select.who_cooks
          - scene.romantic_lights
          - sensor.brightness
    - type: picture-glance
      column:
        start: 2
        width: 3
      row:
        start: 1
        height: 1
      config:
        title: Kitchen
        image: https://images.unsplash.com/photo-1497366672149-e5e4b4d34eb3?ixlib=rb-0.3.5&q=80&fm=jpg&crop=entropy&cs=tinysrgb&w=900&h=200&fit=crop&ixid=eyJhcHBfaWQiOjF9&s=5cc8b6574a7d9cf7235fd90b9ad21d12
        entities:
          - sensor.outside_temperature
          - switch.decorative_lights
    - type: custom:circle-sensor-card
      column:
        start: 5
        width: 1
      row:
        start: 3
        height: 1
      config:
        entity: sensor.outside_humidity
        show_card: true
        stroke_color: '#17b742'
        stroke_width: 14
    - type: custom:circle-sensor-card
      column:
        start: 6
        width: 1
      row:
        start: 3
        height: 1
      config:
        entity: sensor.outside_temperature
        show_card: true
        stroke_width: 14
        min: 0
        max: 40
```
