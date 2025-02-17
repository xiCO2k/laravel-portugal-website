<template>
  <div>
    <div class="space-y-1">
      <h3
        id="main-navigation"
        class="px-2 mb-2 text-xxs leading-4 font-semibold uppercase tracking-wider text-gray-500"
      >
        Navigation
      </h3>

      <!-- Dashboard -->
      <app-menu-link
        :active="isActive('dashboard')"
        :href="route('dashboard')"
      >
        <home-icon class="h-4 w-4 text-gray-400 mr-1" />
        <span>{{ $t('app.menu.dashboard') }}</span>
      </app-menu-link>

      <app-menu-link
        :active="isActiveIfStartsWith('links.')"
        :href="route('links.index')"
      >
        <link-icon class="h-4 w-4 text-gray-400 mr-1" />
        <span>{{ $t('app.menu.links') }}</span>
      </app-menu-link>

      <!-- Admin Menu -->
      <app-menu-collapse
        v-if="$hasRole('admin') || $hasRole('moderator')"
        :active="isActiveIfStartsWith('admin.')"
      >
        <template #trigger>
          <finger-print-icon class="h-4 w-4 text-gray-400 mr-1" />
          <span>{{ $t('app.menu.admin') }}</span>
        </template>

        <app-menu-link-sub
          :active="isActiveIfStartsWith('admin.links.')"
          :href="route('admin.links.index')"
        >
          <link-icon class="h-4 w-4 text-gray-400 mr-1" />
          <span>{{ $t('app.menu.admin-links') }}</span>
        </app-menu-link-sub>

        <app-menu-link-sub
          :active="isActiveIfStartsWith('admin.tags.')"
          :href="route('admin.tags.index')"
        >
          <tag-icon class="h-4 w-4 text-gray-400 mr-1" />
          <span>{{ $t('app.menu.admin-tags') }}</span>
        </app-menu-link-sub>
      </app-menu-collapse>

      <div class="mt-8">
        <h3 class="px-2 mb-2 mt-4 text-xxs leading-4 font-semibold text-gray-500 uppercase tracking-wider">
          {{ $t('app.menu.useful-links') }}
        </h3>

        <div
          aria-labelledby="help-center"
          class="space-y-1 dark:text-gray-400"
          role="group"
        >
          <a
            class="group btn-menu px-2 py-2"
            href="https://laravel.com/docs/8.x/installation"
            target="_blank"
          >
            <external-link-icon class="h-4 w-4 text-gray-400 mr-1" />
            <span class="truncate">
              {{ $t('app.menu.laravel-docs') }}
            </span>
          </a>
          <a
            class="group btn-menu px-2 py-2"
            href="https://laravel-news.com/"
            target="_blank"
          >
            <external-link-icon class="h-4 w-4 text-gray-400 mr-1" />
            <span class="truncate">
              {{ $t('app.menu.laravel-news') }}
            </span>
          </a>
          <a
            class="group btn-menu px-2 py-2"
            :href="$page.props.meta.social.discord"
            target="_blank"
          >
            <external-link-icon class="h-4 w-4 text-gray-400 mr-1" />
            <span class="truncate">
              {{ $t('app.menu.laravel-pt-discord') }}
            </span>
          </a>
        </div>
      </div>

      <!-- Dashboard -->
      <app-menu-link
        class="mt-2"
        :active="false"
        :href="route('landing')"
      >
        <arrow-left-icon class="h-4 w-4 text-gray-400 mr-1" />
        <span>{{ $t('app.menu.back-to-landing') }}</span>
      </app-menu-link>
    </div>
  </div>
</template>

<script>
import AppMenuLink from "@/Layouts/Backend/Partials/AppMenuLink";
import AppMenuCollapse from "@/Layouts/Backend/Partials/AppMenuCollapse";
import AppMenuLinkSub from "@/Layouts/Backend/Partials/AppMenuLinkSub";
import {
    FingerPrintIcon,
    LinkIcon,
    HomeIcon,
    ExternalLinkIcon,
    TagIcon,
    ArrowLeftIcon,
} from "@heroicons/vue/outline";

export default {
    components: {
        AppMenuLinkSub,
        AppMenuCollapse,
        AppMenuLink,
        FingerPrintIcon,
        LinkIcon,
        HomeIcon,
        ExternalLinkIcon,
        TagIcon,
        ArrowLeftIcon
    },
    methods: {
        isActive(...routes) {
            return routes.some(route => this.route().current(route));
        },
        isActiveIfStartsWith(keyword){
            return this.route().current().startsWith(keyword);
        }
    }
}
</script>
