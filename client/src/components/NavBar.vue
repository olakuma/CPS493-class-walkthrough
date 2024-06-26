<script setup lang="ts">
import { ref } from 'vue';
import { RouterLink } from 'vue-router'; 
import LoginBadge from './LoginBadge.vue';
import FlyoutPanel from './FlyoutPanel.vue';
import ShoppingCart from './ShoppingCart.vue';
import { count as cartCount } from "@/model/shoppingCart"

const isActive = ref(false);
const isShoppingCartOpen = ref(false);

</script>

<template>
    <nav class="navbar" role="navigation" aria-label="main navigation" :class="{ isShoppingCartOpen }">
        <div class="navbar-brand">
            <a class="navbar-item">
                <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="28" height="28" />
            </a>

            <a role="button" class="navbar-burger" :class="{ 'is-active': isActive }" @click="isActive = !isActive" aria-label="menu" aria-expanded="false" data-target="navbarBasicExample">
                <span aria-hidden="true"></span>
                <span aria-hidden="true"></span>
                <span aria-hidden="true"></span>
            </a>
        </div>

        <div id="navbarBasicExample" class="navbar-menu" :class="{ 'is-active': isActive }">
            <div class="navbar-start">
                <RouterLink class="navbar-item" to="/">Home</RouterLink>
                <RouterLink class="navbar-item" to="/about">About</RouterLink>
                <RouterLink class="navbar-item" to="/products">Products</RouterLink>
                <RouterLink class="navbar-item" to="/map">Map</RouterLink>

                <div class="navbar-item has-dropdown is-hoverable">
                    <a class="navbar-link">
                        More
                    </a>

                    <div class="navbar-dropdown">
                        <a class="navbar-item">
                            About
                        </a>
                        <a class="navbar-item">
                            Jobs
                        </a>
                        <a class="navbar-item">
                            Contact
                        </a>
                        <hr class="navbar-divider">
                        <a class="navbar-item">
                            Report an issue
                        </a>
                    </div>
                </div>
            </div>

            <div class="navbar-end">
                <div class="navbar-item">
                    <a class="button" :class="{ 'is-active': isShoppingCartOpen }" @click.prevent="isShoppingCartOpen = !isShoppingCartOpen">
                        <span class="icon">
                            <i class="fas fa-shopping-cart"></i>
                        </span>
                        <i class="tag is-danger is-rounded is-small" v-if="cartCount">{{ cartCount }}</i>
                    </a>
                </div>
                <div class="navbar-item">
                    <LoginBadge />
                </div>
            </div>
        </div>
    </nav>
    <FlyoutPanel :class="{ 'is-active': isShoppingCartOpen }">
        <ShoppingCart />
    </FlyoutPanel>
</template>


<style scoped>
    @media (min-width: 641px){
        .navbar {
            margin-right: 2rem;
            transition: margin-right 0.5s ease-in-out;
        }
        .navbar.isShoppingCartOpen {
            margin-right: 20rem;
        }
    }

    .tag.is-small {
        position: absolute;
        transform: translate(50%, -30%);
        font-size: x-small;
    }

    .router-link-active {
        font-weight: bold;
        border-bottom: 2px solid #00d1b2;
    }
</style>
