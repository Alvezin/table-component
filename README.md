# Componente de tabela - VUE 2

Props aceitas pelo componente: 

## `table-columns` 
  - Um array de objetos com o nome das colunas

## `table-cell-config`
  - Um array que contém a 'configuração' de cada celula da linha:
  ```javascript 
  {
    attrToShow: 'Atributo do objeto passado que será apresentado nas célula de terminada coluna',
    path: 'Atributo opcional, onde é passado o caminho de componente externo que pode ser adicionado na célula',
    atributos: 'opcional, um objeto com os atributos do componente externo a ser renderizado',
   }
   ```
   
## `items`
    - Array com os itens a serem apresentados na tabela
    
    
# SLOTS

## `#cell`
  - Você pode ter acesso ao template das celulas dos items, juntos com alguns valores: 
     * `itemIndex`: index do item em relação ao array passado no componente
     * `attribute`: indica qual atributo está sendo passado na determinada célula
     * `value`: o valor que está sendo passado na célula
     
## `#beforeCellContent`
  - Aqui pode ser adicionado dados antes do conteúdo normal da célula, temos acesso a alguns valores:
     * `itemIndex`: index do item em relação ao array passado no componente
     * `attribute`: indica qual atributo está sendo passado na determinada célula
     
## `#afterCellContent`
  - Aqui pode ser adicionado dados após o conteúdo normal da célula, temos acesso a alguns valores:
     * `itemIndex`: index do item em relação ao array passado no componente
     * `attribute`: indica qual atributo está sendo passado na determinada célula
     
## `#lastColumn`
  - Acesso a última coluna da tabela, pode adicionar itens como botões, etc, valores que tem acesso:
     * `itemIndex`: index do item em relação ao array passado no componente
     * `id`: id do objeto
