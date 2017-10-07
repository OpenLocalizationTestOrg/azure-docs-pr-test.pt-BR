---
title: aaaSetting um cluster do Service Fabric usando o Visual Studio | Microsoft Docs
description: "Descreve como tooset a uma malha de serviço de cluster usando o modelo do Gerenciador de recursos do Azure criado por um projeto do grupo de recursos do Azure no Visual Studio"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: adegeo
editor: 
ms.assetid: bd2c0511-36c9-4828-8dc3-69e4b6a70567
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/21/2017
ms.author: mikhegn
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: adb0dd2169a28b46e832c6f06c998cbed0c473f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-service-fabric-cluster-by-using-visual-studio"></a>Configurar um cluster do Service Fabric usando o Visual Studio
Este artigo descreve como tooset a uma malha de serviço do Azure de cluster usando o Visual Studio e um modelo do Gerenciador de recursos do Azure. Vamos usar um modelo de saudação do Azure do Visual Studio recurso grupo projeto toocreate. Depois de saudação modelo foi criado, ele pode ser implantado diretamente tooAzure do Visual Studio. Ele também pode ser usado em um script, ou como parte do recurso de CI (integração contínua).

## <a name="create-a-service-fabric-cluster-template-by-using-an-azure-resource-group-project"></a>Criar um modelo de cluster do Service Fabric usando um projeto de grupo de recursos do Azure
tooget iniciado, abra o Visual Studio e criar um projeto do grupo de recursos do Azure (está disponível no hello **nuvem** pasta):

![Caixa de diálogo Novo Projeto com o projeto do Grupo de Recursos do Azure selecionado][1]

Você pode criar uma nova solução do Visual Studio para este projeto ou adicioná-lo a solução existente de tooan.

