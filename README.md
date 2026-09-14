# VibeLab Rádio

Um player de rádio focado em "Vibe Coding" que captura músicas (YouTube, SoundCloud, etc.) ao vivo da rede Mastodon (mastodon.social) filtrando pelas hashtags musicais (#np, #nowplaying, etc).

## Estética
- **UI Pro Max**: Design totalmente construído sobre Neomorfismo (Soft UI).
- **Dark/Light Mode Invertido**: Paleta premium focada em tons Areia/Ouro (`#e2c99f`) e Chumbo/Grafite (`#353437`).
- **Glassmorphism Base**: Sombras internas e externas moldando a interface sem bordas rígidas.

## Tecnologias Usadas
- HTML / Svelte / SCSS
- Bundler: Parcel
- Hospedagem recomendada: Nekoweb, GitHub Pages, Cloudflare Pages, etc.

## Como Executar Localmente
1. Instale as dependências: `npm install`
2. Rode o servidor de desenvolvimento: `npm run dev` (Acesse http://localhost:1234)
3. Para construir (build) para produção: `npm run build` (Os arquivos finais ficarão na pasta `dist`).

## Deployment (Nekoweb / GitHub Pages)
- **Nekoweb**: Basta rodar `npm run build` e arrastar o conteúdo da pasta `dist` para dentro do seu painel no Nekoweb.
- **GitHub Pages**: Envie este repositório para o GitHub e ative o GitHub Pages apontando para usar GitHub Actions, ou crie uma branch `gh-pages` com o conteúdo da pasta `dist`.

## Histórico de Modificações (Changelog)
- Clone do projeto original (EldritchCafe/radio).
- Tradução completa da interface para Português (pt-BR).
- Refatoração da identidade visual para "VibeLab Rádio".
- Remoção do logo antigo e substituição por logotipo CSS/SVG tipográfico.
- Remoção das abas de 'Sobre' e 'Configurações' para manter a interface focada apenas no player.
- Paleta de cores redesenhada para tons quentes e cinzas.
- Refatoração do CSS aplicando margens internas e externas (Padding) para melhor disposição dos campos de vidro.
- Transformação total para estética Neomórfica (Luz e Sombra Invertidas).
- Hardcode da instância `mastodon.social` nas variáveis do aplicativo para varredura sem necessidade de tela de configuração.
