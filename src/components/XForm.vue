<template>
  <!-- <pre>{{ obj }}</pre> -->
  <form :style="{ display: 'flex', 'flex-direction': 'column' }">
    <!-- todo: add code -->
    <component
      v-for="(field, index) in fields.length"
      :key="index"
      :is="fields[index].component ?? 'input'"
      :type="fields[index].type"
      :placeholder="fields[index]['placeholder'] ?? fields[index]['field']"
      :value="obj[fields[index].field]"
      :name="fields[index].field"
      @input="onInput($event.target.value, index)"
      :style="{ 'margin-top': '10px' }"
    />
  </form>
</template>

<script>
export default {
  // todo: add code
  props: {
    obj: Object,
    fields: Object,
  },
  emits: ['update:obj'],
  methods: {
    onInput(value, index) {
      // console.log(value, index);
      try {
        let objCopy = { ...this.obj };
        objCopy[this.fields[index].field] = value;
        // console.log(objCopy);
        this.$emit('update:obj', objCopy);
      } catch (err) {
        console.log(err);
      }
    },
  },
};
</script>
