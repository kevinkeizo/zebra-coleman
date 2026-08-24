# ZEBRA COLEMAN — Plataforma de Treino

Checklist de treino upper/lower com diagrama de execução, vídeo a um toque,
registro de carga por exercício e calendário de acompanhamento.

## Como usar
Abre o `index.html` no navegador. Duplo clique funciona, mas **prefira a extensão
Live Server do VS Code** — em `file://` o YouTube bloqueia o player embutido, então
o botão de play abre o vídeo numa aba nova em vez de tocar dentro do modal.

## O programa
5 dias, 3 exercícios por dia, split upper/lower alternado com sexta de ombro e braço.
Faixa principal de 8-12 reps, 4-5 séries nos compostos, 1-2 reps na reserva na última série.

Volume semanal calibrado pelos landmarks MEV/MAV (Renaissance Periodization):

| Músculo     | Séries/semana | MEV |
|-------------|---------------|-----|
| Peito       | 8             | 8   |
| Costas      | 10            | 10  |
| Ombro       | 8             | 8   |
| Quadríceps  | 9             | 8   |
| Posterior   | 8             | 6   |
| Bíceps      | 8             | 8   |
| Tríceps     | 8             | 6   |
| Panturrilha | 8             | 8   |

Com 15 exercícios a semana fecha exatamente no MEV — o mínimo pra crescer.
Progressão vem da carga, não de mais exercício. Se um dia quiser acelerar,
o caminho é somar séries aos exercícios que já existem, não abrir slots novos.

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
