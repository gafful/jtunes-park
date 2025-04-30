<script>
  import { cn } from "$lib/utils";
  import { getContext } from "svelte";

  let className = "";
  export { className as class };
  export let type = "text";
  export let value = "";
  export let placeholder = "";
  export let disabled = false;
  export let id = undefined;
  export let name = undefined;
  
  // Other props can be passed through $$restProps
</script>

<input
  {id}
  {name}
  {type}
  {placeholder}
  {disabled}
  bind:value
  class={cn(
    "flex h-10 w-full rounded-md border border-input bg-background px-3 py-2 text-sm ring-offset-background",
    "file:border-0 file:bg-transparent file:text-sm file:font-medium",
    "placeholder:text-muted-foreground",
    "focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring focus-visible:ring-offset-2",
    "disabled:cursor-not-allowed disabled:opacity-50",
    className
  )}
  {...$$restProps}
/>