<template>
    <Page>
        <ActionBar title="NEWS">   
        </ActionBar>
        <FlexboxLayout flexDirection="row">
            <StackLayout orientation="vertical">
                <Image :src="item.imgsrc" width="100%" height="400" marginTop="10" stretch="aspectFill"/>
                <Label :text="item.title" fontSize="12" fontStyle="italic" class="title"  />
                <HtmlView :html="item.content" margin="10" fontSize="16" />
            </StackLayout>
            <StackLayout>
                <Label :text="item.content" />
            </StackLayout>
        </FlexboxLayout>
    </Page>
</template>
<script>
export default {
    props:["item"],
    data(){
        return {
        }
    }
}
</script>
<style scoped>
    .title {
        margin: 10 140;
    }
</style>