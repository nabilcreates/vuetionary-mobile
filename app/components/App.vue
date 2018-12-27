<template>
    <Page>
        <ActionBar title="vuetionary" />

        <StackLayout class="main-body-wrapper">

            <GridLayout columns='5*,2*' rows='*' height='40'>
                <TextField v-model='word' hint="Enter text.." col='0' row='0' />
                <Button text="Get Meaning" @tap="getMeaning(word)" col='1' row='0' />
            </GridLayout>

            <ListView for="item in data">
                <v-template>
                    <GridLayout class="dict-items" columns='*' rows='*,*'>
                        <Label textWrap="true" class="message" :text="item.text" col="0" row="0" />
                    </GridLayout>
                </v-template>
            </ListView>

        </StackLayout>
    </Page>
</template>

<script>
    export default {
        data() {
            return {
                word: "random",
                data: [],
            }
        },

        methods: {
            getMeaning(word) {
                let api_key = '04a86ab529b55b53b900403b9530d0e05a753b7502b8eb1a7'
                fetch("https://api.wordnik.com/v4/word.json/" + word + "/definitions?api_key=" + api_key)


                    .then(response => response.json())
                    .then(json => {
                        this.data = json
                        console.log('done fetching' + word)
                    })
            }
        },
    }
</script>

<style scoped>
    ActionBar {
        background-color: #53ba82;
        color: #ffffff;
    }

    .message {
        vertical-align: center;
        text-align: center;
        font-size: 20;
        color: #333333;
    }

    .main-body-wrapper {
        margin: 20px;
    }

    .dict-items {
        margin: 20px 0;
    }

    .dict-items Label {
        text-align: left;
    }

    ListView {
        height: 100%;
    }
</style>