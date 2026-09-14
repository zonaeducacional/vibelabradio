<script context="module">
    import { formatDistance } from 'date-fns'
    import { ptBR } from 'date-fns/locale'
    import { readable } from 'svelte/store'

    const format = (date, baseDate) => formatDistance(date, baseDate, { addSuffix: true, locale: ptBR })

    const now = readable(new Date(), set => {
        const interval = setInterval(() => {
            set(new Date())
        }, 1000)

        return () => clearInterval(interval)
    })
</script>

<script>
    export let date

    $: iso = date.toISOString()
    $: text = format(date, $now)
</script>

<time datetime={iso}>{text}</time>
