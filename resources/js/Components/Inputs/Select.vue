<template>
  <x-input-layout :layout="layout">
    <template #label>
      <slot
        v-if="$slots.label || label"
        name="label"
      >
        <x-form-label
          :label-for="name"
          :value="label"
          @click="onClickLabel"
        />
      </slot>
    </template>

    <div class="relative flex">
      <slot name="before" />
      <select
        :id="name"
        ref="input"
        v-model="modelValue"
        class="form-input"
        :class="[
          hasErrors ? 'danger' : '',
          classesForButtonHasGroupAbove,
          classesForButtonHasGroupBellow
        ]"
        v-bind="$attrs"
      >
        <option
          v-if="empty && showEmpty"
          :value="empty.value"
          v-html="empty.title"
        />
        <option
          v-for="(item, index) in options"
          :key="index"
          :value="item?.value || index"
        >
          {{ item?.text || item?.label || item }}
        </option>
      </select>
      <slot name="after" />
      <div
        v-if="hasErrors && showLeadingErrorIcon"
        class="absolute inset-y-0 right-0 pr-3 flex items-center pointer-events-none"
      >
        <ExclamationCircleIcon class="w-5 h-5 text-red-500" />
      </div>
    </div>
    <x-form-errors
      v-if="hasErrors && showErrors"
      :error="errors"
    />
    <x-form-helper
      v-if="help"
      :text="help"
    />
  </x-input-layout>
</template>
<script>
import {ExclamationCircleIcon} from "@heroicons/vue/solid";
import UseFormInputs from "@/Utils/Mixins/FormInput";
import XInputLayout from "@/Components/Inputs/Layout";
import XFormErrors from "@/Components/Forms/Errors";
import XFormHelper from "@/Components/Forms/Helper";
import XFormLabel from "@/Components/Forms/FormLabel";

export default {
    name: 'XSelect',
    components: {
        XFormLabel,
        XFormHelper,
        XFormErrors,
        XInputLayout,
        ExclamationCircleIcon,
    },
    mixins: [UseFormInputs],
    inheritAttrs: false,
    props: {
        modelValue: {
            default: '',
            required: false,
        },
        options: {
            type: [Array,Object],
            default: () => [],
        },
        showEmpty: {
            type: Boolean,
            default: false,
        },
        empty: {
            type: Object,
            default: () => {
                return {
                    value: null,
                    title: "&mdash;",
                };
            },
        },
    },
};
</script>
