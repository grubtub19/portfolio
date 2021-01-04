<template>
    <div id="sidebar" :class="{ active: isActive }">
        <div class="fixed">
            <div class="sidebar-overlay" @click='showMenu'></div>
            <svg class="plus" @click='showMenu' viewBox="0 0 100 100" version="1.1">
                <g stroke-width="2.5" stroke="#000000" fill="#FFFFFF" fill-rule="nonzero">
                    <path d="M0,50 L100,50" id="Shape"></path>
                    <path d="M50,0 L50,100" id="Shape"></path>
                </g>
            </svg>
            <div class='name-logo'>Peter Robe</div>
            <div class="sidebar-content">
                <h2>Peter Robe</h2>
                <span>Graduate Research Assistant</span>
                    <span>University of Tulsa</span>
            </div>
        </div>
    </div>
</template>
<script>


export default {
    components: {
        
    },
    data: function() {
        return {
            isActive: false
        }
    },
    methods: {
        showMenu() {
            this.isActive = !this.isActive;
        }
    }
}
</script>


<style lang='scss'>
$plus-size: 30px;
$plus-size-md: 50px;
$sidebar-width: 25%;
$sidebar-width-decimal: 0.25;

#sidebar {
    position: absolute;
    z-index: 1;
    width: 100vw;
    height: $sidebar-thickness-top;
    flex-shrink: 0;

    @include md {
        position: relative;
        height: 100vh;
        width: $sidebar-thickness-left;
    }

    .fixed {
        position: fixed;
        height: inherit;
        width: inherit;

        .name-logo {
            position: absolute;
            left: 50%;
            top: 50%;
            transform: translate(-50%, -50%);
            font-weight: 700;
            font-size: 19px;
            line-height: 30px;
            font-family: Muli, Helvetica Neue, Arial, sans-serif;
            z-index: 1;
            color: black;
            writing-mode: horizontal-tb;
            @include md {
                font-size: 34px;
                writing-mode: vertical-lr;
            }
        }
    }
}

.plus {
    transition: all 0.8s cubic-bezier(0.37, -0.04, 0.25, 1);
    position: absolute;
    width: $plus-size;
    height: $plus-size;
    margin: calc((#{$sidebar-thickness-top} - #{$plus-size}) / 2);
    top: 0;
    //left: calc(100% - #{$sidebar-thickness-top});
    left: 0;
    z-index: 2;

    @include md {
        width: $plus-size-md;
        height: $plus-size-md;
        margin: calc((#{$sidebar-thickness-left} - #{$plus-size-md}) / 2);
    }

    g {
        transition: stroke 1s ease-in-out;
        stroke: black;

        #sidebar.active & {
            stroke: white;
        }
    }
}

.sidebar-overlay {
    position: fixed;
    width: 100vw;
    height: 100vh;
    transition: opacity 0.8s cubic-bezier(0.35, 0, 0.25, 1);
    background-color: black;
    opacity: 0%;
    pointer-events: none;

    #sidebar.active & {
        opacity: 40%;
        pointer-events: auto;
    }
}

.sidebar-content {
    transition: all 0.8s cubic-bezier(0.35, 0, 0.25, 1);
    position: fixed;
    background-color: black;
    top: 0;
    left: -100%;
    width: 100%;
    height: 100vh;
    padding: 180px 30px 0 30px;
    color: white;

    @include sm {
        // sidebar - 25% of the area excluding the sidebar
        //left: calc(-#{$sidebar-thickness-left} - (100% - #{$sidebar-thickness-left}) * #{$sidebar-width-decimal});
        //width: calc(#{$sidebar-thickness-left} + (100% - #{$sidebar-thickness-left}) * #{$sidebar-width-decimal});
        left: -$grid-5;
        width: $grid-5;
    }

    #sidebar.active & {
        left: 0;
    }
}

#__layout {
    @include md {
        flex-direction: row!important;
    }
}
</style>
