<template>
  <div
    class="base-tag"
    :class="[
      `base-tag--${color}`,
      `base-tag--${size}`,
      outline ? 'base-tag--outline' : 'base-tag--filled',
    ]"
  >
    <slot />
  </div>
</template>

<script>
import { extendedPalette } from '../../tailwind/theme';

export const Sizes = Object.freeze({
  SMALL: 'small',
  MEDIUM: 'medium',
  LARGE: 'large',
});

const colors = Object.keys(extendedPalette);

export default {
  props: {
    /**
     * One of the extend color palette names: `geyser`, `tuberose`, `gingerrr`,
     * `rose`, `tangerine`, `maroon`, `puce`, `inevitable`, `virginia`,
     * `mosaic`, `eastern`, `caribbean`, or `evergreen`.
     */
    color: {
      type: String,
      default: colors[0],
      validator: (value) => colors.includes(value),
    },
    /** If true, displays the outline version of this tag. */
    outline: {
      type: Boolean,
      default: false,
    },
    /** One of `small`, `medium`, or `large`. */
    size: {
      type: String,
      default: Sizes.MEDIUM,
      validator: (value) => Object.values(Sizes).includes(value),
    },
  },
};
</script>

<style scoped>
.base-tag {
  @apply border
    box-border
    inline-flex
    items-center
    whitespace-no-wrap
    /* For legacy */
    border-solid;
}

@each $size in small, medium, large {
  .base-tag--$(size) {
    @apply font-overline-$(size);
  }
}

.base-tag--small {
  @apply h-4 px-2;
  border-radius: 3px;
}

.base-tag--medium {
  @apply h-6 px-3;
  border-radius: 4px;
}

.base-tag--large {
  @apply h-8 px-4;
  border-radius: 5px;
}

.base-tag--filled {
  @apply border-transparent text-white;
}

.base-tag--filled.base-tag--geyser,
.base-tag--filled.base-tag--tuberose {
  @apply text-gray-2;
}

.base-tag--outline {
  @apply bg-transparent;
}

@each $color in geyser, tuberose, gingerrr, rose, tangerine, maroon, puce,
  inevitable, virginia, mosaic, eastern, caribbean, evergreen
{
  .base-tag--filled.base-tag--$(color) {
    @apply bg-$(color);
  }

  .base-tag--outline.base-tag--$(color) {
    @apply border-$(color) text-$(color);
  }
}
</style>
