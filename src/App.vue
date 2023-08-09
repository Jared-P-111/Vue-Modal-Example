<!-- 
  ------------------------- INFO --------------------------
  This is where we can use our HTML which is just like a component in react. Every component needs to have a template at minimum
  The script and style are optional
-->

<!-- This is the vue tag that makes this a component template. Also notice that we are using a ref in the input tag this connects to the 
     Script area and we access via methods

     Event Modifiers allow us to be specific as to how we want an event to happen. Notice on the button with the click event we add a . after the @click then we can select an event type. For example if we put @click.right that would mean it only works if you right click the button. You can also group them by . so @click.right.shift means hold shift and right click

     When we use what is called slots, we can pass much larger amounts of data as opposed to just using props. To do this we don't use
     a self closing tag instead we open the component and supply children to it. 

     We can also use Named Slots that allow for specific use of data being populated in a targeted tag inside the <slot></slot> we have
     to use another template tag inside of the <Modal> to achieve this. 
-->

<template>
  <div>
    <h1>{{ title }}</h1>
    <input type="text" ref="name" />
    <button @click="handleClick">Click me</button>
    <div v-if="showModal">
      <Modal :header="header" :text="text" theme="sale" @close="toggleModal">
        <!-- 
          Everything in here is considered a "Slot this content (below) <h1> and <p> only shows if we don't pass in default content inside the 
          <slot></slot> in the child component. (Modal)"
        -->
        <h1>Get ya free VUE!!!</h1>
        <p>Grab all the vue you can handle.</p>
        <!-- 
          This is a Named Slot (below) notice the slot directive after template with v-slot:links 
          The links is the assigned name of the slot this allows to target where slots will show up in the 
          child component
        -->
        <template v-slot:links>
          <a href="#">Sign up now!</a>
          <a href="#">More Info</a>
        </template>
      </Modal>
    </div>
    <div v-if="showModalTwo">
      <Modal :header="header" :text="text" theme="bargain" @close="toggleModalTwo">
        <!-- This is default slots and we are not targeting the name="links" -->
        <h1>Sign up to new Modal</h1>
        <p>Oh yea!!!</p>
      </Modal>
    </div>
    <button @click="toggleModal">Modal One</button>
    <button @click="toggleModalTwo">Modal Two</button>
  </div>
</template>

<script>
import Modal from './components/Modal.vue';

export default {
  name: 'App',
  components: { Modal },
  data() {
    return {
      title: 'Vue Learning Application',
      header: 'Vue kicks ass!',
      text: 'Grab your swag and lets roll!!!',
      showModal: false,
      showModalTwo: false,
    };
  },
  //Here we access that ref using the $refs.<ref name here>
  methods: {
    handleClick() {
      console.log(this.$refs.name);
      this.$refs.name.classList.add('active');
      this.$refs.name.focus();
    },
    toggleModal() {
      this.showModal = !this.showModal;
    },
    toggleModalTwo() {
      this.showModalTwo = !this.showModalTwo;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
