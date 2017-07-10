<template>
  <!--
      Form's label and textarea component with standard HTML5 attributes

      Usage:
        <sa-textarea label='label' name='name' id='id' placeholder='placeholder' v-model='data'></sa-textarea>
        * 'label' property is the only required one
  -->
  <div class="field" :class="{'has-text-right': isRtl}">
    <label class="label" :for="id">{{label}}</label>
    <p class="control">
      <textarea class="textarea" :name="name" :id="id" :placeholder="placeholder"
        :class="{'has-text-right': isRtl}" :value="localValue" @input="updateValue($event.target.value)"
      >
      </textarea>
    </p>
  </div>
</template>

<script>
export default {
  name: 'Textarea',
  props: {
    'label'      : { required: true },
    'name'       : { default : '' },
    'id'         : { default : '' },
    'placeholder': { default : '' },
    'value'      : { default : '' }
  },

  data() {
    return {
      isRtl: false,
      localValue: this.value
    }
  },

  mounted() {
    // Read `window.isRtl` at startup
    this.getWindowIsRtl();

    // Listening for `toggleDirecion` event to change the direction of input
    Event.$on('toggleDirection', () => {
      this.getWindowIsRtl();
    });
  },

  methods: {
    getWindowIsRtl() {
      this.isRtl = window.isRtl || false;
    },

    // adding v-model support for this custom component
    updateValue(value) {
      this.localValue = value;
      this.$emit('input', value);
    }
  }
}
</script>
