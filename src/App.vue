<template>
    <div id="app">
        <NavBarComponent id="navSpace"></NavBarComponent>
        <BlocklyComponent id="blocklySpace" :options="options"></BlocklyComponent>
    </div>
</template>

<script>

import Blockly from "blockly";
import NavBarComponent from "./components/NavigationBar/NavigationBar.vue";
import BlocklyComponent from "./components/BlocklyComponent.vue";

console.log("User is currently on platform", navigator.userAgent)


Blockly.Tooltip.HOVER_MS = 100;

import "./components/S4DDebugTool"

// Load blocks
import "./blocks/folders.js"
import "./prompt";
import Theme from '@blockly/theme-modern';

export default {
    name: "app",
    components: {
        BlocklyComponent,
        NavBarComponent
    },
    beforeCreate() {
        this.$root.$i18n.locale = this.$store.state.blocklyLocale;
    },
    mounted() {
        if (window.location.pathname == "/v2") {
            window.location.href = "https://www.youtube.com/watch?v=xvFZjo5PgG0"
        }
        if (window.location.pathname == "/broken") {
            window.location.href = "https://scratch-for-discord-broken.jeremygamer13.repl.co/"
        }
        if (window.location.href.includes("deploy-preview-469--scratch-for-discord.netlify.app")) {
            console.warn("Warning!")
            console.warn("You are using the Netlify site which has a risk of being deprecated.")
            console.warn("Please go to the Vercel site here:")
            console.log("https://scratch-for-discord-469.vercel.app/")
        }
        console.log("...wait a second... a user?")
        console.log("i gotta tell them!")
        console.log(
            "%cCAREFUL WHAT YOU TYPE IN CONSOLE! %cbarry and johnathan are watching all of your moves...",
            "color:red;font-family:system-ui;font-size:2rem;-webkit-text-stroke: 1px black;font-weight:bold",
            "color:DarkRed;font-family:system-ui;font-size:2rem;-webkit-text-stroke: 1px black;font-weight:bold"
        )
        console.log("...")
        for (let i = 0; i < 3; i++) {
            console.log("")
            console.log(
                "%cWARNING! %cIf you use S4D forums, be careful what you paste into here! You are most likely going to get your account hacked.",
                "color:red;font-family:system-ui;font-size:2rem;-webkit-text-stroke: 1px black;font-weight:bold",
                "color:white;font-family:system-ui;font-size:1.75rem;-webkit-text-stroke: 1px black;font-weight:bold"
            )
        }
        if (!("ScratchNative" in window) && window.parent?.ScratchNative) window.ScratchNative = window.parent.ScratchNative;
        const tourDone = localStorage.getItem('tourDone');
        if (tourDone !== null) this.$store.commit('setTour', {
            status: tourDone
        });
        const blocklyLocale = localStorage.getItem('blocklyLocale');
        if (blocklyLocale !== null) {
            this.$store.commit('setLocale', {
                newLocale: blocklyLocale
            });
            this.setLanguage(blocklyLocale);
        }

        if (!this.$store.state.tourDone) {
            this.$tours["start-tour"].start();
            this.$store.commit('setTour', {
                status: true
            });
        }
    },
    data() {
        //month starts at 0 day starts at 1
        if ((new Date().getMonth()) == 3 && ((new Date().getDate())) == 1) {
            return {
                options: {
                    renderer: "zelos",
                    theme: Theme,
                    collapse: true,
                    comments: true,
                    disable: true,
                    maxBlocks: Infinity,
                    trashcan: true,
                    horizontalLayout: false,
                    rtl: true,
                    zoom: {
                        controls: true,
                        startScale: 0.9,
                        maxScale: 3,
                        minScale: 0.3,
                        scaleSpeed: 1.2
                    }
                },
                move: {
                    scrollbars: {
                        horizontal: true,
                        vertical: true
                    },
                    drag: true,
                    wheel: true
                }
                /*
                ,
                    vueTourOptions: {
                        labels: {
                            buttonSkip: this.$t('tour.skip'),
                            buttonPrevious: this.$t('tour.previous'),
                            buttonNext: this.$t('tour.next'),
                            buttonStop: this.$t('tour.finish')
                        },
                        steps: [
                            {
                                target: '#v-step-0',
                                content: this.$t('tour.steps.load_examples'),
                                params: {
                                    enableScrolling: false
                                }
                            },
                            {
                                target: '#v-step-1',
                                content: this.$t('tour.steps.run_test'),
                                params: {
                                    enableScrolling: false
                                }
                            },
                            {
                                target: '#v-step-2',
                                content: this.$t('tour.steps.export_code'),
                                params: {
                                    enableScrolling: false
                                }
                            }
                        ]
                    }
                    */
            }
        } else {
            return {
                options: {
                    renderer: "zelos",
                    theme: Theme,
                    zoom: {
                        controls: true,
                        startScale: 0.9,
                        maxScale: 3,
                        minScale: 0.3,
                        scaleSpeed: 1.2
                    }
                },
                move: {
                    scrollbars: {
                        horizontal: true,
                        vertical: true
                    },
                    drag: true,
                    wheel: true
                }
                /*
                ,
                    vueTourOptions: {
                        labels: {
                            buttonSkip: this.$t('tour.skip'),
                            buttonPrevious: this.$t('tour.previous'),
                            buttonNext: this.$t('tour.next'),
                            buttonStop: this.$t('tour.finish')
                        },
                        steps: [
                            {
                                target: '#v-step-0',
                                content: this.$t('tour.steps.load_examples'),
                                params: {
                                    enableScrolling: false
                                }
                            },
                            {
                                target: '#v-step-1',
                                content: this.$t('tour.steps.run_test'),
                                params: {
                                    enableScrolling: false
                                }
                            },
                            {
                                target: '#v-step-2',
                                content: this.$t('tour.steps.export_code'),
                                params: {
                                    enableScrolling: false
                                }
                            }
                        ]
                    }
                    */
            }
        }
    }
}

</script>

<style>
#app {
    font-family: sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
}

#blocklySpace {
    position: absolute;
    width: 100%;
    height: calc(100% - 66px);
}

.boldtext {
    font-weight: bolder;
}

.testopa {
    opacity: 0.1;
}
</style>
