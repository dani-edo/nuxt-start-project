<template>
  <div>
    <sui-icon
      v-show="showIcon"
      name="icon"
      size="massive"
      class="camera retro icon icon-center"
    />
    <div class="ui container">
      <sui-segment class="serch-container">
        <sui-form @submit.prevent="submitHandeller">
          <sui-input
            v-model="query"
            placeholder="Search everithing..."
            icon="search"
          />
        </sui-form>
      </sui-segment>
      <div>
        <h3 is="sui-header">
          <sui-card-group :items-per-row="3">
            <card-component
              v-for="content in ip.results"
              :key="content.id"
              :image-id="content.id"
              :image-url="content.urls.regular"
              :description="content.description"
              :created-at="content.created_at"
              :alt-description="content.alt_description"
              :likes="content.likes"
            />
          </sui-card-group>
        </h3>
        <!-- <docs-wireframe name="paragraph" /> -->
      </div>
    </div>
    <!-- modal error start -->
    <sui-modal v-model="modalOpen">
      <sui-modal-header>No matching image!</sui-modal-header>
      <sui-modal-actions>
        <sui-button negative @click.native="modalToggle">
          OK
        </sui-button>
      </sui-modal-actions>
    </sui-modal>
    <!-- modal error end -->
  </div>
</template>

<script>
import CardComponent from '~/components/card'

export default {
  name: 'IndexDaniEdot',
  components: {
    CardComponent
  },
  data() {
    return {
      visible: false,
      query: '',
      ip: {
        results: []
      },
      modalOpen: false,
      showIcon: true
    }
  },
  methods: {
    submitHandeller() {
      this.$axios
        .$get('/search/photos', {
          params: {
            query: this.query
          }
        })
        .then((response) => {
          if (response.results.length === 0) {
            this.modalOpen = true
          } else {
            this.ip = response
            this.showIcon = false
          }
        })
        .catch(() => {
          this.modalOpen = true
        })
    },
    modalToggle() {
      this.modalOpen = !this.modalOpen
    }
  }
}
</script>

<style scoped lang="sass">
.serch-container
  position: fixed
  left: 15px
  bottom: 15px
  z-index: 1
.ui.header
  margin-top: 30px
.icon-center
  position: absolute
  top: 50%
  left: 50%
  transform: translate(-50%, -50%)
.modal
  .header
    text-align: center
    padding: .75rem 1rem!important
  button
    margin-left: auto!important;
    margin-right: auto!important;
    display: block;
@media (max-width: 768px)
  .ui.three.cards > .card
    width: 100% !important;
  .serch-container
    left: 0;
    bottom: 0;
</style>
