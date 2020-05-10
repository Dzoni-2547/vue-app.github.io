<template>

    <div class="row"> 

        <div class="text-right"> 
            <div class="dropdown">

                <button class="btn drop-btn dropdown-toggle" type="button" data-toggle="dropdown">
                    {{ data.contract_length.preselected_contract_length }}
                    <span class="caret"></span>
                </button>
                
                <ul class="dropdown-menu dropdown-menu-right">
                    <li v-for="(option, key) in data.contract_length.contract_length_options" :key="key">
                        <a @click="selectType" :data-option="option" href="#">{{ option }}</a>
                    </li> 
                </ul>
            </div> 
        </div>
 

        <!-- CARD BOX LOOP -->
        <div class="col-md-4 col-sm-12 col-xs-12" v-for="item in data.items" :key="item.id"> 
            <div class="card">   
 
                <div v-if="item.is_featured" class="recommended text-center"> 
                    <p>Preporučujemo</p> 
                </div>

            <!-- TITLE --> 
                <h2 class="title flex text-center">{{ item.name }}</h2>    

           
            <!-- DESCRIPTION -->
                <div class="desription min-height flex row"> 
                    <div class="image-cont  text-center col-xs-3 no-padding">
                        <img class="icon" :src="data.assets.tv_category" :alt="data.assets.tv_category" />  
                    </div>   
                    <!-- NOT COMPUTED -->
                    <div class="desc-cont col-xs-9">  
                        <div v-for="description in item.included" :key="description.id"> 
                            <div v-if="description.product_category =='tv'"> 
                                {{ description.long_name }}   
                            </div>    
                        </div> 
                    </div>
                </div> 
 
                <div class="desription row"> 
                    <div class="image-cont  text-center col-xs-3 no-padding">
                        <img class="icon" :src="data.assets.net_category" :alt="data.assets.net_category" />  
                    </div>   
 
                    <div class="desc-cont col-xs-9"> 
                        <div v-for="description in item.included" :key="description.id"> 
                            <div v-if="description.product_category =='net'"> 
                                {{ description.long_name }}   
                            </div>    
                        </div>
                    </div>
                </div> 


            <!-- PRODUCT IMAGE -->
                <div class="product-img-descr flex row" v-for="item in item.promotions" :key="item.id">
                    <div class="col-xs-4 no-padding">
                        <img class="img-responsive" :src="item.promotion_image" :alt="item.id">
                    </div>    
                    
                    <div class="col-xs-8 no-padding img-contents">
                        <div v-html="item.promo_text"></div>
                    </div>
                </div>

 
            <!-- PRODUCT PRICE -->
                <div class="price-cont text-center"> 
                    <span v-html="formatNumber(item.prices.old_price_recurring['Ugovor 24 meseca'])" class="old-price">
                         
                    </span>
                   
                    <span v-html="formatNumber(item.prices.price_recurring['Ugovor 24 meseca'])"></span>

                    <div v-html="item.prices.old_price_promo_text"></div>     
                </div>     

                
                <button class="button">Naručite</button>
            </div>   
        </div> 
    </div>

</template>

 
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
<script>    
// import resources from '../../resources.json' 

export default {
    name: 'Card',
    data() {
        return {  
            data: []
        }
    },

    components: {},

    computed: {},
 
    methods: { 
        formatNumber(value) { 
            return parseFloat(value).toLocaleString()  + '<span class="currency"> rsd/mes.</span>'
        },
        selectType(target) {   
            console.log( target.target.attributes['data-option'].value  ) 
        }
    },  
   
    mounted () {
        axios
        .get('http://www.mocky.io/v2/5e8465c23000008400cf4395')
        .then(response => {
            this.data = response.data   
        })
        .catch(error => {
            console.log(error)
            this.errored = true
        })   
    }
} 

 
</script>


<style scoped>
 
.row,
.title {
    margin: 0;
}
 
.no-padding,
.dropdown-menu  {
    padding: 0;
}


.flex {
    display: flex;
    align-items: center;
    flex-wrap: wrap;  
    justify-content: center;
    display: -webkit-flex;
    -webkit-align-items: center;
    -webkit-flex-wrap: wrap; 
    -webkit-justify-content: center;
}

 
.dropdown-menu a {
    padding: 6px 15px;
}
.dropdown-menu a:hover {
    color: #fff;
    background: #742d6c;
} 
 
.card {
    margin: 10px 0;
    padding: 10px;
    border-radius: 10px; 
    position: relative;
}

 
.recommended {
    padding: 5px; 
    border-radius: 10px 10px 0 0;
}
.recommended p {
    border-bottom: 1px solid #ddd;
}
.card,
.recommended,
.drop-btn {
    background: #f8f4ec;
}

.title {
    font-size: 48px;
    line-height: 47px;  
    min-height: 115px;
    padding: 10px 15px;
}

.title, 
.img-contents,
.price-cont span,
.recommended {
    color: #742d6c; 
    font-weight: bold; 
    font-style: italic;
}

.desription {
    border-top: 1px solid #ddd;
    padding: 20px 0;
} 
.desription.min-height {
    min-height: 165px;
} 


.icon {
    max-width: 100%;
    max-height: 50px;
} 


.product-img-descr {
    background: #fff;
    margin: 10px;
}
.product-img-descr img {
    max-height: 85px;
} 


.price-cont span {
    font-size: 28px;
    line-height: 48px;
    display: inline-block;
    margin: 0 10px;
}
.price-cont .old-price {
    font-size: 20px;
    text-decoration: line-through;
}
.price-cont div {
    color: #102542;
}


.button {
    background: #742d6c;
    color: #fff;
    padding: 8px;
    margin: 15px 10px;
    border: none;
    border-radius: 10px;
    width: calc(100% - 20px);
    font-size: 18px;
}
.button:hover {
    background: #933988;
}


/********************/

@media (min-width: 991px) {
    .card {
         margin: 40px 0;   
    }
    .recommended {
        padding: 5px;
        position: absolute;
        top: -25px;
        left: 0;
        width: 100%;
        border-radius: 10px 10px 0 0;
    }
}
 

</style>
