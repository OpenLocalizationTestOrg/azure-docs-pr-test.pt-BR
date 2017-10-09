## <a name="repeatability-during-copy"></a>Capacidade de repetição durante a cópia
Quando a cópia tooAzure de dados SQL do SQL Server de outros dados armazena uma repetição de tookeep necessidades em mente tooavoid resultados não intencionais. 

Ao copiar dados tooAzure banco de dados SQL do SQL Server, a atividade de cópia será pela tabela de coletor padrão ACRESCENTAR Olá conjunto de dados toohello por padrão. Por exemplo, ao copiar dados de uma fonte de arquivo CSV (dados de valores separados por vírgula) que contém dois registros tooAzure banco de dados SQL do SQL Server, isso é que tabela Olá parece com:

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

Suponha que você encontrou erros no arquivo de origem e a quantidade de Olá atualizado de busca tubo de too4 2 no arquivo de origem de saudação. Se você executar novamente a fatia de dados Olá para esse período, você encontrará dois novos registros acrescentado tooAzure banco de dados SQL do SQL Server. Olá abaixo assume que nenhuma Olá colunas na tabela de saudação tem restrição de chave primária hello.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

tooavoid isso, você precisará de semântica UPSERT toospecify utilizando uma saudação abaixo 2 mecanismos descrito abaixo.

> [!NOTE]
> Uma fatia pode ser executada novamente automaticamente na fábrica de dados do Azure de acordo com a política de repetição de saudação especificada.
> 
> 

### <a name="mechanism-1"></a>Mecanismo 1
Você pode aproveitar **sqlWriterCleanupScript** propriedade toofirst executar a ação de limpeza quando uma fatia é executada. 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

Olá script de limpeza deve ser executado primeiro durante a cópia para uma determinada fatia que excluirá dados saudação da fatia de toothat Olá tabela SQL correspondente. atividade de saudação subsequentemente inserirá dados saudação no hello tabela SQL. 

Se a fatia de saudação é agora execute novamente, em seguida, você encontrará a quantidade de saudação é atualizada como desejado.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

Suponha que Olá registro Arruela simples é removido do csv original hello. Em seguida, executando novamente fatia de saudação produziria Olá resultados a seguir: 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```
Nada de novo tinha toobe feito. atividade de cópia Olá ficou Olá limpeza script toodelete Olá dados correspondentes para essa fatia. Em seguida, ele lê a entrada de saudação do csv hello (que, em seguida, continha apenas 1 registro) e inseri-lo no hello tabela. 

### <a name="mechanism-2"></a>Mecanismo 2
> [!IMPORTANT]
> No momento, não há suporte para sliceIdentifierColumnName no SQL Data Warehouse do Azure. 

Capacidade de repetição do outro mecanismo tooachieve é ter uma coluna dedicada (**sliceIdentifierColumnName**) no hello tabela de destino. Essa coluna seria usada pelo Azure Data Factory tooensure Olá origem e destino fique sincronizado. Essa abordagem funciona quando há flexibilidade ao alterar ou definir o esquema de tabela SQL de destino de saudação. 

Esta coluna será usada pela fábrica de dados do Azure para fins de repetição e no processo de saudação do Azure Data Factory não fará qualquer esquema toohello tabela é alterado. Modo toouse essa abordagem:

1. Defina uma coluna do tipo binary (32) no destino Olá tabela SQL. Não deve haver nenhuma restrição nessa coluna. Vamos nomear esta coluna como 'ColumnForADFuseOnly' para este exemplo.
2. Usá-lo na atividade de cópia de saudação da seguinte maneira:
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "ColumnForADFuseOnly"
    }
    ```

O Azure Data Factory preencherá essa coluna de acordo com sua necessidade tooensure Olá origem e destino permanecem sincronizados. valores de saudação desta coluna não devem ser usados fora deste contexto por usuário hello. 

Semelhante toomechanism 1, será de atividade de cópia automaticamente primeiro limpar dados Olá para Olá fornecidas fatia do destino Olá tabela SQL e execute a atividade de cópia Olá normalmente tooinsert dados Olá toodestination de origem para essa fatia. 

