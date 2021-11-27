<template>
  <v-container>
       <p>Introduzca el fichero</p>
        <div id="readfile">
        <input v-on:click="readFile" type="file" name="inputfile" id="inputfile">
        <pre id="output"></pre>
    </div>

    <div>
        <p>Métrica</p>
      <v-row align="center">
 
        <v-col class="d-flex" cols="12" sm="6">
          <v-select :items="itemsMetric" label="Seleccione la métrica" dense solo v-model="metric" v-on:change = "selectMetrics"></v-select>
        </v-col>
      </v-row>
    </div>

    <div>
      <p>Número de vecinos considerado</p>

        <v-col
          cols="12"
          sm="6"
          md="3"
        >
          <v-text-field
            label="Solo"
            dense
            solo
            v-on:change = "getNeighbors"
            v-model = neighbor
          ></v-text-field>
        </v-col>

    </div>
      
    <div>
      <p>Tipo de predicción</p>
      <v-row align="center">
        <v-col class="d-flex" cols="12" sm="6">
          <v-select :items="itemsPrediction" label="Seleccione la predicción" dense solo v-model="prediction" v-on:change = "selectPrediction"></v-select>
        </v-col>
      </v-row>
    </div>

    <div>
      <v-btn
        color="primary"
        elevation="2"
        v-on:click="operate"
      >Calcular</v-btn>
    </div>
  </v-container>
</template>

<script>
  export default {


      data: () => ({
        itemsMetric: ['Correlación de Pearson', 'Distancia coseno', 'Distancia Euclídea'],
        itemsPrediction: ['Predicción Simple', 'Diferencia con la media'],
        metric: null,
        neighbor: null,
        prediction: null,
    }),
    
    methods: {
        // readFile() {
        //     // var file = new File([""],"../../public/files/file1.txt");
        //     // var reader = new FileReader();
        //     // reader.readAsText(file);
        //     // reader.onload = function() {
        //     //     console.log(this.result);
        //     // }
            
        // },
        readFile() {
            document.getElementById("inputfile").addEventListener("change", function() {
                var reader = new FileReader();
                var matrix;
                var matrix_content;
                reader.onload = function() {
                    var lines = this.result.split("\n");
                    console.log(lines);
                    matrix = new Array(lines.length).fill(0).map(() => new Array(lines.length).fill(0));
                    for(var i = 0; i < lines.length; i++) {
                        matrix_content = lines;
                        
                        matrix_content = this.result.split(/\s+/);
                        console.log(matrix_content);
                        
                        for (var j = 0; j < (matrix_content.length / lines.length).toFixed(); j++) {
                            // OJO: AQUI CAMBIO DE STRING A INT
                            matrix[i][j] = parseInt(matrix_content[((matrix_content.length / lines.length).toFixed() * i) + j]);
                            console.log((matrix_content.length / lines.length).toFixed());
                        }
                    }
                    console.log(matrix);
                }
                reader.readAsText(this.files[0]);
            })
        },
        selectMetrics() {
             console.log(this.metric);
          
        },
        selectPrediction() {
             console.log(this.prediction);
          
        },
        getNeighbors() {
          console.log(this.neighbor);
        }, 

        operate() {
          switch (this.metric) {
            case 'Correlación de Pearson': 
              console.log('Ha seleccionado Correlación de Pearson')
              break;
            case 'Distancia coseno': 
              console.log('Ha seleccionado Correlación de coseno')
              break;
            case 'Distancia Euclídea': 
              console.log('Ha seleccionado Correlación de Euclidea')
              break;
            default:
                console.log('ERROR: No se ha seleccionado ninguna Correlación.')
          }
        }
    }
}
</script>
