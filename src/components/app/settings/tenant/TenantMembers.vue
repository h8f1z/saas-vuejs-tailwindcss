<template>
  <div>
    <object-list
      :title="title"
      routeNew="/app/settings/organization/members/new"
      v-on:reload="reload"
    >
      <template v-slot:table>
        <div v-if="tenantJoinSettings && isOwnerOrAdmin" class="mb-4">
          <div>
            <h3 class="text-lg leading-6 font-medium text-gray-900">
              {{ $t("settings.tenant.members.invite") }}
              <input
                type="checkbox"
                v-model="enableLink"
                @change="changeLinkSettings($event)"
              />
            </h3>
            <div>
              <p class="mt-1 max-w-2xl text-sm leading-5 text-gray-500">
                {{
                  $t("settings.tenant.members.inviteDescription", [
                    $store.state.tenant.current.name,
                  ])
                }}
                <button
                  v-if="enableLink"
                  class="text-theme-500"
                  @click="updateTenantJoinSettings(true)"
                >
                  {{ $t("settings.tenant.members.inviteResetLink") }}
                </button>
              </p>
            </div>
            <p v-if="enableLink" class="flex-1 block">
              <input
                class="mr-3"
                type="checkbox"
                v-model="requireAcceptance"
                @change="changeLinkSettings($event)"
              />
              <label>{{
                $t("settings.tenant.members.requireAcceptance")
              }}</label>
            </p>
            <div class="col-span-3 sm:col-span-2 mt-4 max-w-lg">
              <div v-if="enableLink" class="mt-1 flex rounded-md shadow-sm">
                <input
                  disabled
                  :value="urlLink"
                  id="company_website"
                  class="border border-theme-100 bg-gray-100 px-2 form-input flex-1 block w-full rounded-l-md transition duration-150 ease-in-out sm:text-sm sm:leading-5"
                />
                <button
                  @click="copyInviteLink()"
                  class="-ml-px relative inline-flex items-center px-4 py-2 border border-gray-300 text-sm leading-5 font-medium rounded-r-md text-gray-700 bg-gray-50 hover:text-gray-500 hover:bg-white focus:outline-none focus:shadow-outline-blue focus:border-blue-300 active:bg-gray-100 active:text-gray-700 transition ease-in-out duration-150"
                >
                  <svg
                    class="h-5 w-5 text-theme-400"
                    viewBox="0 0 20 20"
                    fill="currentColor"
                  >
                    <path d="M8 3a1 1 0 011-1h2a1 1 0 110 2H9a1 1 0 01-1-1z" />
                    <path
                      d="M6 3a2 2 0 00-2 2v11a2 2 0 002 2h8a2 2 0 002-2V5a2 2 0 00-2-2 3 3 0 01-3 3H9a3 3 0 01-3-3z"
                    />
                  </svg>
                  <span class="ml-2">
                    {{
                      copiedUrlLink ? $t("shared.copied") : $t("shared.copy")
                    }}
                  </span>
                </button>
              </div>
            </div>
            <!-- <label>Enable public URL</label>
            <input type="checkbox" v-model="enablePublicUrl" @change="changeLinkSettings($event)" />-->
          </div>
        </div>
        <div v-if="loading">
          <table-row-skeleton></table-row-skeleton>
          <table-row-skeleton></table-row-skeleton>
          <table-row-skeleton></table-row-skeleton>
        </div>
        <div v-else>
          <div v-if="items.length === 0">
            <div
              class="max-w-md mx-auto border-2 border-gray-100 px-4 lg:px-10 flex justify-center py-4 md:py-8 lg:py-12 rounded-lg"
            >
              <div class="text-center flex flex-col justify-center">
                <!-- Empty SVG Starts -->
                <svg
                  id="f20e0c25-d928-42cc-98d1-13cc230663ea"
                  data-name="Layer 1"
                  xmlns="http://www.w3.org/2000/svg"
                  xmlns:xlink="http://www.w3.org/1999/xlink"
                  viewBox="0 0 820.16 780.81"
                >
                  <defs>
                    <linearGradient
                      id="07332201-7176-49c2-9908-6dc4a39c4716"
                      x1="539.63"
                      y1="734.6"
                      x2="539.63"
                      y2="151.19"
                      gradientTransform="translate(-3.62 1.57)"
                      gradientUnits="userSpaceOnUse"
                    >
                      <stop offset="0" stop-color="gray" stop-opacity="0.25" />
                      <stop
                        offset="0.54"
                        stop-color="gray"
                        stop-opacity="0.12"
                      />
                      <stop offset="1" stop-color="gray" stop-opacity="0.1" />
                    </linearGradient>
                    <linearGradient
                      id="0ee1ab3f-7ba2-4205-9d4a-9606ad702253"
                      x1="540.17"
                      y1="180.2"
                      x2="540.17"
                      y2="130.75"
                      gradientTransform="translate(-63.92 7.85)"
                      xlink:href="#07332201-7176-49c2-9908-6dc4a39c4716"
                    />
                    <linearGradient
                      id="abca9755-bed1-4a97-b027-7f02ee3ffa09"
                      x1="540.17"
                      y1="140.86"
                      x2="540.17"
                      y2="82.43"
                      gradientTransform="translate(-84.51 124.6) rotate(-12.11)"
                      xlink:href="#07332201-7176-49c2-9908-6dc4a39c4716"
                    />
                    <linearGradient
                      id="2632d424-e666-4ee4-9508-a494957e14ab"
                      x1="476.4"
                      y1="710.53"
                      x2="476.4"
                      y2="127.12"
                      gradientTransform="matrix(1, 0, 0, 1, 0, 0)"
                      xlink:href="#07332201-7176-49c2-9908-6dc4a39c4716"
                    />
                    <linearGradient
                      id="97571ef7-1c83-4e06-b701-c2e47e77dca3"
                      x1="476.94"
                      y1="156.13"
                      x2="476.94"
                      y2="106.68"
                      gradientTransform="matrix(1, 0, 0, 1, 0, 0)"
                      xlink:href="#07332201-7176-49c2-9908-6dc4a39c4716"
                    />
                    <linearGradient
                      id="7d32e13e-a0c7-49c4-af0e-066a2f8cb76e"
                      x1="666.86"
                      y1="176.39"
                      x2="666.86"
                      y2="117.95"
                      gradientTransform="matrix(1, 0, 0, 1, 0, 0)"
                      xlink:href="#07332201-7176-49c2-9908-6dc4a39c4716"
                    />
                  </defs>
                  <title>no data</title>
                  <rect
                    x="317.5"
                    y="142.55"
                    width="437.02"
                    height="603.82"
                    transform="translate(-271.22 62.72) rotate(-12.11)"
                    fill="#e0e0e0"
                  />
                  <g opacity="0.5">
                    <rect
                      x="324.89"
                      y="152.76"
                      width="422.25"
                      height="583.41"
                      transform="translate(-271.22 62.72) rotate(-12.11)"
                      fill="url(#07332201-7176-49c2-9908-6dc4a39c4716)"
                    />
                  </g>
                  <rect
                    x="329.81"
                    y="157.1"
                    width="411.5"
                    height="570.52"
                    transform="translate(-270.79 62.58) rotate(-12.11)"
                    fill="#fafafa"
                  />
                  <rect
                    x="374.18"
                    y="138.6"
                    width="204.14"
                    height="49.45"
                    transform="translate(-213.58 43.93) rotate(-12.11)"
                    fill="url(#0ee1ab3f-7ba2-4205-9d4a-9606ad702253)"
                  />
                  <path
                    d="M460.93,91.9c-15.41,3.31-25.16,18.78-21.77,34.55s18.62,25.89,34,22.58,25.16-18.78,21.77-34.55S476.34,88.59,460.93,91.9ZM470.6,137A16.86,16.86,0,1,1,483.16,117,16.66,16.66,0,0,1,470.6,137Z"
                    transform="translate(-189.92 -59.59)"
                    fill="url(#abca9755-bed1-4a97-b027-7f02ee3ffa09)"
                  />
                  <rect
                    x="375.66"
                    y="136.55"
                    width="199.84"
                    height="47.27"
                    transform="translate(-212.94 43.72) rotate(-12.11)"
                    fill="#3182ce"
                  />
                  <path
                    d="M460.93,91.9a27.93,27.93,0,1,0,33.17,21.45A27.93,27.93,0,0,0,460.93,91.9ZM470.17,135a16.12,16.12,0,1,1,12.38-19.14A16.12,16.12,0,0,1,470.17,135Z"
                    transform="translate(-189.92 -59.59)"
                    fill="#3182ce"
                  />
                  <rect
                    x="257.89"
                    y="116.91"
                    width="437.02"
                    height="603.82"
                    fill="#e0e0e0"
                  />
                  <g opacity="0.5">
                    <rect
                      x="265.28"
                      y="127.12"
                      width="422.25"
                      height="583.41"
                      fill="url(#2632d424-e666-4ee4-9508-a494957e14ab)"
                    />
                  </g>
                  <rect
                    x="270.65"
                    y="131.42"
                    width="411.5"
                    height="570.52"
                    fill="#fff"
                  />
                  <rect
                    x="374.87"
                    y="106.68"
                    width="204.14"
                    height="49.45"
                    fill="url(#97571ef7-1c83-4e06-b701-c2e47e77dca3)"
                  />
                  <path
                    d="M666.86,118c-15.76,0-28.54,13.08-28.54,29.22s12.78,29.22,28.54,29.22,28.54-13.08,28.54-29.22S682.62,118,666.86,118Zm0,46.08a16.86,16.86,0,1,1,16.46-16.86A16.66,16.66,0,0,1,666.86,164Z"
                    transform="translate(-189.92 -59.59)"
                    fill="url(#7d32e13e-a0c7-49c4-af0e-066a2f8cb76e)"
                  />
                  <rect
                    x="377.02"
                    y="104.56"
                    width="199.84"
                    height="47.27"
                    fill="#3182ce"
                  />
                  <path
                    d="M666.86,118a27.93,27.93,0,1,0,27.93,27.93A27.93,27.93,0,0,0,666.86,118Zm0,44.05A16.12,16.12,0,1,1,683,145.89,16.12,16.12,0,0,1,666.86,162Z"
                    transform="translate(-189.92 -59.59)"
                    fill="#3182ce"
                  />
                  <g opacity="0.5">
                    <rect
                      x="15.27"
                      y="737.05"
                      width="3.76"
                      height="21.33"
                      fill="#47e6b1"
                    />
                    <rect
                      x="205.19"
                      y="796.65"
                      width="3.76"
                      height="21.33"
                      transform="translate(824.47 540.65) rotate(90)"
                      fill="#47e6b1"
                    />
                  </g>
                  <g opacity="0.5">
                    <rect
                      x="451.49"
                      width="3.76"
                      height="21.33"
                      fill="#47e6b1"
                    />
                    <rect
                      x="641.4"
                      y="59.59"
                      width="3.76"
                      height="21.33"
                      transform="translate(523.63 -632.62) rotate(90)"
                      fill="#47e6b1"
                    />
                  </g>
                  <path
                    d="M961,832.15a4.61,4.61,0,0,1-2.57-5.57,2.22,2.22,0,0,0,.1-.51h0a2.31,2.31,0,0,0-4.15-1.53h0a2.22,2.22,0,0,0-.26.45,4.61,4.61,0,0,1-5.57,2.57,2.22,2.22,0,0,0-.51-.1h0a2.31,2.31,0,0,0-1.53,4.15h0a2.22,2.22,0,0,0,.45.26,4.61,4.61,0,0,1,2.57,5.57,2.22,2.22,0,0,0-.1.51h0a2.31,2.31,0,0,0,4.15,1.53h0a2.22,2.22,0,0,0,.26-.45,4.61,4.61,0,0,1,5.57-2.57,2.22,2.22,0,0,0,.51.1h0a2.31,2.31,0,0,0,1.53-4.15h0A2.22,2.22,0,0,0,961,832.15Z"
                    transform="translate(-189.92 -59.59)"
                    fill="#4d8af0"
                    opacity="0.5"
                  />
                  <path
                    d="M326.59,627.09a4.61,4.61,0,0,1-2.57-5.57,2.22,2.22,0,0,0,.1-.51h0a2.31,2.31,0,0,0-4.15-1.53h0a2.22,2.22,0,0,0-.26.45,4.61,4.61,0,0,1-5.57,2.57,2.22,2.22,0,0,0-.51-.1h0a2.31,2.31,0,0,0-1.53,4.15h0a2.22,2.22,0,0,0,.45.26,4.61,4.61,0,0,1,2.57,5.57,2.22,2.22,0,0,0-.1.51h0a2.31,2.31,0,0,0,4.15,1.53h0a2.22,2.22,0,0,0,.26-.45A4.61,4.61,0,0,1,325,631.4a2.22,2.22,0,0,0,.51.1h0a2.31,2.31,0,0,0,1.53-4.15h0A2.22,2.22,0,0,0,326.59,627.09Z"
                    transform="translate(-189.92 -59.59)"
                    fill="#fdd835"
                    opacity="0.5"
                  />
                  <path
                    d="M855,127.77a4.61,4.61,0,0,1-2.57-5.57,2.22,2.22,0,0,0,.1-.51h0a2.31,2.31,0,0,0-4.15-1.53h0a2.22,2.22,0,0,0-.26.45,4.61,4.61,0,0,1-5.57,2.57,2.22,2.22,0,0,0-.51-.1h0a2.31,2.31,0,0,0-1.53,4.15h0a2.22,2.22,0,0,0,.45.26,4.61,4.61,0,0,1,2.57,5.57,2.22,2.22,0,0,0-.1.51h0a2.31,2.31,0,0,0,4.15,1.53h0a2.22,2.22,0,0,0,.26-.45,4.61,4.61,0,0,1,5.57-2.57,2.22,2.22,0,0,0,.51.1h0a2.31,2.31,0,0,0,1.53-4.15h0A2.22,2.22,0,0,0,855,127.77Z"
                    transform="translate(-189.92 -59.59)"
                    fill="#fdd835"
                    opacity="0.5"
                  />
                  <circle
                    cx="812.64"
                    cy="314.47"
                    r="7.53"
                    fill="#f55f44"
                    opacity="0.5"
                  />
                  <circle
                    cx="230.73"
                    cy="746.65"
                    r="7.53"
                    fill="#f55f44"
                    opacity="0.5"
                  />
                  <circle
                    cx="735.31"
                    cy="477.23"
                    r="7.53"
                    fill="#f55f44"
                    opacity="0.5"
                  />
                  <circle
                    cx="87.14"
                    cy="96.35"
                    r="7.53"
                    fill="#4d8af0"
                    opacity="0.5"
                  />
                  <circle
                    cx="7.53"
                    cy="301.76"
                    r="7.53"
                    fill="#47e6b1"
                    opacity="0.5"
                  />
                </svg>
                <!-- Empty SVG Ends -->
                <h4 class="text-base font-medium mb-3">
                  {{ $t("models.shared.createTheFirst") }}
                  {{ $t("models.user.object") }}
                </h4>
                <router-link
                  to="/app/settings/organization/members/new"
                  class="text-center px-4 py-2 border border-transparent text-sm leading-3 font-medium rounded-md text-white bg-theme-600 hover:bg-theme-500 focus:outline-none focus:shadow-outline-blue focus:border-blue-700 active:bg-theme-700 transition duration-150 ease-in-out"
                >
                  <svg
                    aria-hidden="true"
                    focusable="false"
                    data-prefix="fas"
                    data-icon="plus"
                    role="img"
                    xmlns="http://www.w3.org/2000/svg"
                    viewBox="0 0 448 512"
                    class="md:relative mr-2 svg-inline--fa fa-plus fa-w-14 fa-sm"
                    style="bottom: 1px;"
                  >
                    <path
                      fill="currentColor"
                      d="M416 208H272V64c0-17.67-14.33-32-32-32h-32c-17.67 0-32 14.33-32 32v144H32c-17.67 0-32 14.33-32 32v32c0 17.67 14.33 32 32 32h144v144c0 17.67 14.33 32 32 32h32c17.67 0 32-14.33 32-32V304h144c17.67 0 32-14.33 32-32v-32c0-17.67-14.33-32-32-32z"
                      class
                    />
                  </svg>
                  {{ $t("models.shared.createTheFirst") }}
                  {{ $t("models.user.object") }}
                </router-link>
              </div>
            </div>
          </div>
          <div
            v-else
            class="align-middle inline-block min-w-full shadow overflow-hidden sm:rounded-sm border-b border-gray-200"
          >
            <table class="min-w-full divide-y divide-gray-300 text-xs">
              <thead>
                <tr>
                  <!-- <th
                  class="px-2 py-1 bg-gray-200 text-left text-xs leading-2 font-medium text-gray-500 uppercase tracking-wider"
                >
                  ID
                  </th>-->
                  <th
                    class="px-2 py-1 bg-gray-200 text-left text-xs leading-2 font-medium text-gray-500 uppercase tracking-wider"
                  >
                    {{ $t("shared.avatar") }}
                  </th>
                  <th
                    class="px-2 py-1 bg-gray-200 text-left text-xs leading-2 font-medium text-gray-500 uppercase tracking-wider"
                  >
                    {{ $t("settings.profile.role") }}
                  </th>
                  <th
                    class="px-2 py-1 bg-gray-200 text-left text-xs leading-2 font-medium text-gray-500 uppercase tracking-wider"
                  >
                    {{ $t("account.shared.email") }}
                  </th>
                  <th
                    class="px-2 py-1 bg-gray-200 text-left text-xs leading-2 font-medium text-gray-500 uppercase tracking-wider"
                  >
                    {{ $t("settings.profile.name") }}
                  </th>
                  <th
                    class="px-2 py-1 bg-gray-200 text-left text-xs leading-2 font-medium text-gray-500 uppercase tracking-wider"
                  >
                    {{ $t("settings.profile.phone") }}
                  </th>
                  <th
                    class="px-2 py-1 bg-gray-200 text-left text-xs leading-2 font-medium text-gray-500 uppercase tracking-wider"
                  >
                    {{ $t("shared.status") }}
                  </th>
                  <th
                    class="px-2 py-1 bg-gray-200 text-left text-xs leading-2 font-medium text-gray-500 uppercase tracking-wider"
                  >
                    {{ $t("settings.profile.joinedMethod") }}
                  </th>

                  <th class="pr-5 py-2 bg-gray-200 w-10"></th>
                </tr>
              </thead>
              <tbody class="bg-white divide-y divide-gray-200">
                <tr v-for="(item, index) in orderedItems" :key="index">
                  <td
                    class="truncate px-6 py-4 text-sm leading-3 font-medium text-gray-900"
                  >
                    <!-- <img class="w-6 h-6 rounded-full" :src="item.avatar" /> -->
                    <img
                      v-if="item.user && item.user.avatar"
                      class="h-auto xl:h-8 xl:w-8 rounded-md"
                      :src="item.user.avatar"
                      alt
                    />
                    <span
                      v-else
                      class="inline-flex items-center justify-center h-8 w-8 rounded-full bg-theme-500 shadow-xl"
                    >
                      <span
                        class="text-sm font-medium leading-none text-white"
                        >{{ avatarText(item) }}</span
                      >
                    </span>
                  </td>
                  <td
                    class="truncate px-6 py-4 text-sm leading-3 font-medium text-gray-900"
                  >
                    <span
                      class="inline-flex items-center px-3 py-1 rounded-md text-sm font-medium leading-5"
                      :class="getUserRoleClass(item)"
                      >{{ getUserRole(item) }}</span
                    >
                  </td>
                  <td
                    class="truncate px-6 py-4 text-sm leading-3 font-medium text-gray-900"
                  >
                    {{ item.email }}
                    {{ item.email === email ? `(${$t("shared.me")})` : "" }}
                  </td>
                  <td
                    class="truncate px-6 py-4 text-sm leading-3 font-medium text-gray-900"
                  >
                    {{ item.firstName }} {{ item.lastName }}
                  </td>
                  <td
                    class="truncate px-6 py-4 text-sm leading-3 font-medium text-gray-900"
                  >
                    {{ item.phone }}
                  </td>
                  <td
                    class="truncate px-6 py-4 text-sm leading-3 font-medium text-gray-900"
                  >
                    <span
                      class="inline-flex items-center px-3 py-1 rounded-md text-sm font-medium leading-5"
                      :class="getUserStatusClass(item)"
                      >{{ getUserStatus(item) }}</span
                    >
                  </td>
                  <td
                    class="truncate px-6 py-4 text-sm leading-3 font-medium text-gray-900"
                  >
                    <span
                      class="inline-flex items-center px-3 py-1 rounded-md text-sm font-medium leading-5"
                      :class="getUserJoinedClass(item)"
                      >{{ getUserJoined(item) }}</span
                    >
                  </td>
                  <!-- <td
                  class="px-6 py-4 whitespace-no-wrap text-sm leading-3 font-medium text-gray-900"
                >
                  {{ item.id }}
                  </td>-->
                  <!-- <td
                    class="truncate px-6 py-4 text-sm leading-3 font-medium text-gray-900"
                  >{{ item.description }}</td>
                  <td
                    class="px-6 py-4 whitespace-no-wrap text-sm leading-3 text-gray-500"
                  >{{ item.quantity }}</td>
                  <td class="px-6 py-4 whitespace-no-wrap text-sm leading-3 text-gray-500">
                    ${{
                    item.price.toFixed(2).replace(/\d(?=(\d{3})+\.)/g, "$&,")
                    }}
                  </td>
                  <td class="px-6 py-4 whitespace-no-wrap text-sm leading-3 text-gray-500">
                    ${{
                    item.amount.toFixed(2).replace(/\d(?=(\d{3})+\.)/g, "$&,")
                    }}
                  </td>
                  <td class="px-6 py-4 whitespace-no-wrap text-sm leading-3 text-gray-500">
                    <span
                      class="inline-flex items-center px-2 py-0.5 rounded text-xs font-medium leading-4 bg-teal-100 text-teal-800"
                    >{{ item.category }}</span>
                  </td>
                  <td class="px-6 py-4 whitespace-no-wrap text-sm leading-3 text-gray-500">
                    {{
                    moment(item.date)
                    .lang($store.state.locale.locale)
                    .format("LL")
                    }}
                  </td>-->

                  <td
                    class="pr-5 py-4 whitespace-no-wrap text-right text-sm leading-3 font-medium"
                  >
                    <div v-if="pendingAcceptance(item) && isOwnerOrAdmin">
                      <button
                        @click="acceptUser(item, true)"
                        class="bg-teal-500 p-2 text-gray-100 hover:text-teal-200 rounded-md mx-2"
                      >
                        {{ $t("shared.accept") }}
                      </button>
                      <button
                        @click="acceptUser(item, false)"
                        class="bg-red-500 p-2 text-gray-100 hover:text-red-200 rounded-md mx-2"
                      >
                        {{ $t("shared.reject") }}
                      </button>
                    </div>
                    <router-link
                      v-else
                      :to="{
                        path:
                          '/app/settings/organization/members/edit/' + item.id,
                      }"
                      class="text-theme-600 hover:text-theme-900"
                      >{{ $t("shared.edit") }}</router-link
                    >
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
        <div v-if="maxNumberOfUsersReached">
          <div class="bg-theme-50 border-l-4 border-theme-400 p-4 mt-8">
            <div class="flex">
              <div class="flex-shrink-0">
                <svg
                  class="h-5 w-5 text-theme-400"
                  viewBox="0 0 20 20"
                  fill="currentColor"
                >
                  <path
                    fill-rule="evenodd"
                    d="M8.257 3.099c.765-1.36 2.722-1.36 3.486 0l5.58 9.92c.75 1.334-.213 2.98-1.742 2.98H4.42c-1.53 0-2.493-1.646-1.743-2.98l5.58-9.92zM11 13a1 1 0 11-2 0 1 1 0 012 0zm-1-8a1 1 0 00-1 1v3a1 1 0 002 0V6a1 1 0 00-1-1z"
                    clip-rule="evenodd"
                  />
                </svg>
              </div>
              <div class="ml-3">
                <p class="text-sm leading-5 text-theme-700">
                  {{ $t("settings.tenant.members.maxNumberOfUsers") }}
                  <router-link
                    to="/app/settings/organization/subscription"
                    class="font-medium underline text-theme-700 hover:text-theme-600 transition ease-in-out duration-150"
                    >{{ $t("shared.upgrade") }}</router-link
                  >
                </p>
              </div>
            </div>
          </div>
        </div>
      </template>
    </object-list>
    <div class="bg-theme-100 mb-2 rounded-md border border-theme-300 mt-8">
      <div class="rounded-md bg-theme-50 p-4">
        <div class="flex">
          <div class="flex-shrink-0">
            <svg
              class="h-5 w-5 text-theme-400"
              viewBox="0 0 20 20"
              fill="currentColor"
            >
              <path
                fill-rule="evenodd"
                d="M8.257 3.099c.765-1.36 2.722-1.36 3.486 0l5.58 9.92c.75 1.334-.213 2.98-1.742 2.98H4.42c-1.53 0-2.493-1.646-1.743-2.98l5.58-9.92zM11 13a1 1 0 11-2 0 1 1 0 012 0zm-1-8a1 1 0 00-1 1v3a1 1 0 002 0V6a1 1 0 00-1-1z"
                clip-rule="evenodd"
              />
            </svg>
          </div>

          <div class="ml-3">
            <h3 class="text-sm leading-5 font-medium text-theme-800">
              {{ $t("netcoresaas.backendNeeded") }}
            </h3>
            <div class="mt-2 text-sm leading-5 text-theme-700">
              <p>{{ $t("netcoresaas.fakeData") }}</p>
            </div>
            <div class="text-sm leading-5 right-0 -ml-3 mt-2">
              <span class="inline-flex rounded-md ml-2">
                <a
                  href="https://netcoresaas.com/product"
                  target="_blank"
                  class="flex items-center justify-center px-4 py-2 border border-transparent text-sm bg-theme-200 leading-5 font-medium rounded-md text-theme-800 bg-white hover:text-theme-500 focus:outline-none focus:shadow-outline transition ease-in-out duration-150"
                  >{{ $t("netcoresaas.getBackend") }}</a
                >
              </span>
              <span class="inline-flex rounded-md ml-2">
                <a
                  href="https://demo.netcoresaas.com"
                  target="_blank"
                  class="flex items-center justify-center px-4 py-2 border border-transparent text-sm bg-theme-200 leading-5 font-medium rounded-md text-theme-800 bg-white hover:text-theme-500 focus:outline-none focus:shadow-outline transition ease-in-out duration-150"
                  >{{ $t("netcoresaas.demo") }}</a
                >
              </span>
            </div>
          </div>
        </div>
      </div>
    </div>
    <error-modal ref="error-modal"></error-modal>
    <confirm-modal
      ref="confirm-upgrade"
      v-on:yes="yesUpdateSubscription"
    ></confirm-modal>
  </div>
