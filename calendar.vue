<template>
    <v-container  grid-list-md text-xs-center >
     
     <v-layout fluid row justify-center  >

         <v-btn slot="activator" @click="voltarMes()" icon>
             <v-icon class="icone" color="">arrow_back</v-icon>
         </v-btn>
       <v-spacer></v-spacer>

       <v-flex xs3  >
         <v-card  flat dark color="transparent">
           <v-card-text> <b> <font color="#448aff"> {{this.mesAtual}} - {{this.anoAtual}} </font> </b> </v-card-text>
         </v-card>
       </v-flex>

       <v-spacer></v-spacer>
       <v-btn slot="activator" @click="proxMes()" icon>
           <v-icon class="icone">arrow_forward</v-icon>
       </v-btn>

     </v-layout>

     <v-layout row class="scheduleTop" order-xs1>


       <v-flex class="weekDays" d-flex xs2 row  >
         <v-card flat tile dark color="transparent">
           <v-card-text  class="px-0" > <b> SEG </b> </v-card-text>
         </v-card>
       </v-flex>

       <v-flex class="weekDays" d-flex xs2 row >
         <v-card flat tile dark color="transparent">
           <v-card-text class="px-0"> <b> TER </b> </v-card-text>
         </v-card>
       </v-flex>

       <v-flex class="weekDays" d-flex xs2 row >
         <v-card flat tile dark color="transparent">
           <v-card-text class="px-0"> <b>QUA</b> </v-card-text>
         </v-card>
       </v-flex>

       <v-flex class="weekDays" d-flex xs2 row >
         <v-card flat tile dark color="transparent">
           <v-card-text class="px-0"> <b>QUI</b> </v-card-text>
         </v-card>
       </v-flex>

       <v-flex class="weekDays" d-flex xs2 row >
         <v-card flat tile dark color="transparent">
           <v-card-text class="px-0"> <b>SEX</b> </v-card-text>
         </v-card>
       </v-flex>

       <v-flex class="weekDays" d-flex xs2 row >
         <v-card flat tile dark color="transparent">
           <v-card-text class="px-0"> <b>SÁB</b> </v-card-text>
         </v-card>
       </v-flex>

       <v-flex class="weekDays" d-flex xs2 row >
         <v-card flat tile dark color="transparent">
           <v-card-text class="px-0"> <b>DOM</b> </v-card-text>
         </v-card>
       </v-flex>
      


     </v-layout>



     <v-layout row  class="calendary" >

         <v-flex class="scheduleDay" d-flex v-for="(dias, index) in primeiraSemana" :key="index"  xs2 row order-xs2>
           <v-card flat tile dark color="transparent">
             <v-card-text class="px-0"> {{dias.dia}} </v-card-text>
           </v-card>
         </v-flex>

     </v-layout>

      <v-layout row  class="calendary" >

         <v-flex class="scheduleDay" d-flex v-for="(dias, index) in segundaSemana" :key="index"  xs2 row order-xs3>
           <v-card flat tile dark color="transparent">
             <v-card-text class="px-0"> {{dias.dia}} </v-card-text>
           </v-card>
         </v-flex>

      </v-layout>

      <v-layout row  class="calendary" >

         <v-flex class="scheduleDay" d-flex v-for="(dias, index) in terceiraSemana" :key="index"  xs2 row order-xs3>
           <v-card flat tile dark color="transparent">
             <v-card-text class="px-0"> {{dias.dia}} </v-card-text>
           </v-card>
         </v-flex>

      </v-layout>


      <v-layout row  class="calendary" >

         <v-flex class="scheduleDay" d-flex v-for="(dias, index) in quartaSemana" :key="index"  xs2 row order-xs3>
           <v-card flat tile dark color="transparent">
             <v-card-text class="px-0"> {{dias.dia}} </v-card-text>
           </v-card>
         </v-flex>

      </v-layout>

      <v-layout row  class="calendary" >

         <v-flex class="scheduleDay" d-flex v-for="(dias, index) in quintaSemana" :key="index"  xs2 row order-xs3>
           <v-card flat tile dark color="transparent">
             <v-card-text class="px-0"> {{dias.dia}} </v-card-text>
           </v-card>
         </v-flex>

      </v-layout>

     <v-layout row  class="calendary" >

         <v-flex class="scheduleDay" d-flex v-for="(dias, index) in sextaSemana" :key="index"  xs2 row order-xs3>
           <v-card flat tile dark color="transparent">
             <v-card-text class="px-0"> {{dias.dia}} </v-card-text>
           </v-card>
         </v-flex>

      </v-layout>

    </v-container></template>

<script>


