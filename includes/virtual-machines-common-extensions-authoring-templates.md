## <a name="overview-of-azure-resource-manager-templates"></a>Visão geral dos modelos do Gerenciador de Recursos do Azure
Modelos do Gerenciador de recursos do Azure permitem que você toodeclaratively especificar infraestrutura do Azure IaaS Olá no idioma de Json definindo dependências Olá entre os recursos. Para obter uma visão geral detalhada dos modelos do Gerenciador de recursos do Azure, consulte toohello artigo abaixo:

[Visão geral do Grupo de Recursos](../articles/azure-resource-manager/resource-group-overview.md)

## <a name="sample-template-snippet-for-vm-extensions"></a>Trecho de código do modelo de exemplo para extensões de VM
Toodeclaratively implantar extensões de VM como parte de um modelo do Azure Resource Manager requer que você especifique configuração da extensão Olá no modelo de saudação.
Aqui é o formato de saudação para especificar a configuração da extensão hello.

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

Como você pode ver da saudação acima, o modelo de extensão Olá contém duas partes principais:

1. Nome da extensão, editor e versão
2. Configuração da Extensão.

## <a name="identifying-hello-publisher-type-and-typehandlerversion-for-any-extension"></a>Identificação de publicador hello, tipo e typeHandlerVersion para qualquer extensão
Extensões VM do Azure são publicadas pela Microsoft e confiança 3º Publicadores de terceiros e cada extensão é identificada exclusivamente pelo seu typeHandlerVersion publisher, tipo e hello. Elas podem ser determinadas da seguinte maneira:  

