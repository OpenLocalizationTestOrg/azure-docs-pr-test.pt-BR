---
title: "aaaSet a ambientes de preparo para aplicativos web no serviço de aplicativo do Azure | Microsoft Docs"
description: "Saiba como toouse preparado a publicação de aplicativos web no serviço de aplicativo do Azure."
services: app-service
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: mollybos
ms.assetid: e224fc4f-800d-469a-8d6a-72bcde612450
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: 338424100a20bf823323313fb6699e439f367421
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-staging-environments-in-azure-app-service"></a>Configurar ambientes de preparo no Serviço de Aplicativo do Azure
<a name="Overview"></a>

Quando você implanta seu aplicativo web, o aplicativo web no Linux, móvel back-end e aplicativo de API muito[do serviço de aplicativo](http://go.microsoft.com/fwlink/?LinkId=529714), você pode implantar tooa slot de implantação separado em vez de slot de produção saudação padrão durante a execução no hello **padrão**ou **Premium** modo do plano de serviço de aplicativo. Os slots de implantação são, na verdade, aplicativos online com seus próprios nomes de host. Elementos de conteúdo e as configurações de aplicativo podem ser trocados entre os dois slots de implantação, incluindo o slot de produção de hello. Implantar o slot de implantação do aplicativo tooa tem Olá benefícios a seguir:

* Você pode validar as alterações de aplicativo em um slot de implantação de preparo antes de trocá-lo com o slot de produção de hello.
* Implantando um slot de tooa aplicativo pela primeira vez e trocá-lo em produção garantem que todas as instâncias do slot de saudação são aquecidas antes de ser trocadas em produção. Isso elimina o tempo de inatividade quando você for implantar seu aplicativo. Olá redirecionamento do tráfego é contínuo e nenhuma solicitação é descartada como resultado de operações de troca. Todo esse fluxo de trabalho pode ser automatizado por meio da configuração de [Permuta Automática](#Auto-Swap) quando a validação de pré-permuta não é necessária.
* Após uma troca slot Olá com aplicativo preparado anteriormente agora tem Olá aplicativo de produção anterior. Se alterações Olá trocadas no slot de produção de hello estiverem não conforme o esperado, você pode executar Olá que mesma troca imediatamente tooget o "último site conhecido" de volta.

Cada modo de plano do Serviço de Aplicativo dá suporte a um número diferente de slots de implantação. toofind número Olá de slots modo do aplicativo oferece suporte, consulte [preços do serviço de aplicativo](https://azure.microsoft.com/pricing/details/app-service/).

* Quando seu aplicativo tiver vários slots, você não pode alterar o modo de saudação.
* O dimensionamento não está disponível para slots de não produção.
* O gerenciamento de recurso vinculado não tem suporte para slots de não produção. Em Olá [Portal do Azure](http://go.microsoft.com/fwlink/?LinkId=529715) somente, você pode evitar esse impacto potencial em um slot de produção movendo temporariamente o modo de planejamento do hello slot de produção não tooa diferente do serviço de aplicativo. Observe que esse slot de não produção de hello novamente deve compartilhar a saudação mesmo modo com o slot de produção de hello antes que você pode trocar os slots de saudação dois.

<a name="Add"></a>

## <a name="add-a-deployment-slot"></a>Adicionar um slot de implantação
aplicativo Hello deve estar em execução Olá **padrão** ou **Premium** modo na ordem para você tooenable vários slots de implantação.

1. Em Olá [Portal do Azure](https://portal.azure.com/), abra o aplicativo [folha de recursos](../azure-resource-manager/resource-group-portal.md#manage-resources).
2. Escolha Olá **slots de implantação** opção e, em seguida, clique em **adicionar Slot**.
   
    ![Adicionar um novo slot de implantação][QGAddNewDeploymentSlot]
   
   > [!NOTE]
   > Se Olá aplicativo não ainda estiver no hello **padrão** ou **Premium** modo, você receberá uma mensagem indicando modos de saudação tem suportada para habilitar a publicação de preparação. Neste ponto, você tem Olá opção tooselect **atualização** e navegue toohello **escala** guia do aplicativo antes de continuar.
   > 
   > 
3. Em Olá **adicionar um slot** folha, dê um nome de slot hello e selecionar se tooclone configuração do aplicativo de outro slot de implantação existente. Clique em Olá toocontinue de marca de seleção.
   
    ![Fonte de configuração][ConfigurationSource1]
   
    Olá primeira vez que você adicionar um slot, você terá apenas duas opções: configuração de clone do slot de padrão de saudação em produção ou não.
    Depois que você criou vários slots, será capaz de tooclone configuração de um slot diferente de saudação em produção:
   
    ![Fontes de configuração][MultipleConfigurationSources]
4. Na folha de recursos do aplicativo, clique em **slots de implantação**, em seguida, clique em um tooopen do slot de implantação folha de recursos do que slot, com um conjunto de métricas e configuração, assim como qualquer outro aplicativo. Olá nome do slot de saudação é mostrado na parte superior de saudação do hello folha tooremind que você está exibindo Olá slot de implantação.
   
    ![Título do slot de implantação][StagingTitle]
5. Clique em URL do aplicativo hello na folha do slot hello. Observe que o slot de implantação Olá tem seu próprio nome de host e também é um aplicativo em tempo real. slot de implantação da toohello toolimit acesso público, consulte [aplicativo Web do serviço de aplicativo – slots de implantação de produção toonon do bloco da web acesso](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).

Não há nenhum conteúdo após a criação do slot de implantação. Você pode implantar o slot toohello de uma ramificação do repositório diferente, ou um repositório diferente. Você também pode alterar a configuração do slot de saudação. Olá Use publicar perfil ou implantação as credenciais associadas Olá slot de implantação para atualizações de conteúdo.  Por exemplo, você pode [publicar toothis slot com o git](app-service-deploy-local-git.md).

<a name="AboutConfiguration"></a>

## <a name="configuration-for-deployment-slots"></a>Configuração de slots de implantação
Quando você clona a configuração de outro slot de implantação, configuração clonado Olá é editável. Além disso, alguns elementos de configuração seguirá conteúdo Olá em uma troca (não slot específico) enquanto outros elementos de configuração permanecerão no hello mesmo slot após uma troca (slot específico). Hello listas a seguir mostram configuração Olá que mudará quando você troca os slots.

**Configurações que são permutadas**:

* Configurações gerais - como a versão do framework, 32/64 bits, Web sockets
* Configurações do aplicativo (pode ser configurado toostick tooa slot)
* Cadeias de caracteres de Conexão (pode ser configurado toostick tooa slot)
* Mapeamentos de manipulador
* Configurações de monitoramento e diagnóstico
* Conteúdo de Trabalhos Web

**Configurações que não são permutadas**:

* Pontos de extremidade de publicação
* Nomes de domínio personalizados
* Associações e certificados SSL
* Configurações de escala
* Agendadores de Trabalhos Web

tooconfigure uma configuração ou conexão cadeia de caracteres toostick tooa slot do aplicativo (não trocado), Olá acesso **configurações do aplicativo** folha para um slot específico, em seguida, selecione Olá **configuração do Slot** caixa Olá elementos de configuração que devem preferir slot hello. Observe que marcar um elemento de configuração específicos de slot tem o efeito de saudação do estabelecimento de elemento como não swap em todos os slots de implantação Olá associados ao aplicativo hello.

![Configurações de slot][SlotSettings]

<a name="Swap"></a>

## <a name="swap-deployment-slots"></a>Permute slots de implantação 
Você pode trocar os slots de implantação Olá **visão geral** ou **slots de implantação** exibição da folha de recursos do aplicativo.

> [!IMPORTANT]
> Antes de você troca um aplicativo a partir de um slot de implantação em produção, certifique-se de que todas as configurações específicas de slot não são configuradas exatamente como você deseja toohave-lo no destino da troca hello.
> 
> 

1. tooswap slots de implantação, clique em Olá **trocar** botão na barra de comandos de saudação do aplicativo hello, ou na barra de comandos de saudação de um slot de implantação.
   
    ![Botão permutar][SwapButtonBar]

2. Certifique-se de destino Olá permuta origem e de troca estão definidas corretamente. Geralmente, o destino da troca Olá é slot de produção de hello. Clique em **Okey** toocomplete operação de saudação. Quando a conclusão da operação de hello, slots de implantação Olá foram trocados.

    ![Troca completa](./media/web-sites-staged-publishing/SwapImmediately.png)

    Para Olá **troca com visualização** trocar o tipo, consulte [troca com visualização (troca de várias fase)](#Multi-Phase).  

<a name="Multi-Phase"></a>

## <a name="swap-with-preview-multi-phase-swap"></a>Troca com visualização (troca de várias fases)

Troca com visualização, ou troca de várias fases, simplifica a validação de elementos de configuração específicos ao slot, como cadeias de conexão.
Para cargas de trabalho de missão crítica, você deseja toovalidate que Olá aplicativo se comporta conforme o esperado quando a configuração do slot de produção de hello for aplicada, e você deve executar essa validação *antes de* aplicativo hello é alternado para a produção. A troca com visualização é o que você precisa.

> [!NOTE]
> Não há suporte para a troca com visualização em aplicativos Web no Linux.

Quando você usa Olá **troca com visualização** opção (consulte [trocar slots de implantação](#Swap)), serviço de aplicativo hello a seguir:

- Mantém Olá destino slot inalterada para que os carga de trabalho em que slot (por exemplo, produção) não é afetada.
- Aplica-se elementos de configuração de saudação da saudação slot toohello fonte do slot de destino, incluindo cadeias de caracteres de conexão específicos de slot hello e configurações do aplicativo.
- Reinicia os processos de trabalho de saudação no slot de origem hello usando esses elementos de configuração mencionados acima.
- Quando você concluir troca Olá: move slot de origem warmed-up Olá no slot de destino hello. slot de destino Olá é movido para o slot de origem hello como em uma troca manual.
- Quando você cancela a troca de saudação: reaplica elementos de configuração de saudação do slot de origem toohello do slot de origem hello.

Você pode visualizar exatamente como Olá aplicativo se comportará com a configuração do slot de destino hello. Depois de concluir a validação, você concluir troca de saudação em uma etapa separada. Esta etapa tem Olá vantagem adicional que o slot de origem Olá já é aquecido com a configuração desejada hello e os clientes não terão nenhum tempo de inatividade.  

Exemplos de saudação cmdlets do PowerShell do Azure disponíveis para a troca de várias fase são incluídos no hello cmdlets do PowerShell do Azure para a seção de slots de implantação.

<a name="Auto-Swap"></a>

## <a name="configure-auto-swap"></a>Configurar a troca automática
Simplifica de troca automática DevOps cenários em que você deseja toocontinuously implanta seu aplicativo com zero inicialização a frio e tempo de inatividade zero para clientes finais do aplicativo hello. Quando um slot de implantação é configurado para a troca automática em produção, sempre que você enviar por push o slot de toothat de atualização de código, do serviço de aplicativo automaticamente alternará Olá aplicativo em produção após já ter aquecido no slot de saudação.

> [!IMPORTANT]
> Quando você habilitar a troca automática para um slot, certifique-se de configuração do slot de saudação é exatamente configuração Olá destinada ao slot de destino da saudação (geralmente slot de produção de hello).
> 
> 

> [!NOTE]
> Não há suporte para a troca automática em aplicativos Web no Linux.

Configurar a Permuta Automática para um slot é fácil. Siga as etapas de saudação abaixo:

1. Em **Slots de Implantação**, selecione um slot que não esteja em produção e escolha **Configurações do Aplicativo** na folha de recursos do slot.  
   
    ![][Autoswap1]
2. Selecione **na** para **troca automática**, selecione slot de destino desejado Olá em **Slot de troca automática**e clique em **salvar** na barra de comandos de saudação. Certifique-se de configuração para o slot de saudação é exatamente configuração Olá destinada ao slot de destino hello.
   
    Olá **notificações** guia pisca uma verde **êxito** após a conclusão da operação de saudação.
   
    ![][Autoswap2]
   
   > [!NOTE]
   > tootest troca automática para seu aplicativo, primeiro você poderá selecionar um slot de destino não seja de produção em **Slot de troca automática** toobecome familiarizado com o recurso de saudação.  
   > 
   > 
3. Execute um slot de implantação de toothat de envio por push de código. Troca automática ocorrerá após um curto período de tempo e atualização hello será refletida na URL do seu slot de destino.

<a name="Rollback"></a>

## <a name="toorollback-a-production-app-after-swap"></a>um aplicativo de produção após a troca de toorollback
Se qualquer erro for identificado na produção após uma troca de slot, reverter slots Olá tootheir back pré-permuta estados trocando slots de saudação mesmo dois imediatamente.

<a name="Warm-up"></a>

## <a name="custom-warm-up-before-swap"></a>Aquecimento personalizado antes da permuta
Alguns aplicativos podem exigir ações personalizadas de aquecimento. Olá `applicationInitialization` elemento de configuração no Web. config permite que você toospecify inicialização personalizada ações toobe executada antes que uma solicitação é recebida. operação de permuta Olá aguardará esse toocomplete aquecimento personalizado. Este é está um exemplo fragmento do web.config.

    <applicationInitialization>
        <add initializationPage="/" hostName="[app hostname]" />
        <add initializationPage="/Home/About" hostname="[app hostname]" />
    </applicationInitialization>

<a name="Delete"></a>

## <a name="toodelete-a-deployment-slot"></a>toodelete um slot de implantação
Na folha de saudação para um slot de implantação, folha do slot de implantação Olá aberto, clique em **visão geral** (página de saudação padrão) e clique em **excluir** na barra de comandos de saudação.  

![Excluir um slot de implantação][DeleteStagingSiteButton]

<!-- ======== AZURE POWERSHELL CMDLETS =========== -->

<a name="PowerShell"></a>

## <a name="azure-powershell-cmdlets-for-deployment-slots"></a>Cmdlets do PowerShell do Azure para slots de implantação
PowerShell do Azure é um módulo que fornece cmdlets toomanage Azure através do Windows PowerShell, incluindo suporte para gerenciar os slots de implantação no serviço de aplicativo do Azure.

* Para obter informações sobre como instalar e configurar o PowerShell do Azure e sobre a autenticação do Azure PowerShell com sua assinatura do Azure, consulte [como tooinstall e configurar o Microsoft Azure PowerShell](/powershell/azure/overview).  

- - -
### <a name="create-a-web-app"></a>Criar um aplicativo Web
```
New-AzureRmWebApp -ResourceGroupName [resource group name] -Name [app name] -Location [location] -AppServicePlan [app service plan name]
```

- - -
### <a name="create-a-deployment-slot"></a>Criar um slot de implantação
```
New-AzureRmWebAppSlot -ResourceGroupName [resource group name] -Name [app name] -Slot [deployment slot name] -AppServicePlan [app service plan name]
```

- - -
### <a name="initiate-a-swap-with-review-multi-phase-swap-and-apply-destination-slot-configuration-toosource-slot"></a>Inicia uma troca de revisão (troca de várias fase) e aplique o slot de toosource de configuração de slot de destino
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action applySlotConfig -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="cancel-a-pending-swap-swap-with-review-and-restore-source-slot-configuration"></a>Cancelar uma troca pendente (troca com revisão) e restaurar a configuração do slot de origem
```
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action resetSlotConfig -ApiVersion 2015-07-01
```

- - -
### <a name="swap-deployment-slots"></a>Permute slots de implantação
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action slotsswap -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="delete-deployment-slot"></a>Exclua um slot de implantação
```
Remove-AzureRmResource -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots –Name [app name]/[slot name] -ApiVersion 2015-07-01
```

- - -
<!-- ======== Azure CLI =========== -->

<a name="CLI"></a>

## <a name="azure-command-line-interface-azure-cli-commands-for-deployment-slots"></a>Comandos da interface de linha de comando do Azure (CLI do Azure) para slots de implantação
Olá CLI do Azure fornece comandos de plataforma cruzada para trabalhar com o Azure, incluindo suporte para o gerenciamento de slots de implantação do serviço de aplicativo.

* Para obter instruções sobre como instalar e configurar o hello CLI do Azure, incluindo informações sobre como tooconnect CLI do Azure tooyour assinatura do Azure, consulte [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md).
* comandos de saudação do toolist disponíveis para o serviço de aplicativo do Azure no hello CLI do Azure, chame `azure site -h`.

> [!NOTE] 
> Para obter os comandos da [CLI 2.0 do Azure](https://github.com/Azure/azure-cli) para slots de implantação, confira [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot).

- - -
### <a name="azure-site-list"></a>azure site list
Para obter informações sobre aplicativos de saudação na assinatura atual hello, chame **a lista de sites do azure**, conforme mostrado no exemplo a seguir de saudação.

`azure site list webappslotstest`

- - -
### <a name="azure-site-create"></a>azure site create
toocreate um slot de implantação, chame **criar site do azure** e especifique o nome de saudação de um aplicativo existente e nome de saudação do hello slot toocreate, como no exemplo a seguir de saudação.

`azure site create webappslotstest --slot staging`

tooenable de controle de origem para o novo slot hello, use Olá **– git** opção, como no exemplo a seguir de saudação.

`azure site create --git webappslotstest --slot staging`

- - -
### <a name="azure-site-swap"></a>azure site swap
toomake Olá aplicativo de produção de hello de slot de implantação atualizada, use Olá **troca de site do azure** comando tooperform uma operação de permuta, como no exemplo a seguir de saudação. aplicativo de produção de Hello não terá nenhum tempo de inatividade, nem passará uma inicialização a frio.

`azure site swap webappslotstest`

- - -
### <a name="azure-site-delete"></a>azure site delete
toodelete um slot de implantação que não é mais necessário, use Olá **exclusão de site do azure** comando, como no exemplo a seguir de saudação.

`azure site delete webappslotstest --slot staging`

- - -
> [!NOTE]
> Veja um aplicativo Web em ação. [Experimente o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/) imediatamente e crie um aplicativo inicializador de curta duração, sem necessidade de cartão de crédito e sem compromisso.
> 
> 

## <a name="next-steps"></a>Próximas etapas
[Azure serviço de aplicativo Web aplicativo – bloquear slots de implantação de produção toonon web access](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[tooApp Introdução serviço no Linux](./app-service-linux-intro.md)
[avaliação gratuita do Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/)

<!-- IMAGES -->
[QGAddNewDeploymentSlot]:  ./media/web-sites-staged-publishing/QGAddNewDeploymentSlot.png
[AddNewDeploymentSlotDialog]: ./media/web-sites-staged-publishing/AddNewDeploymentSlotDialog.png
[ConfigurationSource1]: ./media/web-sites-staged-publishing/ConfigurationSource1.png
[MultipleConfigurationSources]: ./media/web-sites-staged-publishing/MultipleConfigurationSources.png
[SiteListWithStagedSite]: ./media/web-sites-staged-publishing/SiteListWithStagedSite.png
[StagingTitle]: ./media/web-sites-staged-publishing/StagingTitle.png
[SwapButtonBar]: ./media/web-sites-staged-publishing/SwapButtonBar.png
[SwapConfirmationDialog]:  ./media/web-sites-staged-publishing/SwapConfirmationDialog.png
[DeleteStagingSiteButton]: ./media/web-sites-staged-publishing/DeleteStagingSiteButton.png
[SwapDeploymentsDialog]: ./media/web-sites-staged-publishing/SwapDeploymentsDialog.png
[Autoswap1]: ./media/web-sites-staged-publishing/AutoSwap01.png
[Autoswap2]: ./media/web-sites-staged-publishing/AutoSwap02.png
[SlotSettings]: ./media/web-sites-staged-publishing/SlotSetting.png

