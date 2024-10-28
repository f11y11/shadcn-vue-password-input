<script setup lang="ts">
import { EyeIcon, EyeOffIcon } from 'lucide-vue-next'
const reveal = ref(false)
const value = defineModel({default: ''})
defineEmits<{
  reveal: [],
  hide: [],
}>()

const isFocused = ref(false)
</script>

<template>
  <div
    class="flex rounded-md"
    :class="{ 'ring-2 ring-ring ring-offset-2 ring-offset-background ring-primary': isFocused }"
  >
    <Input
      v-model="value"
      :type="reveal ? 'text' : 'password'"
      class="border-e-0 rounded-e-none focus-visible:ring-0 focus-visible:outline-8"
      tabindex="0"
      @focus="isFocused = true"
      @blur="isFocused = false"
    />
    <Button
      variant="outline"
      size="icon"
      class="text-muted-foreground border-s-0 rounded-s-none"
      aria-label="Toggle password visibility"
      :aria-pressed="reveal"
      aria-description="Reveal password"
      @click="reveal = !reveal; $emit(reveal ? 'reveal' : 'hide');"
      tabindex="-1"
    >
      <component
        :is="reveal ? EyeOffIcon : EyeIcon"
        class="size-4"
      />
    </Button>
  </div>
</template>
