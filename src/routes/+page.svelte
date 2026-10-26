
<script>
    import Quote from "#lib/components/Quote.svelte";
    import { onMount } from "svelte";


    
    // Target location
    const targetLat = 42.05910523134263;
    const targetLon = 19.517268301553923;

    // Maximum distance: 15 meters
    const maxDistance = 500;

    // Controls visibility of the sixth quote
    let showSixthQuote = $state(false);

    // Calculate distance between two GPS locations
    function calculateDistance(lat1, lon1, lat2, lon2) {
        const R = 6371000; // Earth radius in meters

        const dLat = (lat2 - lat1) * Math.PI / 180;
        const dLon = (lon2 - lon1) * Math.PI / 180;

        const a =
            Math.sin(dLat / 2) ** 2 +
            Math.cos(lat1 * Math.PI / 180) *
            Math.cos(lat2 * Math.PI / 180) *
            Math.sin(dLon / 2) ** 2;

        return 2 * R * Math.atan2(
            Math.sqrt(a),
            Math.sqrt(1 - a)
        );
    }

    // Watch the user's current location
    onMount(() => {
        if (!navigator.geolocation) return;

        const watchId = navigator.geolocation.watchPosition(
            (position) => {
                const distance = calculateDistance(
                    position.coords.latitude,
                    position.coords.longitude,
                    targetLat,
                    targetLon
                );

                // Show the quote only within 15 meters
                showSixthQuote = distance <= maxDistance;
            },

            (error) => {
                // Hide the quote if location is unavailable
                showSixthQuote = false;
                console.error("Geolocation error:", error.message);
            },

            {
                enableHighAccuracy: true,
                maximumAge: 0,
                timeout: 20000
            }
        );

        // Stop tracking when leaving the page
        return () => navigator.geolocation.clearWatch(watchId);
    });

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
                </Quote>
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

            <!-- Sixth quote: visible within 15 meters -->
            {#if showSixthQuote}
                <div class="rounded-3xl bg-orange-200 p-5 shadow-lg transition-all duration-300 hover:-translate-y-2 hover:shadow-2xl">
                    <Quote author="Secret Quote">
                        Every place has a story. Discover yours.
                    </Quote>
                </div>
            {/if}

        </div>

    </div>

</main>
