<script>
import InputWithSelect from '@/components/form/InputWithSelect';

export default {
  components: { InputWithSelect },
  props:      {
    spec: {
      type:    Object,
      default: () => {
        return {}
        ;
      }
    },
    label: {
      type:    String,
      default: ''
    },
    placeholder: {
      type:    String,
      default: ''
    },
    options: {
      type:    Array,
      default: () => {}
    }
  },

  data() {
    return {
      types: this.options || ['exact', 'prefix', 'regexp'], value: Object.values(this.spec)[0] || '', type: Object.keys(this.spec)[0] || 'exact'
    };
  },
  methods: {
    selectType(type) {
      this.type = type;
    },
    change() {
      const { type, value } = this;
      const out = {};

      out[type] = value;
      this.$emit('input', out );
    },
    update(input) {
      this.value = input.text;
      this.type = input.selected;
      this.change();
    }
  }
};
</script>

<template>
  <div class="match-input">
    <InputWithSelect :options="types" :text-value="spec[type]" :label="label" :placeholder="placeholder" @input="update" />
  </div>
</template>
