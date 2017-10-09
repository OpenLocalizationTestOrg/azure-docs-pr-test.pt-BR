---
title: "um espaço de trabalho do aprendizado de máquina do aaaManage | Microsoft Docs"
description: "Gerenciar espaços de trabalho do access tooAzure aprendizado de máquina, implantar e gerenciar os serviços da web de API ML"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: daf3d413-7a77-4beb-9a7a-6b4bdf717719
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye
ms.openlocfilehash: 7bd378d82aa46f4340ca974c7dc5a612c089cdca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-machine-learning-workspace"></a>Gerenciar um espaço de trabalho do Azure Machine Learning

> [!NOTE]
> Para obter informações sobre como gerenciar serviços Web no portal de serviços de Web do aprendizado de máquina hello, consulte [gerenciar um serviço Web usando o portal de serviços de Web de aprendizado de máquina do Azure Olá](machine-learning-manage-new-webservice.md).
> 
> 

Você pode gerenciar espaços de trabalho do aprendizado de máquina em qualquer Olá portal do Azure ou Olá portal clássico do Azure.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="use-hello-azure-portal"></a>Use Olá portal do Azure

toomanage um espaço de trabalho Olá portal do Azure:

1. Entrar toohello [portal do Azure](https://portal.azure.com/) usando uma conta de administrador de assinatura do Azure.
2. Na caixa de pesquisa de saudação na parte superior de saudação da página Olá, insira "espaços de trabalho do aprendizado de máquina" e, em seguida, selecione **espaços de trabalho aprendizado de máquina**.
3. Clique em espaço de trabalho de saudação deseja toomanage.

Além de informações de gerenciamento de recursos padrão toohello e opções disponíveis, você pode:

- Exibição **propriedades** - essa página exibe informações de espaço de trabalho e recursos de Olá, e você pode alterar a assinatura de saudação e o grupo de recursos que esse espaço de trabalho está conectado com.
- **Ressincronizar as chaves de armazenamento** -espaço de trabalho Olá mantém a conta de armazenamento toohello de chaves. Se a conta de armazenamento Olá altera as chaves, então você pode clicar em **Resync chaves** toosynchronize chaves de saudação com espaço de trabalho de saudação.

Serviços de web hello toomanage associados a este espaço de trabalho, usar o portal de serviços de Web do aprendizado de máquina hello. Consulte [gerenciar um serviço Web usando o portal de serviços de Web de aprendizado de máquina do Azure Olá](machine-learning-manage-new-webservice.md) para obter informações completas.

> [!NOTE]
> toodeploy ou gerenciar novos serviços da web, você deve ser atribuído um colaborador ou função de administrador no serviço web do hello assinatura toowhich Olá é implantada. Se você convidar outro espaço de trabalho de aprendizado de máquina usuário tooa, você deve atribui-los tooa a função Colaborador ou o administrador de assinatura de saudação antes de implantar ou gerenciar os serviços web. 
> 
>Para obter mais informações sobre como definir permissões de acesso, consulte [exibir as atribuições de acesso para usuários e grupos no portal do Azure – visualização pública do hello](../active-directory/role-based-access-control-manage-assignments.md).

## <a name="use-hello-azure-classic-portal"></a>Use Olá portal clássico do Azure

Usando Olá portal clássico do Azure, você pode gerenciar seus espaços de trabalho do aprendizado de máquina para:

* Monitorar como o espaço de trabalho hello está sendo usado
* Configurar Olá tooallow de espaço de trabalho ou negar acesso
* Gerenciar serviços Web criados no espaço de trabalho de saudação
* Excluir espaço de trabalho de saudação

Além disso, a guia Painel Olá fornece uma visão geral do uso do espaço de trabalho e uma visão geral rápida das suas informações de espaço de trabalho.  

> [!TIP]
> No estúdio de aprendizado de máquina do Azure, em Olá **serviços WEB** guia, você pode adicionar, atualizar ou excluir um serviço Web de aprendizado de máquina.
> 
> 

toomanage um espaço de trabalho Olá portal clássico do Azure:

1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com/) usando o Microsoft Azure conta - use conta Olá associado Olá assinatura do Azure.
2. No painel de serviços do Microsoft Azure hello, clique em **APRENDIZADO de máquina**.
3. Clique em espaço de trabalho de saudação deseja toomanage.

página de espaço de trabalho Olá tem três guias:

* **PAINEL** -permite que você tooview uso de espaço de trabalho e informações
* **CONFIGURAR** -permite que o espaço de trabalho de toohello de acesso toomanage
* **SERVIÇOS WEB** -permite que serviços Web toomanage que foram publicados deste espaço de trabalho

### <a name="toomonitor-how-hello-workspace-is-being-used"></a>toomonitor como o espaço de trabalho hello está sendo usado
Clique em Olá **painel** guia.

No painel de saudação, você pode exibir o uso geral do seu espaço de trabalho e obter uma visão geral rápida das informações de espaço de trabalho.

* Olá **de computação** gráfico mostra os recursos de computação hello está sendo usados pelo espaço de trabalho de saudação. Você pode alterar Olá exibição toodisplay relativo ou absolutos e você pode alterar o período de tempo de saudação exibido no gráfico de saudação.
* **Visão geral de uso** exibe o armazenamento do Azure que está sendo usado pelo espaço de trabalho de saudação.
* **Visão rápida** fornece um resumo das informações do espaço de trabalho e links úteis.

