<script>
    let {children, author="Not known"} = $props();

    // Store the quote element
    let quoteElement;

    // Copy the quote text
   async function copyQuote() {
        //Copy
        await navigator.clipboard.writeText(quoteElement.textContent.trim());

        //Notification
        let permission=Notification.permission;
        if(permission !== "granted"){
            permission = await Notification.requestPermission();
        }
        if (permission === "granted") {
            new Notification("Quote copied", {
                body: "You successfully copied this Quote",
            });
        }
    }
    //Share
    async function share() {
                await navigator.share({
                    title: "Please read my quote",
                    text: quoteElement.innerText.trim(),
                });
    }
</script>

<div>

    <header>
        {author} says:
    </header>


<blockquote class="border border-black p-4" bind:this={quoteElement}>
 
    {@render children?.()}


</blockquote>

<!-- Button to copy the quote text -->
<button onclick={copyQuote} class="border border-black p-2">
    Copy
</button>

<button onclick={share} class="border border-black p-2">
Share 
</button>

</div>