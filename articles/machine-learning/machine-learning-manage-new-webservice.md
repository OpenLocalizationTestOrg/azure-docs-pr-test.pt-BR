---
title: "portal de serviços de Web de aprendizado de máquina do Azure Olá aaaUse | Microsoft Docs"
description: "Gerenciar espaços de trabalho do access tooAzure aprendizado de máquina, implantar e gerenciar os serviços da web de API ML"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: jhubbard
editor: cgronlun
ms.assetid: b62cf2ca-dd2a-4a83-bb54-469f948fb026
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: v-donglo
ms.openlocfilehash: 04b49027fc0ab227382b320310088bb66aafacc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-web-service-using-hello-azure-machine-learning-web-services-portal"></a>Gerenciar um serviço Web usando o portal de serviços de Web de aprendizado de máquina do Azure Olá
Você pode gerenciar seus serviços Web clássico e o novo de aprendizado de máquina usando o portal de serviços Web de aprendizado de máquina do Microsoft Azure hello. Como os serviços Web clássicos e os novos serviços Web têm base em tecnologias subjacentes diferentes, você tem recursos de gerenciamento um pouco diferentes para cada um deles.

No portal de serviços de Web do aprendizado de máquina hello, você pode:

* Monitore como o serviço web de hello está sendo usado.
* Configurar descrição hello, atualizar chaves Olá Olá web service (novo), atualize seu armazenamento conta chave (apenas para novo), habilitar registro em log e habilitar ou desabilitar dados de exemplo.
* Exclua o serviço web de saudação.
* Criar, excluir ou atualizar planos de cobranças (somente Novo).
* Adicionar e excluir pontos de extremidade (somente Clássico)

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="permissions-toomanage-new-resources-manager-based-web-services"></a>Permissões toomanage novo Gerenciador de recursos com base em serviços web

Os Novos serviços Web são implantados como recursos do Azure. Como tal, você deve ter Olá permissões corretas toodeploy e gerenciar novos serviços da web.  toodeploy ou gerenciar novos serviços da web, você deve ser atribuído um colaborador ou função de administrador no serviço web do hello assinatura toowhich Olá é implantada. Se você convidar outro espaço de trabalho de aprendizado de máquina usuário tooa, você deve atribui-los tooa a função Colaborador ou o administrador de assinatura de saudação antes de implantar ou gerenciar os serviços web. 

Se usuário Olá não tem Olá corrigir recursos de tooaccess permissões no portal de serviços de Web de aprendizado de máquina do Azure hello, eles receberão Olá erro a seguir ao tentar toodeploy um serviço web:

*A implantação de serviço Web falhou. Essa conta não tem suficiente acesso toohello assinatura do Azure que contém Olá espaço de trabalho. Toodeploy tooAzure um serviço Web, Olá deve ser a mesma conta de convidado toohello espaço de trabalho e ser toohello acesso determinada assinatura do Azure que contém a saudação espaço de trabalho.*

Para obter mais informações sobre como criar um espaço de trabalho, consulte [Criar e compartilhar um espaço de trabalho do Azure Machine Learning](machine-learning-create-workspace.md).

Para obter mais informações sobre como definir permissões de acesso, consulte [exibir as atribuições de acesso para usuários e grupos no portal do Azure – visualização pública do hello](../active-directory/role-based-access-control-manage-assignments.md).


## <a name="manage-new-web-services"></a>Gerenciar novos serviços Web
toomanage seus serviços Web novo:

