<script>
  /**
   * @event {{ toggled: boolean; }} toggle
   */

  /**
   * Specify the toggle size
   * @type {"default" | "sm"}
   */
  export let size = "default";

  /** Set to `true` to toggle the checkbox input */
  export let toggled = false;

  /** Set to `true` to disable checkbox input */
  export let disabled = false;

  /** Specify the label for the untoggled state */
  export let labelA = "Off";

  /** Specify the label for the toggled state */
  export let labelB = "On";

  /** Specify the label text */
  export let labelText = "";

  /** Set an id for the input element */
  export let id = "ccs-" + Math.random().toString(36);

  /**
   * Specify a name attribute for the checkbox input
   * @type {string}
   */
  export let name = undefined;

  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  $: dispatch("toggle", { toggled });
</script>

<!-- svelte-ignore a11y-mouse-events-have-key-events -->
<div
  class:bx--form-item="{true}"
  {...$$restProps}
  on:click
  on:mouseover
  on:mouseenter
  on:mouseleave
>
  <input
    type="checkbox"
    class:bx--toggle-input="{true}"
    class:bx--toggle-input--small="{size === 'sm'}"
    checked="{toggled}"
    on:change
    on:change="{() => {
      toggled = !toggled;
    }}"
    on:keyup
    on:keyup="{(e) => {
      if (e.key === ' ' || e.key === 'Enter') {
        e.preventDefault();
        toggled = !toggled;
      }
    }}"
    on:focus
    on:blur
    disabled="{disabled}"
    id="{id}"
    name="{name}"
  />
  <label
    aria-label="{labelText ? undefined : $$props['aria-label'] || 'Toggle'}"
    for="{id}"
    class:bx--toggle-input__label="{true}"
  >
    <slot name="labelText">
      {labelText}
    </slot>
    <span class:bx--toggle__switch="{true}">
      <span aria-hidden="true" class:bx--toggle__text--off="{true}">
        {labelA}
      </span>
      <span aria-hidden="true" class:bx--toggle__text--on="{true}">
        {labelB}
      </span>
    </span>
  </label>
</div>
