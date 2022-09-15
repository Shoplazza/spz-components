# spz-tabs
Tabs, quickly change panes of local content.

## Usage

The `spz-tabs` component allows you to display content tabs. 

-   An `spz-tabs` accepts one `<ul role="tabs">` elements as its direct
    tab menus.
-   Each `<li role="tab">` is the heading for on of `<div role="tabpanel">` element, and `li` s `data-panel` value matchs `div` s `data-id` value.
```html
    <spz-tabs layout="container">
      <ul role="tabs">
        <li role="tab" data-panel='home'>Home</li>
        <li role="tab" data-panel='profile' active>Profile</li>
        <li role="tab" data-panel='messages' >Messages</li>
      </ul>
    
      <!-- Tab panes -->
      <div role="tabpanel" data-id="home">home</div>
      <div role="tabpanel" data-id="profile">profile</div>
      <div role="tabpanel" data-id="messages">messages</div>
    </spz-tabs>
```

#### Layout and style

Must be set to `container`.

## Attributes

### `active`

Added to `li` element to initial display tab content.

## Action

### `tabChange`

tab change