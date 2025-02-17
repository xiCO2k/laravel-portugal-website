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
      <textarea
        :id="name"
        ref="input"
        v-model="modelValue"
        :name="name"
        :autocomplete="name"
        :class="[
          hasErrors ? 'danger' : '',
          classesForButtonHasGroupAbove,
          classesForButtonHasGroupBellow
        ]"
        class="form-input"
        :rows="rows"
        v-bind="$attrs"
      />
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
    name: 'XInputTextArea',
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
        rows: {
            default: 3,
            required: false
        }
    },
};
</script>
