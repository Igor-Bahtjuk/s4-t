
<script lang="ts">
    import { hello } from "$lib";
    import AlertDialog from "$widgets/AlertDialog.svelte";
    import { onMount }  from "svelte";

    let version = 4;
    let array:number[] = [];

    // let ref:AlertDialog|null;

    onMount(()=>{

       
    })
    
    async function onClick(){
        version++;
        array = [...array,version]

        // let re = await ref?.open("Okay","okay","yes","no", (()=>{

        // }))
       
    }

</script>

   <div class="parent">

    <span>Svelete {version}</span>
    <i class={`fa-regular ${version % 2 == 0 ? "fa-heart" : "fa-star"} icons`}></i>

    <button on:click={onClick}>
        Hey
    </button>
    

    {#each array as item}
    <span>Svelete {item}</span>
    {/each}


    <!-- <AlertDialog bind:this={ref} ></AlertDialog> -->


   </div>


   <style>
    .icons{
        font-size: 50px;
        color: red;
    }
    .parent{
        padding-top: 25px;
        gap: 15px;
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
    }
    span{
        font-size: 31px;
    }
    button{
        cursor: pointer;
        width: 150px;
        height: 35px;
        border-radius: 5px;
        outline: none;
        border: none;
        background-color: var(--accentColor);
        color: white;
    }

   </style>


