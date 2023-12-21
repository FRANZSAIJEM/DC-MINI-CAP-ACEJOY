<script setup>
import { ref } from 'vue';
import ApplicationLogo from '@/Components/ApplicationLogo.vue';
import Dropdown from '@/Components/Dropdown.vue';
import DropdownLink from '@/Components/DropdownLink.vue';
import NavLink from '@/Components/NavLink.vue';
import ResponsiveNavLink from '@/Components/ResponsiveNavLink.vue';
import { Link } from '@inertiajs/vue3';

import { onMounted, provide } from 'vue';
const selectedColor = ref('green'); // Default background color
provide('color', selectedColor)

const showingNavigationDropdown = ref(false);
const sidebarWidth = ref(200); // Initial width of the sidebar
const minSidebarWidth = 64; // Minimum width of the sidebar
const maxSidebarWidth = 200; // Maximum width of the sidebar
const smallSizeThreshold = 100; // Adjust this threshold as needed

const toggleSidebarWidth = () => {
  sidebarWidth.value = sidebarWidth.value === minSidebarWidth ? maxSidebarWidth : minSidebarWidth;
};
</script>



<template>
  <div class="min-h-screen flex bg-gray-100 dark:bg-gray-900">
    <!-- Sidebar -->
    <aside :style="{ width: `${sidebarWidth}px`, transition: 'width 0.5s' }" class="bg-white dark:bg-blue-800 border-r border-blue-100 dark:border-blue-700">
      <!-- Resizable Button -->
      <div class="cursor-pointer" @click="toggleSidebarWidth">
        <div class="flex justify-end">
          <button v-if="sidebarWidth <= smallSizeThreshold" style="font-size: 30px;">
            <i class="fa-solid fa-caret-right text-white hover:text-black p-7 duration-100"></i>
          </button>

          <button v-else style="font-size: 30px;">
            <i class="fa-solid fa-caret-left text-white hover:text-black p-5 duration-100"></i>
          </button>
        </div>
      </div>

      <!-- Logo -->
      <div class="mt-5" style="display: grid; place-content: center;">
        <img width="150px" class="rounded-full" src="https://i.pinimg.com/736x/a3/a3/02/a3a302a2a45417308911b70b71eb4f89.jpg" alt="">
      </div>

      <!-- Links -->
      <div class="mt-10" style="display: grid; place-content: center;">
        <!-- Check if sidebarWidth is less than or equal to a threshold for small size -->
        <NavLink v-if="sidebarWidth <= smallSizeThreshold" style="font-size: 25px;" :href="route('dashboard')">
          <i class="fa fa-dashboard"></i>
        </NavLink>

        <!-- Otherwise, show only the icon -->
        <NavLink v-else style="font-size: 20px;" :href="route('dashboard')">
          <div style="width: 150px;"><i class="fa fa-dashboard"></i><span style="margin-left: 10px;">Home</span></div>
        </NavLink>

      </div>





         <!-- Links -->
      <div class="mt-10" style="display: grid; place-content: center;">
        <!-- Check if sidebarWidth is less than or equal to a threshold for small size -->
        <NavLink v-if="sidebarWidth <= smallSizeThreshold" style="font-size: 25px;" :href="route('index')">
          <i class="fa-solid fa-fish"></i>
        </NavLink>

        <!-- Otherwise, show only the icon -->
        <NavLink v-else style="font-size: 20px;" :href="route('index')">
          <div style="width: 150px;"><i class="fa-solid fa-fish"></i><span style="margin-left: 7px;">Fish</span></div>
        </NavLink>

      </div>







       <!-- Links -->
       <div class="mt-10 mb-10" style="display: grid; place-content: center;">
        <!-- Check if sidebarWidth is less than or equal to a threshold for small size -->
        <NavLink v-if="sidebarWidth <= smallSizeThreshold" style="font-size: 25px;" :href="route('dateIndex')">
            <i class="fa-solid fa-calendar"></i>
        </NavLink>

        <!-- Otherwise, show only the icon -->
        <NavLink v-else style="font-size: 20px;" :href="route('dateIndex')">
          <div style="width: 150px;"><i class="fa-solid fa-calendar"></i><span style="margin-left: 7px;">Calendar</span></div>
        </NavLink>

      </div> <hr> <br>

      <label v-if="sidebarWidth <= smallSizeThreshold" for="colorSelect" class="block text-gray-100 ms-5" style="font-size: 30px;"><i class="fa-solid fa-droplet"></i></label>
      <label v-else for="colorSelect" class="block text-gray-100 text-center"><i class="fa-solid fa-droplet"></i> Select a color:</label>

        <select id="colorSelect" v-model="selectedColor" class="w-full p-2 border rounded-md">
            <option value="red" class="py-2">High</option>
            <option value="blue" class="py-2">Mid</option>
            <option value="green" class="py-2">Low</option>
        </select>


    </aside>



    <!-- Main Content -->
    <div class="flex-1 flex flex-col overflow-hidden">
      <nav class="bg-white dark:bg-blue-800 border-b border-blue-100 dark:border-blue-700">
        <!-- Primary Navigation Menu -->
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div class="flex justify-between h-16">
            <div class="flex">
              <!-- Logo -->
              <!-- <div class="shrink-0 flex items-center">
                <Link :href="route('dashboard')">
                  <ApplicationLogo
                    class="block h-9 w-auto fill-current text-gray-800 dark:text-gray-200"
                  />
                </Link>
              </div> -->

              <!-- Navigation Links -->
              <div class="text-white mt-2">
                <!-- <NavLink :href="route('dashboard')" :active="route().current('dashboard')">
                  Dashboard
                </NavLink> -->
                <h1 style="margin-left: -225px; font-size: 30px;"><i class="fa-solid fa-fish"></i> Fish Store</h1>
              </div>
            </div>

            <div class="hidden sm:flex sm:items-center sm:ms-6">
              <!-- Settings Dropdown -->
              <div class="ms-3 relative">
                <Dropdown align="right" width="48">
                  <template #trigger>
                    <span class="inline-flex rounded-md">
                      <button
                        type="button"
                        class="inline-flex items-center px-3 py-2 border border-transparent text-sm leading-4 font-medium rounded-md text-gray-500 dark:text-gray-400 bg-white dark:bg-gray-800 hover:text-gray-700 dark:hover:text-gray-300 focus:outline-none transition ease-in-out duration-150"
                      >
                        {{ $page.props.auth.user.name }}
                        <svg
                          class="ms-2 -me-0.5 h-4 w-4"
                          xmlns="http://www.w3.org/2000/svg"
                          viewBox="0 0 20 20"
                          fill="currentColor"
                        >
                          <path
                            fill-rule="evenodd"
                            d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z"
                            clip-rule="evenodd"
                          />
                        </svg>
                      </button>
                    </span>
                  </template>

                  <template #content>
                    <DropdownLink :href="route('profile.edit')"> Profile </DropdownLink>
                    <DropdownLink :href="route('logout')" method="post" as="button">
                      Log Out
                    </DropdownLink>
                  </template>
                </Dropdown>
              </div>
            </div>

            <!-- Hamburger -->
            <div class="-me-2 flex items-center sm:hidden">
              <button
                @click="showingNavigationDropdown = !showingNavigationDropdown"
                class="inline-flex items-center justify-center p-2 rounded-md text-gray-400 dark:text-gray-500 hover:text-gray-500 dark:hover:text-gray-400 hover:bg-gray-100 dark:hover:bg-gray-900 focus:outline-none focus:bg-gray-100 dark:focus:bg-gray-900 focus:text-gray-500 dark:focus:text-gray-400 transition duration-150 ease-in-out"
              >
                <svg class="h-6 w-6" stroke="currentColor" fill="none" viewBox="0 0 24 24">
                  <path
                    :class="{
                      hidden: showingNavigationDropdown,
                      'inline-flex': !showingNavigationDropdown,
                    }"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M4 6h16M4 12h16M4 18h16"
                  />
                  <path
                    :class="{
                      hidden: !showingNavigationDropdown,
                      'inline-flex': showingNavigationDropdown,
                    }"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M6 18L18 6M6 6l12 12"
                  />
                </svg>
              </button>
            </div>
          </div>
        </div>

        <!-- Responsive Navigation Menu -->
        <div
          :class="{ block: showingNavigationDropdown, hidden: !showingNavigationDropdown }"
          class="sm:hidden"
        >
          <div class="pt-2 pb-3 space-y-1">
            <ResponsiveNavLink :href="route('dashboard')" :active="route().current('dashboard')">
              Dashboard
            </ResponsiveNavLink>
          </div>

          <!-- Responsive Settings Options -->
          <div class="pt-4 pb-1 border-t border-gray-200 dark:border-gray-600">
            <div class="px-4">
              <div class="font-medium text-base text-gray-800 dark:text-gray-200">
                {{ $page.props.auth.user.name }}
              </div>
              <div class="font-medium text-sm text-gray-500">{{ $page.props.auth.user.email }}</div>
            </div>

            <div class="mt-3 space-y-1">
              <ResponsiveNavLink :href="route('profile.edit')"> Profile </ResponsiveNavLink>
              <ResponsiveNavLink :href="route('logout')" method="post" as="button">
                Log Out
              </ResponsiveNavLink>
            </div>
          </div>
        </div>
      </nav>

      <!-- Page Heading -->
      <header class="bg-white dark:bg-gray-800 shadow" v-if="$slots.header">
        <div class="max-w-7xl mx-auto py-6 px-4 sm:px-6 lg:px-8">
          <slot name="header" />
        </div>
      </header>

      <!-- Page Content -->
      <main class="flex-1 overflow-x-hidden overflow-y-auto bg-gray-100 dark:bg-gray-900">
        <div class="max-w-7xl mx-auto py-6 px-4 sm:px-6 lg:px-8">
          <slot />
        </div>
      </main>
    </div>
  </div>
</template>
