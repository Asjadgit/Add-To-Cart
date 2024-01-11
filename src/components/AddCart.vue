<template>
    <button @click="toggleSidebar">Show Cart</button>
    <div class="main">
        <div class="fruit">
            <h1>Cherry</h1>
            <img src="@/assets/cherry-removebg-preview.png" alt="Cherry">
            <h4>Price : $4</h4>
            <label for="qty-cherry">Qty</label>
            <input type="number" placeholder="Enter Qty" id="qty-cherry" v-model="qty"><br><br>
            <button @click="addToCart('Cherry',4,qty)">Add to Cart</button>
        </div>

        <div class="fruit">
            <h1>Strawberry</h1>
            <img src="@/assets/strawberry-removebg-preview.png" alt="Strawberry">
            <h4>Price $6</h4>
            <label for="qty-strawberry">Qty</label>
            <input type="number" placeholder="Enter Qty" id="qty-strawberry" v-model="qty"><br><br>
            <button @click="addToCart('Strawberry',6,qty)">Add to Cart</button>
        </div>

        <div class="fruit">
            <h1>Kiwi</h1>
            <img src="@/assets/kiwi-removebg-preview.png" alt="Kiwi">
            <h4>Price : $10</h4>
            <label for="qty-kiwi">Qty</label>
            <input type="number" placeholder="Enter Qty" id="qty-kiwi" v-model="qty"><br><br>
            <button @click="addToCart('Kiwi',19,qyu)">Add to Cart</button>
        </div>

        <div class="sidebar" v-show="showSidebar">
            <div class="cart-items">
                <div v-for="(item, index) in cartItem" :key="index">
                    Item Name : {{ item.name }} - Qty: {{ item.qty }} - Total: ${{ item.totalPrice }}
                </div>
            </div>
            <button @click="toggleSidebar">Close</button>
        </div>
    </div>
</template>


<script>
export default{
    data(){
        return {
            qty: 0,
            cartItem: [],
            showSidebar: false 
        }
    },
    methods : {
        addToCart(name,price,qty){
            const totalPrice = price * qty;

            const existFruit = this.cartItem.findIndex(item=>item.name === name);
            if(existFruit !== -1){
                this.cartItem[existFruit].qty += qty;
                this.cartItem[existFruit].totalPrice += totalPrice;
            }else{
                this.cartItem.push({name,qty,totalPrice});
            }
            
        },
        toggleSidebar() {
            this.showSidebar = !this.showSidebar;
        }
    }
}

</script>
<style>
.main {
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
}

.fruit {
    width: 300px;
    height: 350px;
    /* Increased height to accommodate the image */
    border: 2px solid #000;
    margin: 10px;
    text-align: center;
}

.fruit img {
    max-width: 35%;
    max-height: 40%;
}

#qty-cherry,
#qty-strawberry,
#qty-kiwi {
    width: 80px;
    margin-left: 10px;
    padding: 5px 8px;
}

button {
    width: 120px;
    padding: 5px 10px;
    cursor: pointer;
    background-color: #91291a;
    border-radius: 8px;
    border: none;
    color: white;
    /* Add text color */
    margin-top: 10px;
    /* Add some space between input and button */
}
.sidebar {
    z-index: 1;
    transition: ease-in-out 0.4s;
}
</style>
