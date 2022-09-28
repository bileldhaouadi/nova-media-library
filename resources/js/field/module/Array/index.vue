<template>
  <div>
    <draggable
      :class="'flex flex-wrap nml-display-' + type"
      v-if="array && array.length"
      item-key="id"
      v-model="array"
      @end="changeArray(array)"
    >
      <template #item="{ element }">
        <div class="w-32">
          <div class="title truncate text-center" v-text="element.title || element.name" />
          <img class="w-32 h-40" :src="element.url" />
          <button v-if="isForm" @click="remove(element.id)" type="button" class="toolbar-button hover:text-primary-500 px-2" style="position: absolute; right: 0; top: 0;">
              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor" width="24" height="24" class="inline-block" role="presentation"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"></path></svg>
          </button>
        </div>
      </template>
    </draggable>

    <div
      class="card border border-lg border-50 max-w-xs p-8 text-center cursor-pointer max-w-xs"
      v-else-if="isForm"
      @click="popup = true"
    >
      {{ __("Select Files") }}
    </div>

    <div class="mt-4" v-if="isForm && array && array.length">
      <a
        class="cursor-pointer dim inline-block text-primary font-bold"
        @click="popup = true"
      >
        {{ __("Media Library") }}
      </a>

      <a
        class="cursor-pointer dim inline-block text-danger font-bold ml-8"
        @click="changeArray([])"
      >
        {{ __("Clear") }}
      </a>
    </div>

    <transition name="fade" mode="out-in">
      <Library v-if="popup" isArray :field="field" />
    </transition>
  </div>
</template>

<script src="./script.js"></script>
