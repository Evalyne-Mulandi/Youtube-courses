<template>
    <div
      class="flex justify-center flex-col gap-y-3 items-center mx-auto p-3 text-slate-900 text-3xl dark:bg-slate-800 bg-slate-400"
      v-if="!auth"
    >
      <Terms :msg="msg" />
    </div>
    <div
      class="font-sans bg-grey-lighter flex flex-col min-h-screen w-full dark:bg-slate-900 bg-slate-200"
      v-else
    >
      <div>
        <div class="dark:bg-slate-800 bg-slate-200">
          <div class="container mx-auto px-4">
            <div class="flex items-center md:justify-between py-4">
              <!-- Mobile menu -->
              <button
                type="button"
                class="inline-flex md:hidden items-center justify-center rounded-md bg-white dark:border-indigo-500 dark:bg-slate-300 p-2 text-gray-400 hover:bg-gray-100 hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-inset focus:ring-indigo-500"
                @click="toggleMode"
              >
                <span class="sr-only">Close main menu</span>
                <!-- Menu icon -->
                <svg
                  v-if="!mode"
                  xmlns="http://www.w3.org/2000/svg"
                  class="h-5 w-5 fill-black"
                  viewBox="0 0 20 20"
                  fill="currentColor"
                >
                  <path
                    fill-rule="evenodd"
                    d="M3 5a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zM3 10a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zM3 15a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1z"
                    clip-rule="evenodd"
                  />
                </svg>
  
                <svg
                  v-else
                  class="h-6 w-6"
                  xmlns="http://www.w3.org/2000/svg"
                  fill="none"
                  viewBox="0 0 24 24"
                  stroke-width="1.5"
                  stroke="currentColor"
                  aria-hidden="true"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    d="M6 18L18 6M6 6l12 12"
                  />
                </svg>
              </button>
              <!-- End of mobile close -->
              <div>
                <ToggleMode />
              </div>
  
              <div class="w-1/4 md:w-auto md:flex text-right">
                <div>
                  <img
                    class="inline-block h-8 w-8 rounded-full bg-slate-700 dark:bg-slate-800"
                    src=""
                    alt=""
                  />
                </div>
  
                <div class="hidden md:block md:flex md:items-center ml-2 dark:text-white">
                  <span class="dark:text-white text-black text-sm mr-1">{{
                    auth ? msg : "not signed in"
                  }}</span>
                  <div>
                    <svg
                      class="fill-current dark:text-white text-gray-700 h-4 w-4 block opacity-50"
                      xmlns="http://www.w3.org/2000/svg"
                      viewBox="0 0 20 20"
                    >
                      <path
                        d="M4.516 7.548c.436-.446 1.043-.481 1.576 0L10 11.295l3.908-3.747c.533-.481 1.141-.446 1.574 0 .436.445.408 1.197 0 1.615-.406.418-4.695 4.502-4.695 4.502a1.095 1.095 0 0 1-1.576 0S4.924 9.581 4.516 9.163c-.409-.418-.436-1.17 0-1.615z"
                      />
                    </svg>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <!-- MOBILE MENU -->
        <div class="block md:hidden dark:bg-slate-800 bg-slate-200 pl-32" v-show="mode">
          <div class="flex">
            <a
              href="#"
              class="no-underline dark:text-white text-black md:text-white flex items-center py-4 border-b border-blue-dark"
            >
              <svg
                class="h-6 w-6 fill-current mr-2"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
              >
                <path
                  fill-rule="evenodd"
                  d="M3.889 3h6.222a.9.9 0 0 1 .889.91v8.18a.9.9 0 0 1-.889.91H3.89A.9.9 0 0 1 3 12.09V3.91A.9.9 0 0 1 3.889 3zM3.889 15h6.222c.491 0 .889.384.889.857v4.286c0 .473-.398.857-.889.857H3.89C3.398 21 3 20.616 3 20.143v-4.286c0-.473.398-.857.889-.857zM13.889 11h6.222a.9.9 0 0 1 .889.91v8.18a.9.9 0 0 1-.889.91H13.89a.9.9 0 0 1-.889-.91v-8.18a.9.9 0 0 1 .889-.91zM13.889 3h6.222c.491 0 .889.384.889.857v4.286c0 .473-.398.857-.889.857H13.89C13.398 9 13 8.616 13 8.143V3.857c0-.473.398-.857.889-.857z"
                />
              </svg>
              Dashboard
            </a>
          </div>
          <div class="flex">
            <nuxt-link
              to="/"
              class="no-underline dark:text-white text-black md:text-white md:opacity-100 flex items-center py-4 border-b border-transparent hover:opacity-100 md:hover:border-grey-dark"
            >
              <svg
                class="h-6 w-6 fill-current mr-2"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
              >
                <path
                  d="M8 7h10V5l4 3.5-4 3.5v-2H8V7zm-6 8.5L6 12v2h10v3H6v2l-4-3.5z"
                  fill-rule="nonzero"
                />
              </svg>
              Home
            </nuxt-link>
          </div>
          <div class="flex">
            <div class="relative inline-block text-left pt-2">
              <div>
                <button
                  @click="this.closeAccount = !this.closeAccount"
                  type="button"
                  class="inline-flex w-full justify-center rounded-md border dark:border-gray-300 border-indigo-700 bg-slate-800 px-4 py-2 text-sm bg-transparent font-medium dark:text-gray-200 text-indigo-600 shadow-sm focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 focus:ring-offset-gray-100"
                  id="menu-button"
                  aria-expanded="true"
                  aria-haspopup="true"
                >
                  Accounts
                  <!-- Heroicon name: mini/chevron-down -->
                  <svg
                    class="-mr-1 ml-2 h-5 w-5"
                    xmlns="http://www.w3.org/2000/svg"
                    viewBox="0 0 20 20"
                    fill="currentColor"
                    aria-hidden="true"
                  >
                    <path
                      fill-rule="evenodd"
                      d="M5.23 7.21a.75.75 0 011.06.02L10 11.168l3.71-3.938a.75.75 0 111.08 1.04l-4.25 4.5a.75.75 0 01-1.08 0l-4.25-4.5a.75.75 0 01.02-1.06z"
                      clip-rule="evenodd"
                    />
                  </svg>
                </button>
              </div>
              <div
                v-show="closeAccount"
                class="absolute right-0 z-10 mt-2 w-56 origin-top-right rounded-md bg-white dark:bg-slate-700 shadow-lg ring-1 ring-black ring-opacity-5 focus:outline-none"
                role="menu"
                aria-orientation="vertical"
                aria-labelledby="menu-button"
                tabindex="-1"
              >
                <div
                  class="py-1 dark:bg-slate-800 bg-slate-300 border-white rounded-md"
                  role="none"
                >
                  <!-- Active: "bg-gray-100 text-gray-900", Not Active: "text-gray-700" -->
                  <nuxt-link
                    to="/AdminRegister"
                    href="#"
                    class="text-gray-700 dark:text-gray-400 block px-4 py-2 text-sm"
                    role="menuitem"
                    tabindex="-1"
                    id="menu-item-0"
                    >Add Account</nuxt-link
                  >
  
                  <form method="POST" action="#" role="none">
                    <button
                      @click="logout"
                      type="submit"
                      class="text-gray-700 dark:text-gray-400 block w-full px-4 py-2 text-left text-sm"
                      role="menuitem"
                      tabindex="-1"
                      id="menu-item-3"
                    >
                      Sign out
                    </button>
                  </form>
                </div>
              </div>
            </div>
          </div>
          <div class="flex">
            <nuxt-link
              to="/AddSong"
              class="no-underline dark:text-white text-black md:text-white md:opacity-100 flex items-center py-4 border-b border-transparent hover:opacity-100 md:hover:border-grey-dark"
            >
              <svg
                class="h-6 w-6 fill-current mr-2"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
              >
                <path
                  d="M11 12h2v2h9s-.149-4.459-.2-5.854C21.75 6.82 21.275 6 19.8 6h-3.208l-1.197-2.256C15.064 3.121 14.951 3 14.216 3H9.783c-.735 0-.847.121-1.179.744-.165.311-.7 1.318-1.196 2.256H4.199c-1.476 0-1.945.82-2 2.146C2.145 9.473 2 14 2 14h9v-2zM9.649 4.916c.23-.432.308-.516.817-.516h3.067c.509 0 .588.084.816.516L14.924 6h-5.85l.575-1.084zM13 17h-2v-2H2.5s.124 1.797.199 3.322c.031.633.218 1.678 1.8 1.678H19.5c1.582 0 1.765-1.047 1.8-1.678.087-1.568.2-3.322.2-3.322H13v2z"
                  fill-rule="nonzero"
                />
              </svg>
              Add Song
            </nuxt-link>
          </div>
          <div class="flex">
            <nuxt-link
              to="/Setting"
              class="no-underline dark:text-white text-black md:opacity-100 flex items-center py-4 border-b border-transparent hover:opacity-100 md:hover:border-grey-dark"
            >
              <svg
                class="h-6 w-6 fill-current mr-2"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 24 24"
              >
                <path
                  d="M18.783 12c0-1.049.646-1.875 1.617-2.443a8.932 8.932 0 0 0-.692-1.672c-1.089.285-1.97-.141-2.711-.883-.741-.74-.968-1.621-.683-2.711a8.732 8.732 0 0 0-1.672-.691c-.568.97-1.595 1.615-2.642 1.615-1.048 0-2.074-.645-2.643-1.615-.58.172-1.14.403-1.671.691.285 1.09.059 1.971-.684 2.711-.74.742-1.621 1.168-2.711.883A8.797 8.797 0 0 0 3.6 9.557c.97.568 1.615 1.394 1.615 2.443 0 1.047-.645 2.074-1.615 2.643.173.58.404 1.14.691 1.672 1.09-.285 1.971-.059 2.711.682.741.742.969 1.623.684 2.711.532.288 1.092.52 1.672.693.568-.973 1.595-1.617 2.643-1.617 1.047 0 2.074.645 2.643 1.617a8.963 8.963 0 0 0 1.672-.693c-.285-1.088-.059-1.969.683-2.711.741-.74 1.622-1.166 2.711-.883.287-.532.52-1.092.692-1.672-.973-.569-1.619-1.395-1.619-2.442zM12 15.652a3.653 3.653 0 1 1 0-7.306 3.653 3.653 0 0 1 0 7.306z"
                  fill-rule="nonzero"
                />
              </svg>
              Settings
            </nuxt-link>
          </div>
        </div>
        <div
          class="hidden bg-blue-dark md:block dark:bg-slate-800 bg-indigo-600 md:border-b"
        >
          <div class="container mx-auto px-4">
            <!-- MD MENU -->
            <div class="md:flex">
              <div class="flex -mb-px mr-8">
                <a
                  href="#"
                  class="no-underline dark:text-white text-gray-600 md:text-white flex items-center py-4 border-b border-blue-dark"
                >
                  <svg
                    class="h-6 w-6 fill-current mr-2"
                    xmlns="http://www.w3.org/2000/svg"
                    viewBox="0 0 24 24"
                  >
                    <path
                      fill-rule="evenodd"
                      d="M3.889 3h6.222a.9.9 0 0 1 .889.91v8.18a.9.9 0 0 1-.889.91H3.89A.9.9 0 0 1 3 12.09V3.91A.9.9 0 0 1 3.889 3zM3.889 15h6.222c.491 0 .889.384.889.857v4.286c0 .473-.398.857-.889.857H3.89C3.398 21 3 20.616 3 20.143v-4.286c0-.473.398-.857.889-.857zM13.889 11h6.222a.9.9 0 0 1 .889.91v8.18a.9.9 0 0 1-.889.91H13.89a.9.9 0 0 1-.889-.91v-8.18a.9.9 0 0 1 .889-.91zM13.889 3h6.222c.491 0 .889.384.889.857v4.286c0 .473-.398.857-.889.857H13.89C13.398 9 13 8.616 13 8.143V3.857c0-.473.398-.857.889-.857z"
                    />
                  </svg>
                  Dashboard
                </a>
              </div>
              <div class="flex -mb-px mr-8">
                <nuxt-link
                  to="/"
                  class="no-underline text-white opacity-50 md:text-white md:opacity-100 flex items-center py-4 border-b border-transparent hover:opacity-100 md:hover:border-grey-dark"
                >
                  <svg
                    class="h-6 w-6 fill-current mr-2"
                    xmlns="http://www.w3.org/2000/svg"
                    viewBox="0 0 24 24"
                  >
                    <path
                      d="M8 7h10V5l4 3.5-4 3.5v-2H8V7zm-6 8.5L6 12v2h10v3H6v2l-4-3.5z"
                      fill-rule="nonzero"
                    />
                  </svg>
                  Home
                </nuxt-link>
              </div>
              <div class="flex -mb-px mr-8">
                <div class="relative inline-block text-left pt-2">
                  <div>
                    <button
                      @click="this.closeAccount = !this.closeAccount"
                      type="button"
                      class="inline-flex w-full justify-center rounded-md border border-gray-300bg-slate-800 px-4 py-2 text-sm bg-transparent font-medium text-gray-200 shadow-sm focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 focus:ring-offset-gray-100"
                      id="menu-button"
                      aria-expanded="true"
                      aria-haspopup="true"
                    >
                      Accounts
                      <!-- Heroicon name: mini/chevron-down -->
                      <svg
                        class="-mr-1 ml-2 h-5 w-5"
                        xmlns="http://www.w3.org/2000/svg"
                        viewBox="0 0 20 20"
                        fill="currentColor"
                        aria-hidden="true"
                      >
                        <path
                          fill-rule="evenodd"
                          d="M5.23 7.21a.75.75 0 011.06.02L10 11.168l3.71-3.938a.75.75 0 111.08 1.04l-4.25 4.5a.75.75 0 01-1.08 0l-4.25-4.5a.75.75 0 01.02-1.06z"
                          clip-rule="evenodd"
                        />
                      </svg>
                    </button>
                  </div>
                  <div
                    v-show="closeAccount"
                    class="absolute right-0 z-10 mt-2 w-56 origin-top-right rounded-md bg-white dark:bg-slate-700 shadow-lg ring-1 ring-black ring-opacity-5 focus:outline-none"
                    role="menu"
                    aria-orientation="vertical"
                    aria-labelledby="menu-button"
                    tabindex="-1"
                  >
                    <div
                      class="py-1 dark:bg-slate-800 bg-slate-300 border border-white rounded-md"
                      role="none"
                    >
                      <!-- Active: "bg-gray-100 text-gray-900", Not Active: "text-gray-700" -->
                      <nuxt-link
                        to="/AdminRegister"
                        href="#"
                        class="text-gray-700 dark:text-gray-400 block px-4 py-2 text-sm"
                        role="menuitem"
                        tabindex="-1"
                        id="menu-item-0"
                        >Add Account</nuxt-link
                      >
  
                      <form method="POST" action="#" role="none">
                        <button
                          @click="logout"
                          type="submit"
                          class="text-gray-700 dark:text-gray-400 block w-full px-4 py-2 text-left text-sm"
                          role="menuitem"
                          tabindex="-1"
                          id="menu-item-3"
                        >
                          Sign out
                        </button>
                      </form>
                    </div>
                  </div>
                </div>
              </div>
              <div class="flex -mb-px mr-8">
                <nuxt-link
                  to="/AddSong"
                  class="no-underline text-white opacity-50 md:text-white md:opacity-100 flex items-center py-4 border-b border-transparent hover:opacity-100 md:hover:border-grey-dark"
                >
                  <svg
                    class="h-6 w-6 fill-current mr-2"
                    xmlns="http://www.w3.org/2000/svg"
                    viewBox="0 0 24 24"
                  >
                    <path
                      d="M11 12h2v2h9s-.149-4.459-.2-5.854C21.75 6.82 21.275 6 19.8 6h-3.208l-1.197-2.256C15.064 3.121 14.951 3 14.216 3H9.783c-.735 0-.847.121-1.179.744-.165.311-.7 1.318-1.196 2.256H4.199c-1.476 0-1.945.82-2 2.146C2.145 9.473 2 14 2 14h9v-2zM9.649 4.916c.23-.432.308-.516.817-.516h3.067c.509 0 .588.084.816.516L14.924 6h-5.85l.575-1.084zM13 17h-2v-2H2.5s.124 1.797.199 3.322c.031.633.218 1.678 1.8 1.678H19.5c1.582 0 1.765-1.047 1.8-1.678.087-1.568.2-3.322.2-3.322H13v2z"
                      fill-rule="nonzero"
                    />
                  </svg>
                  Add Song
                </nuxt-link>
              </div>
              <div class="flex -mb-px">
                <nuxt-link
                  to="/Setting"
                  class="no-underline text-white opacity-50 md:text-white md:opacity-100 flex items-center py-4 border-b border-transparent hover:opacity-100 md:hover:border-grey-dark"
                >
                  <svg
                    class="h-6 w-6 fill-current mr-2"
                    xmlns="http://www.w3.org/2000/svg"
                    viewBox="0 0 24 24"
                  >
                    <path
                      d="M18.783 12c0-1.049.646-1.875 1.617-2.443a8.932 8.932 0 0 0-.692-1.672c-1.089.285-1.97-.141-2.711-.883-.741-.74-.968-1.621-.683-2.711a8.732 8.732 0 0 0-1.672-.691c-.568.97-1.595 1.615-2.642 1.615-1.048 0-2.074-.645-2.643-1.615-.58.172-1.14.403-1.671.691.285 1.09.059 1.971-.684 2.711-.74.742-1.621 1.168-2.711.883A8.797 8.797 0 0 0 3.6 9.557c.97.568 1.615 1.394 1.615 2.443 0 1.047-.645 2.074-1.615 2.643.173.58.404 1.14.691 1.672 1.09-.285 1.971-.059 2.711.682.741.742.969 1.623.684 2.711.532.288 1.092.52 1.672.693.568-.973 1.595-1.617 2.643-1.617 1.047 0 2.074.645 2.643 1.617a8.963 8.963 0 0 0 1.672-.693c-.285-1.088-.059-1.969.683-2.711.741-.74 1.622-1.166 2.711-.883.287-.532.52-1.092.692-1.672-.973-.569-1.619-1.395-1.619-2.442zM12 15.652a3.653 3.653 0 1 1 0-7.306 3.653 3.653 0 0 1 0 7.306z"
                      fill-rule="nonzero"
                    />
                  </svg>
                  Settings
                </nuxt-link>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="flex-grow container mx-auto sm:px-4 pt-6 pb-8">
        <div
          class="dark:bg-slate-800 bg-slate-300 border-t border-b sm:border-l sm:border-r sm:rounded shadow mb-6"
        >
          <div class="border-b px-6">
            <div class="flex justify-between -mb-px">
              <div class="hidden lg:flex">
                <button
                  type="button"
                  class="appearance-none py-4 dark:text-white text-gray-700 border-b border-blue-dark mr-6"
                >
                  ....
                </button>
                <button
                  type="button"
                  class="appearance-none py-4 dark:text-white text-gray-700 border-b border-transparent hover:border-grey-dark mr-6"
                >
                  ....
                </button>
                <button
                  type="button"
                  class="appearance-none py-4 dark:text-white text-gray-700 border-b border-transparent hover:border-grey-dark"
                >
                  ....
                </button>
              </div>
            </div>
          </div>
          <div class="flex items-center px-6 lg:hidden">
            <div class="flex-grow flex-no-shrink py-6">
              <div class="dark:text-white text-gray-700 mb-2">
                <span class="text-5xl dark:text-white text-gray-700">Users</span>
                <span
                  class="text-3xl align-top dark:text-white text-gray-700 rounded-full p-1"
                ></span>
              </div>
            </div>
          </div>
          <div class="hidden lg:flex">
            <div class="w-1/3 text-center py-8">
              <div class="border-r">
                <div class="text-white mb-2">
                  <span class="text-5xl dark:text-white text-gray-700">Users</span>
                  <span class="text-xl align-top text-white rounded-full bg-blue-600 p-1"
                    >74</span
                  >
                </div>
                <div
                  class="text-sm uppercase text-grey tracking-wide dark:text-white text-gray-700"
                >
                  All User
                </div>
              </div>
            </div>
            <div class="w-1/3 text-center py-8">
              <div class="border-r">
                <div class="dark:text-white text-gray-700 mb-2">
                  <span class="text-5xl dark:text-white text-gray-700">You</span>
                  <span class="text-xl align-top text-white rounded-full bg-blue-600 p-1"
                    >-</span
                  >
                </div>
                <div
                  class="text-sm uppercase text-grey tracking-wide dark:text-white text-gray-700"
                >
                  ...
                </div>
              </div>
            </div>
            <div class="w-1/3 text-center py-8">
              <div>
                <div class="text-whiteer mb-2">
                  <span class="text-5xl dark:text-white text-gray-700">Track</span>
                  <span class="text-xl align-top text-white rounded-full bg-blue-600 p-1"
                    >-</span
                  >
                </div>
                <div
                  class="text-sm uppercase text-grey tracking-wide dark:text-white text-gray-700"
                >
                  percentage(%)
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="flex flex-wrap -mx-4">
          <div class="w-full mb-6 lg:mb-0 lg:w-1/2 px-4 flex flex-col">
            <div
              class="flex-grow flex flex-col dark:bg-slate-800 bg-slate-300 border-t border-b sm:rounded sm:border shadow overflow-hidden"
            >
              <div class="border-b">
                <div class="flex justify-between px-6 -mb-px flex-row">
                  <h3 class="dark:text-white text-gray-700 py-4 font-normal text-lg">
                    All Users
                  </h3>
                </div>
              </div>
              <div
                class="flex-grow flex px-6 py-6 dark:text-white text-gray-700 items-center border-b -mx-4"
                v-for="user in users[0]"
                :key="user._id"
              >
                <div class="w-2/5 xl:w-1/4 px-4 flex items-center">
                  <div class="bg-orange inline-flex mr-3">
                    {{ user.email }}
                  </div>
                  <span class="text-lg dark:text-white text-gray-700"></span>
                </div>
                <div class="hidden md:flex lg:hidden xl:flex w-1/4 px-4 items-center">
                  <div
                    class="bg-orange h-2 rounded-full flex-grow mr-2 dark:text-white text-gray-700"
                  ></div>
                </div>
                <div class="flex w-3/5 md:w/12">
                  <div class="w-1/2 px-4">
                    <div class="text-right dark:text-white text-gray-700"></div>
                  </div>
                  <div class="w-1/2 px-4">
                    <div class="text-right text-grey dark:text-white text-gray-700">
                      ....
                    </div>
                  </div>
                </div>
              </div>
  
              <div class="px-6 py-4">
                <div class="text-center text-grey dark:text-white text-gray-700">
                  Users emails
                </div>
              </div>
            </div>
          </div>
          <div class="w-full lg:w-1/2 px-4">
            <div
              class="dark:bg-slate-800 border-t border-b sm:rounded sm:border shadow bg-slate-300"
            >
              <div class="border-b">
                <div class="flex justify-between px-6 -mb-px">
                  <h3 class="dark:text-white text-gray-700 py-4 font-normal text-lg">
                    Recent Activity
                  </h3>
                </div>
              </div>
              <div>
                <div class="text-center px-6 py-4">
                  <div class="py-8">
                    <div class="mb-4">
                      <svg
                        class="inline-block fill-current dark:text-white text-gray-700 h-16 w-16"
                        xmlns="http://www.w3.org/2000/svg"
                        viewBox="0 0 20 20"
                      >
                        <path
                          d="M11.933 13.069s7.059-5.094 6.276-10.924a.465.465 0 0 0-.112-.268.436.436 0 0 0-.263-.115C12.137.961 7.16 8.184 7.16 8.184c-4.318-.517-4.004.344-5.974 5.076-.377.902.234 1.213.904.959l2.148-.811 2.59 2.648-.793 2.199c-.248.686.055 1.311.938.926 4.624-2.016 5.466-1.694 4.96-6.112zm1.009-5.916a1.594 1.594 0 0 1 0-2.217 1.509 1.509 0 0 1 2.166 0 1.594 1.594 0 0 1 0 2.217 1.509 1.509 0 0 1-2.166 0z"
                        />
                      </svg>
                    </div>
                    <p class="text-2xl font-medium mb-4 dark:text-white text-gray-700">
                      ALL songs you've added
                    </p>
                    <div class="" v-for="song in songs[0]" :key="song._id">
                      <p
                        class="text-grey max-w-xs mx-auto lowercase font-mono dark:text-white text-gray-700"
                      >
                        {{ song.title }}
                      </p>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <!-- <script>
  import { ref } from "vue";
  import Terms from "../components/Terms.vue";
  import ToggleMode from "../components/toggleMode.vue";
  import useToast from "../composables/useToast";
  
  export default {
    setup() {
      let auth = ref(false);
      let mode = ref(false);
      let msg = ref("");
      let closeAccount = ref(false);
      let id = ref("");
      let users = ref([]);
      let songs = ref([]);
      return { auth, msg, id, closeAccount, mode, users, songs };
    },
    async mounted() {
      try {
        /*  let url = "http://localhost:7000/Admin"; */
  
        const response = await fetch("/api/user/", {
          credentials: "include",
          headers: {
            "Content-type": "application/json",
          },
        });
        if (response.ok) {
          const content = await response.json();
          this.auth = true;
          this.msg = content.message.name;
          this.id = content.message.email;
          console.log(content);
        } else {
          const content = await response.json();
          this.msg = content.message;
          this.auth = false;
          console.log(content);
        }
      } catch (error) {
        console.log(error);
      }
      this.getAllUsers();
      this.getAllSongs();
    },
    methods: {
      async logout() {
        /* let url = "http://localhost:7000/AdminLogout"; */
        let url = "/api/user/AdminLogout";
        let res = await fetch(url, {
          method: "POST",
          credentials: "include",
          headers: {
            "Content-type": "application/json",
          },
        });
        if (res.ok) {
          let data = await res.json();
          useToast().success(data.message);
          setTimeout(async () => {
            await this.$router.push("/AdminLogin");
          }, 6000);
          location.reload();
        } else {
          let data = await res.json();
          useToast().error(data.message);
          await this.$router.push("/AdminRegister");
          location.reload();
        }
      },
      async getAllSongs() {
        let songUrl = "/api/s1/Songs";
        const res = await fetch(songUrl, {
          method: "GET",
          headers: { "Content-type": "application/json" },
        });
        if (res.ok) {
          const resp = await res.json();
          this.songs = [...this.songs, resp];
        } else {
          const resp = await res.json();
          console.log(resp);
        }
      },
      async getAllUsers() {
        let url = "/api/v1/getUsers";
        const res = await fetch(url, {
          method: "GET",
          headers: { "Content-type": "application/json" },
        });
        if (res.ok) {
          const resp = await res.json();
          this.users = [...this.users, resp];
        } else {
          const resp = await res.json();
          console.log(resp);
        }
      },
      toggleMode() {
        this.mode = !this.mode;
      },
    },
    components: { Terms, ToggleMode },
    computed: {},
  };
  </script> -->