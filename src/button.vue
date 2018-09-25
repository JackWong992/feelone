<template>
    <button class="g-button" :class="{[`icon-${iconPosition}`]: true}"
    @click="$emit('click')">
        <g-icon  class="icon" :name="icon" v-if="icon && !loading "></g-icon>
        <g-icon  name="loading" class="loading icon" v-if="loading"></g-icon>
        <div class="content">
            <slot></slot>
        </div>
    </button>
</template>
<script>
    import  Icon from './icon'
    export  default  {
        components: {
            'g-icon': Icon
        },
        props:{
            icon: {},
            loading: {
                type: Boolean,
                default: false
            },
            iconPosition: {
                type: String,
                default: 'left',
                validate(value){
                    if( value !== 'left' && value !=='right'){
                        return false
                    }else{
                        return true
                    }
                }
            }
        }
    }
</script>

<style lang="scss">
    @keyframes spin {
        0%{ transform: rotate(0deg); }
        100%{ transform: rotate(360deg) }
    }
    .g-button{
        font-size: var(--font-size);
        height: var(--button-height);
        padding: 0 1em;
        font: inherit;
        border-radius: var(--border-radius);
        border: 1px solid var(--border-color);
        background: var(--button-bg);
        display: inline-flex;
        vertical-align: middle;//解决inline-flex带来的按钮不对齐
        justify-content: center;
        align-items: center;
        &:hover {border-color: var(--border-color-hover);}
        &:active {background-color: var(--button-active-bg);}
        &:focus {outline: none;}
        > .content{ order: 2; }
        > .icon{ order: 1;margin-right: .1em;}
        &.icon-right{
            > .content{order: 1;}
            >.icon{order: 2; margin-left:.1em;margin-right: 0;}
        }
        .loading{
            animation: spin 1s infinite linear;
        }
    }


</style>