> [!NOTE]
> Se você não vir o projeto de grupo de recursos do Azure Olá no nó de nuvem hello, você não tem Olá SDK do Azure instalado. Inicie o Web Platform Installer ([instalá-lo agora](http://www.microsoft.com/web/downloads/platform.aspx) se você ainda não tiver) e, em seguida, pesquise por "Azure SDK para .NET" e instalar a versão de saudação que é compatível com sua versão do Visual Studio.
> 
> 

Depois de pressionar o botão Okey hello, o Visual Studio solicitará que você tooselect modelo de Gerenciador de recursos de saudação desejado toocreate:

![Selecione a caixa de diálogo do Modelo do Azure com o modelo de Cluster do Service Fabric selecionado][2]

Selecione o modelo de Cluster do Service Fabric hello e botão de ocorrências Olá Okey novamente. projeto Hello e modelo do Gerenciador de recursos de saudação agora foram criados.

## <a name="prepare-hello-template-for-deployment"></a>Prepare o modelo de saudação para implantação
Antes de modelo de saudação é cluster de saudação toocreate implantado, você deve fornecer valores hello necessário para parâmetros de modelo. Esses valores de parâmetro são lidos da saudação `ServiceFabricCluster.parameters.json` arquivo, que está na saudação `Templates` pasta do projeto de grupo de recursos de saudação. Abra o arquivo hello e fornecer Olá valores a seguir:

| Nome do parâmetro | Descrição |
| --- | --- |
| adminUserName |nome de Olá Olá da conta de administrador para máquinas de malha do serviço (nós). |
| certificateThumbprint |Olá a impressão digital do certificado Olá protege cluster hello. |
| sourceVaultResourceId |Olá *ID de recurso* do Cofre de chaves Olá onde Olá certificado que protege cluster hello está armazenado. |
| certificateUrlValue |URL de Olá Olá cluster do certificado de segurança. |

modelo do Gerenciador de recursos de malha de serviço do Visual Studio Olá cria um cluster seguro que é protegido por um certificado. Esse certificado é identificado pelo Olá último três parâmetros de modelo (`certificateThumbprint`, `sourceVaultValue`, e `certificateUrlValue`), e ela deve existir em um **Azure Key Vault**. Para obter mais informações sobre como toocreate Olá certificado de segurança de cluster, consulte [cenários de segurança de cluster do Service Fabric](service-fabric-cluster-security.md#x509-certificates-and-service-fabric) artigo.

## <a name="optional-change-hello-cluster-name"></a>Opcional: altere o nome do cluster Olá
Cada cluster do Service Fabric tem um nome. Quando um cluster de malha é criado no Azure, o nome do cluster determina (junto com hello região do Azure) nome de sistema de nome de domínio (DNS) Olá para cluster hello. Por exemplo, se você nomear seu cluster `myBigCluster`e o local de hello (região do Azure) saudação do grupo de recursos que hospedará o novo cluster de saudação é Leste dos EUA, Olá nome DNS de cluster Olá será `myBigCluster.eastus.cloudapp.azure.com`.

Por padrão nome do cluster Olá é gerado automaticamente e tornará exclusivo, anexando um prefixo de "cluster" tooa sufixo aleatório. Isso torna muito fácil toouse modelo de saudação como parte de um **integração contínua** system (CI). Se você quiser toouse um nome específico para o cluster, o que é significativo tooyou, defina o valor de saudação de saudação `clusterName` variável no arquivo de modelo do Gerenciador de recursos de saudação (`ServiceFabricCluster.json`) nome tooyour escolhido. É a variável primeiro Olá definida no arquivo.

## <a name="optional-add-public-application-ports"></a>Opcional: adicionar portas públicas do aplicativo
Também convém portas de aplicativo pública Olá toochange para cluster Olá antes de implantá-lo. Por padrão, o modelo de saudação abre apenas duas portas TCP públicas (80 e 8081). Se você precisar de mais de seus aplicativos, modificar a definição de Balanceador de carga do Azure de saudação no modelo de saudação. Olá definição é armazenada no arquivo de modelo principal de saudação (`ServiceFabricCluster.json`). Abra o arquivo e procure por `loadBalancedAppPort`. Cada porta está associada a três artefatos:

1. Uma variável de modelo que define o valor da porta TCP Olá para a porta de saudação:
   
    ```json
    "loadBalancedAppPort1": "80"
    ```
2. Um *investigação* que define a frequência e de quanto tempo Olá balanceador de carga do Azure tenta toouse um nó específico do Service Fabric antes de falhar em tooanother um. Olá investigações fazem parte da saudação recursos do balanceador de carga. Esta é a definição de investigação de saudação para Olá primeiro aplicativo porta:
   
    ```json
    {
        "name": "AppPortProbe1",
        "properties": {
            "intervalInSeconds": 5,
            "numberOfProbes": 2,
            "port": "[variables('loadBalancedAppPort1')]",
            "protocol": "Tcp"
        }
    }
    ```
3. Um *regra de balanceamento de carga* que une porta hello e investigação hello, que permite a balanceamento de carga em um conjunto de nós de cluster do Service Fabric:
   
    ```json
    {
        "name": "AppPortLBRule1",
        "properties": {
            "backendAddressPool": {
                "id": "[variables('lbPoolID0')]"
            },
            "backendPort": "[variables('loadBalancedAppPort1')]",
            "enableFloatingIP": false,
            "frontendIPConfiguration": {
                "id": "[variables('lbIPConfig0')]"
            },
            "frontendPort": "[variables('loadBalancedAppPort1')]",
            "idleTimeoutInMinutes": 5,
            "probe": {
                "id": "[concat(variables('lbID0'),'/probes/AppPortProbe1')]"
            },
            "protocol": "Tcp"
        }
    }
    ```
   Se aplicativos Olá que você planeje toodeploy toohello cluster precisam de mais portas, pode adicioná-los, criar investigação adicional e definições de regra de balanceamento de carga. Para obter mais informações sobre como toowork com o balanceador de carga do Azure por meio de modelos do Gerenciador de recursos, consulte [começar a criar um balanceador de carga interno usando um modelo](../load-balancer/load-balancer-get-started-ilb-arm-template.md).

## <a name="deploy-hello-template-by-using-visual-studio"></a>Implante o modelo de saudação usando o Visual Studio
Depois que você salvou todos Olá valores de parâmetros necessários no`ServiceFabricCluster.param.dev.json` arquivo, são o modelo de saudação toodeploy pronto e criar o cluster do Service Fabric. Clique em projeto saudação do grupo de recursos no Gerenciador de soluções do Visual Studio e escolha **implantar | Nova implantação...** . Se necessário, o Visual Studio mostrará Olá **implantar tooResource grupo** caixa de diálogo solicitando que você tooauthenticate tooAzure:

![Implantar a caixa de diálogo de grupo tooResource][3]

caixa de diálogo Olá permite escolher um grupo de recursos do Gerenciador de recursos existente para cluster hello e permite que você Olá opção toocreate um novo. Normalmente faz sentido toouse um grupo de recursos separado para um cluster do Service Fabric.

Depois de tocar Olá implantar botão, o Visual Studio solicitará que você tooconfirm valores de parâmetro de modelo de saudação. Olá ocorrência **salvar** botão. Um parâmetro não tem um valor persistente: senha da conta administrativa Olá para cluster hello. Você precisará tooprovide um valor de senha ao Visual Studio solicitará um.

> [!NOTE]
> Começando com o Azure SDK 2.9, o Visual Studio oferece suporte à leitura de senhas do **Cofre de Chaves do Azure** durante a implantação. Na caixa de diálogo de parâmetros de modelo Olá, observe que Olá `adminPassword` caixa de texto de parâmetro tem um pequeno ícone de "chave" na saudação à direita. Esse ícone permite que você tooselect um segredo do Cofre de chaves existente como a senha administrativa Olá para cluster hello. Verifique toofirst-se de habilitar o acesso do Gerenciador de recursos do Azure para implantação de modelo em Olá avançada políticas de acesso de seu Cofre de chaves. 
> 
> 

Você pode monitorar o progresso de saudação do processo de implantação de saudação na janela de saída do Visual Studio hello. Concluída a implantação de modelo hello, o novo cluster é toouse pronto!

> [!NOTE]
> Se o PowerShell nunca foi usado tooadminister Azure da máquina de saudação que você está usando agora, será necessário toodo housekeeping um pouco.
> 
> 1. Habilitar o PowerShell script executando Olá [ `Set-ExecutionPolicy` ](https://technet.microsoft.com/library/hh849812.aspx) comando. Para os computadores de desenvolvimento a política "irrestrita" é geralmente aceitável.
> 2. Decidir se tooallow coleta de dados de diagnóstico de comandos do PowerShell do Azure e execute [ `Enable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619303.aspx) ou [ `Disable-AzureRmDataCollection` ](https://msdn.microsoft.com/library/mt619236.aspx) conforme necessário. Isso evitará solicitações desnecessárias durante a implantação do modelo.
> 
> 

Se houver erros, vá toohello [portal do Azure](https://portal.azure.com/) Olá Abrir grupo de recursos implantados em e. Clique em **todas as configurações**, em seguida, clique em **implantações** na folha de configurações de saudação. Uma implantação com falha do grupo de recursos deixa informações detalhadas sobre o diagnóstico nesse local.

> [!NOTE]
> Clusters Service Fabric exigem um determinado número de nós toobe toomaintain disponibilidade e preservam o estado - tooas chamado "mantêm o quórum." Portanto, não é seguro tooshut para baixo de todas as máquinas de saudação em cluster hello, a menos que você executou antes um [backup completo do estado do seu](service-fabric-reliable-services-backup-restore.md).
> 
> 

## <a name="next-steps"></a>Próximas etapas
* [Saiba mais sobre como configurar o cluster do Service Fabric usando Olá portal do Azure](service-fabric-cluster-creation-via-portal.md)
* [Saiba como toomanage e implantar aplicativos do Service Fabric usando o Visual Studio](service-fabric-manage-application-in-visual-studio.md)

<!--Image references-->
[1]: ./media/service-fabric-cluster-creation-via-visual-studio/azure-resource-group-project-creation.png
[2]: ./media/service-fabric-cluster-creation-via-visual-studio/selecting-azure-template.png
[3]: ./media/service-fabric-cluster-creation-via-visual-studio/deploy-to-azure.png
