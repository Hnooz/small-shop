<template>
<div>
   <main class="container mx-auto px-6 py-8">
        <div class="flex items-center">
            <h1 class="font-semibold text-2xl text-teal-400">All Product</h1>

            <svg class="w-5 h-5 font-semibold text-xl text-teal-400 mx-2" fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" viewBox="0 0 24 24" stroke="currentColor">
                <path d="M16 11V7a4 4 0 00-8 0v4M5 9h14l1 12H4L5 9z"></path>
            </svg>
        </div>
      
        <div class="grid gap-6 grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 mt-6">
            <div class="p-6 bg-gray-300 border-b-2 border-teal-300 rounded-lg shadow-2xl" v-for="product in products" :key="product.index"> 
                <div> 
                    <img class="h-64 w-full object-cover rounded-lg" :src="product.photo" alt="no">
                </div>

                <div class="border-b-2 border-teal-200">
                    <h1 class="my-5 font-semibold text-2xl text-teal-400">{{ product.name }}</h1>
                </div>

                <div class="flex items-center justify-between mt-5">
                    <span class="font-medium text-teal-300">${{ product.price }}</span>

                    <div class="rounded-lg hover:bg-teal-800 bg-teal-900">
                        <button @click.once="addToCart(product)" type="button" class="px-2 py-1 font-semibold text-xl text-teal-200 hover:text-white">To Cart</button>
                    </div>
                </div>                
            </div>
        </div>

        <div class="mt-12" v-if="carts.length != 0">
            <div class="border-b-2 border-t-2 border-teal-200 flex items-center px-4 py-3">
                <h1 class="font-semibold text-2xl text-teal-400">Cart</h1>

                <svg class="w-5 h-5 font-semibold text-xl text-teal-400 mx-2" fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" viewBox="0 0 24 24" stroke="currentColor">
                    <path d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 2a2 2 0 11-4 0 2 2 0 014 0z"></path>
                </svg>
            </div>
    
            <div class="grid gap-6 grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 mt-8">
                <div class="p-6 bg-gray-300 border-b-2 border-teal-300 rounded-lg shadow-2xl" v-for="(cart,index) in carts" :key="index"> 
                    <div> 
                        <img class="h-64 mt-6 rounded-lg w-full object-cover" :src="cart.photo" alt="product">
                    </div>

                    <div class="border-b-2 border-teal-200">
                        <h1 class="my-5 font-semibold text-2xl text-teal-400">{{ cart.name }}</h1>
                    </div>

                    <div class="flex items-center justify-between mt-5">
                        <span class="font-medium text-teal-300">${{ cart.price }}</span>

                        <span class="font-medium text-teal-400">{{ subtotals[index] }}</span>

                        <div class="flex justify-between items-center -mx-1">
                            <svg @click="increment(cart,index)" class="h-5 w-5 cursor-pointer font-semibold text-xl text-teal-400 hover:text-teal-300 mx-1" fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" viewBox="0 0 24 24" stroke="currentColor">
                                <path d="M12 9v3m0 0v3m0-3h3m-3 0H9m12 0a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                            </svg>

                            <span class="font-mediumd text-teal-400">
                                {{ cart.quantity }}
                            </span>
                            
                            <svg @click="decrement(cart,index)" class="h-5 w-5 font-semibold text-xl text-teal-400 hover:text-teal-300 mx-1" fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" viewBox="0 0 24 24" stroke="currentColor">
                                <path d="M15 12H9m12 0a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                            </svg>
                        </div>
                    </div>                
                </div>
            </div>
        </div>
    </main>

    <footer class="bg-teal-900 mt-6">
        <div class="container mx-auto px-6 py-4 flex justify-between items-center">
            <div class="text-teal-200 font-semibold uppercase">total price</div>

            <span class="text-teal-200 font-semibold uppercase">${{ total }}</span>

            <p class="text-teal-200 font-semibold uppercase">Made With <span class="text-red-500 text-2xl">&hearts;</span>  By Hnooz</p>
        </div>
    </footer>
</div>
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
        };
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
};
</script>
