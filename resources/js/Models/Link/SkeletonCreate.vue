<template>
  <inertia-link
    :href="route('links.create')"
    class="flex flex-col rounded-lg shadow-lg overflow-hidden border-2 border-gray-300 border-dashed hover:border-gray-400 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-primary-500"
  >
    <div class="flex-1 bg-transparent p-6 flex flex-col justify-between mx-auto">
      <div class="mx-auto my-auto text-center items-center justify-center">
        <link-icon class="mx-auto h-12 w-12 text-gray-400" />
        <h2 class="mt-2 text-lg font-medium text-gray-900">
          {{ $t('app.links-create-skeleton-title') }}
        </h2>
        <p class="mt-1 text-sm text-gray-500">
          {{ $t('app.links-create-skeleton-text') }}
        </p>
      </div>
    </div>
  </inertia-link>
</template>
<script>
import {LinkIcon} from '@heroicons/vue/outline';
export default {
    components: {
        LinkIcon
    },
};
</script>
