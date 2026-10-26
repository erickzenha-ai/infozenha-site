# Site da InfoZenha

Site institucional de uma página da InfoZenha: assistência técnica de notebooks em Goiânia desde 2001. O objetivo é levar o visitante para uma conversa no WhatsApp.

- **No ar:** https://erickzenha-ai.github.io/infozenha-site/
- **Domínio definitivo:** infozenhanotebooks.com.br (a registrar; veja "Ligar o domínio" abaixo)
- **Briefing:** `E:\InfoZenha\04 Site\BRIEFING-SITE.md`
- **Contexto da empresa:** `E:\InfoZenha\CLAUDE.md`

Site estático (HTML, CSS e um pouco de JavaScript), sem framework, hospedado de graça no GitHub Pages. Este repositório é separado do sistema de gestão e **não contém dados de clientes**.

## Arquivos

| Arquivo | Para que serve |
| --- | --- |
| `index.html` | A página inteira (textos, estilo e o script dos seminovos) |
| `seminovos.json` | Lista de seminovos exibida no site |
| `assets/` | Favicon, ícones e imagem de compartilhamento (`img/og-image.png`) |
| `robots.txt` e `sitemap.xml` | Para o Google encontrar o site |
| `404.html` | Página de "não encontrado" |
| `dominio/CNAME` | Arquivo pronto para o domínio infozenhanotebooks.com.br (ainda **fora** da raiz de propósito) |

## Atualizar os seminovos

Os cards da seção "Seminovos revisados, com garantia" vêm do arquivo `seminovos.json`. Não é preciso mexer no HTML.

```json
{
  "atualizado_em": "2026-10-26",
  "seminovos": [
    {
      "modelo": "Dell Latitude 5490",
      "configuracao": "Intel Core i5 8ª geração · 16 GB de memória · SSD 256 GB · tela 14\"",
      "preco": 2490,
      "garantia": "90 dias",
      "foto": "assets/img/seminovos/dell-latitude-5490.webp",
      "disponivel": true
    }
  ]
}
```

| Campo | O que colocar |
| --- | --- |
| `modelo` | Marca e modelo. Vai na mensagem do botão "Tenho interesse" |
| `configuracao` | Processador, memória, SSD, tela |
| `preco` | Número sem "R$" e sem ponto de milhar (ex.: `2490` ou `2490.50`). Use `null` para mostrar "Consulte" |
| `condicao` | Condição de pagamento (ex.: `"Até 4x sem juros no cartão"`). Pode deixar `""` |
| `garantia` | Texto livre (ex.: `"90 dias"`). Pode deixar `""` |
| `foto` | Caminho da foto em WebP. Vazio (`""`) mostra o bloco [FOTO] |
| `disponivel` | `false` esconde o card sem apagar (útil quando vender) |
| `exemplo` | Só no card de exemplo: mostra a etiqueta "EXEMPLO". **Apague o card de exemplo quando cadastrar o primeiro seminovo real** |

Para mostrar só a mensagem "Novos seminovos toda semana…", deixe a lista vazia: `"seminovos": []`.

**Fotos:** tire em boa luz e fundo limpo, converta para **WebP** em https://squoosh.app (largura de cerca de 800 px, qualidade 75), salve em `assets/img/fotos/` e coloque o caminho no campo `foto`. A imagem aparece num quadro quadrado de fundo escuro, sem cortes (anúncios quadrados ficam perfeitos).

**Quando vender:** troque `"disponivel": true` por `false` (o card some na hora). Quando não houver nenhum disponível, o site mostra sozinho a mensagem "Novos seminovos toda semana…".

**Futuro:** o plano é gerar este `seminovos.json` direto do estoque do sistema de gestão, sem cadastro duplicado.

## Publicar uma alteração

Qualquer alteração enviada para a branch `main` vai ao ar em cerca de 1 minuto.

- **Pelo site do GitHub:** abra o arquivo em github.com/erickzenha-ai/infozenha-site, clique no lápis (Edit), altere e clique em **Commit changes**.
- **Pelo computador:** na pasta `E:\InfoZenha\04 Site\infozenha-site`, rode `git add -A`, `git commit -m "Atualiza seminovos"` e `git push`.

## O que falta trocar (marcado no site)

- **Fotos:** o topo e a seção "Por que" já usam fotos reais (`assets/img/fotos`, originais em `E:\InfoZenha\05 Fotos Infozenha`). Ideal no futuro: uma foto de bancada com **notebook** (a atual mostra peças de celular) e fotos reais dos seminovos no lugar das imagens de fabricante dos anúncios.
- **Depoimentos:** os 3 cards "Espaço para avaliação do Google" devem ser trocados por avaliações reais do Google (não inventar). No `index.html`, procure por `depoimento`.
- **Instagram:** no rodapé está "em breve". Trocar pelo link do perfil quando confirmado (e adicionar em `sameAs` nos dados estruturados).
- **Horário de atendimento:** a confirmar; quando definir, dá para incluir no rodapé e nos dados estruturados (`openingHours`).

## Ligar o domínio infozenhanotebooks.com.br

1. **Registre** o domínio em https://registro.br (cerca de R$ 40 por ano).
2. **No Registro.br**, abra o domínio → **DNS** → **Editar zona** (use os servidores DNS do próprio Registro.br) e crie:

   | Tipo | Nome | Valor |
   | --- | --- | --- |
   | A | (vazio, raiz) | 185.199.108.153 |
   | A | (vazio, raiz) | 185.199.109.153 |
   | A | (vazio, raiz) | 185.199.110.153 |
   | A | (vazio, raiz) | 185.199.111.153 |
   | CNAME | www | erickzenha-ai.github.io |

3. **Segurança (recomendado):** no GitHub, em **Settings (da conta) → Pages → Add a domain**, verifique `infozenhanotebooks.com.br`. O GitHub mostra um registro **TXT** para criar no Registro.br. Isso impede que outra pessoa use o seu domínio no GitHub.
4. **No repositório**, vá em **Settings → Pages → Custom domain**, digite `infozenhanotebooks.com.br` e clique em **Save**. Isso cria o arquivo `CNAME` na raiz (o mesmo que está em `dominio/CNAME`).
5. Aguarde a propagação (de minutos a algumas horas) e marque **Enforce HTTPS**.
6. **Depois que o domínio estiver no ar**, troque `https://erickzenha-ai.github.io/infozenha-site/` por `https://infozenhanotebooks.com.br/` em `index.html`, `robots.txt` e `sitemap.xml`, e o link `/infozenha-site/` do `404.html` por `/`.

O `CNAME` não fica na raiz desde já porque, sem o domínio registrado e apontado, o GitHub tentaria redirecionar o site para um endereço que ainda não existe e ele sairia do ar.
