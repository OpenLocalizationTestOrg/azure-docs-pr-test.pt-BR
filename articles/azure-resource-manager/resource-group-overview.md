---
title: "Visão geral do Gerenciador de recursos de aaaAzure | Microsoft Docs"
description: "Descreve como toouse Gerenciador de recursos do Azure para implantação, gerenciamento e controle de acesso de recursos no Azure."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 76df7de1-1d3b-436e-9b44-e1b3766b3961
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: tomfitz
ms.openlocfilehash: a44fccd96d722c006224145d71cc44292255debf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-overview"></a>Visão geral do Azure Resource Manager
infraestrutura de saudação para seu aplicativo normalmente é composta de vários componentes – talvez uma máquina virtual, conta de armazenamento e rede virtual, ou um aplicativo web, banco de dados, servidor de banco de dados e 3º serviços de terceiros. Tais componentes não são vistos como entidades separadas, em vez disso, eles são mostrados como partes relacionadas e interdependentes de uma única entidade. Você deseja toodeploy, gerenciar e monitorá-los como um grupo. Gerenciador de recursos do Azure permite que você toowork com recursos de saudação em sua solução como um grupo. Você pode implantar, atualizar ou excluir todos os recursos de saudação para sua solução em uma única operação coordenada. Usar um modelo para a implantação e esse modelo pode ser útil para ambientes diferentes, como teste, preparação e produção. Gerenciador de recursos fornece segurança, auditoria e marcação recursos toohelp gerenciar seus recursos após a implantação. 

## <a name="terminology"></a>Terminologia
Se você estiver tooAzure novo Gerenciador de recursos, há alguns termos que você pode não estar familiarizado com.

