<template>
  <aside class="bg-white shadow-lg transition-all duration-300 ease-in-out border-r border-gray-200"
    :class="collapsed ? 'w-20' : 'w-64'">
    <div class="p-4 border-b border-gray-200">
      <div class="flex items-center justify-between">
        <div v-if="!collapsed" class="flex items-center">
          <div class="w-8 h-8 bg-gradient-to-br from-teal-400 to-teal-600 rounded-lg flex items-center justify-center">
            <span class="text-white font-bold text-sm">NF</span>
          </div>
        </div>
        <button @click="$emit('toggle')" class="p-1.5 rounded-lg hover:bg-gray-100 transition-colors">
          <svg class="w-5 h-5 text-gray-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
              :d="collapsed ? 'M13 5l7 7-7 7M5 5l7 7-7 7' : 'M11 19l-7-7 7-7m8 14l-7-7 7-7'" />
          </svg>
        </button>
      </div>
    </div>

    <nav class="p-2">
      <ul class="space-y-2">
        <li v-for="item in menuItems" :key="item.name">
          <a v-if="!item.href" href="#" class="flex items-center p-3 rounded-lg text-gray-700 hover:bg-gray-100 transition-colors"
             :class="collapsed ? 'justify-center px-2' : ''"
             @click.prevent="handleMenuItemClick(item)">
            <svg class="transition-all duration-300" 
                 :class="collapsed ? 'w-6 h-6' : 'w-5 h-5'"
                 fill="currentColor" 
                 viewBox="0 0 24 24">
              <path :d="item.icon"/>
            </svg>
            <span v-if="!collapsed" class="ml-3">{{ item.name }}</span>
          </a>
          <router-link v-else :to="item.href" class="flex items-center p-3 rounded-lg transition-colors"
             :class="[
               isActive(item) ? 'bg-blue-50 text-blue-700 font-medium' : 'text-gray-700 hover:bg-gray-100',
               collapsed ? 'justify-center px-2' : ''
             ]"
             exact-active-class="bg-blue-50 text-blue-700 font-medium">
            <svg class="transition-all duration-300" 
                 :class="collapsed ? 'w-6 h-6' : 'w-5 h-5'"
                 fill="currentColor" 
                 viewBox="0 0 24 24">
              <path :d="item.icon"/>
            </svg>
            <span v-if="!collapsed" class="ml-3">{{ item.name }}</span>
          </router-link>
        </li>
      </ul>
    </nav>
  </aside>
</template>

<script>
export default {
  props: {
    collapsed: Boolean
  },
  data() {
    return {
      menuItems: [
        {
          name: 'Dashboard',
          href: '/',
          icon: 'M3 13h1v7c0 1.103.897 2 2 2h12c1.103 0 2-.897 2-2v-7h1a1 1 0 0 0 .707-1.707l-9-9a.999.999 0 0 0-1.414 0l-9 9A1 1 0 0 0 3 13z'
        },
        {
          name: 'Records',
          href: '/add-record',
          icon: 'M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zm-5 14H7v-2h7v2zm3-4H7v-2h10v2zm0-4H7V7h10v2z'
        },
        {
          name: 'My Account',
          href: null,
          icon: 'M12 12c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm0 2c-2.67 0-8 1.34-8 4v2h16v-2c0-2.66-5.33-4-8-4z'
        },
        {
          name: 'Users',
          href: null,
          icon: 'M16 11c1.66 0 2.99-1.34 2.99-3S17.66 5 16 5c-1.66 0-3 1.34-3 3s1.34 3 3 3zm-8 0c1.66 0 2.99-1.34 2.99-3S9.66 5 8 5C6.34 5 5 6.34 5 8s1.34 3 3 3zm0 2c-2.33 0-7 1.17-7 3.5V19h14v-2.5c0-2.33-4.67-3.5-7-3.5zm8 0c-.29 0-.62.02-.97.05 1.16.84 1.97 1.97 1.97 3.45V19h6v-2.5c0-2.33-4.67-3.5-7-3.5z'
        },
        {
          name: 'Security',
          href: null,
          icon: 'M18 8h-1V6c0-2.76-2.24-5-5-5S7 3.24 7 6v2H6c-1.1 0-2 .9-2 2v10c0 1.1.9 2 2 2h12c1.1 0 2-.9 2-2V10c0-1.1-.9-2-2-2zm-6 9c-1.1 0-2-.9-2-2s.9-2 2-2 2 .9 2 2-.9 2-2 2zM9 8V6c0-1.66 1.34-3 3-3s3 1.34 3 3v2H9z'
        },
        {
          name: 'Change Theme',
          href: null,
          icon: 'M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z'
        },
        {
          name: 'Info',
          href: null,
          icon: 'M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm1 15h-2v-6h2v6zm0-8h-2V7h2v2z'
        }
      ]
    }
  },
  methods: {
    isActive(item) {
      if (!item.href) return false;
      if (item.href === '/') return this.$route.path === '/';
      return this.$route.path.startsWith(item.href);
    },
    handleMenuItemClick(item) {
      this.$emit('menu-click', item.name);
    }
  }
}
</script>

<style scoped>
a {
  transition: background-color 0.2s ease, color 0.2s ease;
}

.router-link-active {
  @apply bg-blue-50 text-blue-700 font-medium;
}

a:not(.router-link-active):hover {
  @apply bg-gray-100;
}
</style>