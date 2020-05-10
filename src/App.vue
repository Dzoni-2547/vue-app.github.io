<template>

    <div id="app">  
        <div class="container">
            
            <div class="main-content"> 
            
                <Card /> 
            
            </div> 
  
        </div> 
    </div>

</template>


<script>
import Card from './components/Card.vue'   
// import usersTable from './components/usersTable.vue'   

export default {
    name: 'App',
    components: {
        Card
        // usersTable, 
    }
}
</script>


<style> 

body {
    font-family: "Calibri";
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale; 
    color: #1a1a1a;
    font-size: 15px;
    font-weight: normal;
    margin: 0;
    padding: 0;
} 
p {
    margin: 0;
}

.main-content {
    padding: 30px 0;
}

@media (max-width: 991px) {
    .container {
         width: 100%;  
    }
}


</style>
