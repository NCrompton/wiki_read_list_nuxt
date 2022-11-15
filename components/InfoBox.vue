<template>
  <c-box border-width="1px" rounded="lg" overflow="hidden" h="500px" width="300px" :m="5" position="relative"
    :class="selected ? 'selected' : ''" transition>
    <c-image :src="img" overflow="hidden" w="300px" h="200px" style="object-fit:cover" />
    <c-box p="4" max-width="300px" max-height="260px" overflow="hidden" position="relative">
      <c-text fontSize="4xl" color="gray.500" lineHeight="100%" pb="20px">{{ place }}</c-text>
      <c-text fontSize="sm" justify>{{ describe }}</c-text>
    </c-box>
    <c-box position="absolute" direction="row" bottom="0" m="4" alignItems="center">
      <c-badge fontSize="sm" color="gray.500">{{ kind }}</c-badge>
    </c-box>
    <c-icon-button v-if="false" aria-label="Search database" :icon="selected ? 'check' : 'close'" size="xs"
      position="absolute" top="0" m="4" opacity="0.4" @click="itemSelected" />
    <div class="check-btn" @click="itemSelected">
      <c-icon :class="selected ? 'ibtn inactive' : 'ibtn active'" name="check" ref="check_btn" />
      <c-icon :class="selected ? 'ibtn active' : 'ibtn inactive'" name="close" ref="close_btn" />
    </div>
  </c-box>
</template>
<script lang="js">
import { ref } from "vue"

export default {
  name: "Infobox",
  inject: ['$chakraColorMode', '$toggleColorMode'],
  data(props) {
    const selected = ref(false)
    const check_btn = ref(null)
    const close_btn = ref(null)
    return {
      showModal: false,
      mainStyles: {
        dark: {
          bg: 'gray.700',
          color: 'whiteAlpha.900'
        },
        light: {
          bg: 'white',
          color: 'gray.900'
        }
      },
      selected,
    }
  },
  props: {
    img: {
      type: String,
    },
    place: {
      type: String,
    },
    describe: {
      type: String,
    },
    kind: {
      type: String,
    },
    callback: {
      type: Function,
    }
  },
  methods: {
    itemSelected() {
      this.selected = !this.selected
      this.callback(this.place)
      //this.$refs.check_btn.classList.
      console.log(this.selected)
    }
  },
}
</script>
<style lang="css">
.check-btn .inactive {
  opacity: 0;
}

.check-btn .active {
  opacity: 0.4;
}

.check-btn .ibtn {
  transition: opacity 0.4s;
  position: absolute;
  background: #aaa;
  top: 0;
  margin: 20px;
  padding: 6px;
  width: 30px;
  height: 30px;
  border-radius: 20px;
}

.selected {
  box-shadow: 0px 0px 10px #5f5;
}
</style>
