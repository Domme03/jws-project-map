<template>
  <router-link :to="`/project/${project.id}`">
    <b-card class="project-list-item" no-body>
      <b-card-img v-if="project.teaserImg"
        class="teaser-img"
        :src="project.teaserImg[0].thumbnails.large.url"
        :alt="project.name"
        top
      />
      <div v-else class="teaser-img-placeholder"></div>

      <h3 class="project-list-item__title">
        {{ project.name }}
      </h3>
      <b-card-body :sub-title="null">
        <category-badge
          v-for="category in project.category"
          v-bind:key="category"
          :category-id="category"
        />
        <div v-if="project.country"><country-label :country-id="project.country" /></div>
        <div>Project State: {{ project.state }}</div>
      </b-card-body>
    </b-card>
  </router-link>
</template>

<script>
import CategoryBadge from '@/components/CategoryBadge.vue'
import CountryLabel from '@/components/CountryLabel.vue'

export default {
  components: { CategoryBadge, CountryLabel },
  name: 'ProjectListItem',
  props: {
    project: {
      type: Object,
      required: false,
      default: null
    }
  }
}
</script>

<style lang="scss" scoped>
a {
  color: inherit;
  text-decoration: none;
}

.project-list-item {
  width: 320px;
  margin: 10px;

  &__title {
    padding: 1rem;
    font-size: 1.2em;
    text-decoration: none;
    color: #eee;
    background-color: rgb(61, 94, 158);
  }
}
.teaser-img {
  width: auto;
  height: 200px;
  object-fit: cover;
  object-position: 100% 0;
}
.teaser-img-placeholder {
  width: auto;
  height: 200px;
  background-color: #eee;
}

</style>