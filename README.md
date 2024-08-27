# analise-de-dados-dief
análise dos documentos DIEF (Declaração de Informações Econômico-Fiscais) no contexto do SPED-EFD (Sistema Público de Escrituração Digital – Escrituração Fiscal Digital)
# Projeto de Análise de Dados e Automação de Processos para DIEF (SPED-EFD)

## Descrição
Este projeto tem como objetivo otimizar o processo de leitura e análise dos documentos DIEF no contexto do SPED-EFD.

## Problema
A análise manual dos documentos DIEF apresentava desafios significativos, como altos tempos de processamento e uma maior probabilidade de erros.

## Solução
Desenvolvi uma solução de automação que inclui leitura e processamento eficiente, análise acurada e melhoria de performance.

# Passos para Modelagem de Dados usando Power Query

## Importar o Documento DIEF:

1. Abra o Excel e vá para a guia **Dados**.
2. Clique em **Obter Dados** e selecione a fonte de dados apropriada (por exemplo, arquivo Excel, CSV, TXT, etc.).
3. Navegue até o documento DIEF e importe-o.

## Transformar Dados no Power Query:

- O Power Query Editor será aberto automaticamente. Aqui, você pode transformar os dados conforme necessário.

## Limpar e Transformar Dados:

- **Remover Colunas Desnecessárias:** Clique com o botão direito na coluna que você não precisa e selecione **Remover**.
- **Filtrar Dados:** Aplique filtros para remover ou selecionar dados específicos.
- **Alterar Tipos de Dados:** Certifique-se de que as colunas têm os tipos de dados corretos (por exemplo, número, texto, data).
- **Dividir Colunas:** Se uma coluna contiver múltiplas informações (por exemplo, "Item:1234 - Descrição: ABC"), você pode dividi-la usando **Dividir Coluna > Por Delimitador**.
- **Unpivot/Colapsar Colunas:** Se você tiver colunas que representam valores diferentes, pode ser útil usar a função **Desagrupar Colunas** para transformar colunas em linhas.

## Mesclar e Combinar Dados:

- Se o documento DIEF estiver dividido em várias tabelas ou planilhas, você pode combinar essas tabelas usando a função **Mesclar Consultas** ou **Anexar Consultas**.

## Adicionar Colunas Calculadas:

- Use a opção **Adicionar Coluna** para criar colunas calculadas baseadas em expressões ou fórmulas.

## Aplicar Outras Transformações:

- **Agrupar Por:** Agrupe os dados por uma ou mais colunas para sumarizar informações.
- **Pivotear Colunas:** Se precisar reorganizar os dados, use a função **Pivotar Colunas**.
- **Ordenar Dados:** Ordene as colunas conforme necessário.

## Carregar Dados de Volta para o Excel:

- Quando estiver satisfeito com as transformações, clique em **Fechar e Carregar** para carregar os dados de volta no Excel.
- Você pode carregar os dados como uma tabela ou criar um relatório dinâmico (por exemplo, Tabela Dinâmica).
  
## Criando um Codigo M

let
    Fonte = Excel.Workbook(File.Contents("C:\Caminho\Para\Seu\Arquivo.xlsx"), null, true),
    Tabela1 = Fonte{[Name="Tabela1"]}[Data],
    ColunasRemovidas = Table.RemoveColumns(Tabela1,{"ColunaQueNaoQuero"}),
    TipoAlterado = Table.TransformColumnTypes(ColunasRemovidas,{{"Data", type date}, {"Valor", type number}}),
    LinhasFiltradas = Table.SelectRows(TipoAlterado, each ([Valor] > 1000)),
    ColunaCalculada = Table.AddColumn(LinhasFiltradas, "Valor com Imposto", each [Valor] * 1.18),
    DadosFinal = Table.RemoveColumns(ColunaCalculada,{"Valor"})
in
    DadosFinal
- Este código M faz o seguinte:
- Importa os dados de um arquivo Excel.
- Remove uma coluna desnecessária.
- Altera o tipo de dados de algumas colunas.
- Filtra as linhas com base em um critério.
- Adiciona uma nova coluna calculada.
- Remove a coluna original após o cálculo.
  
  ## Observações
  
- A estrutura exata do código dependerá dos dados específicos e das transformações necessárias.
- Após configurar isso uma vez, o Power Query permite que você atualize os dados automaticamente quando o documento DIEF é atualizado, sem precisar repetir todo o processo manualmente.
