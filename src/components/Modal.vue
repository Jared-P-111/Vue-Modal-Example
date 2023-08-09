<template>
  <div class="backdrop" @click.self="closeModal">
    <div class="modal" :class="{ sale: theme === 'sale' }">
      <h1>{{ header }}</h1>
      <p>{{ text }}</p>
      <slot></slot>
      <div class="actions">
        <!-- Here is where we bring in a named slot from App-->
        <slot name="links"></slot>
      </div>
      <button @click="closeModal">close</button>
    </div>
  </div>
</template>

<!--
  Here we (Below) take in props from the Modal component that is nested in the App.vue file we specified a prop and we need to tell vue that we are a
  accepting props we do this in the script tag for the Vue component. Its important to note that the props can be dynamic or static the theme prop is coming in as static while the text / header is dynamic capable cause its passed in with the data() from the app component. 

  Using $emit allows us to send up an event bubble through the child to the parent to tell it to listen
  for changes. We will emit the 'close' that will be picked up in the parent look at the @close attached inside the modal component this points to the toggleModal in the data -> methods()
-->

<script>
export default {
  //🔥🔥🔥🔥🔥🔥🔥 BRING IN YOUR PROPS!!!!!!!!
  props: ['header', 'text', 'theme'],
  methods: {
    closeModal() {
      this.$emit('close');
    },
  },
};
</script>

<!-- 
  Scoped makes the styles only apply to the current component you could also increase the specificity by using modal as the 
  Targeted selector for example if you put modal h1 {} that would only apply the styles here to this modal.
-->
<style scoped>
.modal {
  width: 400px;
  padding: 20px;
  margin: 100px auto;
  background: white;
  border-radius: 10px;
}

.backdrop {
  top: 0;
  position: fixed;
  background: rgba(0, 0, 0, 0.5);
  width: 100%;
  height: 100%;
}

h1 {
  color: rgb(13, 133, 133);
  border: none;
  padding: 0;
}

.modal.sale {
  background: crimson;
  color: white;
}

.modal.sale h1 {
  color: white;
}
</style>
