<template>
    <div id="sidebar" :class="{ active: isActive }">
        <div class="fixed">
            <div class="bar">
                <div class ="nav-button">
                    <svg class="plus" @click='showMenu' viewBox="0 0 100 100" version="1.1">
                        <g stroke-width="2.5" stroke="#000000" fill="#FFFFFF" fill-rule="nonzero">
                            <path d="M0,50 L100,50" id="Shape"></path>
                            <path d="M50,0 L50,100" id="Shape"></path>
                        </g>
                    </svg>
                </div>
                <div class='name-logo'>Peter Robe</div>
            </div>
            <div class="menu">
                <div class="background"></div>
                
                <div class="menu-container">
                    <div class="menu-item">
                        <div class="menu-icon"><img src="~/static/paper.png"/></div>
                        <p>Research</p>
                    </div>
                    <div class="menu-item">
                        <div class="menu-icon"><img src="~/static/paper.png"/></div>
                        <p>Research</p>
                    </div>
                    <div class="menu-item">
                        <div class="menu-icon"><img src="~/static/paper.png"/></div>
                        <p>Research</p>
                    </div>
                    <div class="menu-item">
                        <div class="menu-icon"><img src="~/static/paper.png"/></div>
                        <p>Research</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import gsap from 'gsap'

export default {
    
    components: {
        
    },
    data: function() {
        return {
            isActive: false,
            tween: new gsap.timeline({paused:true})
        }
    },
    mounted: function() {
        this.tween.set(".menu", { display: "flex" })

        this.tween.to(".plus", 0.3, { rotation: 135, ease: "power3.easeOut"})
        this.tween.from(".menu .background", 0.3, { width: 0, ease: "power3.easeOut"}, "<")

        this.tween.from(".menu-container", 0.3, { opacity: 0 })
        this.tween.from(".menu-container h2", 0.3, { y: -20, ease: "power3.easeOut"}, "<")
        this.tween.from(".menu-container p", 0.3, { y: 20, ease: "power3.easeOut", stagger: 0.04}, "<")

        this.tween.addPause(),

        this.tween.to(".menu-container p", 0.3, { y: 20, ease: "power3.easeOut", stagger: { each: 0.04, from: "end"}})
        this.tween.to(".menu-container h2", 0.3, { y: -20, ease: "power3.easeOut"}, "<")

        this.tween.to(".menu-container", 0.3, { opacity: 0 }, "-=0.2")
        this.tween.to(".menu .background", 0.3, { width: 0, ease: "power3.easeOut"}, "<")

        this.tween.to(".plus", 0.3, { rotation: 0, ease: "power3.easeOut"}, "<")
        
        this.tween.set(".menu", { display: "none" })
    },
    methods: {
        showMenu() {
            if(this.tween.isActive()) {
                return
            }
            if(this.isActive) {
                this.tween.play()
            } else {
                this.tween.restart()
            }
            this.isActive = !this.isActive;
        }
    }
}
</script>

<style lang='scss'>

$plus-padding: 20%;
$sidebar-width: 25%;
$sidebar-width-decimal: 0.25;

#sidebar {
    // sidebar at top on sm-
    position: relative;
    z-index: 1;
    width: 100%;
    height: $sidebar-thickness-top;
    flex-shrink: 0;

    @include md {
        // sidebar on left on md+
        position: relative;
        height: 100vh;
        width: $sidebar-thickness-left;
    }

    .fixed {
        position: fixed;
        height: inherit;
        width: inherit;

        display: flex;
        flex-flow: column;
        
        @include md {
            flex-flow: row;
        }
    }
}

.bar {

    border-bottom: solid 1px $line-color;

    @include md {
        border-bottom: none;
        border-right: solid 1px $line-color;
    }

    .nav-button {
        // Nav button is the square at the top left of the sidebar
        position: relative;
        width: $sidebar-thickness-top;
        height: $sidebar-thickness-top;

        // Sepatator is on the right on sm-
        border-right: solid 1px $line-color;

        @include md {
            width: $sidebar-thickness-left;
            height: $sidebar-thickness-left;

            // Separator is on the bottom on md+
            border-bottom: solid 1px $line-color;
            border-right: 0;
        }

        .plus {
            position: absolute;
            width: 100%;
            height: 100%;
            padding: $plus-padding;
            top: 0;
            left: 0;
            z-index: 2;

            g {
                transition: stroke 1s ease-in-out;
                stroke: white;

                #sidebar.active & {
                    stroke: white;
                }
            }
        }
    }
}

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
    color: $text-color;
    writing-mode: horizontal-tb;

    @include md {
        font-size: 34px;
        writing-mode: vertical-lr;
    }
}

.menu {
    justify-content: center;
    flex-grow: 1;
    display: none;
    position: absolute;
    top: 100%;
    left: 0;

    width: 100%;
    height: calc(100vh - #{$sidebar-thickness-top});
    color: white;

    @include md {
        width: calc(100vw - #{$sidebar-thickness-left});
        height: 100vh;
        top: 0;
        left: 100%;
    }

    .menu-container {
        display: flex;
        flex-flow: row wrap;
        position: relative;
        padding: 100px 100px;

        @include ultra {
                width: 100%;
            }

        .menu-item {
            
            width: 100%;
            position: relative;

            @include sm {
                width: 50%;
            }

            @include ultra {
                width: 25%;
            }

            .menu-icon {
                //Not perfect on mobile
                height: 90%;

                img {
                    object-fit: contain;
                    width: 100%;
                    height: 100%;
                    margin: 0;
                }
            }

            p {
                //Doesn't do anything
                height: 20%;
            }

            
        }


    }

    .background {
        position: absolute;
        width: 100%;
        height: 100%;
        background-color: #ed1d27;
    }


}
</style>
