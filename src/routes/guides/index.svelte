<script context="module">
    export async function load({ fetch }) {
        // const res = await fetch('https://jsonplaceholder.typicode.com/posts')
        const res = await fetch('/guides.json')
        const {guides}  = await res.json() 
        console.log(guides)

        if(res.ok){
            return {
                props:{
                    guides
                }
            }
        }
        return{
            status: res.status,
            error: new Error ('Could not fetch the guides')
        }
    }
</script>

<script>
    export let guides


</script>
<div class="guides">
    <ul>
        <!-- <li><a href="/">Home 1</a></li>
        <li><a href="/">Home 2</a></li> -->
        {#each guides as guide}
        <li>
            <a sveltekit::prefetch href={`/guides/${guide.id}`}>{guide.title}</a>
        </li>
        {/each}
    </ul>
</div>

<style>
    .guides {
        margin-top: 20ox;
    }
    ul  {
        list-style-type: none;
        padding:0;
    }
    a {
        display: inline-block;
        margin-top: 10px;
        padding: 10px;
        border: 1px dotted rgb(255,255,255,0.2);

    }
</style>