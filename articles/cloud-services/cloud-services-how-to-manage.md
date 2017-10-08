---
title: "tarefas de gerenciamento de serviço de nuvem de aaaCommon (clássico) | Microsoft Docs"
description: "Saiba como os serviços de nuvem toomanage em Olá portal clássico do Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 41a30e50-067c-485b-96fd-434a6d057abc
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: 03b1d632f1480d0f65c87b7f8ffc747417acf7b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-cloud-services"></a>Como os serviços de nuvem tooManage
> [!div class="op_single_selector"]
> * [Portal do Azure](cloud-services-how-to-manage-portal.md)
> * [Portal clássico do Azure](cloud-services-how-to-manage.md)
>
>

Em Olá **serviços de nuvem** área da saudação clássico do Azure portal, você pode atualizar uma função de serviço ou uma implantação, promover uma implantação de preparo tooproduction, vincular o serviço de nuvem tooyour recursos para que você possa ver recursos Olá dependências e escala Olá recursos juntos e excluir um serviço de nuvem ou uma implantação.

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a>Como atualizar uma função ou implantação de Serviço de Nuvem
Se precisar de código do aplicativo hello tooupdate para seu serviço de nuvem, use **atualização** no painel de saudação **serviços de nuvem** página, ou **instâncias** página. Você pode atualizar única função ou todas as funções. Você precisará tooupload um novo pacote de serviço e o arquivo de configuração de serviço.

