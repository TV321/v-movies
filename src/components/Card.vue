<template>
    <div>
        <h3>Card</h3>
        <p>This is the {{ movie }} card</p>
    </div>
</template>

<script>
export default {
    props: {
        movie: String
    }
}
</script>