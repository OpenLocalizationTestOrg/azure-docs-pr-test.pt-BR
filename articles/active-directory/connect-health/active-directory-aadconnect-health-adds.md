---
title: aaaUsing do Azure AD Connect Health com AD DS | Microsoft Docs
description: "Esta é hello Azure AD Connect Health página que discutiremos como toomonitor AD DS."
services: active-directory
documentationcenter: 
author: arluca
manager: femila
editor: curtand
ms.assetid: 19e3cf15-f150-46a3-a10c-2990702cd700
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: e2fb6be65407d02c214dcab385b85d6cb54f48de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-ad-connect-health-with-ad-ds"></a>Usar o Azure AD Connect Health com o AD DS
Olá documentação a seguir é toomonitoring específico Active Directory Domain Services com o Azure AD Connect Health. Olá suporte para versões do AD DS são: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 e Windows Server 2016.

Para saber mais sobre como monitorar o AD FS com o Azure AD Connect Health, veja [Usando o Azure AD Connect Health com o AD FS](active-directory-aadconnect-health-adfs.md). Além disso, para obter informações sobre como monitorar o Azure AD Connect (Sincronização) com o Azure AD Connect Health, confira [Usar o Azure AD Connect Health para Sincronização](active-directory-aadconnect-health-sync.md).

![Azure AD Connect Health para AD DS](./media/active-directory-aadconnect-health/aadconnect-health-adds-entry.png)

## <a name="alerts-for-azure-ad-connect-health-for-ad-ds"></a>Alertas do Azure AD Connect Health para AD DS
Olá seção alertas no Azure AD Connect Health para AD DS, fornece uma lista de alertas ativas e resolvidas, controladores de domínio tooyour relacionados. Selecionar um alerta ativo ou resolvido abre uma nova folha com informações adicionais, junto com as etapas de resolução e links toosupporting documentação. Cada tipo de alerta pode ter uma ou mais instâncias, que correspondem a tooeach Olá de controladores de domínio afetados por esse alerta específica. Inferior Olá da folha de alerta hello, duas vezes em um controlador de domínio afetado tooopen uma folha adicional com mais detalhes sobre essa instância de alerta.

Nesta folha, você pode habilitar notificações por email para alertas e alterar o intervalo de tempo de saudação na exibição. Expandir o intervalo de tempo de saudação permite alertas resolvidos antes de toosee.

![Erro de sincronização do Azure AD Connect](./media/active-directory-aadconnect-health/aadconnect-health-adds-alerts.png)

## <a name="domain-controllers-dashboard"></a>Painel Controladores de Domínio
Esse painel fornece uma exibição topológica de seu ambiente, juntamente com as principais métricas operacionais e o status de integridade de cada um dos controladores de domínio monitorados. métricas de saudação apresentada identificá tooquickly, controladores de domínio que podem exigir mais investigação. Por padrão, somente um subconjunto de colunas de saudação é exibido. No entanto, você pode encontrar todo o conjunto de colunas disponíveis, Olá clicando duas vezes o comando de colunas de saudação. Selecionando colunas hello mais importantes para você, ativa esse painel em um único e fácil colocar tooview integridade de saudação do seu ambiente do AD DS.

![Controladores de Domínio](./media/active-directory-aadconnect-health/aadconnect-health-adds-domainsandsites-dashboard.png)

Controladores de domínio podem ser agrupados por seus respectivos domínios ou um site, que é útil para entender a topologia do ambiente hello. Por fim, se você clicar duas vezes cabeçalho de folha Olá, painel Olá maximiza a tooutilize Olá disponível espaço na tela. Este modo de exibição maior será útil quando várias colunas forem exibidas.

## <a name="replication-status-dashboard"></a>Painel Status de Replicação
Esse painel fornece uma exibição da topologia de replicação e o status de replicação de saudação controladores de domínio monitorados. status de saudação da tentativa de replicação mais recente Olá estiver listado, juntamente com a documentação útil para qualquer erro for encontrado. Você pode clicar duas vezes um controlador de domínio com um erro, tooopen uma nova folha com informações como: detalhes sobre o erro hello, as etapas de resolução recomendado e links tootroubleshooting documentação.

![Status de replicação](./media/active-directory-aadconnect-health/aadconnect-health-adds-replication.png)

## <a name="monitoring"></a>Monitoramento
Esse recurso fornece tendências gráficas dos contadores de desempenho diferentes, que são coletados continuamente de cada um dos controladores de domínio Olá monitorado. O desempenho de um controlador de domínio pode ser comparado facilmente em todos os outros controladores de domínio monitorados na floresta. Além disso, você pode ver vários contadores de desempenho lado a lado, o que é útil ao solucionar problemas no ambiente.

![Monitoramento](./media/active-directory-aadconnect-health/aadconnect-health-adds-monitoring.png)

Por padrão, podemos ter pré-selecionados quatro contadores de desempenho; No entanto, você pode incluir outras pessoas clicando Olá filtro comando e selecionando ou desmarcando qualquer contador de desempenho desejado. Além disso, você pode clicar duas vezes uma tooopen de gráfico de contador de desempenho uma nova folha, que inclui pontos de dados para cada um dos controladores de domínio Olá monitorado.

## <a name="related-links"></a>Links relacionados
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Instalação do Agente do Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Operações de Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Usando o Azure AD Connect Health com o AD FS](active-directory-aadconnect-health-adfs.md)
* [Usando o Azure AD Connect Health para sincronização](active-directory-aadconnect-health-sync.md)
* [Perguntas frequentes do Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Histórico de versão do Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)

