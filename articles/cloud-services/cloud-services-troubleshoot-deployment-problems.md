---
title: "problemas de implantação de serviço de nuvem aaaTroubleshoot | Microsoft Docs"
description: "Há alguns problemas comuns que você pode encontrar ao implantar um tooAzure de serviço de nuvem. Este artigo fornece soluções toosome deles."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: a18ae415-0d1c-4bc4-ab6c-c1ddea02c870
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 15aea4f2b2913d95f3378b2e9762b232531f3c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-service-deployment-problems"></a>Solucionar problemas de implantação do serviço de nuvem
Quando você implanta um tooAzure de pacote de aplicativo de serviço de nuvem, você pode obter informações sobre a implantação de saudação do hello **propriedades** painel Olá portal do Azure. Você pode usar os detalhes de saudação em toohelp neste painel você solucionar problemas com o serviço de nuvem Olá, e você pode fornecer esse tooAzure informações sobre o suporte ao abrir uma nova solicitação de suporte.

Você pode encontrar hello **propriedades** painel da seguinte maneira:

* Em Olá portal do Azure, clique em implantação de saudação do seu serviço de nuvem **todas as configurações**e, em seguida, clique em **propriedades**.
* Em Olá portal clássico do Azure, clique em implantação de saudação do seu serviço de nuvem **painel**, localizado no canto inferior direito de saudação da página de saudação (em **visão rápida**). Lembre-se de que não há um rótulo de "Propriedades" nesse painel.

> [!NOTE]
> Você pode copiar o conteúdo de saudação do hello **propriedades** na área de transferência do painel toohello Olá ícone no canto superior direito de saudação do painel de saudação.
>
>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="problem-i-cannot-access-my-website-but-my-deployment-is-started-and-all-role-instances-are-ready"></a>Problema: não consigo acessar meu site, mas minha implantação foi iniciada e todas as instâncias de função estão prontas
link de URL do site Olá mostrado no portal de saudação não inclui a porta de saudação. porta padrão de saudação para sites é 80. Se seu aplicativo for configurado toorun em uma porta diferente, você deve adicionar Olá correto da porta número toohello URL ao acessar o site de saudação.

1. No hello portal do Azure, clique em implantação de saudação do seu serviço de nuvem.
2. Em Olá **propriedades** painel da saudação portal do Azure, verifique portas Olá Olá para instâncias de função (em **pontos de extremidade de entrada**).
3. Se a porta de saudação não for 80, adicione Olá correto da porta valor toohello URL ao acessar o aplicativo hello. toospecify uma porta não padrão, digite a URL de hello, seguido por dois-pontos (:), seguido pelo número da porta hello, sem espaços.

## <a name="problem-my-role-instances-recycled-without-me-doing-anything"></a>Problema: minhas instâncias de funções foram recicladas sem que eu tenha realizado nenhuma ação
Recuperação de serviço ocorre automaticamente quando o Azure detecta nós do problema e, portanto, move nós de toonew de instâncias de função. Quando isso ocorrer, você poderá ver suas instâncias de função serem recicladas automaticamente. toofind se do serviço de recuperação ocorreu:

1. No hello portal do Azure, clique em implantação de saudação do seu serviço de nuvem.
2. Em Olá **propriedades** painel da saudação portal do Azure, examine as informações de saudação e determinar se a recuperação de serviço ocorreu durante o tempo de saudação observado funções hello reciclagem.

As funções também serão recicladas aproximadamente uma vez por mês durante as atualizações do SO host e do SO convidado.  
Para obter mais informações, consulte Olá postagem de blog [função reinicializações de instância devido atualizações de tooOS](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx)

## <a name="problem-i-cannot-do-a-vip-swap-and-receive-an-error"></a>Problema: não consigo fazer uma permuta de VIP. Recebi uma mensagem de erro
Uma permuta de VIP não é permitida se uma atualização de implantação estiver em andamento. As atualizações de implantação podem ocorrer automaticamente quando:

* Um novo sistema operacional convidado está disponível e você está configurado para receber atualizações automáticas.
* A recuperação de serviço ocorre.

toofind out se atualizar uma automática está impedindo de fazer uma permuta de VIP:

1. No hello portal do Azure, clique em implantação de saudação do seu serviço de nuvem.
2. Em Olá **propriedades** painel da saudação portal do Azure, examine valor Olá **Status**. Se for **pronto**, em seguida, verifique **última operação** toosee se aconteceu alguma recentemente que possam impedir a permuta de VIP de saudação.
3. Repita as etapas 1 e 2 para implantação de produção de hello.
4. Se uma atualização automática estiver em andamento, aguarde toofinish antes de tentar permuta de VIP de saudação toodo.

## <a name="problem-a-role-instance-is-looping-between-started-initializing-busy-and-stopped"></a>Problema: uma instância de função está alternando entre os estados Iniciado, Inicializando, Ocupado e Parado
Essa condição pode indicar um problema com o código, pacote ou arquivo de configuração do aplicativo. Nesse caso, você deve ter o status de saudação toosee capaz de alterar os intervalos de alguns minutos e hello portal do Azure pode dizer algo como **reciclagem**, **ocupado**, ou **Inicializando**. Isso indica que há algo errado com o aplicativo hello que está impedindo a instância de função hello de execução.

Para obter mais informações sobre como tootroubleshoot para esse problema, consulte Olá postagem de blog [dados de diagnóstico de computação do Azure PaaS](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx) e [toorecycle de funções que causa problemas de comuns](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md).

## <a name="problem-my-application-stopped-working"></a>Problema: meu aplicativo parou de funcionar
1. No hello portal do Azure, clique em instância de função hello.
2. Em Olá **propriedades** painel da saudação portal do Azure, considere Olá tooresolve condições a seguir seu problema:
   * Se a instância de função hello tiver sido interrompida recentemente (você pode verificar o valor de saudação do **contagem de anulações**), implantação de saudação pode estar sendo atualizada. Aguarde toosee se a instância de função hello retoma o funcionamento por conta própria.
   * Se a instância de função hello **ocupado**, verifique o toosee de código do aplicativo se hello [StatusCheck](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.statuscheck) evento é manipulado. Talvez você precise tooadd ou corrigir algum código que trate esse evento.
   * Percorrer os dados de diagnóstico hello e solucionar problemas na postagem de blog Olá [dados de diagnóstico de computação do Azure PaaS](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).

> [!WARNING]
> Se você reciclar o serviço de nuvem, você redefinir propriedades de saudação para implantação hello, apagando efetivamente as informações de saudação do problema original hello.
>
>

## <a name="next-steps"></a>Próximas etapas
Confira mais [artigos sobre solução de problemas](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) para serviços de nuvem.

toolearn como função de serviço de nuvem tootroubleshoot problemas usando dados de diagnóstico do computador de PaaS do Azure, consulte [série do blog de Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).