> [!NOTE]
> Olá **tooML entrar Studio** link abre o estúdio de aprendizado de máquina usando Olá Account da Microsoft você está conectado. Olá Account da Microsoft usada toosign no toohello toocreate portal clássico do Azure um espaço de trabalho não tem automaticamente permissão tooopen esse espaço de trabalho. tooopen um espaço de trabalho, você deve estar conectado toohello Account da Microsoft que foi definido como proprietário de saudação do espaço de trabalho de saudação ou se precisar de tooreceive um convite de espaço de trabalho da saudação toojoin Olá proprietário.
> 
> 

### <a name="toogrant-or-suspend-access-for-users"></a>toogrant ou suspender acesso aos usuários
Clique em Olá **configurar** guia.

Na guia de configuração de saudação, você pode:

* Suspenda o espaço de trabalho do aprendizado de máquina do acesso toohello clicando em Negar. Os usuários não será capaz de tooopen o espaço de trabalho de saudação no estúdio de aprendizado de máquina. toorestore acessar, clique em permitir.

toomanage outras contas que têm acesso toohello espaço de trabalho no estúdio de aprendizado de máquina, clique em **tooML entrar Studio** em hello **painel** guia (consulte a Observação do hello anterior sobre  **Sign-in tooML Studio**). Isso abre o espaço de trabalho Olá no estúdio de aprendizado de máquina. Aqui, clique em Olá **configurações** guia e, em seguida, **usuários**. Você pode clicar em **CONVIDAR usuários mais** toogive usuários acessar toohello de espaço de trabalho, ou selecione um usuário e clique em **remover**.

### <a name="toomanage-web-services-in-this-workspace"></a>Serviços de web toomanage neste espaço de trabalho
Clique em Olá **serviços WEB** guia.

Isso exibe uma lista de serviços Web publicados desse espaço de trabalho.
toomanage um serviço web, clique em nome de saudação na página de serviço Olá lista tooopen Olá Web.

Um serviço Web pode ter um ou mais pontos de extremidade definidos.

* Você pode definir mais pontos de extremidade no ponto de extremidade de adição toohello "Padrão". tooadd Olá ponto de extremidade, clique em **gerenciar pontos de extremidade** na parte inferior de saudação do portal de serviços de Web de aprendizado de máquina do Azure Olá painel tooopen hello.
* toodelete um ponto de extremidade (você não pode excluir o ponto de extremidade hello "Padrão"), clique Olá a caixa de seleção no início de saudação da linha do ponto de extremidade hello e clique em **excluir**. Isso remove o ponto de extremidade Olá Olá serviço Web.
  
  > [!NOTE]
  > Se um aplicativo estiver usando o ponto de extremidade de serviço de web hello quando o ponto de extremidade de saudação é excluído, o aplicativo hello receberá Olá um erro próxima vez que ele tenta tooaccess serviço de saudação.
  > 
  > 

Clique em nome de saudação de um tooopen de ponto de extremidade de serviço Web-lo. 

No painel de Olá, você pode exibir o uso geral do serviço Web durante um período de tempo. Você pode selecionar tooview período Olá menu Olá período suspensa no canto superior direito de saudação de gráficos do uso de saudação. painel Olá mostra Olá informações a seguir:

* **Solicitações ao longo do tempo** exibe um gráfico de etapa do número de saudação de solicitações nos Olá período de tempo selecionado. Ele pode ajudar a identificar se houver picos de uso.
* **Solicitações de solicitação-resposta** exibe Olá o número total de chamadas de solicitação-resposta serviço Olá recebeu via hello período de tempo selecionado e quantos deles falha.
* **Tempo médio de solicitação-resposta de computação** exibe uma média de tempo de saudação necessário tooexecute Olá recebeu solicitações.
* **Solicitações em lote** exibe o número total saudação do serviço de saudação de solicitações em lote recebeu via Olá período de tempo selecionado e quantos deles falha.
* **Média de latência do trabalho** exibe uma média de tempo de saudação necessário tooexecute Olá recebeu solicitações.
* **Erros** exibe a agregação do número de erros que ocorreram Olá no serviço de web toohello chamadas.
* **Custos de serviços** exibe encargos Olá para o plano de cobrança Olá associadas ao serviço de saudação.

Página Configurar de saudação, você pode atualizar Olá propriedades a seguir:

* **Descrição** permite que você tooenter uma descrição para Olá serviço da Web. Descrição é um campo obrigatório.
* **Registro em log** permite erro tooenable ou Desabilitar log no ponto de extremidade de saudação. Para obter mais informações sobre Registrar em Log, veja Habilitar [registro em log de serviços Web do Machine Learning](machine-learning-web-services-logging.md).
* **Habilitar dados de exemplo** permite que você tooprovide dados de exemplo que você pode usar o serviço do tootest Olá solicitação-resposta. Se você criou o serviço web de saudação no estúdio de aprendizado de máquina, dados de exemplo hello são obtidos da dados saudação seu tootrain usado seu modelo. Se você criou o serviço Olá programaticamente, dados saudação provém de dados de exemplo hello fornecido como parte do pacote JSON de saudação.

