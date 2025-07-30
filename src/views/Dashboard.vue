<template>
  <div class="flex h-screen bg-gray-50">
     <Sidebar :collapsed="isCollapsed" @toggle="toggleSidebar" />

    <div class="flex-1 flex flex-col overflow-hidden">
      <header class="bg-white shadow-sm border-b border-gray-200 px-6 py-4">
        <div class="flex items-center">
          <svg class="w-6 h-6 text-blue-600 mr-3" fill="currentColor" viewBox="0 0 24 24">
            <path
              d="M3 13h1v7c0 1.103.897 2 2 2h12c1.103 0 2-.897 2-2v-7h1a1 1 0 0 0 .707-1.707l-9-9a.999.999 0 0 0-1.414 0l-9 9A1 1 0 0 0 3 13z" />
          </svg>
        </div>
      </header>

      <main class="flex-1 overflow-y-auto p-6">
        <div class="max-w-7xl mx-auto">
          <div class="mb-8">
            <h2 class="text-xl font-semibold text-gray-800 mb-6">Summaries</h2>

            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 mb-6">
              <div class="bg-white p-6 rounded-lg shadow-sm border border-gray-200 hover:shadow-md transition-shadow">
                <h3 class="text-sm font-medium text-gray-600 mb-2">Total Records</h3>
                <p class="text-2xl font-bold text-gray-900">2,847</p>
              </div>

              <div class="bg-white p-6 rounded-lg shadow-sm border border-gray-200 hover:shadow-md transition-shadow">
                <h3 class="text-sm font-medium text-gray-600 mb-2">Records Pending</h3>
                <p class="text-2xl font-bold text-orange-600">156</p>
              </div>

              <div class="bg-white p-6 rounded-lg shadow-sm border border-gray-200 hover:shadow-md transition-shadow">
                <h3 class="text-sm font-medium text-gray-600 mb-2">Processes Pending</h3>
                <p class="text-2xl font-bold text-red-600">23</p>
              </div>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
              <div class="bg-white p-6 rounded-lg shadow-sm border border-gray-200 hover:shadow-md transition-shadow">
                <h3 class="text-sm font-medium text-gray-600 mb-2">Submitted Today</h3>
                <p class="text-2xl font-bold text-green-600">47</p>
              </div>

              <div class="bg-white p-6 rounded-lg shadow-sm border border-gray-200 hover:shadow-md transition-shadow">
                <h3 class="text-sm font-medium text-gray-600 mb-2">Submitted this Month</h3>
                <p class="text-2xl font-bold text-blue-600">1,284</p>
              </div>
            </div>
          </div>

          <div>
            <h2 class="text-xl font-semibold text-gray-800 mb-6">Quick Menu</h2>

            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
              <button
                class="bg-white p-6 rounded-lg shadow-sm border border-gray-200 hover:shadow-md hover:border-blue-300 transition-all text-left group">
                <div class="flex items-center">
                  <div
                    class="w-10 h-10 bg-blue-100 rounded-lg flex items-center justify-center group-hover:bg-blue-200 transition-colors">
                    <svg class="w-5 h-5 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                        d="M12 6v6m0 0v6m0-6h6m-6 0H6" />
                    </svg>
                  </div>
                  <span class="ml-4 font-medium text-gray-900">Add a new record</span>
                </div>
              </button>

              <button
                class="bg-white p-6 rounded-lg shadow-sm border border-gray-200 hover:shadow-md hover:border-blue-300 transition-all text-left group">
                <div class="flex items-center">
                  <div
                    class="w-10 h-10 bg-green-100 rounded-lg flex items-center justify-center group-hover:bg-green-200 transition-colors">
                    <svg class="w-5 h-5 text-green-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                        d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                        d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z" />
                    </svg>
                  </div>
                  <span class="ml-4 font-medium text-gray-900">View past records</span>
                </div>
              </button>

              <button
                class="bg-white p-6 rounded-lg shadow-sm border border-gray-200 hover:shadow-md hover:border-blue-300 transition-all text-left group">
                <div class="flex items-center">
                  <div
                    class="w-10 h-10 bg-purple-100 rounded-lg flex items-center justify-center group-hover:bg-purple-200 transition-colors">
                    <svg class="w-5 h-5 text-purple-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                        d="M9 5H7a2 2 0 00-2 2v10a2 2 0 002 2h8a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2" />
                    </svg>
                  </div>
                  <span class="ml-4 font-medium text-gray-900">Process new records</span>
                </div>
              </button>
            </div>
          </div>
        </div>
      </main>
    </div>
  </div>
</template>

<script>
import Sidebar from '../components/Sidebar.vue';

export default {
  components: {
    Sidebar
  },
  data() {
    return {
      isCollapsed: false
    }
  },
  methods: {
    toggleSidebar() {
      this.isCollapsed = !this.isCollapsed;
    }
  }
}
</script>