</template>

<script lang="ts">
import Component from "vue-class-component";
import BaseComponent from "../../../../components/shared/BaseComponent.vue";
import ErrorModal from "@/components/shared/modals/ErrorModal.vue";
import ConfirmModal from "@/components/shared/modals/ConfirmModal.vue";
import ObjectList from "../../../../components/shared/forms/ObjectList.vue";
import { report } from "process";
import TableRowSkeleton from "@/components/shared/skeletons/TableRowSkeleton.vue";
import { IUserDTO } from "../../../../app/models/system/account/IUserDTO";
import {
  TenantUserRole,
  ITenantUserDTO,
  TenantUserJoined,
  TenantUserStatus,
} from "../../../../app/models/system/account/ITenantDTO";
import { Prop } from "vue-property-decorator";
import { mapGetters } from "vuex";
import { StripeProduct } from "../../../../app/models/subscription/StripeProduct";

@Component({
  components: { ObjectList, TableRowSkeleton, ConfirmModal },
  computed: {
    ...mapGetters("tenant", {
      activeProduct: "activeProduct",
      memberCount: "memberCount",
      isOwnerOrAdmin: "isOwnerOrAdmin",
    }),
    ...mapGetters("account", {
      email: "email",
    }),
  },
})
export default class TenantMembersComponent extends BaseComponent {
  @Prop()
  public propTenantApiKey!: string;
  @Prop({ default: "Users" }) readonly title!: string;

