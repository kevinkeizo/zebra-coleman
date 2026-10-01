# ZEBRA COLEMAN — Plataforma de Treino

Checklist de treino upper/lower com diagrama de execução, vídeo a um toque,
registro de carga série a série e calendário de acompanhamento.

## Como usar
Abre o `index.html` no navegador. Duplo clique funciona, mas **prefira a extensão
Live Server do VS Code** — em `file://` o YouTube bloqueia o player embutido, então
o botão de play abre o vídeo numa aba nova em vez de tocar dentro do modal.

## O programa
5 dias: dois de perna (Segunda e Quarta, **idênticos** entre si), dois upper
(Terça e Quinta) e um de ombro/braço (Sexta). Dia de perna é 5 exercícios —
Agachamento na rack + Cadeira adutora + Cadeira abdutora + Leg press + Cadeira
extensora — o resto segue 4 por dia. Priorizado equipamento de máquina onde
existe bom equivalente — mais seguro, mais fácil de manter execução limpa
sem supervisão.

Volume semanal calibrado pelos landmarks MEV/MAV (Renaissance Periodization):

| Músculo                  | Séries/semana | MEV | MAV   | Situação |
|---------------------------|---------------|-----|-------|----------|
| Peito                      | 8             | 8   | 12-20 | no MEV |
| Costas                     | 10            | 10  | 14-22 | no MEV |
| Ombro                      | 11            | 8   | 16-22 | acima do MEV |
| Quadríceps                 | 24            | 8   | 12-18 | bem acima do MAV |
| Posterior de coxa          | 0             | 6   | 10-16 | ⚠️ **zerado** |
| Bíceps                     | 8             | 8   | 14-20 | no MEV |
| Tríceps                    | 7             | 6   | 10-14 | acima do MEV |
| Panturrilha                | 0             | 8   | 12-16 | ⚠️ **zerado** |

Mais dois isolados fora da tabela padrão (adutores 8 séries, glúteo médio via
abdutora 6 séries) — reforço pontual, não substituem grupo grande nenhum.

**Panturrilha e posterior de coxa saíram do programa de propósito** — decisão
explícita do usuário, pra focar o dia de perna só no que ele realmente faz na
academia. Quadríceps ficou com volume bem acima do ideal (agachamento + leg
press + extensora, nos dois dias de perna) — isso é esperado quando o foco
migra de "mais exercícios variados" pra "menos exercícios, mais pesados,
repetidos". Se um dia quiser reintroduzir panturrilha ou posterior, é só pedir.

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
