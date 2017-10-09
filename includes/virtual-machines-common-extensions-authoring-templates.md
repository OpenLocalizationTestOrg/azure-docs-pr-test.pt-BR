## <a name="overview-of-azure-resource-manager-templates"></a><span data-ttu-id="14cd5-101">Visão geral dos modelos do Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="14cd5-101">Overview of Azure Resource Manager templates</span></span>
<span data-ttu-id="14cd5-102">Modelos do Gerenciador de recursos do Azure permitem que você toodeclaratively especificar infraestrutura do Azure IaaS Olá no idioma de Json definindo dependências Olá entre os recursos.</span><span class="sxs-lookup"><span data-stu-id="14cd5-102">Azure Resource Manager templates allow you toodeclaratively specify hello Azure IaaS infrastructure in Json language by defining hello dependencies between resources.</span></span> <span data-ttu-id="14cd5-103">Para obter uma visão geral detalhada dos modelos do Gerenciador de recursos do Azure, consulte toohello artigo abaixo:</span><span class="sxs-lookup"><span data-stu-id="14cd5-103">For a detailed overview of Azure Resource Manager Templates, please refer toohello article below:</span></span>

[<span data-ttu-id="14cd5-104">Visão geral do Grupo de Recursos</span><span class="sxs-lookup"><span data-stu-id="14cd5-104">Resource Group Overview</span></span>](../articles/azure-resource-manager/resource-group-overview.md)

## <a name="sample-template-snippet-for-vm-extensions"></a><span data-ttu-id="14cd5-105">Trecho de código do modelo de exemplo para extensões de VM</span><span class="sxs-lookup"><span data-stu-id="14cd5-105">Sample template snippet for VM extensions</span></span>
<span data-ttu-id="14cd5-106">Toodeclaratively implantar extensões de VM como parte de um modelo do Azure Resource Manager requer que você especifique configuração da extensão Olá no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="14cd5-106">Deploying VM extensions as part of an Azure Resource Manager template requires you toodeclaratively specify hello extension configuration in hello template.</span></span>
<span data-ttu-id="14cd5-107">Aqui é o formato de saudação para especificar a configuração da extensão hello.</span><span class="sxs-lookup"><span data-stu-id="14cd5-107">Here is hello format for specifying hello extension configuration.</span></span>

      {
      "type": "Microsoft.Compute/virtualMachines/extensions",
      "name": "MyExtension",
      "apiVersion": "2015-05-01-preview",
      "location": "[parameters('location')]",
      "dependsOn": ["[concat('Microsoft.Compute/virtualMachines/',parameters('vmName'))]"],
      "properties":
      {
      "publisher": "Publisher Namespace",
      "type": "extension Name",
      "typeHandlerVersion": "extension version",
      "settings": {
      // Extension specific configuration goes in here.
      }
      }
      }

<span data-ttu-id="14cd5-108">Como você pode ver da saudação acima, o modelo de extensão Olá contém duas partes principais:</span><span class="sxs-lookup"><span data-stu-id="14cd5-108">As you can see from hello above, hello extension template contains two main parts:</span></span>

1. <span data-ttu-id="14cd5-109">Nome da extensão, editor e versão</span><span class="sxs-lookup"><span data-stu-id="14cd5-109">Extension name, publisher and version</span></span>
2. <span data-ttu-id="14cd5-110">Configuração da Extensão.</span><span class="sxs-lookup"><span data-stu-id="14cd5-110">Extension Configuration.</span></span>

## <a name="identifying-hello-publisher-type-and-typehandlerversion-for-any-extension"></a><span data-ttu-id="14cd5-111">Identificação de publicador hello, tipo e typeHandlerVersion para qualquer extensão</span><span class="sxs-lookup"><span data-stu-id="14cd5-111">Identifying hello publisher, type, and typeHandlerVersion for any extension</span></span>
<span data-ttu-id="14cd5-112">Extensões VM do Azure são publicadas pela Microsoft e confiança 3º Publicadores de terceiros e cada extensão é identificada exclusivamente pelo seu typeHandlerVersion publisher, tipo e hello.</span><span class="sxs-lookup"><span data-stu-id="14cd5-112">Azure VM extensions are published by Microsoft and trusted 3rd party publishers and each extension is uniquely identified by its publisher,type and hello typeHandlerVersion.</span></span> <span data-ttu-id="14cd5-113">Elas podem ser determinadas da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="14cd5-113">These can be determined as following:</span></span>  

