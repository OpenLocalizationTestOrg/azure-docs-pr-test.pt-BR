---
title: "aaaGetting de Introdução ao DSC de automação do Azure | Microsoft Docs"
description: "Explicações e exemplos das tarefas mais comuns de saudação no Azure Automation desejado configuração de estado (DSC)"
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
editor: tysonn
ms.assetid: a3816593-70a3-403b-9a43-d5555fd2cee2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/21/2016
ms.author: magoedte;eslesar
ms.openlocfilehash: 82910c96e928b9264c2e1b52a5c98dc47273dcc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-automation-dsc"></a>Introdução ao DSC de Automação do Azure
Este tópico explica como toodo Olá tarefas mais comuns com o Azure automação desejado configuração de estado (DSC), como criar, importar e compilar configurações, integração muito gerenciar máquinas e exibir relatórios. Para obter uma visão geral do que o DSC de Automação do Azure é, consulte [Visão geral do DSC da Automação do Azure](automation-dsc-overview.md). Para obter a documentação da DSC, consulte [Visão Geral da Configuração de Estado Desejado do Windows PowerShell](https://msdn.microsoft.com/PowerShell/dsc/overview).

Este tópico fornece um guia passo a passo de toousing DSC de automação do Azure. Se você quiser um ambiente de exemplo que já está configurado sem Olá etapas descritas neste tópico, você pode usar [Olá seguinte modelo do ARM](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup). Esse modelo define um ambiente completo do DSC de Automação do Azure, incluindo uma VM do Azure que é gerenciada pelo DSC de Automação do Azure.

## <a name="prerequisites"></a>Pré-requisitos
toocomplete Olá exemplos neste tópico, a seguinte Olá é necessários:

* Uma conta de Automação do Azure. Para obter instruções sobre como criar uma conta Executar Como de Automação do Azure, consulte [Conta Executar Como do Azure](automation-sec-configure-azure-runas-account.md).
* Uma VM do Azure Resource Manager (não clássica) executando o Windows Server 2008 R2 ou posterior. Para obter instruções sobre como criar uma VM, consulte [criar sua primeira máquina virtual Windows no hello portal do Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md)

## <a name="creating-a-dsc-configuration"></a>Criando uma configuração de DSC
Vamos criar um simples [configuração DSC](https://msdn.microsoft.com/powershell/dsc/configurations) que garante a presença de saudação ou ausência de saudação **Web-Server** recurso (IIS) do Windows, dependendo de como você atribui a nós.

1. Inicie Olá ISE do Windows PowerShell (ou qualquer editor de texto).
2. Saudação de tipo texto a seguir:
   
    ```powershell
    configuration TestConfig
    {
        Node WebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Present'
                Name                 = 'Web-Server'
                IncludeAllSubFeature = $true
   
            }
        }
   
        Node NotWebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Absent'
                Name                 = 'Web-Server'
   
            }
        }
        }
    ```
3. Salve o arquivo hello como `TestConfig.ps1`.

Essa configuração chama um recurso em cada bloco de nó, hello [recurso WindowsFeature](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), que garante a presença de saudação ou ausência de saudação **Web-Server** recurso.

## <a name="importing-a-configuration-into-azure-automation"></a>Importando uma configuração na Automação do Azure
Em seguida, podemos vai importar configuração de saudação para Olá conta de automação.

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. No menu de Hub hello, clique em **todos os recursos** e, em seguida, Olá nome de sua conta de automação.
3. Em Olá **conta de automação** folha, clique em **configurações DSC**.
4. Em Olá **configurações DSC** folha, clique em **adicionar uma configuração de**.
5. Em Olá **Importar configuração** folha, procurar toohello `TestConfig.ps1` arquivo no seu computador.
   
    ![Captura de tela de hello * * folha Importar configuração * *](./media/automation-dsc-getting-started/AddConfig.png)
6. Clique em **OK**.

## <a name="viewing-a-configuration-in-azure-automation"></a>Exibindo uma configuração na Automação do Azure
Depois de importar uma configuração, você pode exibi-lo no portal do Azure de saudação.

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. No menu de Hub hello, clique em **todos os recursos** e, em seguida, Olá nome de sua conta de automação.
3. Em Olá **conta de automação** folha, clique em **configurações DSC**
4. Em Olá **configurações DSC** folha, clique em **TestConfig** (esse é nome hello da configuração de saudação você importou no procedimento anterior Olá).
5. Em Olá **TestConfig configuração** folha, clique em **Exibir código-fonte configuração**.
   
    ![Captura de tela da folha de configuração TestConfig Olá](./media/automation-dsc-getting-started/ViewConfigSource.png)
   
    Um **fonte de configuração TestConfig** folha é aberta, exibindo o código do PowerShell Olá para configuração de saudação.

## <a name="compiling-a-configuration-in-azure-automation"></a>Compilando uma configuração na Automação do Azure
Antes de aplicar um nó de tooa de estado desejado, uma configuração DSC definindo o estado deve ser compilada em uma ou mais configurações de nó (documento MOF) e colocada no servidor de Pull de DSC de automação de saudação. Para obter uma descrição mais detalhada da compilação das configurações na DSC de Automação do Azure, consulte [Compilando as configurações na DSC de Automação do Azure](automation-dsc-compile.md). Para obter mais informações sobre a compilação das configurações, consulte [Configurações da DSC](https://msdn.microsoft.com/PowerShell/DSC/configurations).

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. No menu de Hub hello, clique em **todos os recursos** e, em seguida, Olá nome de sua conta de automação.
3. Em Olá **conta de automação** folha, clique em **configurações DSC**
4. Em Olá **configurações DSC** folha, clique em **TestConfig** (nome de saudação do hello importado anteriormente configuração).
5. Em Olá **TestConfig configuração** folha, clique em **compilar**e, em seguida, clique em **Sim**. Isso inicia um trabalho de compilação.
   
    ![Captura de tela da folha de configuração TestConfig Olá realce de botão de compilação](./media/automation-dsc-getting-started/CompileConfig.png)

> [!NOTE]
> Quando você compila uma configuração na automação do Azure, ele implanta automaticamente a qualquer servidor de pull criado nó configuração MOFs toohello.
> 
> 

## <a name="viewing-a-compilation-job"></a>Exibindo um trabalho de compilação
Depois de iniciar uma compilação, você pode exibi-lo no hello **trabalhos de compilação** lado a lado no hello **configuração** folha. Olá **trabalhos de compilação** bloco mostra atualmente em execução, concluído e trabalhos com falha. Quando você abre uma folha de trabalho de compilação, mostra informações sobre o trabalho incluindo erros ou avisos encontrados, parâmetros de entrada usado na configuração de saudação e compilação logs.

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. No menu de Hub hello, clique em **todos os recursos** e, em seguida, Olá nome de sua conta de automação.
3. Em Olá **conta de automação** folha, clique em **configurações DSC**.
4. Em Olá **configurações DSC** folha, clique em **TestConfig** (nome de saudação do hello importado anteriormente configuração).
5. Em Olá **trabalhos de compilação** lado a lado de saudação **TestConfig configuração** folha, clique em qualquer um dos trabalhos de saudação listados. Um **trabalho de compilação** abre folha, rotulado com data Olá Olá trabalho de compilação foi iniciado.
   
    ![Captura de tela da folha de trabalho de compilação de saudação](./media/automation-dsc-getting-started/CompilationJob.png)
6. Clique em qualquer lado a lado no hello **trabalho de compilação** folha toosee mais detalhes sobre o trabalho de saudação.

## <a name="viewing-node-configurations"></a>Exibindo configurações de nó
A conclusão com êxito de um trabalho de compilação cria uma ou mais novas configurações de nó. Uma configuração de nó é um documento MOF é implantado toohello servidor de pull e pronto toobe extraída e aplicada por um ou mais nós. Você pode exibir as configurações de nó de saudação em sua conta de automação em Olá **configurações do nó DSC** folha. Uma configuração de nó tem um nome com o formulário de saudação *ConfigurationName*. *NodeName*.

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. No menu de Hub hello, clique em **todos os recursos** e, em seguida, Olá nome de sua conta de automação.
3. Em Olá **conta de automação** folha, clique em **configurações do nó DSC**.
   
    ![Captura de tela da folha de configurações do nó DSC Olá](./media/automation-dsc-getting-started/NodeConfigs.png)

## <a name="onboarding-an-azure-vm-for-management-with-azure-automation-dsc"></a>Integrando uma VM do Azure para o gerenciamento com o DSC de Automação do Azure
Você pode usar o DSC de automação do Azure toomanage Azure VMs (clássico e o Gerenciador de recursos), VMs locais, máquinas Linux, AWS VMs e máquinas físicas locais. Neste tópico, abordaremos como tooonboard somente máquinas virtuais do Gerenciador de recursos do Azure. Para obter informações sobre a integração de outros tipos de computadores, consulte [Integrando computadores para o gerenciamento pela DSC de Automação do Azure](automation-dsc-onboarding.md).

### <a name="tooonboard-an-azure-resource-manager-vm-for-management-by-azure-automation-dsc"></a>tooonboard uma VM do Azure Resource Manager para o gerenciamento de DSC de automação do Azure
1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. No menu de Hub hello, clique em **todos os recursos** e, em seguida, Olá nome de sua conta de automação.
3. Em Olá **conta de automação** folha, clique em **nós DSC**.
4. Em Olá **nós DSC** folha, clique em **adicionar a máquina virtual do Azure**.
   
    ![Captura de tela da folha de nós de DSC Olá realce de botão de adicionar a máquina virtual do Azure Olá](./media/automation-dsc-getting-started/OnboardVM.png)
5. Em Olá **adicionar VMs do Azure** folha, clique em **selecionar máquinas virtuais tooonboard**.
6. Em Olá **selecione VMs** folha, selecione Olá VM que você deseja tooonboard e clique em **Okey**.
   
   > [!IMPORTANT]
   > Ela deve ser uma VM do Azure Resource Manager executando o Windows Server 2008 R2 ou posterior.
   > 
   > 
7. Em Olá **adicionar VMs do Azure** folha, clique em **configurar dados de registro**.
8. Em hello **registro** folha, insira o nome da saudação Olá da configuração de nó que você deseja tooapply toohello VM em Olá **nome de configuração de nó** caixa. Isso deve corresponder exatamente o nome de saudação de uma configuração de nó Olá conta de automação. Fornecer um nome neste ponto é opcional. Você pode alterar a configuração de nó de saudação atribuída após o nó de saudação de integração.
   Marque **Reinicializar o Nó se Necessário** e clique em **OK**.
   
    ![Captura de tela da folha de registro Olá](./media/automation-dsc-getting-started/RegisterVM.png)
   
    configuração do nó Olá especificado será aplicado toohello VM em intervalos especificados por Olá **frequência do modo de configuração**, e Olá VM verificará a configuração de nó toohello atualizações em intervalos especificados por Olá  **Frequência de atualização**. Para obter mais informações sobre como esses valores são usados, consulte [Configurando Olá Gerenciador de configurações Local](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).
9. Em Olá **adicionar VMs do Azure** folha, clique em **criar**.

Azure iniciará o processo de saudação de integração hello VM. Quando for concluído, Olá VM será exibido no hello **nós DSC** folha em Olá conta de automação.

## <a name="viewing-hello-list-of-dsc-nodes"></a>Exibição de lista de saudação de nós de DSC
Você pode exibir a lista de saudação de todos os computadores que foram incorporados para gerenciamento na sua conta de automação em Olá **nós DSC** folha.

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. No menu de Hub hello, clique em **todos os recursos** e, em seguida, Olá nome de sua conta de automação.
3. Em Olá **conta de automação** folha, clique em **nós DSC**.

## <a name="viewing-reports-for-dsc-nodes"></a>Exibindo relatórios para nós DSC
Cada vez que DSC de automação do Azure executa uma verificação de consistência em um nó gerenciado, o nó Olá envia um servidor de pull de toohello voltar de relatório de status. Você pode exibir esses relatórios na folha de saudação para esse nó.

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. No menu de Hub hello, clique em **todos os recursos** e, em seguida, Olá nome de sua conta de automação.
3. Em Olá **conta de automação** folha, clique em **nós DSC**.
4. Em Olá **relatórios** lado a lado, clique em qualquer um dos relatórios de saudação na lista de saudação.
   
    ![Captura de tela da folha de relatório Olá](./media/automation-dsc-getting-started/NodeReport.png)

Na folha de saudação para um relatório individual, você pode ver Olá segue as informações de status para manter a consistência correspondente Olá verificar:

* Olá relatar o status — se o nó de saudação é "Compatíveis", a configuração de hello "Não", ou "nó hello não é compatível com" (quando o nó hello está em **applyandmonitor** modo e hello máquina não está em estado de saudação desejado).
* hora de início da saudação para verificação de consistência de saudação.
* tempo de execução total consistência Olá Olá verificar.
* verificação de tipo de saudação de consistência.
* Erros, incluindo a mensagem de erro e o código de erro de saudação. 
* Todos os recursos DSC usados na configuração de Olá e o estado de saudação de cada recurso (se o nó de saudação está no estado de saudação desejado para esse recurso) — você pode clicar em cada recurso tooget informações mais detalhadas sobre esse recurso.
* nome de saudação, o endereço IP e o modo de configuração do nó de saudação.

Você também pode clicar em **Exibir relatório bruto** toosee Olá dados reais que Olá nó enviam toohello server. Para obter mais informações sobre como usar esses dados, consulte [Usando um servidor de relatório da DSC](https://msdn.microsoft.com/powershell/dsc/reportserver).

Pode levar algum tempo depois de um nó é incorporada antes que o primeiro relatório de saudação está disponível. Talvez seja necessário toowait backup too30 minutos para o primeiro relatório de saudação após você integrar um nó.

## <a name="reassigning-a-node-tooa-different-node-configuration"></a>Reatribuindo uma configuração de nó diferente do nó tooa
Você pode atribuir uma configuração de nó diferente de toouse um nó de Olá um atribuídas inicialmente.

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. No menu de Hub hello, clique em **todos os recursos** e, em seguida, Olá nome de sua conta de automação.
3. Em Olá **conta de automação** folha, clique em **nós DSC**.
4. Em Olá **nós DSC** folha, clique no nome de saudação do nó Olá deseja tooreassign.
5. Na folha de saudação do nó, clique em **atribuir nó**.
   
    ![Captura de tela da folha de nó Olá realce de botão de nó atribuir Olá](./media/automation-dsc-getting-started/AssignNode.png)
6. Em Olá **atribuir a configuração do nó** folha, selecione Olá nó configuração toowhich você quiser tooassign Olá nó e, em seguida, clique em **Okey**.
   
    ![Captura de tela da folha de configuração do nó atribuir Olá](./media/automation-dsc-getting-started/AssignNodeConfig.png)

## <a name="unregistering-a-node"></a>Cancelando o registro de um nó
Se você não quiser mais um toobe nó gerenciado pelo DSC de automação do Azure, você pode cancelar seu registro.

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. No menu de Hub hello, clique em **todos os recursos** e, em seguida, Olá nome de sua conta de automação.
3. Em Olá **conta de automação** folha, clique em **nós DSC**.
4. Em Olá **nós DSC** folha, clique no nome de saudação do nó Olá deseja toounregister.
5. Na folha de saudação do nó, clique em **Unregister**.
   
    ![Captura de tela da folha de nó Olá realce de botão de cancelamento de registro de saudação](./media/automation-dsc-getting-started/UnregisterNode.png)

## <a name="related-articles"></a>Artigos relacionados
* [Visão geral do DSC de Automação do Azure](automation-dsc-overview.md)
* [Máquinas de integração para o gerenciamento pelo DSC de Automação do Azure](automation-dsc-onboarding.md)
* [Visão Geral da Configuração de Estado Desejado do Windows PowerShell](https://msdn.microsoft.com/powershell/dsc/overview)
* [cmdlets da DSC de Automação do Azure](/powershell/module/azurerm.automation/#automation)
* [preço da DSC de Automação do Azure](https://azure.microsoft.com/pricing/details/automation/)

