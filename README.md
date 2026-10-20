# Simulador de Investimentos em FIIs - Lester Finance Invest App

Este repositório contém a resolução do desafio prático de desenvolvimento de um simulador de investimentos focado em Fundos Imobiliários (FIIs) utilizando o Microsoft Excel. O objetivo foi transformar dados financeiros em uma ferramenta interativa com "cara de aplicativo", automatizando projeções e alocações de ativos por perfil.

## Informações de Entrega
- **Arquivo da Planilha:** `simulador_investimentos.xlsx` (Disponível na raiz deste repositório).
- **Status do Projeto:** 100% Concluído, validado e testado matematicamente.

---

## Perguntas de Negócio Respondidas pela Ferramenta
1. **Quanto investir por mês?** Definido na célula `B5` (Aporte Mensal Desejado) como **R\$ 5.000,00**.
2. **Por quantos anos?** Definido na célula `B7` (Prazo) como **15 anos**.
3. **Qual a taxa de rendimento mensal?** Definido na célula `B6` como **1% ao mês**.
4. **Quanto de patrimônio vai acumular?** Calculado dinamicamente na célula `B10`, resultando em **R\$ 1.997.864,15** para o cenário estipulado.
5. **Quanto vai receber de dividendos por mês?** Calculado na célula `B11`, resultando em uma renda passiva estimada de **R\$ 15.982,91 por mês**.

---

## Aplicação Prática das Fórmulas (Engenharia Financeira)

### 1. Função VF (Valor Futuro) com Referências Absolutas (\$)
Para calcular a projeção de patrimônio acumulado ao longo do tempo (cenários de 2 a 30 anos) sem que as fórmulas quebrassem ao serem arrastadas, aplicamos o travamento de células com o símbolo `$` (Referência Absoluta) nas variáveis fixas de Taxa (`$B$6`) e Aporte (`$B$5`). 
- **Fórmula aplicada na célula B14 (Cenário de 2 anos):** `=VF($B$6; A14*12; -$B$5; 0)`.
*(O prazo `A14` foi multiplicado por 12 para converter os anos em meses, garantindo a capitalização dos juros compostos de forma correta)*.

### 2. Função PROCV para Alocação por Perfil
Criamos uma aba de `Apoio` contendo uma **Chave Composta** única baseada na concatenação do Perfil com o Tipo de Fundo (ex: `Conservador_Tijolo`). Na aba principal do `Simulador`, a coluna de Participação (%) busca dinamicamente essa chave e retorna o percentual exato do perfil selecionado na célula `B8`.
- **Fórmula aplicada na célula B21 (Participação do Tijolo):** `=PROCV($B$8&"_"&A21; Apoio!$D$2:$E$10; 2; FALSO)`.

---

## Intervalos Nomeados Criados
Para tornar o código das fórmulas legível para usuários leigos e auditores, substituímos os endereços padrões do Excel por intervalos nomeados de negócio:
- `salario_mensal` ➔ Vinculado à célula `B3`.
- `aporte_desejado` ➔ Vinculado à célula `B5`.
- `taxa_rendimento` ➔ Vinculado à célula `B6`.

---

## Perfis de Investimento Configurados (Soma 100%)
As porcentagens foram distribuídas na aba de Apoio garantindo o fechamento estrito de 100% de alocação por carteira:
- **Conservador (Utilizado nos testes):** 50% Tijolo, 30% Papel, 20% FOF.
- **Moderado:** 40% Tijolo, 40% Papel, 20% FII Agro.
- **Arrojado:** 20% Tijolo, 30% Papel, 50% Ações/FIIs Desenvolvimento.

---

## Melhorias Visuais em relação ao Modelo Base do Expert
- **Visual Clean App:** Remoção completa das linhas de grade padrão do Excel (guia Exibir), deixando o fundo branco e focado, simulando uma interface de software financeiro.
- **Design System Premium:** Aplicação de formatação condicional cinza sutil para células calculadas de saída, bloqueando visualmente a edição indevida do usuário.
- **Gráfico de Radar Interativo:** Inclusão de um gráfico de teia que se redesenha automaticamente em tempo real assim que o perfil do investidor é alterado, facilitando a tomada de decisão.
