<template>
    <div id="select-view">
        <h1 id="lang-title" v-italic>{{ texts.title }}</h1>

        <div id="select">
            <l-select-lang
                    v-for="lang of content"
                    v-text="lang.name"

                    :selected="lang.code === selected"

                    @select="select(lang.code)"
            />
        </div>

        <l-power-button id="back" type="back" />
    </div>
</template>

<script>
    import LPowerButton from '@/components/PowerButton';
    import LSelectLang from '@/components/SelectLang';
    import { save, settings } from '@/settings';
    import { languages, trans } from '@/translations';

    export default {
        name: 'l-lang-select',
        components: { LPowerButton, LSelectLang },
        data() {
            return {
                content: languages || [],
                selected: settings.language || "",
                texts: {
                    title: trans('languages')
                }
            }
        },

        methods: {
            select(lang) {
                settings.language = lang;
                save();
                this.$router.back();
            }
        }
    }
</script>

<style lang="scss" scoped>
    @import "../theme";

    #select-view {
        font-family: 'Lato', 'Noto Sans', sans-serif;
        font-weight: 300;

        color: $outer-foreground;

        display: flex;
        flex-direction: column;
        justify-content: space-between;
        align-items: center;
    }

    #lang-title {
        font-size: 72px;
        font-weight: 300;
        margin-top: 7vh;
    }

    #select {
        display: flex;
        flex-wrap: nowrap;
        flex-direction: column;
        overflow: auto;

        font-family: 'Lato', 'Noto Sans', sans-serif;
        font-weight: normal;
        font-size: 44px;

        text-align: center;
        margin-bottom: 7vh;
    }
</style>
