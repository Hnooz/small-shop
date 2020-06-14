<template>
   <main class="">
       <div class="flex mt-12 pl-10">
            <h1 class="font-semibold text-2xl text-teal-400">All Product</h1>
       <svg class="w-5 font-semibold text-xl text-teal-400 ml-2" fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" viewBox="0 0 24 24" stroke="currentColor"><path d="M16 11V7a4 4 0 00-8 0v4M5 9h14l1 12H4L5 9z"></path></svg>
       </div>
      
       <div class="grid md:grid-cols-3 grid-cols-1 pl-5 mt-12 border-b-2 border-teal-200" >
           <div class="bg-gray-300 border-b-2 border-teal-300 mb-12 mx-16 rounded-lg shadow-2xl" v-for="product in products" :key="product.index"> 
               
                <div class="md:px-5 px-5"> 
                    <img class="h-64 mt-4 rounded-lg w-64" :src="product.photo" alt="no">
                </div>
                <div class="border-b-2 border-teal-200 pl-5">
                    <h1 class="my-5 font-semibold text-2xl text-teal-400">{{product.name}}</h1>
                </div>
                <div class="flex items-center justify-between pb-4 pt-3">
                <span class="pl-5 font-medium text-teal-300">${{product.price}}</span>
                <div class="mr-6 rounded-lg hover:bg-teal-800  bg-teal-900">
                    <button @click.once="addToCart(product)" type="button" class="px-2 py-1 font-semibold text-xl text-teal-200 hover:text-white">To Cart</button>
                </div>
                </div>                
           </div>
           
       </div>
    <div v-show="carts.length != 0">
       <div class="border-b-2 border-teal-200 flex mt-4 pb-4 pl-10 shadow-lg">
           <h1 class="font-semibold text-2xl text-teal-400">Cart</h1>
            <svg class="w-5 font-semibold text-xl text-teal-400 ml-2" fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" viewBox="0 0 24 24" stroke="currentColor">
                <path d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 2a2 2 0 11-4 0 2 2 0 014 0z"></path>
            </svg>
       </div>
 
         <div class="grid md:grid-cols-2 grid-cols-1 pl-5 mt-12 border-b-2 border-teal-200" >
           <div class="bg-gray-300 border-b-2 border-teal-300 mb-12 mx-16 rounded-lg shadow-2xl" v-for="(cart,index) in carts" :key="index"> 
               
                <div class="flex justify-center"> 
                    <img class="h-64 mt-6 rounded-lg w-64" :src="cart.photo" alt="product">
                </div>
                <div class="border-b-2 border-teal-200  md:px-12">
                    <h1 class="my-5 font-semibold text-2xl text-teal-400 px-4">{{cart.name}}</h1>
                </div>
                <div class="mx-4 flex items-center justify-between pb-4 pt-3 md:px-16 md:mx-0">
                    <span class=" font-medium text-teal-300">${{cart.price}}</span>

                    <span class="font-medium text-teal-400"> {{subtotals[index]}}</span>
                    <div class="md:mr-6 flex justify-between">
    
                        <svg @click="increment(cart,index)" class="h-5 w-5 cursor-pointer font-semibold text-xl text-teal-400 hover:text-teal-300 mr-1" fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" viewBox="0 0 24 24" stroke="currentColor">
                            <path d="M12 9v3m0 0v3m0-3h3m-3 0H9m12 0a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                        </svg>

                        <span class="font-mediumd text-teal-400">
                            {{cart.quantity}}
                        </span>
                        
                        <svg @click="decrement(cart,index)" class="h-5 w-5 font-semibold text-xl text-teal-400 hover:text-teal-300 ml-1" fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" viewBox="0 0 24 24" stroke="currentColor">
                            <path d="M15 12H9m12 0a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                        </svg>
                    </div>
                </div>                
           </div>
       </div>
       <div class="bg-teal-900 flex justify-between py-5"> 
           <h1 class="text-teal-200 font-semibold uppercase pl-20">total price</h1>
           <h1 class="text-teal-200 font-semibold uppercase pr-16">${{total}}</h1>
           <h1 class="text-teal-200 font-semibold uppercase pr-16">Made With <span class="text-red-500 text-2xl">&hearts;</span>  By Hnooz</h1>
       </div>
        
    </div>
   
   </main>
</template>

<script>
export default {
    name:'Product',
    data() {
        return {
           
            products:[
                {name:'test', photo:'https://images.unsplash.com/photo-1491637639811-60e2756cc1c7?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=369&q=80', price:100, quantity:1}, 
                {name:'test', photo:'https://images.unsplash.com/photo-1491637639811-60e2756cc1c7?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=369&q=80', price:200, quantity:1}, 
                {name:'test', photo:'https://images.unsplash.com/photo-1491637639811-60e2756cc1c7?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=369&q=80', price:300, quantity:1},
                {name:'test', photo:'https://images.unsplash.com/photo-1491637639811-60e2756cc1c7?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=369&q=80', price:400, quantity:1},
                {name:'test', photo:'https://images.unsplash.com/photo-1491637639811-60e2756cc1c7?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=369&q=80', price:500, quantity:1},
                {name:'test', photo:'https://images.unsplash.com/photo-1491637639811-60e2756cc1c7?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=369&q=80', price:600, quantity:1},
            ],
             carts:[],
             count:0,
             total:0,
             subtotals:[],
        }
    },

    methods: {
        addToCart(product)
        {
            this.carts.push(product);
            this.subtotals.push(product.price);
            this.total = this.total + product.price;

        },

        increment(cart,index)
        {
            cart.quantity++;
            this.subtotals[index] = cart.quantity * cart.price;
            this.total = this.total + cart.price;
            
        },

        decrement(cart,index)
        { 
            cart.quantity--;

            if (cart.quantity == 0) {
                this.carts.pop(cart);
               this.subtotals.pop();
            }
            this.subtotals[index] = this.subtotals[index] - cart.price;
            this.total = this.total - cart.price;

            

        },


        
    },

}
</script>

<style>
    
</style>