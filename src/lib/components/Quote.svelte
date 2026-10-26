
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

<div class="flex h-full flex-col">

    <!-- Author -->
    <header class="mb-4 flex items-center gap-2 text-lg font-bold text-gray-800">
        {author} says:
    </header>

    <!-- Quote -->
    <blockquote
        class="mb-6 flex-1 rounded-2xl border-l-4 border-purple-500 bg-white/60 p-5 text-lg italic leading-relaxed text-gray-800 shadow-sm"
        bind:this={quoteElement}
    >
        {@render children?.()}
    </blockquote>

    <!-- Buttons -->
    <div class="flex gap-3">

        <!-- Copy button -->
        <button
            onclick={copyQuote}
            class="flex-1 cursor-pointer rounded-xl bg-white px-4 py-3 font-semibold text-purple-700 shadow-md transition-all duration-300 hover:scale-105 hover:bg-purple-100"
        >
             Copy
        </button>

        <!-- Share button -->
        <button
               class="flex-1 cursor-pointer rounded-xl bg-purple-600 px-4 py-3 font-semibold text-white shadow-md transition-all duration-300 hover:scale-105 hover:bg-purple-700"
        >
             Share
        </button>

    </div>

</div>
