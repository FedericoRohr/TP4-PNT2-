<template>
  <section class="src-components-formulario">
    <div class="jumbotron">
      <h1>Formulario</h1>
      <vue-form :state="formState" @submit.prevent="enviar">
        <validate tag="div">
          <label for="nombre">Nombre</label>
          <input
            type="text"
            id="nombre"
            class="form-control"
            autocomplete="off"
            v-model.trim="formData.nombre"
            name="nombre"
            required
            :minlength="nombreMinLength"
            :maxlength="nombreMaxLength"
          />

          <field-messages name="nombre" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">
              Nombre obligatorio
            </div>
            <div slot="minlength" class="alert alert-danger mt-1">
              Este campo debe tenere al menos {{ nombreMinLength }}
            </div>
          </field-messages>
        </validate>
        <!------------------------------------------EDAD--------------------------------------------------->
        <validate tag="div">
          <label for="edad">Edad</label>
          <input
            type="number"
            id="edad"
            class="form-control"
            autocomplete="off"
            v-model.trim="formData.edad"
            name="edad"
            required
            :min="edadmin"
            :max="edadmax"
          />

          <field-messages name="edad" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">
              Edad obligatoria
            </div>
            <div slot="min" class="alert alert-danger mt-1">
              Edad minima {{ edadmin }}
            </div>
            <div slot="max" class="alert alert-danger mt-1">
              Edad maxima {{ edadmax }}
            </div>
          </field-messages>
        </validate>

        <!------------------------------------------MAIL--------------------------------------------------->

        <validate tag="div">
          <label for="mail">Mail</label>
          <input
            type="email"
            id="mail"
            class="form-control"
            autocomplete="off"
            v-model.trim="formData.mail"
            name="mail"
            required
          />

          <field-messages name="mail" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">
              Email no valido
            </div>
          </field-messages>
        </validate>

        <!------------------------------------------BOTON--------------------------------------------------->
        <button type="submit" :disabled="formState.$invalid">enviar</button>
      </vue-form>
      <!------------------------------------------TABLA--------------------------------------------------->
      <div class="table-responsive">
        <table class="table table-dark">
          <tr>
            <th>#</th>
            <th>Nombre</th>
            <th>Edad</th>
            <th>Mail</th>
          </tr>
          <tr v-for="(usuario, index) in usuarios" v-bind:key="index">
            <td>{{ index + 1 }}</td>
            <td>{{ usuario.nombre }}</td>
            <td>{{ usuario.edad }}</td>
            <td>{{ usuario.mail }}</td>
          </tr>
        </table>
      </div>
    </div>
  </section>
</template>


<script>
export default {
  name: "src-components-formulario",
  props: [],
  mounted() {},
  data() {
    return {
      formState: {},
      formData: this.getInitialData(),
      nombreMinLength: 5,
      nombreMaxLength: 15,
      edadmin: 18,
      edadmax: 120,
      usuarios: [],
    };
  },
  methods: {
    getInitialData() {
      return {
        nombre: null,
        edad: null,
        mail: null,
      };
    },
    enviar() {
      this.usuarios.push({ ...this.formData });

      this.formData = this.getInitialData();
      this.formState._reset();
    },
  },
  computed: {},
};
</script>

<style scoped lang="css">
.jumbotron {
  background-color: violet;
  color: white;
}
span {
  color: black;
}
</style>
