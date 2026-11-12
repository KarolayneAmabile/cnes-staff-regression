# Regressão: número de profissionais em estabelecimentos de saúde (CNES)

Projeto de **regressão** que busca prever **quantos profissionais de saúde trabalham em um estabelecimento** a partir das
características cadastradas no CNES (Cadastro Nacional de Estabelecimentos de Saúde), como tipo de unidade, gestão,
esfera administrativa, turno, serviços e estado.

## O que está sendo feito

O objetivo, seguindo a especificação do projeto ([enunciado.txt](enunciado.txt)), é implementar e comparar
**Regressão Linear com regularização Ridge** e **Gradiente Descendente** (treino e predição), avaliando com **R²**, **MSE** e **erro absoluto (MAE)**.

Etapas do notebook [Trabalho_Regressão.ipynb](Trabalho_Regressão.ipynb):

1. **Carga dos dados:** consulta SQL no BigQuery que junta a tabela de estabelecimentos do CNES com a contagem de
   profissionais distintos (cartão nacional de saúde) de cada estabelecimento, em janeiro de 2026: cerca de 472 mil
   estabelecimentos e 205 colunas.
2. **Limpeza:** remoção de identificadores, endereços, dados bancários e colunas constantes ou 100% nulas; preenchimento
   dos poucos nulos restantes com `nao_informado`.
3. **Preparação:** separação do alvo (`qtd_profissionais`), divisão treino/teste (80/20), one-hot encoding das colunas
   categóricas e padronização das numéricas, resultando em 307 atributos.
4. **Análise de correlação** de cada atributo com o alvo (em andamento).

Próximas etapas previstas na especificação: avaliação do desbalanceamento, visualização com t-SNE (sem e com rótulos),
Ridge × Gradiente Descendente com R², MSE e erro absoluto, análise dos pesos e da variação dos parâmetros ao longo do treino.

## Como rodar

O notebook foi feito para o **Google Colab**, porque usa a autenticação do Google para consultar o BigQuery.

1. Abra o notebook no Colab.
2. Crie (ou use) um projeto no [Google Cloud](https://console.cloud.google.com/) com a API do BigQuery ativada e troque
   o valor de `PROJETO` pelo ID do seu projeto. Ele é usado para contabilizar as consultas ao BigQuery.
3. Execute todas as células (`Ambiente de execução › Executar tudo`) e autorize o acesso quando o Colab pedir.

A biblioteca `basedosdados` é instalada pela primeira célula. As demais dependências (pandas, numpy, scikit-learn,
matplotlib) já vêm no Colab.

## Dataset

- **Fonte:** CNES – Cadastro Nacional de Estabelecimentos de Saúde, do **DATASUS / Ministério da Saúde**.
- **Acesso:** tabelas tratadas e disponibilizadas no BigQuery pela [Base dos Dados](https://basedosdados.org/)
  (`basedosdados.br_ms_cnes.estabelecimento` e `basedosdados.br_ms_cnes.profissional`).

Créditos dos dados ao Ministério da Saúde (DATASUS) e à Base dos Dados pelo tratamento e disponibilização.

## Arquivos

| Arquivo | Conteúdo |
|---|---|
| `Trabalho_Regressão.ipynb` | Notebook do projeto |
| `enunciado.txt` | Enunciado do projeto |

## Créditos

Trabalho desenvolvido para a disciplina de **Inteligência Artificial** do curso de Bacharelado em Ciência da Computação
do Instituto Federal de Goiás (IFG), ministrada pelo
[Prof. Dr. Daniel Xavier de Sousa](https://www.escavador.com/sobre/3446148/daniel-xavier-de-sousa).

Feito pelas alunas **Karolayne Amábile Brito Borges** e **[Ana Laura Machado Pereira](https://github.com/aanalaura)**.

## Licença

O código deste projeto está sob a [licença MIT](LICENSE). A base de dados segue a licença e os termos de uso da sua fonte original.
