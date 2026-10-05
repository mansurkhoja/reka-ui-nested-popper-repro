<script setup>
import {
  DropdownMenuContent, DropdownMenuItem, DropdownMenuPortal, DropdownMenuRoot, DropdownMenuTrigger,
  PopoverAnchor, PopoverContent, PopoverPortal, PopoverRoot, PopoverTrigger,
  TooltipContent, TooltipPortal, TooltipProvider, TooltipRoot, TooltipTrigger,
} from 'reka-ui'
import { ref } from 'vue'
import WithTooltip from './WithTooltip.vue'

const workaround = ref(false)
</script>

<template>
  <p>Click each button. The content should open below it.</p>

  <!-- 1. Popover without a tooltip: works -->
  <div class="row">
    <PopoverRoot>
      <PopoverTrigger data-button="popover">
        Popover
      </PopoverTrigger>
      <PopoverPortal>
        <PopoverContent class="content" data-test="popover" side="bottom">
          Popover content
        </PopoverContent>
      </PopoverPortal>
    </PopoverRoot>
    <span>1. Popover without a tooltip (works)</span>
  </div>

  <!-- 2. Popover with a tooltip, composed like in the Composition guide: broken -->
  <div class="row">
    <PopoverRoot>
      <TooltipProvider>
        <TooltipRoot>
          <TooltipTrigger as-child>
            <PopoverTrigger data-button="popover-tooltip">
              Popover + tooltip
            </PopoverTrigger>
          </TooltipTrigger>
          <TooltipPortal>
            <TooltipContent class="content">
              Tooltip
            </TooltipContent>
          </TooltipPortal>
        </TooltipRoot>
      </TooltipProvider>
      <PopoverPortal>
        <PopoverContent class="content" data-test="popover-tooltip" side="bottom">
          Popover content
        </PopoverContent>
      </PopoverPortal>
    </PopoverRoot>
    <span>2. Popover with a tooltip (content is not positioned)</span>
  </div>

  <!-- 3. DropdownMenu with a tooltip: broken -->
  <div class="row">
    <DropdownMenuRoot>
      <TooltipProvider>
        <TooltipRoot>
          <TooltipTrigger as-child>
            <DropdownMenuTrigger data-button="menu-tooltip">
              Menu + tooltip
            </DropdownMenuTrigger>
          </TooltipTrigger>
          <TooltipPortal>
            <TooltipContent class="content">
              Tooltip
            </TooltipContent>
          </TooltipPortal>
        </TooltipRoot>
      </TooltipProvider>
      <DropdownMenuPortal>
        <DropdownMenuContent class="content" data-test="menu-tooltip" side="bottom">
          <DropdownMenuItem>Menu item</DropdownMenuItem>
        </DropdownMenuContent>
      </DropdownMenuPortal>
    </DropdownMenuRoot>
    <span>3. DropdownMenu with a tooltip (content is not positioned)</span>
  </div>

  <!-- 4. TooltipRoot below PopoverAnchor, in its own component: works -->
  <div class="row">
    <PopoverRoot v-model:open="workaround">
      <PopoverAnchor as-child>
        <WithTooltip text="Tooltip">
          <button data-button="workaround" @click="workaround = !workaround">
            Anchor + tooltip
          </button>
        </WithTooltip>
      </PopoverAnchor>
      <PopoverPortal>
        <PopoverContent class="content" data-test="workaround" side="bottom">
          Popover content
        </PopoverContent>
      </PopoverPortal>
    </PopoverRoot>
    <span>4. TooltipRoot inside PopoverAnchor, in a separate component (works)</span>
  </div>
</template>
