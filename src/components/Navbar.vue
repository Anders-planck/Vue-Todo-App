<template>
<header>
    <nav>
        <router-link to="/" class="logo">
            TODO
        </router-link>
        <div class="links" v-show="!mobile">
            <ul>
                <router-link to="/" class="link">Home</router-link>
                <router-link to="/services" class="link">Services</router-link>
                <router-link to="/about" class="link">About</router-link>
                <router-link to="/loginRegister" class="link">Login/Register</router-link>
            </ul>
        </div>
    </nav>
    <menuIcon class="menuIcon" @click="toogleNavMobile" v-show="mobile"/>
    <transition name="navMobile">
        <div class="navMobile" v-show="navMobile">
            <router-link to="/" class="logo">
                TODO
            </router-link>
            <ul class="links">
                <router-link to="/" class="link">Home</router-link>
                <router-link to="/services" class="link">Services</router-link>
                <router-link to="/about" class="link">About</router-link>
                <router-link to="/loginRegister" class="link">Login/Register</router-link>
            </ul>
        </div>
    </transition>
    
</header>
</template>

<script>
import menuIcon from '@/components/Icons/menuIcon'

export default {
    name:'Navbar',
    components:{
        menuIcon,
    },
    created(){
        window.addEventListener('resize',this.checkScreen)
        this.checkScreen()
    },
    data(){
        return{
            mobile:null,
            navMobile:null,
            window:null,
        }
    },
    methods:{
        toogleNavMobile(){
            this.navMobile=!this.navMobile
        },
        checkScreen(){
            this.window=window.innerWidth
            if(this.window <= 750){
                this.mobile=true
                return
            }else{
                this.mobile=false
                this.navMobile=false
                return
            }
        }
    }
}
</script>

<style lang="scss">

*{
    margin: 0;
    padding: 0;
}

header{
    padding: 1rem 2rem;
    position: relative;
    box-shadow: 10px 9px 26px 5px rgba(237,237,237,0.56);
    nav{
        width: 80%;
        margin: 0 auto;
        display: flex;
        align-items: center;
        justify-content: space-between;
        .logo{
            flex: 0.3;
            font-size: 2rem;
            font-weight: 700;
            color:#2c3e50;
            text-decoration: none;
            &:hover{
                color: #42b983;
            }
        }
        .links{
            flex: 0.4;
            ul{
                display: flex;
                align-items: center;
                .link{
                    font-weight: bold;
                    color: #2c3e50;
                    text-decoration: none;
                    font-size: 1.2rem;
                    margin-right: 1.5rem;
                    text-transform: uppercase;
                    &:last-child{
                        margin-right: 0;
                    }
                    &.router-link-exact-active {
                        color: #42b983;
                    }
                    &:hover{
                        color: #42b983;
                    }
                }
            }
        }
    }
    .menuIcon{
        position: fixed;
        top: 1.5rem;
        right: 3rem;
    }

    .navMobile{
        position: fixed;
        top: 0;
        left: 0;
        background: #2c3e50;
        color: #ecf0f1;
        display: flex;
        flex-direction: column;
        width: 250px;
        height: 100vh;
        .logo{
            flex: 0.03;
            font-size: 2rem;
            font-weight: 900;
            padding: 1rem;
            text-align: center;
            color:#ecf0f1;
            text-decoration: none;
            &:hover{
                color: #42b983;
            }    
        }
        .links{
            display: flex;
            flex-direction: column; 
            padding:1rem;
            .link{
                font-weight: bold;
                color: #ecf0f1;
                text-decoration: none;
                font-size: 1.2rem;
                border-radius: 5px;
                padding: 1rem 0;
                text-transform: uppercase;
                margin:  0.1rem;
                transition: all 0.1s ease-in-out;
                &:last-child{
                    margin:  0;
                }
                &.router-link-exact-active {
                    color: #42b983;
                    transform: scale(1.05);
                    transform: translateX(2rem);
                }
                &:hover{
                    color: #42b983;
                    transform: scale(1.05);
                    transform: translateX(2rem);
                }
            }   
        }
    }
    .navMobile{
        max-width: 250px;
    }
    .navMobile-enter-active,
    .navMobile-leave-active{
        transition: all 1s ease-in-out;
    }

    .navMobile-enter{
        transform: translateX(-250px);
        opacity: 0;
    }
    .navMobile-enter-to{
        transform: translateX(0);
        opacity: 1;
    }
    .navMobile-leave-to{
        transform: translateX(-250px);
        opacity: 0;
    }
    .navMobile-leave{
        transform: translateX(0);
        opacity: 1;
    }
}

</style>