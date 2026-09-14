<button class="header__sideBtn" on:click={() => openPage()}>Sobre</button>
<Portal target="{document.body}">
    <ContextPage name="Sobre" open={open} on:close={closePage}>
        <p class="txtbig">Esta rádio é alimentada pelas publicações feitas na rede social <a href="https://joinmastodon.org/" target="_blank">Mastodon</a>. O objetivo principal é criar um espaço para descobrir músicas fora da sua bolha habitual. Espero que você aproveite!</p>
        <hr>
        <h2>De onde vêm as músicas?</h2>
        <p>O aplicativo busca todas as publicações públicas que contêm um link de mídia e uma hashtag de música (você pode configurar isso nas Configurações). Suportamos apenas links do Youtube por enquanto, mas outras plataformas estão planejadas.<br>
        Não possuímos os direitos das músicas, então elas são reproduzidas no player da plataforma original.</p>
        <h2>Como faço para que minha música toque na rádio?</h2>
        <p>Basta fazer uma publicação pública no Mastodon contendo uma das hashtags configuradas no app e um link do Youtube.</p>
        <h2>Posso usar a rádio no celular?</h2>
        <p>Como é um webapp, ele deve funcionar. No entanto, o Player do Youtube permite a reprodução apenas quando você está na página, parando se a tela desligar ou se você mudar de aplicativo. Isso prejudica um pouco a experiência mobile.<br>
        Infelizmente, enquanto o Youtube mantiver esse comportamento, a experiência em dispositivos móveis terá limitações.</p>
        <h2>Como posso entrar em contato para reportar um problema, dar uma ideia ou mandar uma mensagem?</h2>
        Se você é desenvolvedor, pode criar uma "issue" no <a href="https://github.com/EldritchCafe/radio" target="_blank">repositório do Github</a>. Para qualquer outra coisa, você pode entrar em contato com o mantenedor <a href="https://mastodon.social/@sergiosalinas" target="_blank">Sérgio Salinas (@sergiosalinas@mastodon.social)</a> no Mastodon.
    </ContextPage>
</Portal>

<script>
    import Portal from 'svelte-portal'
    import ContextPage from '/src/components/ContextPage'

    let open = false

    let openPage = () => {
        open = true
    }

    let closePage = () => {
        open = false
    }
</script>
