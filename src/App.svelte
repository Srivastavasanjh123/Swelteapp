<script>
    let services = [];
    let name = '';
    let description = '';
    let price = '';

    const addService = () => {
        if (!name || !description || !price) {
            alert("All fields are required!");
            return;
        }
        
        services = [...services, { id: Date.now(), name, description, price }];
        name = '';
        description = '';
        price = '';
    };

    const deleteService = (id) => {
        services = services.filter(service => service.id !== id);
    };

    const updateService = (id) => {
        const serviceToUpdate = services.find(service => service.id === id);
        name = serviceToUpdate.name;
        description = serviceToUpdate.description;
        price = serviceToUpdate.price;
        deleteService(id);
    };

    const autoResize = (event) => {
        const textarea = event.target;
        textarea.style.height = 'auto'; // Reset height to auto to calculate the new height
        textarea.style.height = `${textarea.scrollHeight}px`; // Set the height based on scrollHeight
    };
</script>

<style>
    main {
        text-align: center;
        padding: 2rem;
        max-width: 600px;
        margin: auto;
    }

    form {
        display: flex;
        flex-direction: column;
        gap: 1rem;
    }

    input, textarea {
        padding: 0.5rem;
        border: 1px solid #ccc;
        border-radius: 4px;
        width: 100%;
    }

    textarea {
        max-height: 200px; /* Optional max height */
        resize: none; /* Prevent manual resizing */
        overflow: hidden; /* Hide scrollbar */
    }

    button {
        padding: 0.5rem;
        background-color: #28a745;
        color: white;
        border: none;
        border-radius: 4px;
        cursor: pointer;
    }

    button:hover {
        background-color: #218838;
    }

    .service-list {
        margin-top: 2rem;
        text-align: left;
    }

    .service-item {
        border: 1px solid #ccc;
        padding: 1rem;
        margin-bottom: 1rem;
        border-radius: 4px;
    }

    .delete-button {
        background-color: #dc3545;
        border: none;
        color: white;
        padding: 0.5rem;
        border-radius: 4px;
        cursor: pointer;
    }

    .delete-button:hover {
        background-color: #c82333;
    }
</style>

<main>
    <h1>Healthcare Services</h1>

    <form on:submit|preventDefault={addService}>
        <input type="text" bind:value={name} placeholder="Service Name" />
        <textarea bind:value={description} placeholder="Service Description" on:input={autoResize}></textarea>
        <input type="number" bind:value={price} placeholder="Service Price" />
        <button type="submit">Add Service</button>
    </form>

    <div class="service-list">
        {#each services as { id, name, description, price }}
            <div class="service-item">
                <h3>{name}</h3>
                <p>{description}</p>
                <p>Price: ${price}</p>
                <button on:click={() => updateService(id)}>Edit</button>
                <button class="delete-button" on:click={() => deleteService(id)}>Delete</button>
            </div>
        {/each}
    </div>
</main>
