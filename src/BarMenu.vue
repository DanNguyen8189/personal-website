/*Template for menu across the top*/
<template>
    <div>
        <img id='signature' src='http://i.imgur.com/EglY7hp.png' style='width:10%;height:10%;'>
        <ul id= 'navigationlinks'>
            <!--create a button for each item in menuItems, which was passed down from Navigation-component-->
            <li v-for='item in menuItems' 
                :key = 'item.id'
                :class="{ 'active': (item === mutableSelected) }">
                    <button @click = 'mutableSelected = item; goTo(item.route)'>{{ item.id }}</button>
            </li>
        </ul>
    </div>
</template>

<script>
export default{
    data(){
        return{
            mutableSelected: this.selected,
            /*Inline props are same as an immutable value, 
            because every time the parent re-renders, the mutated child prop will be reset back to the inline value. 
            If you want to allow inline props as the initial value, declare a field in your data that uses the 
            props value*/
        }
    },
    /*data expected from parent component (Navigation-component)*/ 
    props:{
        selected: {
            type: String,
            required: true
        },
        menuItems: {
            type: Array,
            required: true
        },
    },
    methods:{
        /*goHome(){
            this.$router.push('/');
        },
        goAbout(){
            this.$router.push('/about');
        },*/
        goTo(routeDirection){
            this.$router.push(routeDirection);
        }
    }
}
</script>

<style scoped>
#signature{
    left: 15px;
    float: left;
    margin: 0;
    min-width: 200px;
    max-width: 200px;
    min-height: 120px;
    max-height: 120px;
    opacity: 0.6;
}
@media screen and (min-aspect-ratio: 1/1){
    #signature{
        min-width: 120px;
        max-width: 120px;
        min-height: 72px;
        max-height: 72px;
    }
}
#navigationlinks{
    display: inline-block;
    padding: 0;
    margin: 0;
    margin-top: 7px;
} 
#navigationlinks li{
    float:left; /*determines order of the links. Floating right does it backwards*/
    list-style:none;
    font-size: inherit;
    font-family: inherit;
    color: rgba(255, 255, 255, 0.74);
    box-sizing: border-box;
} 

#navigationlinks button{
    background: none;
    border: none;
    text-shadow:0px 1px 0px rgba(0,0,0,0.5);
    color: inherit;
    transition: inherit;
    padding: 25px 32px;
}
@media screen and (min-aspect-ratio: 1/1){
    #navigationlinks button{
        padding: 12px 32px;
    }
}
#navigationlinks button:hover, #navigationlinks button:active{
    background-color: rgba(255, 255, 255, 0.055);
    text-decoration:underline;
    outline: 2px double rgba(126, 211, 180, 0.5);
    color:#7ed3b4;
}
button:focus {
    outline-color:aquamarine;
}
.active{
    color: #7ed3b4 !important; 
    font-weight: bold;
}
</style>

