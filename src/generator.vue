<template>
  <div class="box">
    <div class="field is-horizontal">
      <div class="field-body">
        <h4 class="title is-4" style="margin-bottom:0" v-if="!editMode">{{name}}</h4>
        <b-field v-if="editMode">
          <b-input size="is-small" v-model="name" placeholder="Nombre" type="text"></b-input>
        </b-field>
        <button style="margin-top: -5px; border-radius: 20px;margin-left: 10px;" v-if="!editMode" @click="refresh" class="button is-warning">
          <b>&#8635;</b>
        </button>
      </div>
    </div>
    <field
      v-for="(field, index) in fields"
      :editMode="editMode"
      :updateField="updateField"
      :name="field.name"
      :options="field.options"
      :id="index"
      :key="index"/>
      <br>
      <button @click="newField" v-if="editMode" class="button">Nuevo Campo</button>
      <button @click="saveGenerator"  v-if="editMode" class="button">Guardar generador </button>
      <button @click="editGenerator" v-if="!editMode" class="button">Editar generador </button>
      <button @click="viewGenerator" v-if="editMode" class="button">Ver generador </button>
  </div>
</template>

<script>
  import field from './field.vue'
  export default {
    name: 'generator',
    components: {field},
    data () {
      return {
        fields: [{name:'Nombre', result: 'Holo', options:'a, b', id: 0}],
        editMode: false
      }
    },
    methods: {
      newField: function() {
        this.fields.push({})
      },
      refresh: function() {
        console.log('refesh')
        this.$eventHub.$emit('refresh-all')
      },
      saveGenerator: function() {
        console.log('save')
      },
      editGenerator: function() {
      this.editMode = true
      },
      viewGenerator: function() {
        this.editMode = false
      },
      updateField: function(field) {
        console.log("field________",field)
        let id = field['id']
        this.fields[id] = field
      },
    },
    props: {
      name: {
        type: String,
        default: '',
      }
    }
  }
</script>