1. Entrar toohello [serviços Web de aprendizado de máquina do Microsoft Azure](https://services.azureml.net/quickstart) Olá portal usando sua conta do Microsoft Azure - conta de saudação de uso que está associado com a assinatura do Azure.
2. No menu de saudação, clique em **serviços Web**.

Isso exibe uma lista de serviços Web implantados para sua assinatura. 

toomanage um serviço Web, clique em serviços da Web. Na página de serviços Web do hello, você pode:

* Clique em Olá web serviço toomanage-lo.
* Clique em hello plano de cobrança para Olá web serviço tooupdate-lo.
* Excluir um serviço Web.
* Copie um serviço web e implantá-lo tooanother região.

Quando você clica em um serviço web, página de início rápido de serviço Olá web é aberto. página de início rápido do Olá web serviço tem duas opções de menu que permitem que você toomanage seu serviço web:

* **PAINEL** -permite o uso do serviço Web tooview.
* **CONFIGURAR** - permite que você tooadd um texto descritivo, atualização Olá chave de conta de armazenamento Olá associado Olá serviço da Web e habilitar ou desabilitar dados de exemplo.

### <a name="monitoring-how-hello-web-service-is-being-used"></a>Como o serviço web de hello está sendo usado de monitoramento
Clique em Olá **painel** guia.

No painel de Olá, você pode exibir o uso geral do serviço Web durante um período de tempo. Você pode selecionar tooview período Olá menu Olá período suspensa no canto superior direito de saudação de gráficos do uso de saudação. painel Olá mostra Olá informações a seguir:

* **Solicitações ao longo do tempo** exibe um gráfico de etapa do número de saudação de solicitações nos Olá período de tempo selecionado. Ele pode ajudar a identificar se houver picos de uso.
* **Solicitações de solicitação-resposta** exibe Olá o número total de chamadas de solicitação-resposta serviço Olá recebeu via hello período de tempo selecionado e quantos deles falha.
* **Tempo médio de solicitação-resposta de computação** exibe uma média de tempo de saudação necessário tooexecute Olá recebeu solicitações.
* **Solicitações em lote** exibe o número total saudação do serviço de saudação de solicitações em lote recebeu via Olá período de tempo selecionado e quantos deles falha.
* **Média de latência do trabalho** exibe uma média de tempo de saudação necessário tooexecute Olá recebeu solicitações.
* **Erros** exibe a agregação do número de erros que ocorreram Olá no serviço de web toohello chamadas.
* **Custos de serviços** exibe encargos Olá para o plano de cobrança Olá associadas ao serviço de saudação.

### <a name="configuring-hello-web-service"></a>Configurando o serviço web de saudação
Clique em Olá **configurar** opção de menu.

Você pode atualizar Olá propriedades a seguir:

* **Descrição** permite que você tooenter uma descrição para Olá serviço da Web.
* **Título** permite que você tooenter um título para Olá serviço Web
* **Chaves** permite que você toorotate as chaves de API primária e secundárias.
* **Chave de conta de armazenamento** permite que você tooupdate Olá chave Olá conta de armazenamento associada com alterações de serviço da Web hello. 
* **Habilitar dados de exemplo** permite que você tooprovide dados de exemplo que você pode usar o serviço do tootest Olá solicitação-resposta. Se você criou o serviço web de saudação no estúdio de aprendizado de máquina, dados de exemplo hello são obtidos da dados saudação seu tootrain usado seu modelo. Se você criou o serviço Olá programaticamente, dados saudação provém de dados de exemplo hello fornecido como parte do pacote JSON de saudação.

### <a name="managing-billing-plans"></a>Gerenciando planos de cobranças
Clique em Olá **planos** opção de menu da página de início rápido do Olá web services. Você também pode clicar no plano Olá associado com toomanage de serviço Web específico que o plano.

* **Novo** permite que você toocreate um novo plano.
* **Instância do plano de adicionar ou remover** permite muito "expansão" uma capacidade de tooadd plano existente.
* **Atualização/DownGrade** permite muito "crescer" uma capacidade de tooadd plano existente.
* **Excluir** permite que você toodelete um plano.

Clique em um plano tooview seu painel. Olá painel fornece instantâneo ou plano de uso durante um determinado período de tempo. tooselect Olá tooview de período de tempo, clique em Olá **período** suspensa no canto superior direito de saudação do painel. 

Painel de planos de saudação fornece Olá informações a seguir:

* **Descrição do plano** exibe informações sobre os custos de saudação e associado ao plano de saudação de capacidade.
* **Planejar o uso** exibe o número de saudação de transações e horas de computação que serão cobradas em relação ao plano de saudação.
* **Serviços Web** exibe Olá número de serviços Web que estão usando esse plano.
* **Principais por chamadas a serviços Web** exibe serviços Web do hello superior quatro que estão fazendo chamadas que são cobradas em relação ao plano de saudação.
* **Principais serviços da Web por horas de computação** exibe serviços Web do hello superior quatro que estão usando recursos de computação que são cobrados em relação ao plano de saudação.

## <a name="manage-classic-web-services"></a>Gerenciar Serviços Web clássicos
> [!NOTE]
> procedimentos de Olá nesta seção são serviços de web clássico toomanaging relevantes por meio do portal de serviços de Web de aprendizado de máquina do Azure hello. Para obter informações sobre como gerenciar Web clássico serviços por meio de Olá estúdio de aprendizado de máquina e Olá portal, clássico do Azure, consulte [gerenciar um espaço de trabalho do aprendizado de máquina do Azure](machine-learning-manage-workspace.md).
> 
> 

toomanage seus serviços Web clássico:

1. Entrar toohello [serviços Web de aprendizado de máquina do Microsoft Azure](https://services.azureml.net/quickstart) Olá portal usando sua conta do Microsoft Azure - conta de saudação de uso que está associado com a assinatura do Azure.
2. No menu de saudação, clique em **Web Services clássico**.

toomanage um serviço Web clássico, clique em **Web Services clássico**. Na página de Web Services clássico hello, você pode:

* Clique em pontos de extremidade do Olá web serviço tooview Olá associado.
* Excluir um serviço Web.

Quando você gerenciar um serviço Web clássico, você gerenciar cada um dos pontos de extremidade Olá separadamente. Quando você clica em um serviço web na página de serviços Web hello, lista de saudação de pontos de extremidade associado ao serviço de saudação é aberta. 

Na página de ponto de extremidade do serviço de Web clássico hello, você pode adicionar e excluir pontos de extremidade no serviço de saudação. Para saber mais sobre a adição de pontos de extremidade, veja [Criação de pontos de extremidade](machine-learning-create-endpoint.md).

Clique em uma página de início rápido Olá pontos de extremidade tooopen Olá web service. Na página de início rápido do hello, há duas opções de menu que permitem que você toomanage seu serviço web:

* **PAINEL** -permite o uso do serviço Web tooview.
* **CONFIGURAR** -permite que você tooadd um texto descritivo, ative o log de erros e desativar, chave de saudação de atualização de conta de armazenamento Olá associado Olá serviço da Web e habilitar e desabilitar dados de exemplo.

### <a name="monitoring-how-hello-web-service-is-being-used"></a>Como o serviço web de hello está sendo usado de monitoramento
Clique em Olá **painel** guia.

No painel de Olá, você pode exibir o uso geral do serviço Web durante um período de tempo. Você pode selecionar tooview período Olá menu Olá período suspensa no canto superior direito de saudação de gráficos do uso de saudação. painel Olá mostra Olá informações a seguir:

* **Solicitações ao longo do tempo** exibe um gráfico de etapa do número de saudação de solicitações nos Olá período de tempo selecionado. Ele pode ajudar a identificar se houver picos de uso.
* **Solicitações de solicitação-resposta** exibe Olá o número total de chamadas de solicitação-resposta serviço Olá recebeu via hello período de tempo selecionado e quantos deles falha.
* **Tempo médio de solicitação-resposta de computação** exibe uma média de tempo de saudação necessário tooexecute Olá recebeu solicitações.
* **Solicitações em lote** exibe o número total saudação do serviço de saudação de solicitações em lote recebeu via Olá período de tempo selecionado e quantos deles falha.
* **Média de latência do trabalho** exibe uma média de tempo de saudação necessário tooexecute Olá recebeu solicitações.
* **Erros** exibe a agregação do número de erros que ocorreram Olá no serviço de web toohello chamadas.
* **Custos de serviços** exibe encargos Olá para o plano de cobrança Olá associadas ao serviço de saudação.

### <a name="configuring-hello-web-service"></a>Configurando o serviço web de saudação
Clique em Olá **configurar** opção de menu.

Você pode atualizar Olá propriedades a seguir:

* **Descrição** permite que você tooenter uma descrição para Olá serviço da Web. Descrição é um campo obrigatório.
* **Registro em log** permite erro tooenable ou Desabilitar log no ponto de extremidade de saudação. Para obter mais informações sobre Registrar em Log, veja Habilitar [registro em log de serviços Web do Machine Learning](machine-learning-web-services-logging.md).
* **Habilitar dados de exemplo** permite que você tooprovide dados de exemplo que você pode usar o serviço do tootest Olá solicitação-resposta. Se você criou o serviço web de saudação no estúdio de aprendizado de máquina, dados de exemplo hello são obtidos da dados saudação seu tootrain usado seu modelo. Se você criou o serviço Olá programaticamente, dados saudação provém de dados de exemplo hello fornecido como parte do pacote JSON de saudação.

## <a name="grant-or-suspend-access-tooweb-services-for-users-in-hello-portal"></a>Conceder ou suspender acesso tooWeb serviços para os usuários no portal de saudação
Usando Olá portal clássico do Azure, você pode permitir ou negar acesso a usuários toospecific.

### <a name="access-for-users-of-new-web-services"></a>Acesso para usuários dos Novos Serviços Web
tooenable toowork outros usuários com os serviços da Web no portal de serviços de Web de aprendizado de máquina do Azure hello, você deve adicioná-los como administradores de co em sua assinatura do Azure.

Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com/) usando o Microsoft Azure conta - use conta Olá associado Olá assinatura do Azure.

1. No painel de navegação de saudação, clique em **configurações**, em seguida, clique em **administradores**.
2. Na parte inferior de saudação da janela de saudação, clique em **adicionar**. 
3. Na caixa de diálogo ADD A CO-ADMINISTRATOR do hello, digite o endereço de email de saudação da pessoa Olá que ser tooadd como coadministrador e assinatura hello, em seguida, selecione que você deseja Olá tooaccess coadministrador.
4. Clique em **Salvar**.

### <a name="access-for-users-of-classic-web-services"></a>Acesso para usuários dos Serviços Web Clássicos
toomanage um espaço de trabalho:

Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com/) usando o Microsoft Azure conta - use conta Olá associado Olá assinatura do Azure.

