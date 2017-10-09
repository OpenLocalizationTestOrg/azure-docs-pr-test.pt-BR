
### <a name="cacheskuname"></a><span data-ttu-id="b00a7-101">cacheSKUName</span><span class="sxs-lookup"><span data-stu-id="b00a7-101">cacheSKUName</span></span>
<span data-ttu-id="b00a7-102">camada de preços Olá Olá do Cache Redis do Azure nova.</span><span class="sxs-lookup"><span data-stu-id="b00a7-102">hello pricing tier of hello new Azure Redis Cache.</span></span>

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

<span data-ttu-id="b00a7-103">modelo Olá define os valores de saudação que são permitidos para este parâmetro (básico ou padrão) e atribui um valor padrão (Basic) se nenhum valor for especificado.</span><span class="sxs-lookup"><span data-stu-id="b00a7-103">hello template defines hello values that are permitted for this parameter (Basic or Standard), and assigns a default value (Basic) if no value is specified.</span></span> <span data-ttu-id="b00a7-104">Basic fornece um único nó com vários tamanhos de backup too53 GB.</span><span class="sxs-lookup"><span data-stu-id="b00a7-104">Basic provides a single node with multiple sizes available up too53 GB.</span></span>
<span data-ttu-id="b00a7-105">Padrão fornece dois nós primário/réplica com vários tamanhos de backup de SLA de too53 GB e 99,9%.</span><span class="sxs-lookup"><span data-stu-id="b00a7-105">Standard provides two-node Primary/Replica with multiple sizes available up too53 GB and 99.9% SLA.</span></span>

### <a name="cacheskufamily"></a><span data-ttu-id="b00a7-106">cacheSKUFamily</span><span class="sxs-lookup"><span data-stu-id="b00a7-106">cacheSKUFamily</span></span>
<span data-ttu-id="b00a7-107">família Olá Olá SKU.</span><span class="sxs-lookup"><span data-stu-id="b00a7-107">hello family for hello sku.</span></span>

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


### <a name="cacheskucapacity"></a><span data-ttu-id="b00a7-108">cacheSKUCapacity</span><span class="sxs-lookup"><span data-stu-id="b00a7-108">cacheSKUCapacity</span></span>
<span data-ttu-id="b00a7-109">tamanho de saudação de nova instância de Cache Redis do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b00a7-109">hello size of hello new Azure Redis Cache instance.</span></span> 

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


<span data-ttu-id="b00a7-110">Olá modelo define os valores de saudação que são permitidos para este parâmetro (0, 1, 2, 3, 4, 5 ou 6) e atribui um valor padrão (1) se nenhum valor for especificado.</span><span class="sxs-lookup"><span data-stu-id="b00a7-110">hello template defines hello values that are permitted for this parameter (0, 1, 2, 3, 4, 5 or 6), and assigns a default value (1) if no value is specified.</span></span> <span data-ttu-id="b00a7-111">Esses números correspondem a tamanhos de cache toofollowing: 0 = 250 MB, 1 = 1 GB, 2 = 2,5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB</span><span class="sxs-lookup"><span data-stu-id="b00a7-111">Those numbers correspond toofollowing cache sizes: 0 = 250 MB, 1 = 1 GB, 2 = 2.5 GB, 3 = 6 GB, 4 = 13 GB, 5 = 26 GB, 6 = 53 GB</span></span>

