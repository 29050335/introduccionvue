<template>
  <html>
    <head>
    <meta charset="utf-8">
    <link rel="icon" href="/favicon.ico" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
   <!-- Latest compiled and minified CSS -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@3.3.7/dist/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">
     <title>Vue Example</title><meta charset="UTF-8" />
  </head>
  <body>
    <div class="container">
      <div class="row">
        <div class="col-xs-12">
          <h1 class="jumbotron">VueJs</h1>
             <div id="app">
            <!-- Alumna: <b> {{ message }} </b> -->
            <table class="table table-stripped">
              <thead>
                <tr>
                  <th style="width:40px;"></th>
                  <th>Descripcion</th>
                  <th style="width:200px;">Monto</th>
                  <th style="width:100px;">Cancelado?</th>
                </tr>
              </thead>
              <tbody>

                <tr >
                <td></td>
                <td>
                  <input type="text" class="form-control" v-model='name' />
                </td>
                <td>
                  <input type="text" class="form-control" v-model='amount'  />
                </td>
                <td>
                  <button @click="add()" type="text" class="btn btn-success btn-block">Agregar</button>
                </td>
                </tr>

                <tr v-if="items.length === 0">
                  <td colspan="4" class="text-center">
                    No se han encontrado archivos
                  </td>
                </tr>
                <tr v-for="item, index in items">
                  
                  <td>
                  <!-- v-on:click abreviado seria con arroba @-->
                  <button
                   @click="remove(index)"
                   type="button" class="btn btn-danger btn-xs">
                    <i class="glyphicon glyphicon-trash"></i>
                  </button>
                  </td>
                  <td>{{ item.name}}</td>
                  <td>{{ item.amount.toFixed(2) }}</td>
                  <td class="text-center" :title="item.paid ? 'Si' : 'No'">
                    <button 
                    @click="changeToPaid(item)"
                    class="btn btn-default btn-sm" v-bind:class="{ 'btn-success': item.paid }">
                      <i v-if="item.paid" class="glyphicon glyphicon-ok"></i>
                      <i v-if="!item.paid" class="glyphicon glyphicon-remove"></i>
                    </button>
                  </td>
                </tr>
              </tbody>

              <tfoot>
                <tr>
                  <td></td>
                  <td class="text-right">Total: <b>{{ totalAmount() }}</b></td>
                  <td></td>
                  <td></td>
                </tr>
              </tfoot>


            </table>
             </div>
        </div>
      </div>
    </div>

    </body>
  </html>
</template>

  <script>
  export default{
    data: () => ({   
      
      newEntry: {
       name:'',
       amount: 0,
       paid: false
      },

      items:[
        { name: 'Servicios', amount: 200, paid: false},
        { name: 'Hosting de Anexsoft', amount: 90, paid: true},
      ]
   
      
    }),
   
    
    methods: {
        remove: function(index){
          this.items.splice(index, 1);
        },
        add(){
          this.items.push({
            name:this.newEntry.name,
            amount: parseFloat(this.newEntry.amount),
            paid:false
          });
          this.newEntry.name = '';
          this.newEntry.amount = 0;
        },
        changeToPaid(item){
          item.paid = !(item.paid); 
        },
        totalAmount(){
          var total =  this.items.reduce(function(a, b){
            return a + b.amount;
          }, 0);

          return total.toFixed(2);
        }
      },
  }
  
  </script>
  
 
  
  
