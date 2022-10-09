<script lang="ts" setup>
  export let color = "primary";

  let bg;
  let hoverBg;
  switch (color) {
    case "primary":
      bg = "bg-emerald-400";
      hoverBg = "hover:bg-emerald-600";
      break;
    case "secondary":
      bg = "bg-cyan-400";
      hoverBg = "hover:bg-cyan-600";
      break;
    default:
      bg = "bg-rose-400";
      hoverBg = "hover:bg-rose-600";
      break;
  }
</script>

<button
  type="button"
  class="
      min-w-[100px]
      p-2
      rounded-md
      text-white
      transition
      duration-700
      {bg}
      {hoverBg}
    "
>
  <slot />
</button>
