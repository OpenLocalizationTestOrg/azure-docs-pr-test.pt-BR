
### <a name="cacheskuname"></a>cacheSKUName
camada de preços Olá Olá do Cache Redis do Azure nova.

    "cacheSKUName": {
      "type": "string",
      "allowedValues": [
        "Basic",
        "Standard"
      ],
      "defaultValue": "Basic",
      "metadata": {
        "description": "hello pricing tier of hello new Azure Redis Cache."
      }
    },

modelo Olá define os valores de saudação que são permitidos para este parâmetro (básico ou padrão) e atribui um valor padrão (Basic) se nenhum valor for especificado. Basic fornece um único nó com vários tamanhos de backup too53 GB.
Padrão fornece dois nós primário/réplica com vários tamanhos de backup de SLA de too53 GB e 99,9%.

### <a name="cacheskufamily"></a>cacheSKUFamily
família Olá Olá SKU.

    "cacheSKUFamily": {
      "type": "string",
      "allowedValues": [
        "C"
      ],
      "defaultValue": "C",
      "metadata": {
        "description": "hello family for hello sku."
      }
    },


### <a name="cacheskucapacity"></a>cacheSKUCapacity
tamanho de saudação de nova instância de Cache Redis do Azure hello. 

    "cacheSKUCapacity": {
      "type": "int",
      "allowedValues": [
        0,
        1,
        2,
        3,
        4,
        5,
        6
      ],
      "defaultValue": 0,
      "metadata": {
        "description": "hello size of hello new Azure Redis Cache instance. "
      }
    }


Olá modelo define os valores de saudação que são permitidos para este parâmetro (0, 1, 2, 3, 4, 5 ou 6) e atribui um valor padrão (1) se nenhum valor for especificado. Esses números correspondem a tamanhos de cache toofollowing: 0 = 250 MB, 1 = 1 GB, 2 = 2,5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB

