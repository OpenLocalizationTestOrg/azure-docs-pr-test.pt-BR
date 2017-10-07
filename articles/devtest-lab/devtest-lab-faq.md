---
title: aaaAzure perguntas frequentes sobre o DevTest Labs | Microsoft Docs
description: Encontre as respostas a perguntas de Azure DevTest Labs toocommon
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: afe83109-b89f-4f18-bddd-b8b4a30f11b4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: tarcher
ms.openlocfilehash: 07d4c870eca21856750a472ed503de4a2734a438
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-devtest-labs-faq"></a>Perguntas frequentes sobre o Azure DevTest Labs
Este artigo responde algumas das perguntas mais comuns de saudação sobre Azure DevTest Labs.

**Geral**
## <a name="what-if-my-question-isnt-answered-here"></a>E se dúvida não foi respondida aqui?
Caso sua pergunta não esteja listada aqui, fale conosco e nós o ajudaremos a encontrar uma resposta.

* Postar uma pergunta em Olá [Disqus thread](#comments) final Olá essas perguntas Frequentes e entre em contato com a equipe de Cache do Azure hello e outros membros da comunidade sobre este artigo.
* tooreach um público maior, postar uma pergunta em Olá [Fórum do MSDN do Azure DevTest Labs](https://social.msdn.microsoft.com/Forums/azure/home?forum=AzureDevTestLabs)e entre em contato com a equipe do Azure DevTest Labs hello e outros membros da comunidade de saudação.
* toomake uma solicitação de recurso, enviar sua solicitações e ideias toohello [Azure DevTest Labs User Voice](https://feedback.azure.com/forums/320373-azure-devtest-labs).

## <a name="why-should-i-use-azure-devtest-labs"></a>Por que devo usar o Azure DevTest Labs?
O Azure DevTest Labs pode economizar dinheiro e tempo da equipe. Os desenvolvedores podem criar seus próprios ambientes com várias bases diferentes e usar artefatos tooquickly implantar e configurar aplicativos. Usando fórmulas e imagens personalizadas, as máquinas virtuais pode ser salvas como modelos e reproduzidas facilmente. Além disso, os laboratórios oferecem várias políticas configuráveis que permite que os administradores tooreduce desperdiçar e gerenciar ambientes da equipe do laboratório. Essas políticas incluem desligamento automático, limite de custo, máximo de VMs por usuário e tamanhos máximos de VM. Para obter uma explicação mais detalhada do Azure DevTest Labs, leia Olá [visão geral](devtest-lab-overview.md) ou inspecionar hello [vídeo introdutório](/documentation/videos/videos/what-is-azure-devtest-labs).

## <a name="what-does-worry-free-self-service-mean"></a>O que significa "autoatendimento sem preocupação"?
"Autoatendimento preocupações," significa que os desenvolvedores e testadores criam seus próprios ambientes conforme necessário, e os administradores têm segurança Olá saber que o Azure DevTest Labs ajuda a minimizar desperdiçar e controlar os custos. Os administradores podem especificar quais tamanhos de VM são permitidos, o número máximo de saudação de máquinas virtuais, e quando as máquinas virtuais são iniciados e desligar. Azure DevTest Labs também torna fácil toomonitor custos e definir alertas toostay atento como recursos no laboratório Olá estão sendo usados.

## <a name="how-can-i-use-azure-devtest-labs"></a>Como usar o Azure DevTest Labs?
Azure DevTest Labs é útil sempre que precisar de desenvolvimento ou ambientes de teste e deseja tooreproduce-los rapidamente e/ou gerenciá-los com as políticas de redução de custos.

Aqui estão alguns cenários em que nossos clientes usam o Azure DevTest Labs:

* Gerenciando ambientes de desenvolvimento e teste em um só lugar, utilizando políticas tooreduce custo e imagens personalizadas tooshare compilações em equipe hello.
* Desenvolvendo um aplicativo usando o estado do disco durante fases de desenvolvimento Olá Olá toosave imagens personalizadas para.
* Controle de custo de saudação em tooprogress de relação.
* Criando ambientes de teste em massa para testes de garantia de qualidade.
* Usando fórmulas e artefatos tooeasily configurar e reproduzir um aplicativo em vários ambientes.
* Distribuir as VMs para hackathons (trabalho colaboração de desenvolvimento ou teste) e, em seguida, facilmente eliminação provisionamento-las quando o evento Olá termina.

## <a name="how-am-i-billed-for-azure-devtest-labs"></a>Como eu sou cobrado pelo Azure DevTest Labs?
DevTest Labs do Azure é um serviço gratuito, que significa criar laboratórios e configurar artefatos, modelos e políticas de saudação são gratuito. Você paga somente pelos Olá recursos do Azure usados em seus laboratórios, como máquinas virtuais, contas de armazenamento e redes virtuais. Para obter mais informações sobre o custo de saudação de recursos de laboratório, leia sobre [preços do Azure DevTest Labs](https://azure.microsoft.com/pricing/details/devtest-lab/).


**Segurança**
## <a name="what-are-hello-different-security-levels-in-azure-devtest-labs"></a>Quais são Olá diferentes níveis de segurança no Azure DevTest Labs?
O acesso de segurança é determinado pelo [RBAC (controle de acesso baseado em função) do Azure](../active-directory/role-based-access-built-in-roles.md). toounderstand acessar como funciona, ele ajuda a toounderstand Olá diferenças uma permissão, a função e um escopo conforme definido pelo RBAC.

* **Permissão** -uma permissão é uma ação específica de tooa de acesso definidas. Por exemplo, uma permissão pode ser máquinas virtuais de tooall de acesso de leitura.
* **Função** -uma função é um conjunto de permissões que podem ser agrupados e tooa usuário atribuído. Por exemplo, um "proprietário da assinatura" tem tooall acessar os recursos em uma assinatura.
* **Escopo** -um escopo é um nível na hierarquia de saudação do recurso do Azure. Por exemplo, um escopo pode ser um grupo de recursos ou uma única assinatura de laboratório ou Olá inteira.

No escopo de saudação do Azure DevTest Labs, há dois tipos de permissões de usuário toodefine funções: usuário de laboratório e de proprietário de laboratório.

* **Proprietário do laboratório** -um proprietário de laboratório tem Olá acessar tooany recursos no laboratório de saudação. Portanto, eles podem modificar políticas, ler e gravar todas as máquinas virtuais, altere a rede virtual hello e assim por diante.
* **Usuário de laboratório** – um usuário de laboratório pode exibir todos os recursos de laboratório, como VMs, políticas e redes virtuais, mas não pode modificar políticas ou VMs criadas por outros usuários. Também é possível toocreate funções personalizadas Azure DevTest Labs, e você pode aprender como toodo artigo hello, [conceder permissões de usuário políticas de laboratório toospecific](devtest-lab-grant-user-permissions-to-specific-lab-policies.md).

Como os escopos são hierárquicos, quando um usuário tem permissões em um determinado escopo, ele recebe essas permissões automaticamente em cada escopo de nível inferior que está englobado. Por exemplo, se um usuário está atribuído toohello do proprietário da assinatura, em seguida, eles têm tooall acessar os recursos em uma assinatura. Esses recursos incluem todas as máquinas virtuais, todas as redes virtuais e todos os laboratórios. Assim, um proprietário da assinatura herda automaticamente a função hello do proprietário do laboratório. No entanto, Olá oposta não é true. O proprietário de um laboratório tem laboratório tooa de acesso, que é um escopo de menor nível de assinatura de saudação. Portanto, um proprietário de laboratório não é capaz de toosee máquinas de virtuais ou redes virtuais ou todos os recursos que estão fora do laboratório de saudação.

## <a name="how-do-i-create-a-role-tooallow-users-tooperform-a-specific-task"></a>Como criar um tooperform de usuários tooallow função uma tarefa específica?
Um artigo abrangente sobre como funções personalizadas toocreate e atribuir permissões toothat função podem ser encontradas aqui. Aqui está um exemplo de um script que cria a função hello "DevTest Labs usuário avançado", que tem permissão toostart e interromper todas as máquinas virtuais no laboratório hello:

    $policyRoleDef = Get-AzureRmRoleDefinition "DevTest Labs User"
    $policyRoleDef.Actions.Remove('Microsoft.DevTestLab/Environments/*')
    $policyRoleDef.Id = $null
    $policyRoleDef.Name = "DevTest Labs Advance User"
    $policyRoleDef.IsCustom = $true
    $policyRoleDef.AssignableScopes.Clear()
    $policyRoleDef.AssignableScopes.Add("subscriptions/<subscription Id>")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/virtualMachines/Start/action")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/virtualMachines/Stop/action")
    $policyRoleDef = New-AzureRmRoleDefinition -Role $policyRoleDef  


**Integração e automação de CI/CD**
## <a name="does-azure-devtest-labs-integrate-with-my-cicd-toolchain"></a>O Azure DevTest Labs se integra à minha cadeia de ferramentas CI/CD?
Se você estiver usando o VSTS, há um [extensão Azure DevTest Labs tarefas](https://marketplace.visualstudio.com/items?itemName=ms-azuredevtestlabs.tasks) que permite a você tooautomate sua versão do pipeline em Azure DevTest Labs. Alguns dos usos Olá desta extensão incluem:

* Criar e implantar uma VM automaticamente e configurá-lo com a versão mais recente do hello usando as tarefas de cópia de arquivo do Azure ou o PowerShell VSTS.
* Automaticamente captura de estado de saudação de uma máquina virtual depois de testar tooreproduce um bug no hello mesma VM para obter mais informações.
* Excluindo Olá VM final Olá Olá o pipeline da versão quando ele não for mais necessário.

Olá seguir postagens de blog fornecem orientações e informações sobre como usar a extensão do VSTS hello:

* [Azure DevTest Labs – extensão do VSTS](https://blogs.msdn.microsoft.com/devtestlab/2016/06/15/azure-devtest-labs-vsts-extension/)
* [Implantando uma nova VM em uma AzureDevTestLab existente do VSTS](http://www.visualstudiogeeks.com/blog/DevOps/Deploy-New-VM-To-Existing-AzureDevTestLab-From-VSTS)
* [Usando o gerenciamento de liberações do VSTS para implantações contínuas tooAzureDevTestLabs](http://www.visualstudiogeeks.com/blog/DevOps/Use-VSTS-ReleaseManagement-to-Deploy-and-Test-in-AzureDevTestLabs)

Para outros toolchains CI/CD, Olá todos mencionado anteriormente cenários que podem ser obtidos por meio de saudação extensão de tarefas do VSTS pode ser obtida por meio de implantação da mesma forma [modelos do Azure Resource Manager](https://aka.ms/dtlquickstarttemplate) usando [ Cmdlets do PowerShell do Azure](../azure-resource-manager/resource-group-template-deploy.md) e [.NET SDKs](https://www.nuget.org/packages/Microsoft.Azure.Management.DevTestLabs/). Você também pode usar [APIs REST do DevTest Labs](http://aka.ms/dtlrestapis) toointegrate com a cadeia de ferramentas.  


**Máquinas virtuais**
## <a name="why-cant-i-see-certain-vms-in-hello-azure-virtual-machines-blade-that-i-see-within-azure-devtest-labs"></a>Por que não vejo determinadas VMs na folha de máquinas virtuais do Azure Olá que vejo dentro do Azure DevTest Labs?
Quando uma máquina virtual é criada no Azure DevTest Labs, a permissão é dada tooaccess essa VM. É capaz de tooview-lo, tanto na folha de laboratórios hello e hello **máquinas virtuais** folha. Os usuários na função de DevTest Labs Olá podem ver todas as máquinas virtuais criadas no laboratório Olá por meio do laboratório Olá **todas as máquinas virtuais** folha. No entanto, os usuários na função de DevTest Labs Olá não recebem automaticamente os recursos de acesso de leitura tooVM que outros criaram. Portanto, essas máquinas virtuais não são exibidos no hello **máquinas virtuais** folha.

## <a name="what-is-hello-difference-between-custom-images-and-formulas"></a>Qual é a diferença de saudação entre imagens personalizadas e as fórmulas?
Uma imagem personalizada é um VHD (disco rígido virtual) e uma fórmula é uma imagem que você pode definir com configurações adicionais que podem ser salvas e reproduzidas. Uma imagem personalizada pode ser preferível tooquickly criar vários ambientes com hello mesma imagem básica, imutável. Uma fórmula pode ser melhor se desejar tooreproduce Olá configuração da VM com os bits mais recentes do hello, uma sub-rede/rede virtual ou um tamanho específico. Para obter uma explicação mais detalhada, consulte o artigo Olá [comparando imagens personalizadas e as fórmulas em DevTest Labs](devtest-lab-comparing-vm-base-image-types.md).

## <a name="how-do-i-create-multiple-vms-from-hello-same-template-at-once"></a>Como criar várias VMs de saudação mesmo modelo de uma só vez?
Você pode usar o hello [VSTS tarefas extensão](https://marketplace.visualstudio.com/items?itemName=ms-azuredevtestlabs.tasks) ou [gerar um modelo do Azure Resource Manager](devtest-lab-add-vm.md#save-azure-resource-manager-template) durante a criação de uma máquina virtual e [implantar o modelo do Gerenciador de recursos do Azure de saudação do Windows PowerShell ](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="how-do-i-move-my-existing-azure-vms-into-my-azure-devtest-labs-lab"></a>Como mover minhas VMs do Azure existentes para meu laboratório do Azure DevTest Labs?
Siga as etapas de saudação abaixo toocopy seu tooAzure de VMs DevTest Labs existente:

1. Copiar arquivo VHD de saudação da VM existente usando esta [script do Windows PowerShell](https://github.com/Azure/azure-devtestlab/blob/master/Scripts/CopyVHDFromVMToLab.ps1)
2. [Criar imagem personalizada Olá](devtest-lab-create-template.md) dentro de seu laboratório Azure DevTest Labs.
3. Criar uma VM no laboratório de saudação de sua imagem personalizada

## <a name="can-i-attach-multiple-disks-toomy-vms"></a>É possível anexar vários discos toomy VMs?
Há suporte para a anexação tooVMs de vários discos.  

## <a name="if-i-want-toouse-a-windows-os-image-for-my-testing-do-i-have-toopurchase-an-msdn-subscription"></a>Se eu quiser toouse uma imagem do sistema operacional Windows para o meu teste, é necessário toopurchase uma assinatura do MSDN?
Se você precisar toouse imagens de sistema operacional cliente do Windows (Windows 7 ou posterior) para o desenvolvimento ou teste no Azure, em seguida, Sim, você deve:

- [Comprar uma assinatura do MSDN](https://www.visualstudio.com/products/how-to-buy-vs).
- Se você tiver um Enterprise Agreement, crie uma assinatura do Azure com Olá [oferta de desenvolvimento/teste Enterprise](https://azure.microsoft.com/en-us/offers/ms-azr-0148p).

Para obter mais informações sobre Olá créditos do Azure para cada oferta do MSDN, consulte [crédito mensal Azure para assinantes do Visual Studio](https://azure.microsoft.com/en-us/pricing/member-offers/msdn-benefits-details/).

## <a name="how-do-i-automate-hello-process-of-uploading-vhd-files-toocreate-custom-images"></a>Como automatizar o processo de saudação de carregamento de imagens personalizadas do VHD arquivos toocreate?
Há duas opções:

* [AzCopy Azure](../storage/common/storage-use-azcopy.md#blob-upload) pode ser usado toocopy ou carregue as conta de armazenamento toohello arquivos VHD associada laboratório hello.
* [Gerenciador de Armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) é um aplicativo autônomo que é executado no Windows, no OSX e no Linux.   

conta de armazenamento toofind Olá destino associada a seu laboratório, siga estas etapas:

1. Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Selecione **grupos de recursos** no painel esquerdo de saudação do.
3. Localize e selecione o grupo de recursos de saudação associado com seu laboratório.
4. Em Olá **visão geral** folha, selecione uma das contas de armazenamento hello.
5. Selecione **Blobs**.
6. Procure carregamentos na lista de saudação. Se não houver nenhum, retorne tooStep #4 e tente outra conta de armazenamento.
7. Saudação de uso **URL** como seu destino em seu comando AzCopy.

## <a name="how-can-i-automate-hello-process-of-deleting-all-hello-vms-in-my-lab"></a>Como automatizar o processo de saudação de exclusão Olá todas as VMs em meu laboratório?
Além disso toodeleting VMs do seu laboratório Olá portal do Azure, você pode excluir todas as VMs de saudação de seu laboratório usando um script do PowerShell. Olá seguinte exemplo, modificar valores de parâmetro hello em Olá **toochange valores** comentário. Você pode recuperar Olá `subscriptionId`, `labResourceGroup`, e `labName` valores na folha de laboratório Olá no hello portal do Azure.

    # Delete all hello VMs in a lab

    # Values toochange
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource group here>"
    $labName = "<Enter lab name here>"

    # Login tooyour Azure account
    Login-AzureRmAccount

    # Select hello Azure subscription that contains hello lab. This step is optional
    # if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Get hello lab that contains hello VMs toodelete.
    $lab = Get-AzureRmResource -ResourceId ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)

    # Get hello VMs from that lab.
    $labVMs = Get-AzureRmResource | Where-Object {
              $_.ResourceType -eq 'microsoft.devtestlab/labs/virtualmachines' -and
              $_.ResourceName -like "$($lab.ResourceName)/*"}

    # Delete hello VMs.
    foreach($labVM in $labVMs)
    {
        Remove-AzureRmResource -ResourceId $labVM.ResourceId -Force
    }

**Artefatos**
## <a name="what-are-artifacts"></a>O que são os artefatos?
Artefatos são elementos personalizáveis que podem ser usado toodeploy os bits mais recentes ou o desenvolvimento das ferramentas em uma VM. Eles são anexado tooyour VM durante a criação com alguns cliques, e quando Olá VM é provisionado, artefatos Olá implantar e configurar sua VM. Há diversos artefatos preexistentes no nosso [repositório GitHub público](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts), mas você pode [criar seus próprios artefatos](devtest-lab-artifact-author.md) facilmente.


**Configuração do laboratório**
## <a name="how-do-i-create-a-lab-from-an-azure-resource-manager-template"></a>Como criar um laboratório de um modelo do Azure Resource Manager?
Fornecemos um [repositório GitHub de modelos do Azure Resource Manager de laboratório](https://aka.ms/dtlquickstarttemplate) que você pode implantar como-é ou modificar modelos personalizados de toocreate para seus laboratórios. Cada modelo tem um link que você pode clicar em laboratório de saudação toodeploy como-está sob sua própria assinatura do Azure, ou você pode personalizar o modelo de saudação e [implantar usando o PowerShell ou CLI do Azure](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="why-are-my-vms-created-in-different-resource-groups-with-arbitrary-names-can-i-rename-or-modify-these-resource-groups"></a>Por que as minhas VMs são criadas em grupos de recursos diferentes com nomes arbitrários? Posso renomear ou modificar esses grupos de recursos?
Grupos de recursos são criados dessa maneira para permissões de usuário do Azure DevTest Labs toomanage hello e acesso toovirtual máquinas. Enquanto você pode mover o grupo de recursos de tooanother Olá VM com o nome desejado, isso não é recomendável. Estamos trabalhando em melhorar essa experiência tooallow mais flexibilidade.   

## <a name="how-many-labs-can-i-create-under-hello-same-subscription"></a>Laboratórios quantos pode criar em Olá mesma assinatura?
Não há nenhum limite específico no número de saudação de laboratórios que podem ser criados por assinatura. No entanto, recursos Olá usados são limitados por assinatura. Você pode ler sobre Olá [limites e cotas impostas em assinaturas do Azure](../azure-subscription-service-limits.md) e [como tooincrease esses limites](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests).

## <a name="how-many-vms-can-i-create-per-lab"></a>Quantas VMs posso criar por laboratório?
Não há nenhum limite específico no número de saudação de máquinas virtuais que podem ser criados por laboratório. No entanto, recursos Olá usados são limitados por assinatura (núcleos VM por exemplo, IPs públicos, etc.). Você pode ler sobre Olá [limites e cotas impostas em assinaturas do Azure](../azure-subscription-service-limits.md) e [como tooincrease esses limites](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests).

## <a name="how-do-i-share-a-direct-link-toomy-lab"></a>Como faço para compartilhar um laboratório de toomy link direto
um link direto de tooshare tooyour os usuários do laboratório, você pode executar Olá procedimento a seguir:

1. Procure toohello laboratório Olá portal do Azure.
2. Copie a URL de laboratório de saudação do seu navegador e compartilhá-lo com os usuários do laboratório.

> [!NOTE]
> Se os usuários do laboratório são usuários externos com um [conta da Microsoft](#what-is-a-microsoft-account) e Active directory da empresa tooyour não pertencem, ele poderão receber um erro ao navegar link toohello fornecido. Se receberem um erro, instrua os tooclick seu nome no canto superior direito Olá Olá portal do Azure e diretório hello selecione onde laboratório Olá existe da saudação **diretório** seção do menu hello.
>
>

## <a name="what-is-a-microsoft-account"></a>O que é uma conta da Microsoft?
Uma conta da Microsoft é o que você utiliza para quase tudo o que faz com os serviços e dispositivos da Microsoft. É um endereço de email e senha que use toosign em tooSkype, Outlook.com, OneDrive, Windows Phone e Xbox LIVE – isso significa que seus arquivos, fotos, contatos e configurações podem seguir tooany dispositivo.

> [!NOTE]
> Conta da Microsoft usado toobe chamado "Windows Live ID".
>
>


**Solução de problemas**
## <a name="my-artifact-failed-during-vm-creation-how-do-i-troubleshoot-it"></a>Meu artefato falhou durante a criação da VM. Como solucionar isso?
Consulte também[como falhas de artefato de toodiagnose em DevTest Labs](devtest-lab-troubleshoot-artifact-failure.md) toolearn como tooobtain registra sobre seu artefato com falha.

## <a name="why-isnt-my-existing-virtual-network-saving-properly"></a>Por que a minha rede virtual existente não está salvando corretamente?
Uma das possibilidades é que o nome da rede virtual contém pontos. Se assim, tente remover Olá pontos ou substituí-las com hifens e, em seguida, tente salvar Olá rede virtual novamente.

## <a name="why-do-i-get-a-parent-resource-not-found-error-when-provisioning-a-vm-from-powershell"></a>Por que recebo um erro "Recurso pai não encontrado" ao provisionar uma VM do PowerShell?
Quando um recurso é um recurso de tooanother do pai, recurso pai de saudação deve existir antes de criar o recurso de filho hello. Se ele não existir, você receberá um erro **ParentResourceNotFound**. Se você não especificar uma dependência no recurso pai, Olá, recursos do hello filho podem ser implantado antes pai hello.

As VMs são recursos filhos em um laboratório em um grupo de recursos. Quando você usa toodeploy de modelos do Azure Resource Manager por meio do PowerShell, nome do grupo de recursos Olá fornecido no hello script do PowerShell deve ser nome do grupo de recursos saudação do laboratório hello. Para obter mais informações, consulte [Solução de erros comuns de implantação do Azure ](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-common-deployment-errors#parentresourcenotfound).

## <a name="where-can-i-find-more-error-information-if-a-vm-deployment-fails"></a>Onde posso encontrar mais informações sobre erros se há falha na implantação de uma VM?
Erros de implantação de VM são capturados nos logs de atividade de saudação. Você pode encontrar os logs de atividade de máquinas virtuais por meio de saudação laboratório **logs de auditoria** ou **diagnóstico de máquina Virtual** no menu de recursos de saudação na folha VM do laboratório hello (folha Olá exibe depois de selecionar Olá VM do **Minhas máquinas virtuais** lista).

Às vezes, o erro de implantação Olá ocorre antes do início da saudação implantação da VM -, como quando o limite de assinatura de saudação para um recurso criado com hello VM for excedido. Nesse caso, detalhes do erro Olá são capturados no nível de laboratório Olá **logs de atividade** que é possível localizar final Olá Olá **políticas e configurações** configurações. Para obter mais informações sobre como usar a atividade faz logon no Azure, consulte [exibição atividade registra ações de tooaudit em recursos](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-audit).

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]
