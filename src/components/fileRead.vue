<template>
  <v-container>
       <p>hola</p>
        <div id="readfile">
        <input v-on:click="readFile" type="file" name="inputfile" id="inputfile">
        <pre id="output"></pre>
    </div>

    <div>
        Métrica a elegir
    </div>
  </v-container>
</template>

<script>
  export default {


       data() {
        return {
            message: 'Hola'
        }
    },
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
                    matrix = new Array(lines.length).fill(0).map(() => new Array(lines.length).fill(0));
                    for(var i = 0; i < lines.length; i++) {
                        matrix_content = lines;
                        
                        matrix_content = this.result.split(/\s+/);
                        
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
            
        }
    }
}
</script>
