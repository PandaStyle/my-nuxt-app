<template>
  <button @click="append">Append</button>
  <MasonryWall :items="items" :ssr-columns="3" :column-width="300" :gap="16" @append="append">
    <template #default="{ item }">
      <div class="Item">
        <img :src="item.image" />

        <div class="Content">
          <h5 class="text-ellipsis-1l">{{ item.title }}</h5>
          <p class="text-ellipsis-2l">{{ item.content }}</p>
        </div>
      </div>
    </template>
  </MasonryWall>
</template>
<script lang="ts">
import MasonryWall from '@yeger/vue-masonry-wall'

export default {
  name: 'app',
  components: { MasonryWall },
  data() {
    return {
      items: [
        {
          title: 'Sed non ante non cras amet',
          content:
            'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Maecenas non sagittis leo. Vestibulum sit amet metus nec neque dignissim dapibus.',
          image: 'https://picsum.photos/id/1015/600/600',
        },
        {
          title: 'Curabitur sit amet nunc',
          content:
            'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec id mollis erat. Aliquam erat volutpat. Nunc erat lacus, rhoncus nec.',
          image: 'https://picsum.photos/id/1019/600/700',
        },
        {
          title: 'Proin pharetra, ante metus',
          content:
            'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Morbi ac diam ac ex efficitur posuere. Pellentesque cursus pellentesque risus, non.',
          image: 'https://picsum.photos/id/1039/600/800',
        },
      ],
    }
  },
  methods: {
    /**
     * I am mocking a API call that load 20 objects at a time.
     */
    append() {
      for (let i = 0; i < 5; i++) {
        const id = Math.floor(Math.random() * 1000)
        const height = Math.floor(Math.random() * 200) + 600
        const toAppend = {
          title: `Appended ${i}`,
          content:
            'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Maecenas non sagittis leo. Vestibulum sit amet metus nec neque dignissim dapibus.',
          image: `https://picsum.photos/id/${id}/600/${height}`,
        }
        this.items = [...this.items, toAppend]
      } 
    },
  },
}
</script>

<style scoped>
.Item {
  overflow: hidden;
  border-radius: 4px;
  width: 100%;

  background: #f5f5f5;
}

.Content {
  padding: 20px;
}

img {
  object-fit: cover;
  width: 100%;
  height: 100%;
  line-height: 0;
  display: block;
}
</style>
