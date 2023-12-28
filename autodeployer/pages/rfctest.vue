<template>
    <div>
    <div @click="click_scanstart">Start_Scan</div>
    {{rfctest}}
    </div>
</template>

<script>
export default{
    data(){ 
        return {    
            rfctest: "てすと"
        }
    },
    methods: {
        async click_scanstart(){
            try{
                console.log("TRY")
                this.rfctest="mounted"
                const reader=new NDEFReader()

                await reader.scan()

                console.log(reader)
                reader.addEventListener("readingerror", (e)=>{this.rfctest+=`えらー: ${e}`})

                reader.addEventListener("reading", (e)=>{
                    console.log("READING")
                    const ndefmessage=e.message
                    this.rfctest+=`Succeed: ${ndefmessage.records[0].data}-${ndefmessage.records[0].encoding}-${e.serialNumber}`
                })
            }catch(e){
                console.log("CATCH",e)
                this.rfctest+=`きゃっち-${e}`
            }
        }
    }
}
</script>