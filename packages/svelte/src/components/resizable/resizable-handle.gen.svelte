<script lang="ts">
import '@prosekit/web/resizable'

import { resizableHandleProps, resizableHandleEvents } from '@prosekit/web/resizable'
import { ClientUpdate } from '../client-update'
import { useComponent } from '../use-component'
import { useEventHandlers } from '../use-event-handlers'

let attributes: Record<string, unknown> = {}
let eventHandlers: Record<string, (...args: any[]) => any> = {}
let element: HTMLElement | undefined = undefined
const handleChange = useComponent(Object.keys(resizableHandleProps), Object.keys(resizableHandleEvents))

$: {
  [attributes, eventHandlers] = handleChange(element, $$props)
}
</script>

<ClientUpdate>
  <prosekit-resizable-handle {...attributes} use:useEventHandlers={eventHandlers} bind:this={element}>
    <slot />
  </prosekit-resizable-handle>
</ClientUpdate>
