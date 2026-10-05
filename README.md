# reka-ui: popper content is not positioned when its trigger is inside `TooltipRoot`

```sh
npm install
npm run dev
```

Click each button. In cases 2 and 3 the content opens, but its `[data-reka-popper-content-wrapper]` keeps `transform: translate(0px, -200%)`, so it is above the top of the page.

1. Popover without a tooltip: works.
2. `PopoverRoot` > `TooltipRoot` > `TooltipTrigger as-child` > `PopoverTrigger`, like the "Composing multiple primitives" example in the Composition guide (which uses `DialogTrigger`): not positioned.
3. The same with `DropdownMenuTrigger`: not positioned.
4. `TooltipRoot` in a separate component inside `PopoverAnchor as-child`: works.

Tested with reka-ui 2.11.0, 2.10.5 and 2.0.0, Vue 3.5.43, Vite 8.3.2.
