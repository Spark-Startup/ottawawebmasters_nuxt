<template>
  <component
    :is="tag"
    :class="buttonClasses"
    :disabled="disabled || loading"
    :type="type"
    v-bind="$attrs"
    @click="handleClick"
  >
    <span v-if="loading" class="mr-2">
      <Icon name="heroicons:arrow-path-20-solid" class="w-4 h-4 animate-spin" />
    </span>
    <Icon v-if="iconLeft && !loading" :name="iconLeft" :class="iconClasses" />
    <span v-if="$slots.default" :class="{ 'sr-only': iconOnly }">
      <slot />
    </span>
    <Icon v-if="iconRight && !loading" :name="iconRight" :class="iconClasses" />
  </component>
</template>

<script setup lang="ts">
interface ButtonProps {
  variant?: 'primary' | 'secondary' | 'outline' | 'text' | 'danger'
  size?: 'sm' | 'md' | 'lg'
  tag?: string
  type?: 'button' | 'submit' | 'reset'
  disabled?: boolean
  loading?: boolean
  iconLeft?: string
  iconRight?: string
  iconOnly?: boolean
  block?: boolean
}

interface ButtonEmits {
  click: [event: MouseEvent]
}

const props = withDefaults(defineProps<ButtonProps>(), {
  variant: 'primary',
  size: 'md',
  tag: 'button',
  type: 'button',
  disabled: false,
  loading: false,
  iconOnly: false,
  block: false
})

const emit = defineEmits<ButtonEmits>()

const handleClick = (event: MouseEvent) => {
  if (!props.disabled && !props.loading) {
    emit('click', event)
  }
}

const buttonClasses = computed(() => {
  const baseClasses = [
    'inline-flex items-center justify-center font-medium transition-all duration-200',
    'focus:outline-none focus:ring-2 focus:ring-offset-2',
    'disabled:opacity-50 disabled:cursor-not-allowed',
    'relative overflow-hidden'
  ]

  // Size classes
  const sizeClasses = {
    sm: props.iconOnly ? 'p-2' : 'px-3 py-2 text-sm',
    md: props.iconOnly ? 'p-2.5' : 'px-4 py-2.5 text-base',
    lg: props.iconOnly ? 'p-3' : 'px-6 py-3 text-lg'
  }

  // Variant classes based on the design system
  const variantClasses = {
    primary: [
      'bg-[#4292AC] text-[#F7F3E8] border border-[#4292AC]',
      'hover:bg-[#357D96] hover:border-[#357D96]',
      'focus:ring-[#4292AC]/20',
      'active:bg-[#2A6B84] active:scale-95'
    ],
    secondary: [
      'bg-[#2E5944] text-[#F7F3E8] border border-[#2E5944]',
      'hover:bg-[#1B3D2F] hover:border-[#1B3D2F]',
      'focus:ring-[#2E5944]/20',
      'active:bg-[#122921] active:scale-95'
    ],
    outline: [
      'bg-transparent text-[#2E5944] border border-[#2E5944]',
      'hover:bg-[#2E5944] hover:text-[#F7F3E8]',
      'focus:ring-[#2E5944]/20',
      'active:scale-95'
    ],
    text: [
      'bg-transparent text-[#4292AC] border border-transparent',
      'hover:bg-[#D5E6EC] hover:text-[#357D96]',
      'focus:ring-[#4292AC]/20',
      'active:scale-95'
    ],
    danger: [
      'bg-red-600 text-white border border-red-600',
      'hover:bg-red-700 hover:border-red-700',
      'focus:ring-red-500/20',
      'active:bg-red-800 active:scale-95'
    ]
  }

  // Border radius
  const radiusClasses = props.iconOnly ? 'rounded-full' : 'rounded-lg'

  // Block width
  const widthClasses = props.block ? 'w-full' : ''

  return [
    ...baseClasses,
    sizeClasses[props.size],
    ...variantClasses[props.variant],
    radiusClasses,
    widthClasses
  ].filter(Boolean).join(' ')
})

const iconClasses = computed(() => {
  const sizeMap = {
    sm: 'w-4 h-4',
    md: 'w-5 h-5',
    lg: 'w-6 h-6'
  }

  const spacingMap = {
    left: props.iconOnly ? '' : 'mr-2',
    right: props.iconOnly ? '' : 'ml-2'
  }

  return [
    sizeMap[props.size],
    props.iconLeft ? spacingMap.left : '',
    props.iconRight ? spacingMap.right : ''
  ].filter(Boolean).join(' ')
})
</script>