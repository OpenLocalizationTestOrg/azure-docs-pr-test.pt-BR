## <a name="overview-of-azure-resource-manager-templates"></a><span data-ttu-id="3e39a-101">Visão geral dos modelos do Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="3e39a-101">Overview of Azure Resource Manager templates</span></span>
<span data-ttu-id="3e39a-102">O modelo do Azure Resource Manager permite especificar de forma declarativa a infraestrutura IaaS do Azure na linguagem JSON definindo as dependências entre recursos.</span><span class="sxs-lookup"><span data-stu-id="3e39a-102">Azure Resource Manager templates allow you to declaratively specify the Azure IaaS infrastructure in Json language by defining the dependencies between resources.</span></span> <span data-ttu-id="3e39a-103">Para obter uma visão geral detalhada dos Modelos do Azure Resource Manager, consulte os artigos abaixo:</span><span class="sxs-lookup"><span data-stu-id="3e39a-103">For a detailed overview of Azure Resource Manager Templates, please refer to the article below:</span></span>

[<span data-ttu-id="3e39a-104">Visão geral do Grupo de Recursos</span><span class="sxs-lookup"><span data-stu-id="3e39a-104">Resource Group Overview</span></span>](../articles/azure-resource-manager/resource-group-overview.md)

## <a name="sample-template-snippet-for-vm-extensions"></a><span data-ttu-id="3e39a-105">Trecho de código do modelo de exemplo para extensões de VM</span><span class="sxs-lookup"><span data-stu-id="3e39a-105">Sample template snippet for VM extensions</span></span>
<span data-ttu-id="3e39a-106">Implantar as extensões de VM como parte de um modelo do Azure Resource Manager exige uma especificação declarativa e a configuração da extensão no modelo.</span><span class="sxs-lookup"><span data-stu-id="3e39a-106">Deploying VM extensions as part of an Azure Resource Manager template requires you to declaratively specify the extension configuration in the template.</span></span>
<span data-ttu-id="3e39a-107">Veja abaixo o formato para especificar a configuração da extensão.</span><span class="sxs-lookup"><span data-stu-id="3e39a-107">Here is the format for specifying the extension configuration.</span></span>

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

<span data-ttu-id="3e39a-108">Como você pode ver no exemplo acima, o modelo de extensão contém duas partes principais:</span><span class="sxs-lookup"><span data-stu-id="3e39a-108">As you can see from the above, the extension template contains two main parts:</span></span>

1. <span data-ttu-id="3e39a-109">Nome da extensão, editor e versão</span><span class="sxs-lookup"><span data-stu-id="3e39a-109">Extension name, publisher and version</span></span>
2. <span data-ttu-id="3e39a-110">Configuração da Extensão.</span><span class="sxs-lookup"><span data-stu-id="3e39a-110">Extension Configuration.</span></span>

## <a name="identifying-the-publisher-type-and-typehandlerversion-for-any-extension"></a><span data-ttu-id="3e39a-111">Identificando o editor, o tipo e a typeHandlerVersion de qualquer extensão</span><span class="sxs-lookup"><span data-stu-id="3e39a-111">Identifying the publisher, type, and typeHandlerVersion for any extension</span></span>
<span data-ttu-id="3e39a-112">As extensões de VM do Azure são publicadas pela Microsoft e por editores terceiros confiáveis, e cada extensão é identificada exclusivamente por seu editor, tipo e typeHandlerVersion.</span><span class="sxs-lookup"><span data-stu-id="3e39a-112">Azure VM extensions are published by Microsoft and trusted 3rd party publishers and each extension is uniquely identified by its publisher,type and the typeHandlerVersion.</span></span> <span data-ttu-id="3e39a-113">Elas podem ser determinadas da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="3e39a-113">These can be determined as following:</span></span>  

