# ZEBRA COLEMAN — Plataforma de Treino

Checklist de treino upper/lower com diagrama de execução, vídeo a um toque,
registro de carga série a série e calendário de acompanhamento.

## Como usar
Abre o `index.html` no navegador. Duplo clique funciona, mas **prefira a extensão
Live Server do VS Code** — em `file://` o YouTube bloqueia o player embutido, então
o botão de play abre o vídeo numa aba nova em vez de tocar dentro do modal.

## O programa
5 dias, 4 exercícios por dia, split upper/lower alternado com sexta de ombro e braço.
Faixa principal de 8-12 reps, 4-5 séries nos compostos, 1-2 reps na reserva na última
série. Priorizado equipamento de máquina onde existe um bom equivalente (supino, remada,
desenvolvimento, peck deck, cadeira extensora/abdutora/adutora, leg press, mesa
flexora, pulley) — mais seguro e mais fácil de manter execução limpa sem supervisão.
Ficou livre só onde a máquina muda o estímulo de menos (agachamento) ou onde o
halter já é simples o suficiente (elevações, rosca, encolhimento, kickback).

Volume semanal calibrado pelos landmarks MEV/MAV (Renaissance Periodization):

| Músculo                  | Séries/semana | MEV | MAV   | Situação |
|---------------------------|---------------|-----|-------|----------|
| Peito                      | 8             | 8   | 12-20 | no MEV |
| Costas                     | 10            | 10  | 14-22 | no MEV |
| Ombro                      | 11            | 8   | 16-22 | acima do MEV |
| Quadríceps                 | 12            | 8   | 12-18 | **no MAV** |
| Posterior de coxa          | 4             | 6   | 10-16 | ⚠️ **abaixo do MEV** |
| Bíceps                     | 8             | 8   | 14-20 | no MEV |
| Tríceps                    | 7             | 6   | 10-14 | acima do MEV |
| Panturrilha                | 8             | 8   | 12-16 | no MEV |

Mais três isolados fora da tabela padrão de MEV (glúteo médio, adutores, trapézio,
3-4 séries cada) — reforço pontual, não carregam volume de um grupo grande.

68 séries/semana nos grupos rastreados. **Posterior de coxa ficou abaixo do
mínimo** desde que o Stiff (Terça) virou Cadeira adutora — troca pedida
explicitamente, mas o trade-off é real: adutor treina virilha, não isquiotibial,
então esse volume não se soma. Se quiser fechar esse buraco, os dois substitutos
que mantêm o padrão de hip-hinge do Stiff são **pulley entre as pernas** ou
**banco romano** (esse último desloca um pouco o foco pro glúteo/lombar). Até lá,
o posterior sobrevive só da Mesa flexora sentado (Quinta).

Progressão continua vindo principalmente da carga — o campo de kg é o que decide
se o volume de hoje ainda serve amanhã.

Referência: `.claude/skills/hypertrophy-training/` (meta-análises com PMID).

## Estrutura
- `index.html` — página única (HTML + CSS + JS), sem dependência além do Google Fonts.
- `assets/zebra-king.jpg` — retrato do hero (ver `assets/LEIA-ME.txt`).
- `.claude/skills/` — skills de design/UX, treino e pesquisa instaladas no projeto.

## Editar
- Dias e exercícios: array `DATA` dentro da tag `<script>`.
- Ilustrações SVG: objeto `DIAGRAMS`; cada exercício aponta pro desenho certo pela
  chave `fig`, lida pela função `figFor()`.
- Cores e fontes: variáveis CSS no `:root`.

## Progresso salvo

Cada exercício guarda uma **lista de séries**, não uma carga única — quantidade de
blocos = o número previsto no "4 x 8-10" do próprio exercício, com um botão "+" pra
série extra. O recorde de sempre (`recorde: Xkg`) aparece direto no card, sem
precisar abrir o exercício; o 1RM estimado (fórmula de Epley) usa a série mais
pesada do dia, não a última digitada.

Três camadas de persistência, da mais rápida pra mais durável:

1. **`localStorage`** (chave `zebra-coleman/v3`) — fonte imediata, funciona offline.
   `log` guarda por data quais exercícios foram feitos; `loads[ei]` é um array com
   o peso de cada série daquele exercício naquele dia.
2. **Supabase** (tabela `workout_log`, uma linha por série — colunas `set_number` +
   `load_kg`) — toda edição sincroniza sozinha em segundo plano, com debounce de
   500ms pra não disparar uma requisição por tecla. Ao abrir o app em qualquer
   aparelho, ele puxa o que tá no banco e completa o que faltar localmente (local
   sempre vence em conflito, célula a célula). Indicador de status no cabeçalho do
   calendário.
3. **Backup manual** — botões "Baixar backup" / "Restaurar backup" no rodapé exportam
   e importam o `db` inteiro como JSON. Guarda esse arquivo em algum lugar de vez em
   quando; é o que sobrevive mesmo se o navegador limpar tudo (Safari é especialmente
   agressivo nisso em apps instalados na tela de início).

O calendário lê o `log`: dia claro = parcial, dia dourado cheio = treino fechado.
Fim de semana não quebra a sequência. Marcações antigas nunca são apagadas —
o botão "tirar as anilhas" zera só o dia de hoje.
