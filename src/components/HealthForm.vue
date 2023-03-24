<template>

<v-container class=" d-flex flex-column align-center ">
    <v-form class="form mt-8">
        <v-select 
            color="blue"
            v-model="genre"
            ref="genre"
            label="Sexe"
            item-title="title"
            item-value="value"
            :items="[
            {value: 'default', title: 'Homme'}, 
            {value: 'female', title: 'Femme'}]"
            variant="underlined"
            required
        ></v-select>

        <v-text-field 
            color="blue"
            v-model="age"
            label="Age :" 
            ref="age"
            variant="underlined"
            :rules="inputRules"
            type="number"
            required
        ></v-text-field>
        <v-text-field 
            color="blue"
            v-model="taille"
            ref="taille"
            label="Poids :" 
            variant="underlined" 
            :rules="inputRules"
            type="number"
            required
            ></v-text-field>
        <v-text-field 
            color="blue"
            v-model="poids"
            ref="poids"
            label="Taille :" 
            variant="underlined" 
            :rules="inputRules"
            type="number"
            required
            ></v-text-field>

        <v-select 
            color="blue"
            v-model="coeff"
            ref="coeff"
            label="Activité"
            item-title="title"
            item-value="value" 
            :items="[
                { value: 1, title: 'Journée passée au repos allongé' },
                { value: 1.2, title: 'Travail sédentaire assis, pas de sport, moins de 30 min de marche' },
                { value: 1.4, title: 'Travail sédentaire avec 30 min de marche' },
                { value: 1.6, title: 'Travail sédentaire et 1 h à 1 h 15 de sport' },
                { value: 1.7, title: 'Travail sédentaire et 1 h 30 à 2 h de sport' },
                { value: 1.8, title: 'Travail physique avec beaucoup de déplacements et 1 h 30 à 2 h de sport' },
                { value: 2, title: 'Travail physique et 3 à 4 h de sport' }
            ]"
            variant="underlined"
            required>
        </v-select>

        <v-select
        color="blue"
        v-model="metabolisme"
        label="Métabolisme"
        item-title="title"
        item-value="value" 
        :items="[
        {value: 'fast', title: 'Métabolisme qui brûle rapidement (plutôt maigre et sec)'},
        {value: 'slow', title: 'Métabolisme plus lent (prise de poids plus facile)'}
        ]"
        variant="underlined"
        ></v-select>

        <v-btn @click="handleSubmit(); handleChange()" color="blue">
            Calculer
        </v-btn>

        <h2 class="mt-6" v-if="submitted">Vous avez besoin de {{ result }} calories</h2>

    </v-form>
</v-container>
  
</template>

<script>

export default {

  data() {
    return {
      genre: null,
      age: "",
      poids: "",
      taille: "",
      result: null,
      coeff: 1,
      metabolism: null,
      submitted: false,

      inputRules: [
        v=> v.length >= 2 || 'Informations manquantes'
      ]
    };
  },
    methods: {
        handleSubmit() {
            console.log(this.genre)
            console.log(this.coeff)
            console.log(this.age)
            console.log(this.poids)
            console.log(this.taille)
            if (this.$refs.age.validate() && 
            this.$refs.taille.validate() &&
            this.$refs.poids.validate()){
                if (this.genre == "female") {
                    this.result = Math.round(665.1 + (9.56 * this.poids) + (1.85 * this.taille) - (4.67 * this.age) * this.coeff)
                } else if (this.genre == "default") {
                    this.result = Math.round(66.5 + (13.75 * this.poids) + (5 * this.taille) - (6.77 * this.age) * this.coeff)
                }
                console.log(this.result)
                this.submitted = true
            }
        },
        handleChange() {
            if (this.metabolisme == 'fast') {
                this.result = this.result + (0.1 * this.result)
            } else if (this.metabolisme == 'slow') {
                this.result = this.result - (0.1 * this.result)
            }
        }
    }
};
</script>

<style>
.form{
    width: 900px;
}

</style>