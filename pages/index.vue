<template>
  <div class="ui container">
    <sui-segment>
      <sui-form @submit.prevent="submitHandeller">
        <sui-form-field>
          <label>Type everything</label>
          <input v-model="query" placeholder="Type whatever you fuck" />
        </sui-form-field>
        <sui-button type="submit">Submit</sui-button>
      </sui-form>
    </sui-segment>
    <div>
      <sui-segment>
        <sui-checkbox v-model="visible" label="visible" />
      </sui-segment>
      <sui-sidebar-pushable>
        <sui-menu
          is="sui-sidebar"
          :visible="visible"
          animation="overlay"
          width="thin"
          icon="labeled"
          inverted
          vertical
        >
          <sui-menu-item to="/"> <sui-icon name="home" /> Home </sui-menu-item>
          <sui-menu-item to="/">
            <sui-icon name="gamepad" /> Games
          </sui-menu-item>
          <sui-menu-item to="/">
            <sui-icon name="camera" /> Channels
          </sui-menu-item>
        </sui-menu>
        <sui-sidebar-pusher :dimmed="visible">
          <sui-segment>
            <h3 is="sui-header">
              <sui-card-group :items-per-row="3">
                <card-component
                  v-for="content in ip.results"
                  :key="content.id"
                  :image-url="content.urls.regular"
                  :description="content.description"
                  :created-at="content.created_at"
                  :alt-description="content.alt_description"
                  :likes="content.likes"
                />
              </sui-card-group>
            </h3>
            <!-- <docs-wireframe name="paragraph" /> -->
          </sui-segment>
        </sui-sidebar-pusher>
      </sui-sidebar-pushable>
    </div>
    <!-- modal error start -->
    <sui-modal v-model="modalOpen">
      <sui-modal-header>ERROR CUK!</sui-modal-header>
      <sui-modal-content>
        <sui-modal-description>
          <p>
            no matching image
          </p>
        </sui-modal-description>
      </sui-modal-content>
      <sui-modal-actions>
        <sui-button positive @click.native="modalToggle">
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
      modalOpen: false
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
