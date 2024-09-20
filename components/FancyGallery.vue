<template>
  <div id="app" class="p-4">
    <h1 class="mb-2 md:mb-4 font-semibold text-xl">
      Facebook  Design
    </h1>
    <p class="mb-4 md:hidden">
      <a
        href="https://js-vbsiey.stackblitz.io"
        target="_blank"
        class="underline underline-offset-2"
        >View this demo in full size</a
      >
    </p>
    <div class="grid grid-cols-3 gap-4 max-w-xl mx-auto p-10">
      <!-- Image 1 -->
      <a  v-for="(item, index) in galleryItems"
        :key="index"
         data-fancybox="gallery" :href="item.href">

        <img v-if="item.type === 'image'" class="rounded" :src="item.src" />
        <video v-if="item.type === 'video'" class="rounded" controls>
            <source :src="item.src" type="video/mp4" />
            Your browser does not support the video tag.
          </video>
      </a>

      
    </div>

    <p>
      <div class="font-sans"> This text will use the Roboto font. </div>
    </p>
  </div>
</template>

<script setup>
import { Fancybox } from '@fancyapps/ui';
import '@fancyapps/ui/dist/fancybox/fancybox.css';

// Array of gallery items (images and video)
const galleryItems = ref([
  {
    type: 'image',
    href: 'https://lipsum.app/id/46/1600x1200',
    src: 'https://lipsum.app/id/46/200x150',
  },
  {
    type: 'image',
    href: 'https://lipsum.app/id/47/1600x1200',
    src: 'https://lipsum.app/id/47/200x150',
  },
  {
    type: 'image',
    href: 'https://lipsum.app/id/51/1600x1200',
    src: 'https://lipsum.app/id/51/200x150',
  },
  {
    type: 'video',
    href: 'https://www.youtube.com/watch?v=ScMzIvxBSi4',
    src: 'https://www.w3schools.com/html/mov_bbb.mp4',
  },
]);


onMounted(() => {
  Fancybox.bind('[data-fancybox="gallery"]', {
    dragToClose: false,

    Toolbar: {
      display: {
        left: ['close'],
        middle: [],
        right: [],
      },
    },

    Images: {
      zoom: false,
    },

    Thumbs: {
      type: 'classic',
    },

    Carousel: {
      transition: false,
      friction: 0,
    },

    on: {
      'Carousel.ready Carousel.change': (fancybox) => {
        fancybox.container.style.setProperty(
          '--bg-image',
          `url("${fancybox.getSlide().thumbSrc}")`
        );
      },
    },
  });
});
</script>

<style scoped>
.fancybox__backdrop::after {
  content: '';
  position: absolute;
  width: 10%;
  height: 10%;
  filter: blur(2px);
  left: 50%;
  top: 50%;
  transform: scale(11);
  opacity: 0.3;
  background-image: var(--bg-image);
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center center;
}

.fancybox__toolbar {
  padding: 16px;
}

.fancybox__toolbar,
.fancybox__nav {
  --f-button-border-radius: 50%;
  --f-button-bg: rgb(91 78 76 / 64%);
  --f-button-hover-bg: rgb(91 78 76 / 74%);
  --f-button-active-bg: rgb(91 78 76 / 84%);
}

.fancybox__nav {
  --f-button-svg-width: 22px;
  --f-button-svg-height: 22px;
}

.fancybox__thumbs.is-classic {
  --f-thumb-width: 48px;
  --f-thumb-height: 48px;
  --f-thumb-gap: 16px;

  --f-thumb-border-radius: 6px;
  --f-thumb-outline: 0;
}
</style>
