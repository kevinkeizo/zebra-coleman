# ZEBRA COLEMAN — Plataforma de Treino

Checklist de treino upper/lower com diagrama de execução, vídeo a um toque,
registro de carga por exercício e calendário de acompanhamento.

## Como usar
Abre o `index.html` no navegador. Duplo clique funciona, mas **prefira a extensão
Live Server do VS Code** — em `file://` o YouTube bloqueia o player embutido, então
o botão de play abre o vídeo numa aba nova em vez de tocar dentro do modal.

## O programa
5 dias, 4 exercícios por dia, split upper/lower alternado com sexta de ombro e braço.
Faixa principal de 8-12 reps, 4-5 séries nos compostos, 1-2 reps na reserva na última
série. Os 5 exercícios extras (um por dia) são todos de isolamento — cadeira extensora,
elevação pélvica, tríceps kickback, encolhimento e elevação frontal — de baixa exigência
técnica, pra fechar volume sem virar treino complexo.

Volume semanal calibrado pelos landmarks MEV/MAV (Renaissance Periodization):

| Músculo     | Séries/semana | MEV | MAV   | Situação |
|-------------|---------------|-----|-------|----------|
| Peito       | 8             | 8   | 12-20 | no MEV |
| Costas      | 10            | 10  | 14-22 | no MEV |
| Ombro       | 11            | 8   | 16-22 | acima do MEV |
| Quadríceps  | 12            | 8   | 12-18 | **no MAV** |
| Posterior   | 11            | 6   | 10-16 | **no MAV** |
| Bíceps      | 8             | 8   | 14-20 | no MEV |
| Tríceps     | 11            | 6   | 10-14 | **no MAV** |
| Panturrilha | 8             | 8   | 12-16 | no MEV |

82 séries/semana no total (era 63 com 3 por dia). Quadríceps, posterior e tríceps
saíram do piso mínimo e entraram na faixa ótima de crescimento; o resto segue no MEV,
sem nenhum grupo abaixo do mínimo. Progressão continua vindo principalmente da carga —
o campo de kg é o que decide se o volume de hoje ainda serve amanhã.

Referência: `.claude/skills/hypertrophy-training/` (meta-análises com PMID).

## Estrutura
- `index.html` — página única (HTML + CSS + JS), sem dependência além do Google Fonts.
- `assets/zebra-king.jpg` — retrato do hero (ver `assets/LEIA-ME.txt`).
- `.claude/skills/` — skills de design/UX, treino e pesquisa instaladas no projeto.

## Editar
- Dias e exercícios: array `DATA` dentro da tag `<script>`.
- Ilustrações SVG: objeto `DIAGRAMS`; mapeamento nome→desenho na função `diagramFor()`.
- Cores e fontes: variáveis CSS no `:root`.

## Progresso salvo
Tudo fica no `localStorage` sob a chave `zebra-coleman/v2`:

- `log` — por data, quais exercícios foram feitos e com qual carga.
- `loads` — última carga usada em cada exercício, mostrada como dica no card.

O calendário lê o `log`: dia claro = parcial, dia dourado cheio = treino fechado.
Fim de semana não quebra a sequência. Marcações antigas nunca são apagadas —
o botão "tirar as anilhas" zera só o dia de hoje.
