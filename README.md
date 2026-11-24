# Década de 90

<!-- aviso-ia -->
> **Feito com IA.** O código deste repositório foi escrito pelo **Claude Code** (inteligência artificial da Anthropic), a partir das especificações, dos testes e da revisão do autor. Leia antes de usar, como faria com qualquer código.

Base dos **filmes brasileiros lançados entre 1990 e 2001**, da "retomada" do cinema brasileiro: lançamento, distribuidora, salas, público, renda, participação nos festivais de Brasília e Gramado, direção, gênero, produtora e UF.

Página publicada em: https://olgasuite.github.io/decada90/

## A página

- `index.html`: página única (Firebase 10 modular). Leitura pública; a edição só é liberada para o dono, com login Google.
- Busca, filtros e ordenação por qualquer coluna; ficha de cada filme com os dados da Filmografia Brasileira (Cinemateca Brasileira) e do TMDB quando há vínculo.
- Dados na coleção `decada90_filmes` do Firestore, um documento por filme.

## Scripts de dados

Os que gravam simulam por padrão e só gravam com `--gravar`.

| Script | O que faz |
|---|---|
| `importar_planilha.py` | Carga inicial a partir da planilha de origem. **Com `--gravar`, apaga e regrava a coleção inteira**: não rodar depois de edições feitas na página. |
| `ancine_lancamentos.py` | Completa lançamento, público, renda e distribuidora com as listagens da ANCINE, só em campos vazios. |
| `cinemateca_casar.py` | Procura cada título na Filmografia Brasileira e pontua os candidatos (título, ano, direção). Só gera o relatório `casamentos.json/csv`, não grava nada. |
| `cinemateca_importar.py` | Grava os dados da Cinemateca dos casamentos certos (sinopse, duração, elenco, prêmios); dúvidas ficam como candidatos para escolher na página. |
| `cinemateca_datas.py` | Preenche a data de lançamento da Cinemateca, só quando o ano é coerente (não pega a estreia original de relançamentos). |
| `tmdb_casar.py` | Para quem não casou com a Cinemateca, procura no TMDB; dúvidas ficam como candidatos para escolher na página. |
| `padronizar_uf.py` | Padroniza as UFs (sem repetição, em ordem alfabética: `SP/RJ` → `RJ/SP`), a mesma regra que a página aplica ao salvar. |

## Publicar

`publicar.ps1` envia `index.html` e `.nojekyll` para este repositório (GitHub Pages).
