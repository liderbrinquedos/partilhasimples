# Calculadora de Partilha do Simples Nacional

Ferramenta web offline (HTML + JavaScript puro) para calcular a alíquota efetiva, o
imposto total do mês e a partilha por tributo no Simples Nacional, no padrão de saída
do Sankhya OM / PGDAS-D.

## Funcionalidades

- Seletor de anexo (I - Comércio, II - Indústria, III - Serviços)
- Entrada de receita acumulada (RBT12) e faturamento do mês atual
- Identificação automática da faixa (6 faixas, LC 123/2006)
- Alíquota efetiva com 5 casas decimais
- Tabela de partilha por tributo: IRPJ, CSLL, COFINS, PIS/PASEP, CPP, ICMS, IPI e ISS
- Formatação monetária pt-BR e tema escuro responsivo (Tailwind CSS)

## Como usar

1. Abra `index.html` direto no navegador (duplo clique) — não requer servidor.
2. Informe Anexo, RBT12 e faturamento do mês.
3. Clique em **Calcular Partilha**.

A página já executa um cálculo de exemplo ao carregar.

## Estrutura

```
.
├── index.html      # Aplicação completa (estrutura + estilos + lógica)
├── README.md
└── .gitignore
```

## Publicando no GitHub Pages

1. `Settings` > `Pages`
2. Source: **Deploy from a branch**
3. Branch: `main` / `(root)` > **Save**

Acessível em `https://liderbrinquedos.github.io/partilhasimples/`.

## Considerações

- As tabelas de faixas e repartição estão embutidas em `index.html` (`faixasAnexoII`).
- O cálculo atual usa as faixas do Anexo II; a tabela da faixa 5 foi ajustada para
  refletir a proporção de uma tela de referência.
- Não substitui o PGDAS-D nem orientação contábil. Valores oficiais devem ser
  conferidos na Receita Federal.
