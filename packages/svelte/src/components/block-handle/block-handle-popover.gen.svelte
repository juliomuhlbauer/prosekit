<script lang="ts">
import '@prosekit/web/block-handle'

import { blockHandlePopoverProps, blockHandlePopoverEvents } from '@prosekit/web/block-handle'
import { ClientUpdate } from '../client-update'
import { useComponent } from '../use-component'
import { useEventHandlers } from '../use-event-handlers'

let attributes: Record<string, unknown> = {}
let eventHandlers: Record<string, (...args: any[]) => any> = {}
let element: HTMLElement | undefined = undefined
const handleChange = useComponent(Object.keys(blockHandlePopoverProps), Object.keys(blockHandlePopoverEvents))

$: {
  [attributes, eventHandlers] = handleChange(element, $$props)
}
</script>

<ClientUpdate>
  <prosekit-block-handle-popover {...attributes} use:useEventHandlers={eventHandlers} bind:this={element}>
    <slot />
  </prosekit-block-handle-popover>
</ClientUpdate>
