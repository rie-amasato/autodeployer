<template>
    <div>{{rfctest}}</div>
</template>

<script>
export default{
    data(){ 
        return {    
            rfctest: "てすと"
        }
    },
    async mounted(){
        try{
            console.log("TRY")
            const reader=new NDEFReader()

            await reader.scan()
            reader.addEventListener("error", ()=>{this.rfctest="えらー"})

            reader.addEventListener("reading", (message, serialNumber)=>{
                console.log("READING")
                this.rfctest=`${message}-${serialNumber}`
            })
        }catch{
            console.log("CATCH")
            this.rfctest="きゃっち"
        }
    }
}
</script>