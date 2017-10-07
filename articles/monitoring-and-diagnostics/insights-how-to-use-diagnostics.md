---
title: "aaaEnable monitoramento e diagnóstico no Microsoft Azure | Microsoft Docs"
description: "Saiba como tooset o diagnóstico para os seus recursos no Azure."
author: rboucher
manager: carolz
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: af1947a9-c211-4aa1-8924-880a86240be4
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: robb
ms.openlocfilehash: 865d010c5846fff6d871e20eca2bc4ac35028354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-monitoring-and-diagnostics"></a>Habilitar monitoramento e diagnóstico
Em Olá [Portal do Azure](https://portal.azure.com), você pode configurar os dados de monitoramento e diagnóstico avançados, frequentes, sobre seus recursos. Você também pode usar o hello [API REST](https://msdn.microsoft.com/library/azure/dn931932.aspx) ou [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooconfigure diagnóstico programaticamente.

Dados de diagnóstico, monitoramento e métrica no Azure são salvos em uma conta de armazenamento de sua escolha. Isso permite toouse quaisquer ferramentas que você deseja tooread Olá dados, um Gerenciador de armazenamento, ferramentas de terceiros toothird BI tooPower.

## <a name="when-you-create-a-resource"></a>Quando criar um recurso
A maioria dos serviços permitem diagnóstico tooenable quando você criá-los primeiro no hello [Portal do Azure](https://portal.azure.com).

1. Vá muito**novo** e escolha recursos Olá que lhe interessam.
2. Selecione **Configuração opcional**.
    ![Folha Diagnósticos](./media/insights-how-to-use-diagnostics/Insights_CreateTime.png)
3. Selecione **Diagnóstico**e clique  **Em**. Você precisará toochoose conta de armazenamento de saudação que você deseja que o diagnóstico toobe salvo. Você será cobrado de taxas de dados normais para armazenamento e transações quando enviar conta de armazenamento do diagnóstico tooa.
4. Clique em **Okey** e criar o recurso de saudação.

## <a name="change-settings-for-an-existing-resource"></a>Alterar configurações para um recurso existente
Se você já tiver criado um recurso e desejar que as configurações de diagnóstico toochange hello (nível de toochange Olá da coleta de dados, por exemplo), você pode fazer esse direito no hello Portal do Azure.

1. Vá toohello recurso e clique em Olá **configurações** comando.
2. Selecione **Diagnóstico**.
3. Olá **diagnóstico** folha tem todos os diagnósticos possíveis hello e coleta dados para o recurso de monitoramento. Para alguns recursos também pode escolher um **retenção** política para dados hello, tooclean-o da conta de armazenamento.
    ![Diagnóstico de armazenamento](./media/insights-how-to-use-diagnostics/Insights_StorageDiagnostics.png)
4. Depois de escolher as configurações, clique em Olá **salvar** comando. Pode demorar um pouco enquanto para monitorar dados tooshow backup, se você estiver habilitando-lo para Olá primeira vez.

### <a name="categories-of-data-collection-for-virtual-machines"></a>Categorias de coleta de dados para máquinas virtuais
Para máquinas virtuais todas as métricas e os logs serão registrados em intervalos de um minuto para que você sempre tenha Olá a maioria das informações atualizadas sobre o seu computador.

* **Métricas básicas** : métricas de integridade sobre sua máquina virtual, como processador e memória
* **Métricas de rede e Web** : métricas sobre suas conexões de rede e serviços Web
* **Métricas de .NET** : métricas sobre Olá .NET e em aplicativos ASP.NET em execução em sua máquina virtual
* **Métricas SQL** : se você estiver executando o Microsoft SQL Service, suas métricas de desempenho
* **Os logs de eventos do aplicativo Windows** : eventos do Windows que são enviados toohello canal de aplicativo
* **Os logs de eventos do sistema Windows** : eventos do Windows que são enviados toohello canal de sistema. Isso também inclui todos os eventos do [Microsoft Antimalware](http://go.microsoft.com/fwlink/?LinkID=404171&clcid=0x409).
* **Logs de segurança de eventos do Windows** : eventos do Windows que são enviados de canal de segurança toohello
* **Logs de infraestrutura de diagnóstico** : log sobre a infraestrutura de coleção de diagnóstico Olá
* **Logs de IIS** : logs sobre o servidor IIS

Observe que no momento não há suporte para determinadas distribuições do Linux, e, Olá agente convidado deve ser instalado na máquina virtual de saudação.

## <a name="next-steps"></a>Próximas etapas
* [Receba notificações de alerta](insights-receive-alert-notifications.md) sempre que ocorrerem eventos operacionais ou métricas ultrapassarem um limite.
* [Monitorar as métricas de serviço](insights-how-to-customize-monitoring.md) toomake-se de que o serviço está disponível e respondendo.
* [Dimensionar automaticamente a contagem de instância](insights-how-to-scale.md) toomake-se de que a escala de serviço com base na demanda.
* [Monitorar o desempenho do aplicativo](../application-insights/app-insights-azure-web-apps.md) se você quiser toounderstand exatamente como o código está sendo executado na nuvem hello.
* [Exibir eventos e log de atividades](insights-debugging-with-events.md) toolearn tudo o que aconteceu em seu serviço.
* [Controlar a integridade do serviço](insights-service-health.md) toofind out quando o Azure sofreu interrupções de serviço ou degradação de desempenho.