  public tenantApiKey: string = "";
  public items = [] as ITenantUserDTO[];
  private tenantJoinSettings: any = {};
  private enableLink: boolean = false;
  private enablePublicUrl: boolean = false;
  private requireAcceptance: boolean = false;
  private copiedUrlLink: boolean = false;
  private activeProduct!: StripeProduct;
  private memberCount!: number;
  private isOwnerOrAdmin!: boolean;
  private role!: TenantUserRole;
  created() {
    const self = this;
    this.eventBus.$on("user-canceled", () => self.canceled());
    this.eventBus.$on("user-added", (data) => self.added(data));
    this.eventBus.$on("user-saved", (data) => self.saved(data));
    this.eventBus.$on("user-deleted", (data) => self.deleted(data));
  }

  mounted() {
    // SignalService.on("UserAdded", (user: User) => {
    //   this.items.push(user);
    // });
    this.services.tenantUsers.getInvitationSettings().then((response: any) => {
      this.tenantJoinSettings = response.data;
      this.enableLink = this.tenantJoinSettings.linkActive;
      this.enablePublicUrl = this.tenantJoinSettings.publicUrl;
      this.requireAcceptance = this.tenantJoinSettings.requireAcceptance;
    });
    this.reload();
  }
  avatarText(user) {
    if (user) {
      if (user.firstName && user.lastName) {
        if (user.firstName.length > 0 && user.lastName.length > 0) {
          return (user.firstName[0] + user.lastName[0]).toUpperCase();
        } else if (user.firstName.length > 1) {
          return user.firstName.substring(0, 2).toUpperCase();
        } else if (user.email.length > 1) {
          return user.email.substring(0, 2).toUpperCase();
        }
      } else {
        return user.email.substring(0, 2).toUpperCase();
      }
    }
  }
  async reload() {
    this.items = [];
    this.loading = true;
    this.services.tenantUsers
      .getUsers(this.tenantApiKey)
      .then((response: any) => {
        response.data.forEach((element) => {
          this.items.push(element);
        });
      })
      .catch((error) => {
        // @ts-ignore
        this.$refs["error-modal"].show(error);
      })
      .finally(() => {
        this.loading = false;
      });
  }
  canceled() {
    console.log("canceled");
  }
  added(data: ITenantUserDTO) {
    this.reload();
    // console.log("added data:" + JSON.stringify(data));
    // this.items.push(data);
    // // SignalService.invoke(
    //   "AddUser",
    //   this.$store.state.tenant.current.apiKey,
    //   data
    // );
  }
  saved(data) {
    const idx = this.items.findIndex((f) => f.id === data.id);
    // console.log("found: " + JSON.stringify(idx));
    this.items[idx] = data;
  }
  deleted(data) {
    this.items = this.items.filter((f) => f.id !== data.id);
  }
  updateTenantJoinSettings(reset = false) {
    this.services.tenantUsers
      .updateInvitationSettings({
        enableLink: this.enableLink,
        resetLink: reset,
        enablePublicUrl: this.enablePublicUrl,
        requireAcceptance: this.requireAcceptance,
      })
      .then((response: any) => {
        this.tenantJoinSettings = response.data;
        this.enableLink = this.tenantJoinSettings.linkActive;
        this.enablePublicUrl = this.tenantJoinSettings.publicUrl;
        this.requireAcceptance = this.tenantJoinSettings.requireAcceptance;
      });
  }

