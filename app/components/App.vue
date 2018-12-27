<template>
    <Page>
        <ActionBar title="vuetionary" />

        <StackLayout>

            <GridLayout columns='4*,*' rows='*' height='40'>
                <TextField v-model='word' hint="Enter text..." col='0' row='0' />
                <Button text="WDIM?" @tap="getMeaning(word)" col='1' row='0' />
            </GridLayout>

            <StackLayout>
                <ListView for="item in data">
                    <v-template>
                        <GridLayout rows='*,*' columns='*' class='list-group-item'>
                            <Label textWrap="true" class="message" :text="item.text" col="0" row="1" />
                        </GridLayout>
                    </v-template>
                </ListView>
            </StackLayout>

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

        mounted() {
            this.getMeaning(this.word);
        }
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
</style>