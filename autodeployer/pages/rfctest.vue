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
            const reader=new NDEFReader()

            await reader.scan()
            reader.addEventListener("error", ()=>{this.rfctest="えらー"})

            reader.addEventListener("reading", (message, serialNumber)=>{
                this.rfctest=`${message}-${serialNumber}`
            })
        }catch{
            this.rfctest="きゃっち"
        }
    }
}
</script>