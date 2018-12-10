<template>
  <div style="margin-top:5px">
    <div class="field is-horizontal"  v-if="editMode">
      <div class="field-body">
        <b-field>
          <b-input size="is-small" v-model="myName" @input="handleUpdateField" placeholder="Nombre" type="text"></b-input>
        </b-field>
        <b-field>
          <b-input size="is-small" v-model="myOptions" @input="handleUpdateField" placeholder="Opciones" type="textarea"></b-input>
        </b-field>
      </div>
    </div>
    <div v-if="!editMode">
      <b>{{myName}}: </b>
      <label>{{myResult}}</label>
      <button style="margin-top: -5px; border-radius: 20px;font-size: 0.7rem;margin-top: 0px;" size="is-small" @click="refresh" class="button is-warning">
        <b>&#8635;</b>
      </button>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'field',
    data () {
      return {
        myName: '',
        myOptions: '',
        myResult: ''
      }
    },
    methods: {
      refresh: function() {
        if (this.myOptions) {
          let array = this.myOptions.split(',')
          this.myResult = array[Math.floor(Math.random() * array.length)]
        }
      },
      handleUpdateField: function() {
        console.log("handle________", this.myName)
        this.updateField( { id: this.id, name: this.myName, options: this.myOptions, result: this.myResult})
      }
      // updateField() {
      //   // this.$emit('updatedField', { name: this._name, options: this._options, result: this._result})
      // }
    },
    props: 
      ['id', 'name','options', 'editMode', 'updateField']
    ,
    created() {
      this.$eventHub.$on('refresh-all', () => {
        this.refresh()
      })
    },
    mounted() {
      this.myName = this.name
      this.myOptions = this.options
    }
  }
</script>