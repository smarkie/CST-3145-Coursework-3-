<template>
    <div id="checkoutComponent">
        
        <!-- //Checkout Component Displaying orders -->
        <form action="">
            <div class="row col-lg-12  container" id="checkout">
                <div class="col-lg-4">
                    <h3>Checkout Page</h3>

                    <div class="form-group">
                        <label for="firstName">First Name:
                            <input required v-model="order.firstName" type="text">
                    </label>
                    </div>
                    <div class="form-group">
                        <label for="lastName">Last Name:
                            <input required v-model="order.lastName" type="text">
                        </label>
                    </div>
                    <div class="form-group">
                        <label for="phone">Phone Number:
                            <input id="phone" required v-model="order.phone" type="text">
                        </label>
                    </div>
                    <div class="form-group">
                        <label for="year">Acacdemic Year:
                            <select v-model="order.year">
                                <option value="">-</option>
                                <option> 1 </option>
                                <option> 2 </option>
                                <option> 3 </option>
                                <option> 4 </option>
                                <option> 5 </option>
                                <option> 6 </option>
                                <option> 7 </option>
                                <option> 8 </option>
                                <option> 9 </option>
                                <option> 10 </option>
                            </select>
                        </label>
                    </div>
                </div>
                <div class="col-lg-4">
                    
                    <!-- Displaying all the selected lessons-->
                    <h3>Invoice</h3>
                    <p>Name: {{order.firstName}} {{order.lastName}} </p>
                    <p>Phone: {{order.phone}}</p>
                    <p>Acacdemic Year: {{order.year}} </p>

                    <p>Total price: {{order.totalPrice}}</p>
                    <button v-if="canPlaceOrder" @click="placeOrder" type="submit" class="btn btn-info"> Place the order</button>
                    <button v-else  class="btn disabled btn-secondary">Place order</button>
                </div>
                <div class="col-lg-4">
                    <h3>Order List</h3>
                    <div class="" v-for="(cartItem, i) in cartItems" v-bind:key="i">
                        <div class=""><p>Location: {{cartItem.location}}</p> <p>Lesson: {{cartItem.topic}}</p> <p>Space: {{cartItem.space}}</p>    </div>
                        
                         <!-- Remove button -->
                         <a @click="removeFromCart(cartItem)" class=" btn btn-danger"> Remove </a>
                    </div>
                </div>
            </div>
        </form>
    </div>
</template>

<!-- Passing shopping cart as prop-->
<script>
    export default {
        name: 'checkoutComponent',
        props: {
            cartItems: Array
        },
        data() {
            return {
                order:{
                    firstName:"",
                    secondName:"",
                    phone:"",
                    year:"",
                    isGift:"Purchase as a gift",
                    isNotGift:"Purchase for yourself",
                    totalPrice:0,
                },
            }
        },
        
        methods : {
            removeFromCart(product) {
                this.$emit('removeFromCart',product);
            },

            placeOrder: (e) => { 
                alert('The order has been placed!')
                e.preventDefault();
            },
        },

        computed: { // the Computed Property object
            canPlaceOrder:function() {
                console.log(this.order.phone)

                if ((this.order.firstName && this.order.lastName && this.order.phone) && (!isNaN((this.order.phone)))) {
                    return true;
                    }
                else{
                    return false;
                }
            },

        }
    }
</script>
