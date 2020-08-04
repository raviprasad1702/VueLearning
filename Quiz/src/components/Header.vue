<template>
  <header class="text-gray-700 body-font">
    <div
      class="container mx-auto flex flex-wrap p-5 flex-col md:flex-row items-center"
    >
      <a
        class="flex title-font font-medium items-center text-gray-900 mb-4 md:mb-0"
      >
        <svg
          id="Capa_1"
          class="w-10 h-10 text-white p-1 bg-indigo-500 rounded-lg"
          fill="currentColor"
          stroke="none"
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="0"
          viewBox="0 0 512 512"
          xmlns="http://www.w3.org/2000/svg"
        >
          <g>
            <path
              d="m301 0v76h-30c-16.569 0-30 13.431-30 30s13.431 30 30 30h30v75h90v-45c0-8.276 6.724-15 15-15s15 6.724 15 15v45h91v-211z"
            />
            <path
              d="m68 316c0 16.569 13.431 30 30 30s30-13.431 30-30v-30h68v-75h-30c-8.284 0-15-6.716-15-15s6.716-15 15-15h30v-90h-196v195h68z"
            />
            <path
              d="m354 316v-30c0-16.569-13.431-30-30-30s-30 13.431-30 30v30h-68v38c33.091 0 60 26.909 60 60s-26.909 60-60 60v38h195v-196z"
            />
            <path
              d="m226 444c16.569 0 30-13.431 30-30s-13.431-30-30-30h-30v-68h-38c0 33.091-26.909 60-60 60s-60-26.909-60-60h-38v196h196v-68z"
            />
          </g>
        </svg>
        <span class="ml-3 text-xl">Fancy Quiz App</span>
      </a>
      <nav
        class="md:mr-auto md:ml-4 md:py-1 md:pl-4 md:border-l md:border-gray-400 flex flex-wrap items-center text-base justify-center"
      >
        <a class="mr-5 hover:text-gray-900"
          >Counter: {{ numCorrect }}/{{ numTotal }}</a
        >
      </nav>
    </div>
  </header>
</template>

<script>
export default {
  props: ["numCorrect", "numTotal"],
};
</script>
