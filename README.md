JSON-driven website: 
[Step 1](https://github.com/dr-matt-smith/FEDev-JSON-data-driven-website-step-1)
|
[Step 2](https://github.com/dr-matt-smith/FEDev-JSON-data-driven-website-step-2)
|
[Step 3](https://github.com/dr-matt-smith/FEDev-JSON-data-driven-website-step-3)


# FEDev-JSON-data-driven-website-step-4

![module list from JSON](/screenshots/6_all_modules_from_JSON.png)

Step-by-step development of a module details website. Routing in the form `/module/2037`


## 1: Creating our list of modules from the JSON array

Since we've easy access to the JSON array of modules, let's remove the hard-coding of module links in our module list page, and create those links by looping through the module objects.

We can use a Svelte `each` loop, to loop through each module object and display its properties. The general structure of a Svelte `each` loop is as follows:
```html
    {#each arrayName as objectName}
        --do things with objectName.field here--
        e.g. <p>{module.title}</p>
    {:else}
        output if array is empty
        e.g. <p>sorry - I couldn't dind any blog posts to dislay</p> 
    {/each}
```

Our array is named `modules`, so we'll use the singular in our `each` loop:
```html
    {#each modules as module}
    <li>
        <a href="/modules/{module.id}">{module.title}</a>
    </li>
    {:else}
    <li>
        ERROR - no modules found to list here !
    </li>
    {/each}
```

Update page `/routes/modules/+page.svelte`: as follows:

```html
<script>
    import modules from '$lib/data/modules.json';
</script>

<h1>Welcome to Modulesite</h1>

<p>Learn more about year 2 modules</p>
<ul>
    {#each modules as module}
    <li>
        <a href="/modules/{module.id}">{module.title}</a>
    </li>
    {:else}
    <li>
        ERROR - no modules found to list here !
    </li>
    {/each}
</ul>
```


## 2: Test all data-driven by adding details of another module to the JSON data

Update `/lib/data/modules.json` to add details of a 4th module:

```json
[
    {
        "id": 2027,
        "title": "H2027 Front End Development",
        "details": "learn about Svelte and SvelteKit for dynamic website development"
    },
    {
        "id": 2029,
        "title": "COMP H2029 Database Fundamentals",
        "details": "learn about H2029 Database Fundamentals"
    },
    {
        "id": 2031,
        "title": "COMP H2031 Object-Oriented Programming",
        "details": "learn OO Java programming stuff"
    },
    {
        "id": 101,
        "title": "CS-101: Introduction to Computing",
        "details": "if we were a US university, we'd have a 101 module like this for anyone in the university to learn about computing ..."
    }
]
```
