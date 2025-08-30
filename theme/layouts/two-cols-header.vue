<template>
  <div class="slidev-layout two-cols-header w-full h-full">
    <div class="grid grid-cols-1 grid-rows-[min-content_1fr] h-full gap-4">
      <div class="header-section">
        <slot />
      </div>
      <div class="grid grid-cols-2 gap-x-12 flex-1">
        <div class="col-left">
          <slot name="left" />
        </div>
        <div class="col-right">
          <slot name="right" />
        </div>
      </div>
    </div>
  </div>
</template>
