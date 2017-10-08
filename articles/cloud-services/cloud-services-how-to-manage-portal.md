---
title: "tarefas de gerenciamento de serviço de nuvem aaaCommon | Microsoft Docs"
description: "Saiba como os serviços de nuvem toomanage em Olá portal do Azure. Esses exemplos usam Olá portal do Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: cb218ad9-77d4-4149-83db-71159c00767e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: ade8a18a7754edbaae4903230c26c009fef63ed7
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

Em Olá **serviços de nuvem (clássicos)** área de hello Azure portal, você pode atualizar uma função de serviço ou uma implantação, promover uma implantação de preparo tooproduction, vincular o serviço de nuvem tooyour recursos para que você possa ver recursos Olá dependências e escala Olá recursos juntos e excluir um serviço de nuvem ou uma implantação.

Para obter mais informações sobre como tooscale seu serviço de nuvem está disponível [aqui](cloud-services-how-to-scale-portal.md).

## <a name="how-to-update-a-cloud-service-role-or-deployment"></a>Como atualizar uma função ou implantação de Serviço de Nuvem
Se precisar de código do aplicativo hello tooupdate para seu serviço de nuvem, use **atualização** na folha de serviço de nuvem hello. Você pode atualizar única função ou todas as funções. tooupdate, você pode carregar um novo pacote de serviço ou o arquivo de configuração de serviço.

1. Em Olá [portal do Azure][Azure portal], selecione Serviço de nuvem Olá tooupdate desejado. Essa etapa abre a folha de instância de serviço de nuvem hello.
2. Na folha de saudação, clique em Olá **atualização** botão.

    ![Botão Atualizar](./media/cloud-services-how-to-manage-portal/update-button.png)

3. Atualize implantação Olá com um novo arquivo de pacote de serviço (. cspkg) e o arquivo de configuração de serviço (. cscfg).

    ![UpdateDeployment](./media/cloud-services-how-to-manage-portal/update-blade.png)

4. **Opcionalmente,** atualizar o rótulo de implantação hello e conta de armazenamento de saudação.
5. Se nenhuma função tiver apenas uma instância de função, selecione Olá **implantar mesmo se uma ou mais funções contiverem uma única instância** tooenable Olá atualização tooproceed.

    O Azure pode garantir apenas 99,95 por cento de disponibilidade do Serviço de Nuvem durante uma atualização do Serviço de Nuvem se cada função tiver pelo menos duas instâncias de função (máquinas virtuais). Com duas instâncias de função, uma máquina virtual processa solicitações de cliente, enquanto outros hello está atualizada.

6. Verificar **comece** toohave atualização de saudação aplicada após o término hello carregamento do pacote de saudação.
7. Clique em **Okey** toobegin atualização Olá service.

## <a name="how-to-swap-deployments-toopromote-a-staged-deployment-tooproduction"></a>Como: alternar implantações toopromote tooproduction uma implantação de preparo
Quando você decide toodeploy uma nova versão de um serviço de nuvem, estágio e testar a nova versão em seu ambiente de preparo de serviço de nuvem. Use **trocar** tooswitch Olá URLs por quais Olá duas implantações são endereçadas e promovem um novo tooproduction de versão.

Você pode alternar as implantações de saudação **serviços de nuvem** painel de página ou hello.

1. Em Olá [portal do Azure][Azure portal], selecione Serviço de nuvem Olá tooupdate desejado. Essa etapa abre a folha de instância de serviço de nuvem hello.
2. Na folha de saudação, clique em Olá **trocar** botão.

    ![Permutação dos Serviços de Nuvem](./media/cloud-services-how-to-manage-portal/swap-button.png)

3. Olá seguinte prompt de confirmação é aberto.

    ![Permutação dos Serviços de Nuvem](./media/cloud-services-how-to-manage-portal/swap-prompt.png)

4. Depois de verificar as informações de implantação de saudação, clique em **Okey** tooswap implantações de saudação.

    troca de implantação Olá rapidamente acontece porque Olá única alteração é Olá virtual VIPs (endereços IP) para implantações de saudação.

    custos de computação toosave, você pode excluir Olá implantação de preparo depois de verificar se sua implantação de produção está funcionando conforme o esperado.

### <a name="common-questions-about-swapping-deployments"></a>Perguntas comuns sobre troca de implantações

**Quais são os pré-requisitos de saudação para implantações de permuta?**

