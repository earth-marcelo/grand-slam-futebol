# O Grand Slam do Futebol — versão notebook

Reconstrução em código (pandas + Python) do ranking "Grand Slam do Futebol", originalmente publicado como README + infográfico em PDF sem dados brutos versionados.

## O que mudou em relação à v5 (PDF)

A v5 existia apenas como narrativa + PDF, sem tabela de dados nem código. Esta versão:

- Implementa a metodologia como função Python reutilizável, não como cálculo manual
- Reconstrói o dataset dos 7 jogadores originais **usando os números oficiais extraídos do PDF v5** (títulos, gols por fase, ligas nacionais) — validado no notebook: a fórmula recalculada bate com os scores publicados (78,0 do Pelé, 59,3 do Messi etc.) com diferença menor que 0,05 ponto, só arredondamento
- Adiciona a Copa do Mundo de 2026 (Espanha campeã, Argentina vice, 1-0 na prorrogação) e atualiza Messi + adiciona Mbappé como novo entrante (esse sim reconstruído por pesquisa pública, já que não estava na v5 original)

## Metodologia (herdada da v5)

```
Score = 5 × (títulos de Copa do Mundo)
      + 3 × (títulos de Champions League)
      + 2 × (títulos de Libertadores)
      + 1 × (títulos de Mundial de Clubes)
      + 6 × (média de gols por jogo, carreira)
      + 20 × (índice de G+A em Copas do Mundo, ponderado por fase)
      + 0.5 × (títulos de liga nacional)
```

Multiplicador por fase nas Copas do Mundo (gol/assistência vale mais quanto mais avançada a fase):
grupos ×1 → oitavas ×1.5 → quartas ×2 → semifinal ×2.5 → final ×3 (mesma lógica do projeto de seleções).

## Estrutura

```
grand_slam_futebol/
├── README.md
├── requirements.txt
├── data/
│   └── jogadores.csv       # dataset reconstruído, com fonte de cada estimativa documentada no notebook
└── notebooks/
    └── 01_ranking_jogadores.ipynb
```

## Anexo: Brasileirão x La Liga, qual título é mais raro?

A fórmula dá o mesmo peso (×0,5) para título de liga nacional, seja Brasileirão ou La Liga — deliberadamente, porque ela mede resultado (título, gol), não tenta arbitrar "qual liga é tecnicamente melhor" (isso é opinião, sem resposta objetiva).

Só que existe uma pergunta diferente, essa sim mensurável: **quantos clubes diferentes realmente têm chance de ser campeão em cada liga?** Analisado em `notebooks/02_concentracao_ligas.ipynb`:

- **La Liga** (1929–2026, ~97 temporadas): só **9 clubes diferentes** já foram campeões — Real Madrid (36) e Barcelona (29) sozinhos somam 65 dos ~95 títulos distribuídos
- **Brasileirão**, era pontos corridos (2003–2025, 23 temporadas): também **9 clubes diferentes** foram campeões — mas levou só 23 anos pra chegar nesse número, contra quase 100 anos da Espanha
- **Índice de concentração (HHI):** Brasileirão 1.364 vs La Liga 2.620 — a La Liga é quase 2× mais concentrada

Conclusão registrada: **ser campeão brasileiro parece estatisticamente mais raro/imprevisível do que ser campeão espanhol**, mesmo sem entrar no mérito de qual liga tem o nível técnico mais alto (pergunta diferente, sem resposta objetiva). A fórmula principal não muda por causa disso — fica como observação documentada, com dado por trás.

## Infográfico (v6)

`infografico/grand-slam-futebol-v6.pdf` é o infográfico atualizado, no mesmo estilo visual do `grand-slam-futebol-v5.pdf` original, já com Messi atualizado e Mbappé como novo entrante. Fonte editável em `infografico/grand-slam-futebol-v6.html` (HTML/CSS, renderizado para PDF via Chromium headless).

Para publicar no repositório `grand-slam-futebol` no GitHub, basta colocar o PDF na raiz do repo do jeito que a v5 já está (ex.: renomear para `grand-slam-futebol-v6.pdf` e linkar no README do repo).

## Status

- [x] Reconstrução da metodologia em código
- [x] Dataset com os números oficiais dos 7 jogadores, extraídos do PDF v5
- [x] Validação: score recalculado bate com o score publicado (diferença < 0,05 pt)
- [x] Atualização com a Copa de 2026 (Messi sobe para 65,2 pts; Mbappé entra em 3º com 55,9 pts)
- [ ] Refinar a base de carreira do Mbappé (reconstruída por pesquisa pública, menos confiável que os outros 7)
- [ ] Expandir dataset para mais jogadores
- [x] Análise de concentração de título (Brasileirão x La Liga) documentada, sem alterar a fórmula
- [ ] Aplicar o mesmo processo ao projeto Grand Slam das Seleções (dados oficiais já extraídos do PDF, faltando notebook)