* **recurso** -um item gerenciável que está disponível por meio do Azure. Alguns recursos comuns são uma máquina virtual, conta de armazenamento, aplicativo Web, banco de dados e rede virtual, mas há muito mais.
* **grupo de recursos** - Um contêiner que mantém os recursos relacionados a uma solução do Azure. grupo de recursos de saudação pode incluir todos os recursos de saudação para solução hello, ou apenas os recursos que você deseja toomanage como um grupo. Decidir como deseja que os recursos de tooallocate tooresource grupos com base no que torna hello mais sentido para sua organização. Confira [Grupos de recursos](#resource-groups).
* **provedor de recursos** -um serviço que fornece recursos de saudação que você pode implantar e gerenciar por meio do Gerenciador de recursos. Cada provedor de recursos oferece operações para trabalhar com recursos de saudação que são implantados. Alguns provedores de recursos comuns são Microsoft. Compute, que fornece recursos de máquina virtual hello, Microsoft, que fornece o recurso de conta de armazenamento Olá, e Microsoft, que fornece recursos relacionados tooweb aplicativos. Confira [Provedores de recursos](#resource-providers).
* **Modelo do Gerenciador de recursos** -arquivo de um objeto JSON (JavaScript Notation) que define um ou mais recursos toodeploy tooa recurso grupo. Também define dependências Olá entre os recursos de saudação implantado. modelo de saudação pode ser usado toodeploy Olá recursos consistente e repetidamente. Confira [Implantação de modelo](#template-deployment).
* **sintaxe declarativa** -estado de sintaxe que permite que você "aqui está o que pretendo toocreate" sem a necessidade de sequência de saudação toowrite de programação comandos toocreate-lo. modelo do Gerenciador de recursos de saudação é um exemplo de sintaxe declarativa. No arquivo hello, você definir propriedades Olá Olá infraestrutura toodeploy tooAzure. 

## <a name="hello-benefits-of-using-resource-manager"></a>benefícios de saudação do usando o Gerenciador de recursos
O Gerenciador de Recursos fornece vários benefícios:

* Você pode implantar, gerenciar e monitorar todos os recursos de saudação para sua solução como um grupo, em vez de manipular esses recursos individualmente.
* Repetidamente, você pode implantar sua solução em todo o ciclo de vida de desenvolvimento hello e ter certeza de que seus recursos são implantados em um estado consistente.
* Você pode gerenciar sua infraestrutura por meio de modelos declarativos em vez de scripts.
* Você pode definir dependências de saudação entre os recursos para que eles são implantados na ordem correta, Olá.
* Você pode aplicar tooall serviços de controle de acesso no seu grupo de recursos como controle de acesso baseado em função (RBAC) nativamente é integrado à plataforma de gerenciamento de saudação.
* Você pode aplicar marcas tooresources toologically organizar todos os recursos de saudação em sua assinatura.
* Você pode esclarecer a cobrança da sua organização exibindo custos para um grupo de recursos de compartilhamento Olá a mesma marca.  

Gerenciador de recursos fornece um novo toodeploy de maneira e gerenciar suas soluções. Se você usou Olá modelo de implantação anterior e deseja toolearn sobre alterações hello, consulte [Noções básicas sobre o Gerenciador de recursos de implantação e implantação clássica](resource-manager-deployment-model.md).

## <a name="consistent-management-layer"></a>Camada de gerenciamento consistente
Gerenciador de recursos fornece uma camada de gerenciamento consistente para tarefas de saudação executadas por meio do Azure PowerShell, CLI do Azure, portal do Azure, API REST e ferramentas de desenvolvimento. Todas as ferramentas de saudação usam um conjunto comum de operações. Use as ferramentas de saudação que funcionam melhor para você e possam ser usados alternadamente sem confusão. 

Olá imagem a seguir mostra como todas as ferramentas de saudação interagem com hello mesma API do Gerenciador de recursos do Azure. Olá API passa as solicitações toohello o serviço Gerenciador de recursos, que autentica e autoriza Olá solicitações. Gerenciador de recursos, em seguida, encaminha provedores de recursos apropriado Olá solicitações toohello.

![Modelo de solicitação do Gerenciador de Recursos](./media/resource-group-overview/consistent-management-layer.png)

## <a name="guidance"></a>Diretrizes
Olá sugestões a seguir ajudarão a aproveitar ao máximo do Gerenciador de recursos ao trabalhar com suas soluções.

1. Definir e implantar sua infraestrutura por meio da sintaxe declarativa de saudação em modelos do Gerenciador de recursos, em vez de por meio de comandos obrigatório.
2. Defina todas as etapas de implantação e a configuração no modelo de saudação. Você não deve ter nenhuma etapa manual para configurar sua solução.
3. Executar comandos fundamental toomanage seus recursos, como toostart ou parar um aplicativo ou computador.
4. Organizar os recursos com hello mesmo ciclo de vida de um grupo de recursos. Use marcas para as demais organizações de recursos.

Para recomendações sobre modelos, consulte [Práticas recomendadas para criar modelos do Azure Resource Manager](resource-manager-template-best-practices.md).

Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).

## <a name="resource-groups"></a>Grupos de recursos
Existem alguns fatores importantes tooconsider ao definir o grupo de recursos:

1. Todos os recursos de saudação do seu grupo devem compartilhar Olá mesmo ciclo de vida. Você os implanta, atualiza e exclui juntos. Se precisar de um recurso, como um servidor de banco de dados, tooexist em um ciclo de implantação diferentes, ele deve ser em outro grupo de recursos.
2. Cada recurso só pode existir em um grupo de recursos.
3. Você pode adicionar ou remover um grupo de recursos do recurso tooa a qualquer momento.
4. Você pode mover um recurso de um grupo de tooanother de grupo de recursos. Para obter mais informações, consulte [Mover grupo de recursos toonew de recursos ou assinatura](resource-group-move-resources.md).
5. Um grupo de recursos pode conter recursos que residem em regiões diferentes.
6. Um grupo de recursos pode ser usado o controle de acesso tooscope para ações administrativas.
7. Um recurso pode interagir com recursos em outros grupos de recursos. Essa interação é comum quando os recursos de Olá dois relacionados, mas não compartilham Olá mesmo ciclo de vida (por exemplo, aplicativos da web conectar tooa banco de dados).

Ao criar um grupo de recursos, você precisa tooprovide um local para esse grupo de recursos. Você pode estar se perguntando: "Por que um grupo de recursos precisa de um local? E, se recursos Olá podem ter locais diferentes do grupo de recursos hello, por que é local do grupo de recursos de saudação importante em todos os?" grupo de recursos de saudação armazena metadados sobre os recursos de saudação. Portanto, quando você especificar um local para o grupo de recursos hello, você está especificando onde os metadados são armazenados. Por motivos de conformidade, talvez seja necessário tooensure que seus dados são armazenados em uma determinada região.

## <a name="resource-providers"></a>Provedores de recursos
Cada provedor de recursos oferece um conjunto de recursos e operações para trabalhar com um serviço do Azure. Por exemplo, se você quiser toostore chaves e segredos, você trabalha com hello **Microsoft.KeyVault** provedor de recursos. Este provedor de recursos oferece um tipo de recurso chamado **cofres** para a criação de Cofre de chaves hello. 

nome de saudação de um tipo de recurso está no formato de saudação: **{provedor de recursos} / {resource-type}**. Por exemplo, o tipo de Cofre de chaves de saudação é **Microsoft.KeyVault/vaults**.

Antes de começar a implantar seus recursos, você deve obter uma compreensão Olá disponíveis de provedores de recursos. Conhecer os nomes de saudação do recurso provedores e recursos ajuda a definir recursos que você deseja toodeploy tooAzure. Além disso, você precisará locais válidos do tooknow hello e as versões de API para cada tipo de recurso. Para saber mais, veja [Provedores e tipos de recursos](resource-manager-supported-services.md).

## <a name="template-deployment"></a>Implantação de modelo
Com o Gerenciador de recursos, você pode criar um modelo (no formato JSON) que define a infraestrutura de saudação e a configuração de sua solução do Azure. Usando um modelo, você pode implantar a solução repetidamente em todo seu ciclo de vida e com a confiança de que seus recursos serão implantados em um estado consistente. Quando você cria uma solução de portal hello, solução de saudação inclui automaticamente um modelo de implantação. Você não tem toocreate o modelo a partir do zero porque você pode iniciar com o modelo de saudação para sua solução e personalizá-lo toomeet suas necessidades específicas. Você pode recuperar um modelo para um grupo de recursos existente, exportar estado atual de Olá Olá do grupo de recursos ou exibir hello modelo usado para uma determinada implantação. Exibindo Olá [exportado modelo](resource-manager-export-template.md) é toolearn uma maneira útil sobre a sintaxe de modelo de saudação.

toolearn sobre o formato de saudação do modelo de saudação e de como você cria, consulte [criar seu primeiro modelo do Azure Resource Manager](resource-manager-create-first-template.md). Olá tooview sintaxe JSON para tipos de recursos, consulte [definir recursos em modelos do Azure Resource Manager](/azure/templates/).

Gerenciador de recursos processa o modelo de saudação como qualquer outra solicitação (veja imagem Olá para [camada de gerenciamento consistente](#consistent-management-layer)). Ele analisa o modelo hello e converte a sintaxe em operações da API REST para provedores de recursos apropriado de saudação. Por exemplo, quando o Gerenciador de recursos recebe um modelo com hello definição de recurso a seguir:

```json
"resources": [
  {
    "apiVersion": "2016-01-01",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "mystorageaccount",
    "location": "westus",
    "sku": {
      "name": "Standard_LRS"
    },
    "kind": "Storage",
    "properties": {
    }
  }
]
```

Ele converte Olá definição toohello operação da API REST, que é enviada de provedor de recursos do Microsoft toohello a seguir:

```HTTP
PUT
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/mystorageaccount?api-version=2016-01-01
REQUEST BODY
{
  "location": "westus",
  "properties": {
  }
  "sku": {
    "name": "Standard_LRS"
  },   
  "kind": "Storage"
}
```

Como você definir modelos e grupos de recursos é totalmente tooyou e como você deseja toomanage sua solução. Por exemplo, você pode implantar seu aplicativo de três camadas por meio de um único modelo tooa único grupo de recursos.

![modelo de três camadas](./media/resource-group-overview/3-tier-template.png)

Porém, você não tem toodefine toda a sua infraestrutura em um único modelo. Em geral, faz sentido toodivide seus requisitos de implantação em um conjunto de modelos de destino, a finalidade específica. Você pode reutilizar esses modelos facilmente para soluções diferentes. toodeploy uma solução específica, você cria um modelo de mestre que vincula a todos os modelos de saudação necessário. Olá imagem a seguir mostra como toodeploy uma solução de três camadas por meio de um modelo de pai que inclui três aninhada modelos.

![modelo de camadas aninhadas](./media/resource-group-overview/nested-tiers-template.png)

Se você prever os níveis de ter os ciclos de vida separados, você pode implantar os grupos de recursos de tooseparate de três camadas. Aviso Olá recursos ainda podem ser vinculado tooresources em outros grupos de recursos.

![modelo de camada](./media/resource-group-overview/tier-templates.png)

Para obter mais sugestões sobre a criação de modelos, confira [Padrões para a criação de modelos do Azure Resource Manager](best-practices-resource-manager-design-templates.md). Para obter informações sobre modelos aninhados, confira [Usando modelos vinculados com o Azure Resource Manager](resource-group-linked-templates.md).

Gerenciador de recursos do Azure analisa dependências tooensure recursos são criados na ordem correta hello. Se um recurso depende de um valor de outro recurso (como uma máquina virtual que precisa de uma conta de armazenamento para discos), você pode definir uma dependência. Para saber mais, confira [Definindo as dependências nos modelos do Gerenciador de Recursos do Azure](resource-group-define-dependencies.md).

Você também pode usar o modelo de saudação de infraestrutura de atualizações de toohello. Por exemplo, você pode adicionar uma solução de tooyour de recursos e adicionar as regras de configuração para os recursos de saudação que já foram implantados. Se o modelo de saudação especifica criando um recurso, mas esse recurso já existe, o Gerenciador de recursos do Azure executa uma atualização em vez de criar um novo ativo. Azure Resource Manager atualizações Olá existente ativo toohello mesmo estado que seria como novo.  

Gerenciador de recursos fornece extensões para cenários quando precisar de operações adicionais, como instalação de software específico que não está incluído na instalação de saudação. Se você já estiver usando um serviço de gerenciamento de configuração, como DSC, Chef ou Puppet, poderá continuar trabalhando com esse serviço usando as extensões. Para obter informações sobre extensões de máquina virtual, confira [Sobre recursos e extensões de máquina virtual](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Por fim, o modelo de saudação se torna parte do código-fonte Olá para seu aplicativo. Você pode fazer check-in tooyour repositório de código-fonte e atualizá-lo conforme se desenvolve seu aplicativo. Você pode editar o modelo de saudação através do Visual Studio.

Depois de definir o modelo, você está pronto toodeploy Olá recursos tooAzure. Para recursos de saudação do hello comandos toodeploy, consulte:

* [Implantar recursos com modelos do Resource Manager e o Azure PowerShell](resource-group-template-deploy.md)
* [Implantar recursos com modelos do Resource Manager e a CLI do Azure](resource-group-template-deploy-cli.md)
* [Implantar recursos com modelos do Resource Manager e o portal do Azure](resource-group-template-deploy-portal.md)
* [Implantar recursos com modelos do Resource Manager e a API REST do Resource Manager](resource-group-template-deploy-rest.md)

## <a name="tags"></a>Marcas
Gerenciador de recursos fornece um recurso de marcação que permite que você toocategorize recursos de acordo com os requisitos de tooyour para gerenciar ou de cobrança. Use marcas quando você tiver um conjunto complexo de grupos de recursos e recursos e precisa toovisualize esses ativos de maneira de saudação que torne Olá tooyou de mais sentido. Por exemplo, você pode marcar os recursos que servem para uma função semelhante em sua organização ou pertencem toohello mesmo departamento. Sem marcas, os usuários em sua organização podem criar vários recursos que podem ser toolater difícil identificam e gerenciar. Por exemplo, você poderá toodelete todos os recursos de saudação para um projeto específico. Se esses recursos não estão marcados para projeto hello, você terá toomanually encontrá-los. Marcação pode ser uma maneira importante para você tooreduce um custo desnecessário em sua assinatura. 

Recursos não é necessário tooreside em Olá tooshare de grupo de recursos mesmo uma marca. Você pode criar seu próprios tooensure taxonomia de marca que todos os usuários em sua organização usam marcas comum em vez de usuários a aplicação acidental de marcas ligeiramente diferentes (por exemplo, "Departamento" em vez de "Departamento").

saudação de exemplo a seguir mostra uma máquina de virtual tooa marca aplicado.

```json
"resources": [    
  {
    "type": "Microsoft.Compute/virtualMachines",
    "apiVersion": "2015-06-15",
    "name": "SimpleWindowsVM",
    "location": "[resourceGroup().location]",
    "tags": {
        "costCenter": "Finance"
    },
    ...
  }
]
```

tooretrieve todos os recursos de saudação com um valor de marca, usam Olá cmdlet do PowerShell a seguir:

```powershell
Find-AzureRmResource -TagName costCenter -TagValue Finance
```

Ou, hello Azure CLI 2.0 comando a seguir:

```azurecli
az resource list --tag costCenter=Finance
```

Você também pode exibir recursos marcados por meio de saudação portal do Azure.

Olá [relatório de uso](../billing/billing-understand-your-bill.md) para sua assinatura inclui nomes de marca e valores, que permite que você toobreak os custos por marcas. Para obter mais informações sobre marcas, consulte [usando marcas tooorganize seus recursos do Azure](resource-group-using-tags.md).

## <a name="access-control"></a>Controle de acesso
Gerenciador de recursos permite que você toocontrol quem tem acesso toospecific ações para sua organização. Modo nativo, ele integra o controle de acesso baseado em função (RBAC) a plataforma de gerenciamento de saudação e aplica-se que serviços de tooall de controle de acesso no seu grupo de recursos. 

Há dois toounderstand de conceitos principais ao trabalhar com o controle de acesso baseado em função:

* Definições de função - descrevem um conjunto de permissões e podem ser usadas em muitas atribuições.
* Atribuições de função - associam uma definição com uma identidade (usuário ou grupo) para um determinado escopo (assinatura, grupo de recursos ou recurso). atribuição de saudação é herdada por escopos inferiores.

Você pode adicionar plataforma definido toopre de usuários e funções específicas do recurso. Por exemplo, você pode tirar proveito da função de predefinidos Olá chamado leitor que permite que os usuários tooview recursos, mas não alterá-los. Adicionar usuários em sua organização que precisam desse tipo de função de leitor de toohello de acesso e aplicar a assinatura de toohello de função hello, o grupo de recursos ou o recurso.

O Azure fornece Olá quatro funções de plataforma a seguir:

1. O proprietário pode gerenciar tudo, incluindo o acesso
2. Os colaboradores podem gerenciar tudo, exceto o acesso
3. Os leitores podem ver tudo, mas não podem fazer alterações
4. Administrador de acesso do usuário - podem gerenciar recursos de tooAzure de acesso do usuário

O Azure também fornece várias funções específicas de recursos. Alguns tipos comuns são:

1. Colaborador da máquina virtual - pode gerenciar máquinas virtuais, mas não conceder acesso toothem e não pode gerenciar Olá virtual rede ou armazenamento conta toowhich estão conectados
2. Rede colaborador - pode gerenciar todos os recursos de rede, mas não conceder acesso toothem
3. Colaborador da conta de armazenamento - pode gerenciar contas de armazenamento, mas não conceder acesso toothem
4. Colaborador do SQL Server - pode gerenciar servidores SQL e bancos de dados, mas não suas políticas de segurança
5. Colaborador do site - pode gerenciar sites, mas não Olá web planos toowhich estão conectados

Para Olá a lista completa de funções e ações permitidas, consulte [RBAC: criado em funções](../active-directory/role-based-access-built-in-roles.md). Para obter mais informações sobre o controle de acesso baseado em função, consulte [Controle de acesso baseado em função do Azure](../active-directory/role-based-access-control-configure.md). 

Em alguns casos, você deseja toorun código ou script que acessa os recursos, mas não quiser toorun sob as credenciais do usuário. Em vez disso, você deseja toocreate uma identidade chamada de serviço principal para o aplicativo hello e atribuir a função apropriada Olá para a entidade de serviço hello. Gerenciador de recursos permite que você toocreate credenciais para o aplicativo hello e autenticar o aplicativo hello programaticamente. toolearn sobre a criação de entidades de serviço, consulte um dos seguintes tópicos:

* [Usar Azure PowerShell toocreate um serviço principal tooaccess recursos](resource-group-authenticate-service-principal.md)
* [Usar um serviço principal tooaccess recursos de toocreate CLI do Azure](resource-group-authenticate-service-principal-cli.md)
* [Use o aplicativo do portal toocreate Active Directory do Azure e a entidade de serviço que pode acessar os recursos](resource-group-create-service-principal-portal.md)

Explicitamente, você pode bloquear recursos críticos tooprevent os usuários excluam ou modificá-los. Para saber mais, confira [Bloquear recursos com o Gerenciador de Recursos do Azure](resource-group-lock-resources.md).

## <a name="activity-logs"></a>Logs de atividade
O Gerenciador de Recursos registra todas as operações que criam, modificam ou excluem um recurso. Você pode usar o hello atividade logs toofind um erro ao solucionar o problema ou toomonitor como um usuário em sua organização modificado a um recurso. logs de saudação toosee, selecione **logs de atividade** em Olá **configurações** folha para um grupo de recursos. Você pode filtrar logs Olá por muitos valores diferentes, incluindo qual operação de saudação iniciada pelo usuário. Para obter informações sobre como trabalhar com logs de atividade hello, consulte [toomanage Azure dos logs de atividades de exibição recursos](resource-group-audit.md).

## <a name="customized-policies"></a>Políticas personalizadas
Gerenciador de recursos permite que você toocreate personalizado de políticas para gerenciar os recursos. tipos de saudação de políticas que você criar podem incluir diversos cenários. Você pode impor uma convenção de nomenclatura para recursos, limitar os tipos e instâncias de recursos que podem ser implantados ou limitar quais regiões podem hospedar um tipo de recurso. Você pode exigir um valor de marca de cobrança de tooorganize de recursos por departamentos. Criar políticas toohelp reduzir os custos e manter a consistência em sua assinatura. 

Você define políticas com JSON e, em seguida, as aplica à sua assinatura ou em um grupo de recursos. As políticas são diferentes de controle de acesso baseado em função porque eles são aplicados tooresource tipos.

saudação de exemplo a seguir mostra uma política que garante a consistência de marca, especificando que todos os recursos incluem uma marca de costCenter.

```json
{
  "if": {
    "not" : {
      "field" : "tags",
      "containsKey" : "costCenter"
    }
  },
  "then" : {
    "effect" : "deny"
  }
}
```

Há muito mais tipos de políticas que você pode criar. Para obter mais informações, consulte [recursos de toomanage de política de uso e controlar o acesso](resource-manager-policy.md).

## <a name="sdks"></a>SDKs
Os SDKs do Azure estão disponíveis em várias linguagens e plataformas. Cada uma dessas implementações da linguagem está disponível por meio do gerenciador de pacotes do ecossistema e do GitHub.

Aqui estão nossos repositórios do SDK de software livre. Comentários, problemas e solicitações pull são bem-vindos.

* [SDK do Azure para .NET](https://github.com/Azure/azure-sdk-for-net)
* [Bibliotecas de Gerenciamento do Azure para Java](https://github.com/Azure/azure-sdk-for-java)
* [SDK do Azure para Node.js](https://github.com/Azure/azure-sdk-for-node)
* [SDK do Azure para PHP](https://github.com/Azure/azure-sdk-for-php)
* [SDK do Azure para Python](https://github.com/Azure/azure-sdk-for-python)
* [SDK do Azure para Ruby](https://github.com/Azure/azure-sdk-for-ruby)

Para obter informações sobre como usar esses idiomas com seus recursos, confira:

* [Azure para desenvolvedores .NET](/dotnet/azure/?view=azure-dotnet)
* [Azure para desenvolvedores Java](/java/azure/)
* [Azure para desenvolvedores Node.js](/nodejs/azure/)
* [Azure para desenvolvedores do Python](/python/azure/)

> [!NOTE]
> Se Olá SDK não fornece funcionalidade de saudação necessária, você também pode chamar toohello [API REST do Azure](https://docs.microsoft.com/rest/api/resources/) diretamente.
> 
> 

## <a name="next-steps"></a>Próximas etapas
* Para um tooworking introdução simples com modelos, consulte [exportar um modelo do Gerenciador de recursos do Azure de recursos existentes](resource-manager-export-template.md).
* Para obter uma explicação mais completa da criação de um modelo, consulte [Criar seu primeiro modelo do Azure Resource Manager](resource-manager-create-first-template.md).
* funções de saudação toounderstand você pode usar em um modelo, consulte [funções de modelo](resource-group-template-functions.md)
* Para saber mais sobre como usar o Visual Studio com o Resource Manager, veja [Criar e implantar grupos de recursos do Azure com o Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).

Veja uma demonstração em vídeo desta visão geral:

>[!VIDEO https://channel9.msdn.com/Blogs/Azure-Documentation-Shorts/Azure-Resource-Manager-Overview/player]


[powershellref]: https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.2.0/azurerm.resources