1. No painel de serviços do Microsoft Azure hello, clique em **APRENDIZADO de máquina**.
2. Clique em espaço de trabalho de saudação deseja toomanage.
3. Clique em Olá **configurar** guia.

Na guia de configuração Olá, você pode suspender o espaço de trabalho do access toohello aprendizado de máquina clicando **DENY**. Os usuários não será capaz de tooopen o espaço de trabalho de saudação no estúdio de aprendizado de máquina. acesso de toorestore, clique em **permitir**.

usuários toospecific:

toomanage outras contas que têm acesso toohello espaço de trabalho no estúdio de aprendizado de máquina, clique em **tooML entrar Studio** em Olá **painel** guia. Isso abre o espaço de trabalho Olá no estúdio de aprendizado de máquina. Aqui, clique em Olá **configurações** guia e, em seguida, **usuários**. Você pode clicar em **CONVIDAR usuários mais** toogive usuários acessar toohello de espaço de trabalho, ou selecione um usuário e clique em **remover**.

> [!NOTE]
> Olá **tooML entrar Studio** link abre o estúdio de aprendizado de máquina usando Olá Account da Microsoft você está conectado. Olá Account da Microsoft usada toosign no toohello toocreate portal clássico do Azure um espaço de trabalho não tem automaticamente permissão tooopen esse espaço de trabalho. tooopen um espaço de trabalho, você deve estar conectado toohello Account da Microsoft que foi definido como proprietário de saudação do espaço de trabalho de saudação ou se precisar de tooreceive um convite de espaço de trabalho da saudação toojoin Olá proprietário.
> 
> 