Existem dois pré-requisitos essenciais para uma troca de implantação bem-sucedida:

- Se você quiser toouse um endereço IP estático para o slot de produção, você deve reservar um para o slot de preparo também. Caso contrário, a troca de saudação falhará.

- Todas as instâncias de funções de devem ser executado antes que você pode executar uma permuta de saudação. Você pode verificar o status de saudação de instâncias na folha de visão geral de saudação do hello portal do Azure. Como alternativa, você pode usar o hello [Get-AzureRole](/powershell/module/azure/get-azurerole?view=azuresmps-3.7.0) comando no Windows PowerShell.

Observe que atualizações do sistema operacional convidado e operações de recuperação de serviço também pode causar a implantação troca toofail. Para saber mais, confira [Solucionar problemas de implantação do serviço de nuvem](cloud-services-troubleshoot-deployment-problems.md).

**Uma troca incorre em tempo de inatividade para meu aplicativo? Como devo lidar com isso?**

Conforme descrito na seção de última Olá, uma troca de implantação é normalmente rápida, pois ela é apenas uma alteração de configuração no balanceador de carga do Azure Olá. Entretanto, em alguns casos, ela pode levar dez segundos ou mais e resultar em falhas de conexão transitórias. clientes de tooyour do impacto toolimit, considere implementar [lógica de repetição do cliente](../best-practices-retry-general.md).

## <a name="how-to-link-a-resource-tooa-cloud-service"></a>Como: vincular a um serviço de nuvem do recurso tooa
Olá portal do Azure não contém links para recursos juntos como atual portal clássico do Azure hello. Em vez disso, implantar recursos adicionais toohello mesmo grupo de recursos que está sendo usado por Olá serviço de nuvem.

## <a name="how-to-delete-deployments-and-a-cloud-service"></a>Como excluir implantações e um Serviço de Nuvem
Antes de poder excluir um serviço de nuvem, você deve excluir cada implantação existente.

custos de computação toosave, você pode excluir Olá implantação de preparo depois de verificar se sua implantação de produção está funcionando conforme o esperado. Você será cobrado por custos de computação de instâncias de função implantadas que estejam paradas.

Use Olá toodelete do procedimento a seguir, uma implantação ou o serviço de nuvem.

1. Em Olá [portal do Azure][Azure portal], selecione Serviço de nuvem Olá toodelete desejado. Essa etapa abre a folha de instância de serviço de nuvem hello.
2. Na folha de saudação, clique em Olá **excluir** botão.

    ![Permutação dos Serviços de Nuvem](./media/cloud-services-how-to-manage-portal/delete-button.png)

3. Você pode excluir o serviço de nuvem inteira Olá verificando **serviços de nuvem e suas implantações** ou escolha a saudação **implantação de produção** ou hello **implantação de preparo**.

    ![Permutação dos Serviços de Nuvem](./media/cloud-services-how-to-manage-portal/delete-blade.png)

4. Clique em Olá **excluir** botão na parte inferior da saudação.
5. serviço de nuvem Olá toodelete, clique em **excluir serviço de nuvem**. Em seguida, no prompt de confirmação de saudação, clique em **Sim**.

> [!NOTE]
> Quando um serviço de nuvem é excluído e o monitoramento detalhado está configurado, você deve excluir manualmente dados saudação da conta de armazenamento. Para obter informações sobre onde toofind Olá tabelas de métricas, consulte [isso](cloud-services-how-to-monitor.md) artigo.


## <a name="how-to-find-more-information-about-failed-deployments"></a>Como localizar mais informações sobre implantações com falha
Olá **visão geral** folha tem uma barra de status na parte superior da saudação. Quando você clica em barras hello, uma nova folha abre e exibe informações de erro. Se a implantação de saudação não contém quaisquer erros, folha de informações de saudação está em branco.

![Permutação dos Serviços de Nuvem](./media/cloud-services-how-to-manage-portal/status-info.png)



[Azure portal]: https://portal.azure.com

## <a name="next-steps"></a>Próximas etapas
* [Configuração geral do serviço de nuvem](cloud-services-how-to-configure-portal.md).
* Saiba como muito[implantar um serviço de nuvem](cloud-services-how-to-create-deploy-portal.md).
* Configurar um [nome de domínio personalizado](cloud-services-custom-domain-name-portal.md).
* Configurar [certificados SSL](cloud-services-configure-ssl-certificate-portal.md).
