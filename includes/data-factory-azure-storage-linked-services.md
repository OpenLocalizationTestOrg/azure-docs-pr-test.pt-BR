### <a name="azure-storage-linked-service"></a>Serviço vinculado de armazenamento do Azure
Olá **serviço vinculado do armazenamento do Azure** permite que você toolink uma fábrica de dados do Azure de tooan de conta de armazenamento do Azure usando Olá **chave de conta**, que permite a fábrica de dados Olá com toohello de acesso global do Azure Armazenamento. Olá, a tabela a seguir fornece uma descrição para o JSON de elementos específico tooAzure serviço vinculado de armazenamento.

| Propriedade | Descrição | Obrigatório |
|:--- |:--- |:--- |
| type |propriedade de tipo Hello deve ser definida como: **AzureStorage** |Sim |
| connectionString |Especifique informações necessárias tooconnect tooAzure armazenamento para a propriedade connectionString de saudação. |Sim |

Consulte Olá artigo para a chave da conta de saudação tooview/copiar etapas a seguir para um armazenamento do Azure: [exibir, copiar e regenerar as contas de acesso de armazenamento](../articles/storage/common/storage-create-storage-account.md#manage-your-storage-account).

**Exemplo:**  

```json
{  
    "name": "StorageLinkedService",  
    "properties": {  
        "type": "AzureStorage",  
        "typeProperties": {  
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"  
        }  
    }  
}  
```

### <a name="azure-storage-sas-linked-service"></a>Serviço vinculado de SAS de armazenamento do Azure
Uma assinatura de acesso compartilhado (SAS) fornece acesso delegado tooresources na sua conta de armazenamento. Ele permite toogrant um cliente limitado tooobjects permissões na conta de armazenamento para um determinado período de tempo e com um conjunto especificado de permissões, sem ter que tooshare suas chaves de acesso da conta. Olá SAS é um URI que abrange em seus parâmetros de consulta todas as informações de saudação necessárias para o recurso de armazenamento de tooa acesso autenticado. tooaccess recursos de armazenamento com hello SAS, Olá cliente precisa apenas de toopass no construtor apropriado do toohello Olá SAS ou método. Para obter informações detalhadas sobre SAS, consulte [assinaturas de acesso compartilhado: Olá Noções básicas sobre o modelo de SAS](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md)

> [!IMPORTANT]
> O Azure Data Factory agora dá suporte somente a **SAS do serviço**, mas não SAS de conta. Consulte [tipos de assinaturas de acesso compartilhado](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md#types-of-shared-access-signatures) para obter detalhes sobre esses dois tipos e como tooconstruct. Saudação de Observação URL SAS generable do portal do Azure ou o Gerenciador de armazenamento é uma SAS da conta, que não é suportado.
> 

Olá SAS de armazenamento do Azure vinculada serviço permite que você toolink uma conta de armazenamento do Azure tooan data factory do Azure usando uma assinatura de acesso compartilhado (SAS). Ele fornece fábrica de dados Olá com acesso restrito/limite de tempo específicos/tooall recursos (blob/contêiner) no armazenamento de saudação. Olá, a tabela a seguir fornece uma descrição para o JSON de elementos específico tooAzure serviço de armazenamento SAS vinculado. 

| Propriedade | Descrição | Obrigatório |
|:--- |:--- |:--- |
| type |propriedade de tipo Hello deve ser definida como: **o AzureStorageSas** |Sim |
| sasUri |Especifica os recursos de armazenamento do Azure do URI de assinatura de acesso compartilhado toohello como blob, contêiner ou tabela.  |Sim |

**Exemplo:**

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<Specify SAS URI of hello Azure Storage resource>"   
        }  
    }  
}  
```

Ao criar um **URI SAS**, considerando Olá seguinte:  

* Conjunto apropriado de leitura/gravação **permissões** em objetos com base em como Olá vinculados (leitura, gravação, leitura/gravação) de serviço é usado em sua fábrica de dados.
* Defina o **Tempo de expiração** adequadamente. Certifique-se de que objetos de armazenamento Olá acesso tooAzure não expirar dentro do período ativo de saudação do pipeline de saudação.
* URI deve ser criado no contêiner/blob Olá direita ou nível de tabela com base em Olá necessário. Tooan um Uri de SAS BLOBs do Azure permite Olá tooaccess de serviço de fábrica de dados blob específico. Um contêiner de BLOBs do Azure tooan Uri SAS permite Olá tooiterate de serviço de fábrica de dados por meio de blobs no contêiner. Se você precisa de acesso tooprovide mais/menos objetos mais tarde, ou atualização Olá SAS URI, lembre-se de tooupdate Olá vinculado serviço com hello novo URI.   

