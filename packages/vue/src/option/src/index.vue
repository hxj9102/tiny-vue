<!--
 * Copyright (c) 2022 - present TinyVue Authors.
 * Copyright (c) 2022 - present Huawei Cloud Computing Technologies Co., Ltd.
 *
 * Use of this source code is governed by an MIT-style license.
 *
 * THE OPEN SOURCE SOFTWARE IN THIS PRODUCT IS DISTRIBUTED IN THE HOPE THAT IT WILL BE USEFUL,
 * BUT WITHOUT ANY WARRANTY, WITHOUT EVEN THE IMPLIED WARRANTY OF MERCHANTABILITY OR FITNESS FOR
 * A PARTICULAR PURPOSE. SEE THE APPLICABLE LICENSES FOR MORE DETAILS.
 *
 -->
<template>
  <li
    ref="option"
    @mouseenter="hoverItem"
    @click.stop="selectOptionClick"
    @mousedown.stop=""
    class="tiny-select-dropdown__item"
    v-show="visible && state.visible"
    :class="[
      {
        selected: state.itemSelected,
        'is-disabled': disabled || state.groupDisabled || state.limitReached,
        hover: state.hover
      },
      highlightClass
    ]"
  >
    <span v-if="state.select.multiple && !state.select.state.multipleLimit">
      <component :is="`icon-${state.selectCls}`" class="tiny-svg-size" />
    </span>
    <slot>
      <span>{{ state.currentLabel }}</span>
    </slot>
  </li>
</template>

<script lang="tsx">
import { renderless, api } from '@opentiny/vue-renderless/option/vue'
import { $prefix, setup, defineComponent } from '@opentiny/vue-common'
import { iconCheck, iconCheckedSur } from '@opentiny/vue-icon'

export default defineComponent({
  name: $prefix + 'Option',
  componentName: 'Option',
  components: {
    IconCheck: iconCheck(),
    IconCheckedSur: iconCheckedSur()
  },
  props: {
    value: {
      required: true
    },
    label: [String, Number],
    created: Boolean,
    disabled: {
      type: Boolean,
      default: false
    },
    events: {
      type: Object,
      default: () => ({})
    },
    visible: {
      type: Boolean,
      default: true
    },
    highlightClass: String
  },
  setup(props, context) {
    return setup({ props, context, renderless, api, mono: true })
  }
})
</script>
