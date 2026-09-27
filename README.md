# portfolio

Site de perfil de Devanir Ramos Junior. Um `index.html` só — CSS e JS inline,
zero dependência de build, zero framework. Só as fontes vêm do Google Fonts.

Terminal escuro roxo, seções como comandos de shell (`cat sobre.md`,
`tree stack/`, `git log --oneline`), digitação animada na primeira descida,
tema claro/escuro e conteúdo em **português e inglês** no mesmo arquivo.

## Duas línguas (i18n)

A página carrega português e inglês ao mesmo tempo; o CSS esconde o que não
está ativo. A regra:

- Bloco com `data-lang="pt"` ou `data-lang="en"` aparece só naquela língua.
- Bloco **sem** `data-lang` é neutro (botões, nomes de produto) e aparece
  sempre.

Editar um texto = editar os **dois** blocos, um embaixo do outro no HTML. O
seletor no menu troca e recarrega a página de propósito (a animação de
digitação guarda os textos no carregamento), preservando a posição da
rolagem via `sessionStorage`. O idioma vem de `?lang=pt`/`?lang=en` na URL →
o que ficou salvo no navegador → `navigator.language` → português.

## Fora da busca, de propósito

O site é para ser acessado por link direto (LinkedIn, currículo), não por
quem pesquisa o nome no Google. Três camadas cuidam disso:

1. `<meta name="robots" content="noindex, nofollow">` no HTML
2. `_headers` com `X-Robots-Tag: noindex` — nível de servidor, cobre também
   arquivos que não são HTML (só funciona no Cloudflare Pages)
3. `robots.txt` que **permite** o rastreio — de propósito: um crawler
   proibido de baixar a página (`Disallow: /`) nunca chega a ler a tag
   `noindex`, e a URL pode continuar aparecendo na busca sem descrição. Para
   sair do índice, o rastreio precisa ser permitido e a indexação negada.

## Testar local

```bash
python -m http.server 8000
```
