
<script>
    import Quote from "#lib/components/Quote.svelte";
</script>

<main class="min-h-screen bg-gradient-to-br from-purple-100 via-pink-50 to-blue-100 px-6 py-12">

    <div class="mx-auto max-w-6xl">

        <!-- Page title -->
        <div class="mb-12 text-center">
            <h1 class="text-5xl font-extrabold text-purple-700">
                Data Exchange
            </h1>

        </div>

        <!-- Quote cards -->
        <div class="grid grid-cols-1 gap-6 md:grid-cols-2 lg:grid-cols-3">

            <div class="rounded-3xl bg-purple-200 p-5 shadow-lg transition-all duration-300 hover:-translate-y-2 hover:shadow-2xl">
                <Quote author="Albert Einstein">
                    Imagination is more important than knowledge.
                </Quote>
            </div>

            <div class="rounded-3xl bg-pink-200 p-5 shadow-lg transition-all duration-300 hover:-translate-y-2 hover:shadow-2xl">
                <Quote author="Steve Jobs">
                    Be the change that you wish to see in the world.
                </Quote>
            </div>

            <div class="rounded-3xl bg-yellow-200 p-5 shadow-lg transition-all duration-300 hover:-translate-y-2 hover:shadow-2xl">
                <Quote author="Oscar Wilde">
                    Be yourself.
            </div>

            <div class="rounded-3xl bg-green-200 p-5 shadow-lg transition-all duration-300 hover:-translate-y-2 hover:shadow-2xl">
                <Quote author="Mahatma Gandhi">
                Don#t worry, be happy
                </Quote>
            </div>

            <div class="rounded-3xl bg-blue-200 p-5 shadow-lg transition-all duration-300 hover:-translate-y-2 hover:shadow-2xl">
                <Quote author="Walt Disney">
                    If you can dream it, you can do it.
                </Quote>
            </div>

        </div>

    </div>

</main>