1. Em Olá [portal clássico do Azure](https://manage.windowsazure.com/), no painel de saudação **serviços de nuvem** página, ou **instâncias** , clique em **atualização**.

    ![UpdateDeployment](./media/cloud-services-how-to-manage/CloudServices_UpdateDeployment.png)

2. Em **rótulo de implantação**, insira uma implantação de saudação do tooidentify nome (por exemplo, mycloudservice4). Você encontrará o rótulo de implantação de saudação em **início rápido** no painel de saudação.
3. Em **pacote**, use **procurar** o arquivo de pacote de serviço do tooupload hello (. cspkg).
4. Em **configuração**, use **procurar** o arquivo de configuração de serviço do tooupload hello (. cscfg).
5. Em **função**, selecione **todos os** se você quiser tooupgrade todas as funções hello serviço de nuvem. Atualizar tooperform uma única função, selecione Olá função tooupdate. Mesmo se você selecionar uma função específica tooupdate, atualizações de saudação no arquivo de configuração do serviço de saudação são funções de tooall aplicado.
6. Se as alterações de atualização Olá Olá número de funções ou tamanho de saudação de qualquer função, selecione Olá **permitir atualização se alterações de tamanhos de função ou o número de funções** caixa de seleção tooenable Olá atualização tooproceed.

    Lembre-se de que se você alterar o tamanho de saudação de uma função (ou seja, o tamanho de saudação de uma máquina virtual que hospeda uma instância de função) ou Olá número de funções, cada instância de função (máquina virtual) deve ser reinstalada e todos os dados locais serão perdidos.

7. Se nenhuma função de serviço tem apenas uma instância de função, selecione Olá **atualizar mesmo se uma ou mais funções contiverem uma caixa de seleção de instância única** tooenable Olá atualização tooproceed.

    O Azure pode garantir apenas 99,95 por cento de disponibilidade do Serviço de Nuvem durante uma atualização do Serviço de Nuvem se cada função tiver pelo menos duas instâncias de função (máquinas virtuais). Que permite que uma máquina virtual tooprocess cliente solicitações enquanto outros hello está sendo atualizada.

8. Clique em **Okey** toobegin (marca de seleção) atualizando o serviço de saudação.

## <a name="how-to-swap-deployments-toopromote-a-staged-deployment-tooproduction"></a>Como: alternar implantações toopromote tooproduction uma implantação de preparo
Use **trocar** toopromote uma implantação de preparo de uma tooproduction de serviço de nuvem. Quando você decidir toodeploy uma nova versão de um serviço de nuvem, pode preparar e testar a nova versão em seu ambiente de preparo de serviço de nuvem enquanto seus clientes estão usando a versão atual do hello em produção. Quando você estiver pronto toopromote Olá novo tooproduction de versão, você pode usar **trocar** tooswitch Olá URLs pelo qual Olá duas implantações são endereçadas.

Você pode alternar as implantações de saudação **serviços de nuvem** painel de página ou hello.

1. Em Olá [portal clássico do Azure](https://manage.windowsazure.com/), clique em **serviços de nuvem**.
2. Na lista de saudação de serviços de nuvem, clique tooselect de serviço de nuvem Olá-lo.
3. Clique em **Permutar**.

    Olá seguinte prompt de confirmação é aberto.

    ![Permutação dos Serviços de Nuvem](./media/cloud-services-how-to-manage/CloudServices_Swap.png)

4. Depois de verificar as informações de implantação de saudação, clique em **Sim** tooswap implantações de saudação.

    troca de implantação Olá rapidamente acontece porque Olá única alteração é Olá virtual VIPs (endereços IP) para implantações de saudação.

    toosave custos de computação, você pode excluir a implantação Olá no hello ambiente de preparo quando tiver certeza de que a nova implantação de produção de hello é executado como esperado.

### <a name="common-questions-about-swapping-deployments"></a>Perguntas comuns sobre troca de implantações

**Quais são os pré-requisitos de saudação para implantações de permuta?**

Existem dois pré-requisitos essenciais para uma troca de implantação bem-sucedida:

- Se você quiser toouse um endereço IP estático para o slot de produção, você deve reservar um para o slot de preparo também. Caso contrário, a troca de saudação falhará.

- Todas as instâncias de funções de devem ser executado antes que você pode executar uma permuta de saudação. Você pode verificar o status de saudação de suas instâncias em Olá portal clássico do Azure ou usando [Olá comando Get-AzureRole no Windows PowerShell](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0).

Observe que atualizações do sistema operacional convidado e operações de recuperação de serviço também podem causar toofail de trocas de implantação. Confira [Solucionar problemas de implantação do serviço de nuvem](cloud-services-troubleshoot-deployment-problems.md) para obter mais detalhes.

**Uma troca incorre em tempo de inatividade para meu aplicativo? Como devo lidar com isso?**

Conforme descrito na seção de última hello, uma troca de implantação geralmente é muito rápida porque é apenas uma alteração de configuração no balanceador de carga do Azure hello. Entretanto, em alguns casos, ela pode levar dez segundos ou mais e resultar em falhas de conexão transitórias. clientes de tooyour do impacto toolimit, considere implementar [lógica de repetição do cliente](../best-practices-retry-general.md).

## <a name="how-to-link-a-resource-tooa-cloud-service"></a>Como: vincular a um serviço de nuvem do recurso tooa
tooshow dependências do serviço de nuvem em outros recursos, você pode vincular uma instância de banco de dados SQL ou um serviço de nuvem de toohello de conta de armazenamento. Você pode vincular e desvincular recursos Olá **recursos vinculados** da página e, em seguida, monitorar o uso no painel de serviço de nuvem hello. Se uma conta de armazenamento vinculada tiver monitoramento ativado, você pode monitorar o Total de solicitações no painel de serviço de nuvem hello.

Use **Link** toolink um novo ou existente banco de dados SQL instância ou armazenamento conta tooyour serviço de nuvem. Você pode dimensionar, em seguida, banco de dados de saudação junto com a função hello de serviço de nuvem que está usando no hello **escala** página. (Uma conta de armazenamento é dimensionada automaticamente à medida que cresce o uso.) Para obter mais informações, consulte [como tooScale um serviço de nuvem e recursos vinculados](cloud-services-how-to-scale.md).

Você também pode monitorar, gerenciar e dimensionar o banco de dados de saudação em Olá **bancos de dados** nó de saudação portal clássico do Azure.

"Vincular" um recurso nesse sentido não conecta seu recurso de toohello do aplicativo. Se você criar um novo banco de dados usando **Link**, você precisará tooadd Olá conexão cadeias de caracteres tooyour o código do aplicativo e serviço de nuvem Atualize hello. Você também precisará tooadd cadeias de caracteres de conexão, se seu aplicativo usa recursos em uma conta de armazenamento vinculada.

Olá procedimento a seguir descreve como toolink uma nova instância de banco de dados SQL, implantado em um novo servidor de banco de dados SQL, o serviço de nuvem tooa.

### <a name="toolink-a-sql-database-instance-tooa-cloud-service"></a>toolink um serviço de nuvem de tooa de instância de banco de dados SQL
1. Em Olá [portal clássico do Azure](http://manage.windowsazure.com/), clique em **serviços de nuvem**. Em seguida, clique em nome Olá Olá nuvem tooopen Olá de painel de serviço.
2. Clique em **Recursos Vinculados**.

    Olá **recursos vinculados** página será aberta.

    ![LinkedResourcesPage](./media/cloud-services-how-to-manage/CloudServices_LinkedResourcesPage.png)

3. Clique em **Vincular um Recurso** ou em **Vincular**.

    Olá **vincular recurso** assistente é iniciado.

    ![Vincular Página1](./media/cloud-services-how-to-manage/CloudServices_LinkedResources_LinkPage1.png)

4. Clique em **Crie um novo recurso** ou em **Vincular um recurso existente**.
5. Escolha o tipo de saudação do recurso toolink. Em Olá [portal clássico do Azure](http://manage.windowsazure.com/), clique em **banco de dados SQL**. (Olá portal clássico do Azure oferece suporte à vinculação de um serviço de nuvem de tooa de conta de armazenamento.)
6. configuração de banco de dados toocomplete hello, siga as instruções na Ajuda do hello **bancos de dados SQL** área da saudação portal clássico do Azure.

    Você pode acompanhar o progresso de saudação do hello operação na área de mensagem de saudação de vinculação.

    Quando vinculação estiver concluída, você pode monitorar o status de saudação do recurso Olá vinculado no painel de serviço de nuvem hello. Para obter informações sobre como dimensionar um banco de dados SQL vinculado, consulte [como tooScale um serviço de nuvem e recursos vinculados](cloud-services-how-to-scale.md).

### <a name="toounlink-a-linked-resource"></a>toounlink um recurso vinculado
1. Em Olá [portal clássico do Azure](http://manage.windowsazure.com/), clique em **serviços de nuvem**. Em seguida, clique em nome Olá Olá nuvem tooopen Olá de painel de serviço.
2. Clique em **recursos vinculados**e, em seguida, selecione o recurso de saudação.
3. Clique em **Desvincular**. Em seguida, clique em **Sim** no prompt de confirmação de saudação.

    Desvincular um banco de dados SQL não tem nenhum efeito no banco de dados de saudação ou banco de dados do aplicativo hello conexões toohello. Você ainda poderá gerenciar o banco de dados Olá Olá **bancos de dados SQL** área da saudação portal clássico do Azure.

## <a name="how-to-delete-deployments-and-a-cloud-service"></a>Como excluir implantações e um Serviço de Nuvem
Antes de poder excluir um serviço de nuvem, você deve excluir cada implantação existente.

custos de computação toosave, você pode excluir a implantação de preparo depois de verificar se sua implantação de produção está funcionando conforme o esperado. Você é cobrado pelos custos de computação das instâncias de função mesmo que um Serviço de Nuvem não esteja em execução.

Use Olá toodelete do procedimento a seguir, uma implantação ou o serviço de nuvem.

1. Em Olá [portal clássico do Azure](http://manage.windowsazure.com/), clique em **serviços de nuvem**.
2. Selecione o serviço de nuvem hello e, em seguida, clique em **excluir**. (tooselect um serviço de nuvem sem abrir o painel de saudação, clique em qualquer lugar exceto nome hello na entrada de serviço de nuvem hello.)

    Se você tiver uma implantação em preparo ou de produção, você verá um menu de opções toohello semelhante seguindo um na parte inferior da saudação da janela de saudação. Antes de excluir o serviço de nuvem hello, você deve excluir todas as implantações existentes.

    ![Menu de exclusão](./media/cloud-services-how-to-manage/CloudServices_DeleteMenu.png)

3. toodelete uma implantação, clique em **excluir a implantação de produção** ou **excluir a implantação de preparo**. Em seguida, no prompt de confirmação de saudação, clique em **Sim**.
4. Se desejar que o serviço de nuvem toodelete hello, repita a etapa 3, se necessário, toodelete sua outra implantação.
5. serviço de nuvem Olá toodelete, clique em **excluir serviço de nuvem**. Em seguida, no prompt de confirmação de saudação, clique em **Sim**.

> [!NOTE]
> Se o monitoramento detalhado estiver configurado para o serviço de nuvem, Azure não exclui Olá dados de monitoramento de sua conta de armazenamento quando você excluir o serviço de nuvem hello. Você precisará dados de saudação toodelete manualmente. Para obter informações sobre onde toofind Olá tabelas de métricas, consulte "como: acessar dados de monitoramento detalhados fora Olá portal clássico do Azure" em [como serviços em nuvem tooMonitor](cloud-services-how-to-monitor.md).
>
>

## <a name="next-steps"></a>Próximas etapas
* [Configuração geral do serviço de nuvem](cloud-services-how-to-configure.md).
* Saiba como muito[implantar um serviço de nuvem](cloud-services-how-to-create-deploy.md).
* Configurar um [nome de domínio personalizado](cloud-services-custom-domain-name.md).
* Configurar [certificados SSL](cloud-services-configure-ssl-certificate.md).
