# Calculadora de Partilha do Simples Nacional

Ferramenta web offline (HTML + JavaScript puro) para calcular a alíquota efetiva, o
imposto total do mês e a partilha por tributo no Simples Nacional, no padrão de saída
do Sankhya OM / PGDAS-D.

## Funcionalidades

- Focado no **Anexo II - Indústria** (LC 123/2006, redação da LC 155/2016)
- Entrada de RBT12 (12 meses anteriores) e faturamento do mês de apuração
- Identificação automática da faixa a cada cálculo (6 faixas) — troca de faixa é sinalizada
- Alíquota efetiva com 5 casas decimais (art. 18, §1º-A)
- Tabela de partilha por tributo: IRPJ, CSLL, COFINS, PIS/PASEP, CPP, IPI e ICMS
- Avisos legais: ICMS/ISS fora do DAS acima de R$ 3,6 mi (art. 13-A) e excesso de
  R$ 4,8 mi (art. 3º, §§9º e 9º-A)
- Linha de total confere se a repartição fecha 100%
- Formatação monetária pt-BR e tema escuro responsivo (Tailwind CSS)

## Como usar

1. Abra `index.html` direto no navegador (duplo clique) — não requer servidor.
2. Informe o RBT12 e o faturamento do mês.
3. Clique em **Calcular Partilha**.

A página já executa um cálculo de exemplo ao carregar.

## Tabelas do Anexo II - Indústria (LC 123/2006)

### 1. Faixas, alíquota nominal e parcela a deduzir

| Faixa | Receita Bruta em 12 Meses (RBT12) | Alíquota Nominal | Parcela a Deduzir (R$) |
|-------|-----------------------------------|------------------|------------------------|
| 1ª | Até 180.000,00 | 4,50% | - |
| 2ª | De 180.000,01 a 360.000,00 | 7,80% | 5.940,00 |
| 3ª | De 360.000,01 a 720.000,00 | 10,00% | 13.860,00 |
| 4ª | De 720.000,01 a 1.800.000,00 | 11,20% | 22.500,00 |
| 5ª | De 1.800.000,01 a 3.600.000,00 | 14,70% | 85.500,00 |
| 6ª | De 3.600.000,01 a 4.800.000,00 | 30,00% | 720.000,00 |

### 2. Percentual de repartição dos tributos (% do DAS)

| Faixa | IRPJ | CSLL | COFINS | PIS/PASEP | CPP | IPI | ICMS | Total |
|-------|------|------|--------|-----------|-----|-----|------|-------|
| 1ª a 5ª | 5,50% | 3,50% | 11,51% | 2,49% | 37,50% | 7,50% | 32,00% | 100,00% |
| 6ª | 8,50% | 7,50% | 20,96% | 4,54% | 23,50% | 35,00% | 0,00% | 100,00% |

Na 6ª faixa (RBT12 acima de R$ 3.600.000,00) o ICMS não integra o DAS — art. 13-A.

### 3. Fórmulas (art. 18 da LC 123/2006)

```
Alíquota efetiva = (RBT12 × Alíquota nominal − Parcela a deduzir) / RBT12
Imposto do mês   = Faturamento do mês × Alíquota efetiva
Tributo          = Faturamento do mês × Alíquota efetiva × % de repartição
```

A faixa é escolhida pelo **RBT12**, que considera os 12 meses anteriores ao mês de
apuração (art. 18, §1º).

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

- Tabela de faixas, alíquotas nominais, parcelas a deduzir e percentuais de
  repartição conferidos no texto oficial da LC 123/2006 (Planalto) — constam em
  `index.html` (`faixasAnexoII`).
- A faixa depende **apenas do RBT12**; o faturamento do mês é a base de cálculo e
  não altera a faixa.
- Acima de R$ 3.600.000,00 o ICMS deixa de integrar o DAS (art. 13-A).
- Acima de R$ 4.800.000,00 o resultado é apenas referencial: incide excesso e a
  parcela excedente é tributada pela alíquota máxima do Anexo acrescida de 20%
  (art. 18, §§16 e 16-A).
- Não substitui o PGDAS-D nem orientação contábil. Valores oficiais devem ser
  conferidos na Receita Federal.
