<template>
  <sui-modal :open="open">
    <sui-modal-header>ERROR CUK!</sui-modal-header>
    <sui-modal-content>
      <sui-modal-description>
        <p>
          We've found the following gravatar image associated with your e-mail
          address.
        </p>
      </sui-modal-description>
    </sui-modal-content>
    <sui-modal-actions>
      <sui-button positive @click.native="modalToggle">
        OK
      </sui-button>
    </sui-modal-actions>
  </sui-modal>
</template>

<script>
export default {
  name: 'ModalError',
  props: {
    modalOpen: {
      type: Boolean,
      default: true
    }
  },
  computed: {
    open() {
      return this.modalOpen
    }
  },
  methods: {
    modalToggle() {
      this.$emit('modalOpen', !this.modalOpen)
    }
  }
}
</script>
