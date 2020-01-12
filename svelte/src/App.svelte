<script>
    let output;
    async function getTodo() {
        const response = await fetch('http://localhost:5000/todos', {
            method:'GET',
            mode: 'cors',
            headers:{
                'Access-Control-Allow-Origin':'*',
                'Access-Control-Allow-Headers':'*'
            },
            body: null
        })
        const todo = await response.json()
        console.log(todo)
        output = todo;
        if (response.ok) {
            output = Object.values(todo)
            return Object.values(todo)
        } else {
            throw new Error(todo)
        }
    }
    let myTodo = getTodo()
</script>

{#await myTodo}
    <p>...waiting</p>
{:then tadaaam}
    <pre>{JSON.stringify(tadaaam, null,4)}</pre>
    {#each output as a}
        <p>{a.task}</p>
    {/each}
{:catch error}
    <p style="color: red">{error.message}</p>
{/await}


<!-- (async () => { -->
    <!-- let data = {'hash': 'asas','prevHash': 'sddsd'} -->
    <!-- const rawResponse = await fetch('http://localhost:1337/data', { -->
      <!-- method: 'POST', -->
      <!-- headers: { -->
        <!-- 'Accept': 'application/json', -->
        <!-- 'Content-Type': 'application/json' -->
      <!-- }, -->
      <!-- body: JSON.stringify(data) -->
    <!-- }); -->
    <!-- const content = await rawResponse.json(); -->
  <!--  -->
    <!-- console.log(content); -->
  <!-- })(); -->
