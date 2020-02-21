<template>
  <nuxt-link :to="'detail/' + imageId" class="ui card">
    <sui-card class="card-width">
      <sui-image :src="imageUrl" />
      <sui-card-content>
        <sui-card-header class="title">{{ description }}</sui-card-header>
        <sui-card-meta>{{ createdAt }}</sui-card-meta>
        <sui-card-description>{{ altDescription }}</sui-card-description>
      </sui-card-content>
      <sui-card-content extra>
        <sui-icon name="user" />
        {{ likes }} Likes
      </sui-card-content>
    </sui-card>
  </nuxt-link>
</template>

<script>
export default {
  name: 'CardEdo',
  props: {
    imageId: {
      type: String,
      default: ''
    },
    imageUrl: {
      type: String,
      default: ''
    },
    description: {
      type: String,
      default: ''
    },
    createdAt: {
      type: String,
      default: ''
    },
    altDescription: {
      type: String,
      default: ''
    },
    likes: {
      type: Number,
      default: null
    }
  }
}
</script>

<style scoped>
.ui.card > .image,
.ui.cards > .card > .image {
  height: 300px;
  object-fit: cover;
  object-position: top;
}

.content > div {
  text-shadow: 0px 0px 20px white;
}

.title {
  white-space: nowrap;
  overflow-x: hidden;
  text-overflow: ellipsis;
}

.content {
  position: absolute;
  width: 100%;
}
.card-width {
  width: 100%;
}
</style>
