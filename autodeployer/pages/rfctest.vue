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
                reader.addEventListener("readingerror", (e)=>{this.rfctest+=`えらー-${e}`})

                reader.addEventListener("reading", (message, serialNumber)=>{
                    console.log("READING")
                    this.rfctest+=`${message}-${serialNumber}`
                })
            }catch(e){
                console.log("CATCH",e)
                this.rfctest+=`きゃっち-${e}`
            }
        }
    }
}
</script>