export default {
   name: 'calendar',
   components: {

   },
   props: {
   },
   data: () => ({
     meses: [
       "JANEIRO",
       "FEVEREIRO",
       "MARÇO",
       "ABRIL",
       "MAIO",
       "JUNHO",
       "JULHO",
       "AGOSTO",
       "SETEMBRO",
       "OUTUBRO",
       "NOVEMBRO",
       "DEZEMBRO"
     ],
     mesAtual: null,
     nAtual: null,
     anoAtual: null,
     diasNoMes: [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31],
     primeiraSemana: [],
     segundaSemana: [],
     terceiraSemana: [],
     quartaSemana: [],
     quintaSemana: [],
     sextaSemana: [],
     hoje: new Date()
   }),
   mounted() {
     this.getMesAtual()
     this.getAnoAtual()
     this.organizarSemanas()
   },
   computed: {
     primeiroDiaSemana(){
       return new Date(this.anoAtual, this.nAtual, 1).getDay() + 1;
     },

     qntdDiasMes(){
       const isFebruary = this.mesAtual === 2;
       const isLeapYear = (this.anoAtual % 4 == 0 && this.anoAtual % 100 != 0) || this.anoAtual % 400 == 0
       if(isFebruary && isLeapYear){
         return 29
       }
       return this.diasNoMes[this.nAtual]
     },

     semanas(){
       const allSemanas = []
       let mesComecou = false, mesTerminou = false;
       let diaDoMes = 0
       var today = new Date()
      
       for (let w = 1; w <= 6 && !mesTerminou; w++) {
         const semana = []
         for (let d = 1; d <= 7; d++) {

             if (mesComecou == false && d >= this.primeiroDiaSemana) {
               diaDoMes = 1
               mesComecou = true
             }
             else if(mesComecou && !mesTerminou) {
               diaDoMes ++
             }

             semana.push({
               number: diaDoMes,
               numeroDiaSemana: d,
               numeroSemana: w,
               isToday: diaDoMes === today.getDate &&  this.nAtual === today.getMonth - 1 && this.anoAtual === today.getFullYear,
               isFirstDay: diaDoMes === 1,
               isLastDay: diaDoMes === this.qntdDiasMes
             })

             if (mesComecou && !mesTerminou && diaDoMes >= this.qntdDiasMes) {
               diaDoMes = 0;
               mesTerminou = true;
             }

         }

         allSemanas.push(semana)
       }

       return allSemanas;
     },

   },
   methods: {
     proxMes(){
       if(this.nAtual == 11){
         this.nAtual = 0
         this.mesAtual = this.meses[0]
         this.anoAtual = this.anoAtual + 1
         this.organizarSemanas()

       }
       else{
         this.nAtual = this.nAtual + 1
         this.mesAtual = this.meses[this.nAtual]
         this.organizarSemanas()
       }
     },
     voltarMes(){
       if(this.nAtual == 0){
         this.nAtual = 11
         this.mesAtual = this.meses[11]
         this.anoAtual = this.anoAtual - 1
         this.organizarSemanas()

       }
       else{
         this.nAtual = this.nAtual - 1
         this.mesAtual = this.meses[this.nAtual]
         this.organizarSemanas()
       }
     },
     getMesAtual(){
       var today = new Date()
       switch(today.getMonth()) {
         case 0:
           this.mesAtual = "JANEIRO"
           this.nAtual = 0
           break
         case 1:
           this.mesAtual = "FEVEREIRO"
           this.nAtual = 1
           break
         case 2:
           this.mesAtual = "MARÇO"
           this.nAtual = 2
           break
         case 3:
           this.mesAtual = "ABRIL"
           this.nAtual = 3
           break
         case 4:
           this.mesAtual = "MAIO"
           this.nAtual = 4
           break
         case 5:
           this.mesAtual = "JUNHO"
           this.nAtual = 5
           break
         case 6:
           this.mesAtual = "JULHO"
           this.nAtual = 6
           break
         case 7:
           this.mesAtual = "AGOSTO"
           this.nAtual = 7
           break
         case 8:
           this.mesAtual = "SETEMBRO"
           this.nAtual = 8
           break
         case 9:
           this.mesAtual = "OUTUBRO"
           this.nAtual = 9
           break
         case 10:
           this.mesAtual = "NOVEMBRO"
           this.nAtual = 10
           break
         case 11:
           this.mesAtual = "DEZEMBRO"
           this.nAtual = 11
           break
       }
     },
     getAnoAtual(){
       var today = new Date()
       this.anoAtual = today.getFullYear()
     },

     organizarSemanas(){
       this.primeiraSemana = []
       this.segundaSemana = []
       this.terceiraSemana = []
       this.quartaSemana = []
       this.quintaSemana = []
       this.sextaSemana = []
      
       for(let week = 0; week < 6; week++){
         for(let day = 0; day < 7; day ++){
           if(week == 0){
             if(this.semanas[0][day].isFirstDay == true){
               this.primeiraSemana.push({
                 dia: this.semanas[0][day].number
               })
             } else if(this.semanas[0][day].number >=1){
               this.primeiraSemana.push({
                 dia: this.semanas[0][day].number
               })
             } else {
                this.primeiraSemana.push({
                 dia: " "
               })
             }
           } else if(week == 1) {
             this.segundaSemana.push({
                 dia: this.semanas[1][day].number
               })
           } else if(week == 2){
             this.terceiraSemana.push({
               dia: this.semanas[2][day].number
             })
           } else if(week == 3){
             this.quartaSemana.push({
               dia: this.semanas[3][day].number
             })
           } else if(week == 4){
             if(this.semanas[4][day].number > 0){
               this.quintaSemana.push({
                 dia: this.semanas[4][day].number
               })
             }else {
               this.quintaSemana.push({
                 dia: " "
               })
             }
            
           } else if (this.semanas[5]){
             if(this.semanas[5][day].number > 0){
               this.sextaSemana.push({
                 dia: this.semanas[5][day].number
               })
             }else {
               this.sextaSemana.push({
                 dia: " "
               })
             }
           }
         }
       }
       console.log(this.semanas)
      
     }

   }
}
</script>

<style>

.scheduleDay {
 padding: 0;
 margin: 0;
 border: 0;
 min-height: 100px;
 max-height: 150px;
}

.calendary {
 background-color: #424242;
 padding: 0;
 margin: 0;
 border: 0;
 border-radius: 5px;
}
.scheduleTop {
 border-radius: 5px;
 background-color:#448aff;
 max-height: 60px;
}

</style>

