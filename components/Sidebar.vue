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
                <a class='name-logo' href="/">Peter Robe</a>
            </div>
            <div class="menu">
                <div class="background"></div>  
                <div class="menu-container">
                    <div class="name">
                        <h2>PR</h2>
                    </div>
                    <div class="menu-item nav">
                        <a href="about">Machine Learning</a>
                        <a href="resume">Game Engine</a>
                        <a href="contact">Research</a>
                        <a href="soft">Software Dev</a>
                    </div>
                    <div class="menu-item contact">
                        <a href="about">About</a>
                        <a href="resume">Resume</a>
                        <a href="contact">Contact</a>
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
        this.tween.set(".menu", { display: "block" })

        this.tween.to(".plus", 0.3, { rotation: 135, ease: "power3.easeOut"})
        this.tween.from(".menu .background", 0.3, { scaleX: 0, ease: "power3.easeOut"}, "<")

        this.tween.from(".menu-container", 0.3, { opacity: 0 })
        this.tween.from(".menu-icon img", 0.3, { y: -20, ease: "power3.easeOut"}, "<")
        this.tween.from(".menu-label p", 0.3, { y: 20, ease: "power3.easeOut", stagger: 0.04}, "<")

        this.tween.addPause(),

        this.tween.to(".menu-label p", 0.3, { y: 20, ease: "power3.easeOut", stagger: { each: 0.04, from: "end"}})
        this.tween.to(".menu-icon img", 0.3, { y: -20, ease: "power3.easeOut"}, "<")

        this.tween.to(".menu-container", 0.3, { opacity: 0 }, "<")
        this.tween.to(".menu .background", 0.3, { scaleX: 0, ease: "power3.easeOut"})

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

$menu-padding: 10%;
$menu-spacing: 10vw;
$menu-padding-spacing-md: 10vmin;

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
    text-decoration: none;

    @include md {
        font-size: 34px;
        writing-mode: vertical-lr;
    }
}

.menu {
    display: block;
    position: absolute;
    top: 100%;
    left: 0;
    visibility: none;

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
        display: grid;
        grid-gap: 0 40px;
        align-items: unset;
        position: relative;
        top: 50%;
        left: 50%;
        width: fit-content;
        transform: translate(-50%, -50%);

        &::-webkit-scrollbar {
            width: 0px;  /* Remove scrollbar space */
            background: transparent;  /* Optional: just make scrollbar invisible */
        }

        .menu-item {
            width: 100%;
            display: flex;
            flex-direction: column;
            justify-content: center;
            z-index: 1;

            > * {
                transition: transform 0.2s, color 0.2s;
                padding: 5px 0;
                font-family: Roboto;
                font-weight: 100;
                color: white;
                text-decoration: none;
                font-size: 50px;

                &:hover {
                    transform: translateX(10px);
                }
            }

            h4 {
                font-size: 18px;
                font-family: 'SuisseIntl-Book';

                @include sm {
                    font-size: 20px;
                }
                
                @include md {
                    font-size: 1.8vw;
                }
            }
        }

        .name {
            position: relative;
            grid-column-start: 1;
            grid-row-start: 1;
            line-height: 190px;
            font-size: 220px;
            font-weight: 800;
            font-family: 'Kanit';
            margin-left: -10px;
        }

        .nav {
            grid-column-start: 1;
            grid-row-start: 2;
            margin-top: 20px;
        }

        .contact {
            grid-column-start: 2;
            grid-row-start: 1;
        }
    }

    .background {
        position: absolute;
        width: 100%;
        height: 100%;
        transform-origin: left;
        background-color: #000000;
        //background-image: url("~static/The Network.png");
    }
}
</style>