  changeLinkSettings(e) {
    this.updateTenantJoinSettings();
  }
  copyInviteLink() {
    if (this.maxNumberOfUsersReached) {
      // @ts-ignore
      this.$refs["confirm-upgrade"].show(
        this.$t("settings.tenant.members.maxNumberOfUsers") +
          " (" +
          this.maxNumberOfUsers +
          "). " +
          this.$t("shared.upgrade?")
      );
    } else {
      // @ts-ignore
      this.$clipboard(this.urlLink);
      this.copiedUrlLink = true;
    }
  }
  yesUpdateSubscription() {
    this.$router.push({ path: "/app/settings/organization/subscription" });
  }
  getUserRole(item: ITenantUserDTO) {
    return this.$t("settings.profile.roles." + TenantUserRole[item.role]);
  }
  getUserJoined(item: ITenantUserDTO) {
    if (item.status === TenantUserStatus.Active) {
      return this.$t(
        "settings.profile.joined." + TenantUserJoined[item.joined]
      );
    }
  }
  getUserStatus(item: ITenantUserDTO) {
    return this.$t("settings.profile.status." + TenantUserStatus[item.status]);
  }
  getUserRoleClass(item: ITenantUserDTO) {
    switch (item.role as TenantUserRole) {
      case TenantUserRole.Owner:
        return "bg-gray-800 text-gray-100";
      case TenantUserRole.Admin:
        return "bg-theme-200";
      case TenantUserRole.Member:
        return "bg-blue-200";
      case TenantUserRole.Guest:
        return "bg-gray-200";
    }
  }
  getUserJoinedClass(item: ITenantUserDTO) {
    if (item.status === TenantUserStatus.Active) {
      switch (item.joined as TenantUserJoined) {
        case TenantUserJoined.Creator:
          return "bg-gray-800 text-gray-100";
        case TenantUserJoined.JoinedByInvitation:
          return "bg-blue-200";
        case TenantUserJoined.JoinedByLink:
          return "bg-teal-200";
        case TenantUserJoined.JoinedByPublicUrl:
          return "bg-theme-200";
      }
    }
  }
  getUserStatusClass(item: ITenantUserDTO) {
    switch (item.status as TenantUserStatus) {
      case TenantUserStatus.PendingInvitation:
        return "bg-theme-200";
      case TenantUserStatus.PendingAcceptance:
        return "bg-theme-200";
      case TenantUserStatus.Active:
        return "bg-teal-200";
      case TenantUserStatus.Inactive:
        return "bg-red-200";
    }
  }
  pendingAcceptance(item: ITenantUserDTO) {
    return item.status === TenantUserStatus.PendingAcceptance;
  }
  acceptUser(item: ITenantUserDTO, accept: boolean) {
    if (this.isOwnerOrAdmin) {
      item.accepted = accept;
      this.services.tenantUsers
        .acceptUser(item)
        .then((response) => {
          this.reload();
        })
        .catch((error) => {
          // @ts-ignore
          this.$refs["error-modal"].show(error);
        });
    }
  }
  get maxNumberOfUsers(): number {
    return this.activeProduct && this.activeProduct.maxUsers
      ? this.activeProduct.maxUsers
      : 0;
  }
  get maxNumberOfUsersReached() {
    // @ts-ignore
    if (
      this.maxNumberOfUsers > 0 &&
      this.memberCount >= this.maxNumberOfUsers
    ) {
      return true;
    }
    return false;
  }

  get urlLink() {
    if (this.tenantJoinSettings) {
      return location.origin + "/invite/" + this.tenantJoinSettings.link;
    }
  }
  get orderedItems() {
    if (!this.items) {
      return [];
    }
    return this.items.sort((x, y) => {
      return x.role > y.role ? -1 : 1;
    });
  }
}
</script>
