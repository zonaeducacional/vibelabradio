<button class="header__sideBtn" on:click={() => openPage()}>Configurações</button>
<Portal target="{document.body}">
    <ContextPage name="Configurações" open={open} on:close={closePage}>

    <form class="settings" on:submit={handleSubmit}>
        <div class="settings-line">
            <div class="settings-side">
                <div class="settings-side__title">Instância</div>
                <div class="settings-side__subtitle">A instância do Mastodon de onde as publicações são buscadas</div>
            </div>
            <div class="settings-main">
                <input
                    class="f-size-full"
                    type="text" id="domain"
                    name="domain"
                    on:change={event => $domainValue = event.target.value}
                    value={$domainValue}
                >
                {#if !$domainState.valid}
                    <div class="notif notif--error">{$domainState.error}</div>
                {/if}
            </div>
        </div>
        <div class="settings-line">
            <div class="settings-side">
                <div class="settings-side__title">Tags</div>
                <div class="settings-side__subtitle">Quais hashtags são buscadas</div>
            </div>
            <div class="settings-main">
                <TagInput
                    on:change={event => $hashtagsValue = event.detail}
                    value={$hashtagsValue}
                />
                {#if !$hashtagsState.valid}
                    <div class="notif notif--error">{$hashtagsState.error}</div>
                {/if}
                {#if $hashtagsValue.length > 5}
                    <div class="notif notif--warning">Muitas hashtags podem prejudicar o desempenho e o consumo de rede.</div>
                {/if}
            </div>
        </div>
        <button class="btn btn--primary w100" type="submit" disabled={!$valid}>Salvar alterações</button>
    </form>
    </ContextPage>
</Portal>

<script>
    import { getContext } from 'svelte'
    import { writable, derived } from 'svelte/store'
    import Portal from 'svelte-portal'
    import ContextPage from '/src/components/ContextPage'
    import TagInput from '/src/components/TagInput'

    const domain = getContext('domain')
    const hashtags = getContext('hashtags')

    const domainValue = writable($domain)
    const domainState = derived([domainValue], async ([$domainValue], set) => {
        if ($domainValue === '') {
            set({ valid: false, error: 'A Mastodon instance\'s domain is required.' })
        } else {
            try {
                const response = await fetch(`https://${$domainValue}/api/v1/instance`)
                const instance = await response.json()

                if (response.ok) {
                    set({ valid: true, error: null })
                } else {
                    set({ valid: false, error: 'Domain is not a mastodon instance.' })
                }
            } catch (error) {
                set({ valid: false, error: 'Network error when accessing domain. This might be an internet access problem or a typing mistake.' })
            }
        }
    }, { valid: false, error: '' })

    const hashtagsValue = writable($hashtags)
    const hashtagsState = derived([hashtagsValue], ([$hashtagsValue]) => {
        if ($hashtagsValue.some(hashtag => !/^[a-z0-9]+$/i.test(hashtag))) {
            return { valid: false, error: 'Hashtags can only contains alphanumeric characters.' }
        } else if ($hashtagsValue.length === 0) {
            return { valid: false, error: 'At least one hashtag is required.' }
        } else {
            return { valid: true, error: null }
        }
    })

    const valid = derived([domainState, hashtagsState], states => states.every(state => state.valid))

    const handleSubmit = event => {
        event.preventDefault()

        if ($valid) {
            $domain = $domainValue
            $hashtags = $hashtagsValue
            location.reload() // for now
        }
    }


    let open = false

    let openPage = () => {
        open = true
    }

    let closePage = () => {
        open = false
    }
</script>
