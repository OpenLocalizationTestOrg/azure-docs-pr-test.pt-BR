---
title: nuvem de sua infraestrutura de identidade local no hello aaaMonitor.
description: "Esta é hello Azure AD Connect Health página que descreve o que é e por que você usaria."
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 82798ea6-5cd3-4f30-93ae-d56536f8d8e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 84d0b00ec800ba98094343731aa4e7317dfb0c61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-on-premises-identity-infrastructure-and-synchronization-services-in-hello-cloud"></a>Monitorar seus serviços locais de infraestrutura e sincronização de identidade na nuvem Olá
Integridade de conexão do Active Directory (AD do Azure) do Azure ajuda a monitorar e obter ideias sobre sua identidade local hello e infraestrutura de serviços de sincronização. Ele permite que você toomaintain tooOffice uma conexão confiável 365 e Microsoft Online Services, fornecendo recursos de monitoramento para os componentes da chave de identidade, como servidores de serviços de Federação do Active Directory (AD FS), servidores do Azure AD Connect (também conhecidos como o mecanismo de sincronização), controladores de domínio do Active Directory, etc. Ele também torna Olá principais pontos de dados sobre esses componentes facilmente acessível para que você possa obter o uso e outros importante insights toomake informado decisões.

Olá informações são apresentadas em Olá [portal do Azure AD Connect Health](https://aka.ms/aadconnecthealth). No portal do Azure AD Connect Health hello, você pode exibir alertas, monitoramento de desempenho, análise de uso e outras informações. O Azure AD Connect Health permite a Lente única saudação de integridade para os componentes da chave de identidade em um único local.

![O que é a Integridade do Azure AD Connect](./media/active-directory-aadconnect-health/aadconnecthealth2.png)

Como aumentam os recursos de saudação no Azure AD Connect Health, portal Olá fornece um único painel por meio de Lente de saudação da identidade. Você obtém um ambiente ainda mais robusto, íntegro e integrado para seu usuários tooincrease suas tarefas tooget capacidade.

## <a name="why-use-azure-ad-connect-health"></a>Por que usar o Azure AD Connect Health?
Quando você integra seus diretórios locais com o AD do Azure, os usuários estão mais produtivos, porque não há uma identidade comum tooaccess tanto na nuvem e recursos locais. No entanto, essa integração cria o desafio de saudação de assegurar que esse ambiente esteja íntegro, para que os usuários podem acessar com segurança recursos de nuvem no local e em Olá de qualquer dispositivo. O Azure AD Connect Health ajuda a monitorar e obter ideias sobre sua infraestrutura de identidade local que é usado tooaccess Office 365 ou outros aplicativos do AD do Azure. É tão simples quanto instalar um agente em cada um de seus servidores de identidade locais.

## <a name="azure-ad-connect-health-for-ad-fsactive-directory-aadconnect-health-adfsmd"></a>[Azure AD Connect Health para AD FS](active-directory-aadconnect-health-adfs.md)
O Azure AD Connect Health para AD FS dá suporte ao AD FS 2.0 no Windows Server 2008 R2, no Windows Server 2012 e no Windows Server 2012 R2. Ele também suporta o monitoramento do proxy Olá AD FS ou servidores de proxy de aplicativo da web que fornecem autenticação para acesso à extranet. Com uma instalação fácil e de baixo custo de saudação agente de integridade, o Azure AD Connect Health para AD FS fornece Olá conjunto de funcionalidades principais a seguir:

* Monitoramento com alertas tooknow quando servidores de proxy do AD FS e o AD FS não estão íntegros
* Notificações de email para alertas críticos
* Tendências nos dados de desempenho, que são úteis para o planejamento de capacidade do AD FS
* Análise de uso para entradas do AD FS com tabelas dinâmicas (aplicativos, usuários, o local de rede etc.), que são úteis toounderstand como o AD FS está obtendo utilizado
* Relatórios para o AD FS, como os 50 primeiros usuários com tentativas inválidas de nome de usuário/senha e o último endereço IP

Olá vídeo a seguir fornece uma visão geral do Azure AD Connect Health para AD FS.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-AD-Connect-Health--Monitor-you-identity-bridge/player]
>
>

## <a name="azure-ad-connect-health-for-syncactive-directory-aadconnect-health-syncmd"></a>[Azure AD Connect Health para sincronização](active-directory-aadconnect-health-sync.md)
O Azure AD Connect Health para sincronização monitora e fornece informações sobre as sincronizações Olá que ocorrem entre o Active Directory no local e o AD do Azure. O Azure AD Connect Health para sincronização fornece Olá conjunto de funcionalidades principais a seguir:

* Monitoramento com alertas tooknow quando um servidor do Azure AD Connect, também conhecido como Olá mecanismo de sincronização não está íntegro
* Notificações de email para alertas críticos
* Informações operacionais de sincronização, incluindo gráficos de latência para operações de sincronização e tendências em operações diferentes, como adições, atualizações, exclusões
* Visão geral rápida informações sobre propriedades de sincronização e o último êxito exportar tooAzure AD
* Os relatórios sobre erros de sincronização no nível do objeto \(não exigem o Azure AD Premium\)

Olá vídeo a seguir fornece uma visão geral do Azure AD Connect Health para sincronização.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Health-Monitoring-the-sync-engine/player]
>
>

## <a name="azure-ad-connect-health-for-ad-dsactive-directory-aadconnect-health-addsmd"></a>[Azure AD Connect Health para AD DS](active-directory-aadconnect-health-adds.md)
O Azure AD Connect Health para AD DS (Active Directory Domain Services) fornece monitoramento para controladores de domínio instalados no Windows Server 2008 R2, no Windows Server 2012, no Windows Server 2012 R2 e no Windows Server 2016. saudação de instalação do agente de integridade permite que você toomonitor seu local ambiente de nuvem de saudação do AD DS. O Azure AD Connect Health para AD DS fornece Olá conjunto de funcionalidades principais a seguir:

* Monitorar alertas toodetect quando os controladores de domínio estão em estado íntegros e notificações para alertas críticos de email
* Painel de controladores de domínio Hello, que fornece uma exibição rápida da integridade de saudação e o status operacional dos controladores de domínio
* Painel de Status de replicação de saudação que tem informações mais recentes de replicação hello e links tootroubleshooting guias quando forem detectados erros
* Acesso rápido em qualquer lugar tooperformance gráficos de dados de contadores de desempenho populares, que são necessários para fins de monitoramento e solução de problemas

Olá vídeo a seguir fornece uma visão geral do Azure AD Connect Health para AD DS.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-AD-Connect-Health-monitors-on-premises-AD-Domain-Services/player]
>
>

## <a name="get-started-with-azure-ad-connect-health"></a>Introdução ao Azure AD Connect Health
tooget iniciar com o Azure AD Connect Health, Olá use as etapas a seguir:

1. [Obtenha o Azure AD Premium](../active-directory-get-started-premium.md) ou [inicie uma avaliação](https://azure.microsoft.com/trial/get-started-active-directory/).
2. [Baixe e Instale os agentes do Azure AD Connect Health](#download-and-install-azure-ad-connect-health-agent) nos seus servidores de identidade.
3. Painel de integridade de conexão de saudação do AD do Azure View em [https://aka.ms/aadconnecthealth](https://aka.ms/aadconnecthealth).

> [!NOTE]
> Lembre-se de que, antes de ver os dados no painel do Azure AD Connect Health, você precisa tooinstall Olá agentes de integridade de conexão do AD do Azure nos servidores de destino.
>
>

## <a name="download-and-install-azure-ad-connect-health-agent"></a>Baixar e instalar o Agente do Azure AD Connect Health
* Verifique se você [atender aos requisitos de saudação](active-directory-aadconnect-health-agent-install.md#requirements) do Azure AD Connect Health.
* Introdução ao uso do Azure AD Connect Health do AD FS
    * [Baixe o Agente do Azure AD Connect Health para AD FS.](http://go.microsoft.com/fwlink/?LinkID=518973)
    * [Consulte as instruções de instalação de saudação](active-directory-aadconnect-health-agent-install.md#installing-the-azure-ad-connect-health-agent-for-ad-fs).
* Introdução ao uso do Azure AD Connect Health para sincronização
    * [Baixe e instale a versão mais recente de saudação do Azure AD Connect](http://go.microsoft.com/fwlink/?linkid=615771). Olá agente de integridade de sincronização será instalado como parte da instalação do hello Azure AD Connect (versão 1.0.9125.0 ou superior).
* Introdução ao uso do Azure AD Connect Health para o AD DS
    * [Baixe o Agente do Azure AD Connect Health para AD DS](http://go.microsoft.com/fwlink/?LinkID=820540).
    * [Consulte as instruções de instalação de saudação](active-directory-aadconnect-health-agent-install.md#installing-the-azure-ad-connect-health-agent-for-ad-ds).

## <a name="azure-ad-connect-health-portal"></a>Portal do Azure AD Connect Health
portal do Azure AD Connect Health Olá mostra os modos de exibição de alertas, monitoramento de desempenho e análise de uso. Olá https://aka.ms/aadconnecthealth URL leva a folha principal toohello do Azure AD Connect Health. Você pode pensar uma folha como uma janela. Na folha de saudação principal, você vê **início rápido**, serviços no Azure AD Connect Health e opções de configuração adicionais. Consulte Olá explicações breves que siga a captura de tela hello e captura de tela a seguir. Depois de implantar agentes Olá, o serviço de integridade de saudação identifica automaticamente serviços hello Azure AD Connect Health está monitorando.

> [!NOTE]
> Para obter informações sobre licenciamento, consulte Olá [do Azure AD conectar perguntas frequentes sobre](active-directory-aadconnect-health-faq.md) ou hello [página de preços do Azure AD](https://aka.ms/aadpricing).
    
![Portal do Azure AD Connect Health](./media/active-directory-aadconnect-health/portal4.png)

* **Início rápido**: quando você seleciona essa opção, Olá **início rápido** folha é aberta. Você pode baixar o agente do Azure AD Connect Health da saudação selecionando **obter ferramentas**. Você também pode acessar a documentação e fornecer comentários.
* **Serviços de Federação do Active Directory**: essa opção mostra todos os serviços de saudação do AD FS do Azure AD Connect Health está monitorando no momento. Quando você seleciona uma instância, folha Olá que abre mostra informações sobre essa instância de serviço. Essas informações incluem uma análise de visão geral, propriedades, alertas, monitoramento e análise de uso. Leia mais sobre recursos de saudação [usando o Azure AD Connect Health com AD FS](active-directory-aadconnect-health-adfs.md).
* **Azure Active Directory Connect (Sincronização)**: essa opção mostra seus servidores do Azure AD Connect que o Azure AD Connect Health está monitorando atualmente. Quando você selecionar entrada hello, folha Olá que abre mostra informações sobre seus servidores do Azure AD Connect. Leia mais sobre recursos de saudação [usando o Azure AD Connect Health para sincronização](active-directory-aadconnect-health-sync.md).
* **Serviços de domínio do Active Directory**: essa opção mostra todas as florestas do AD DS de saudação do Azure AD Connect Health está monitorando no momento. Quando você seleciona uma floresta, folha Olá que abre mostra informações sobre nessa floresta. Essas informações incluem uma visão geral de informações essenciais, painel de controle de controladores de domínio hello, painel de Status de replicação hello, alertas e monitoramento. Leia mais sobre recursos de saudação [usando o Azure AD Connect Health com AD DS](active-directory-aadconnect-health-adds.md).
* **Configurar**: Esta seção inclui opções tooturn Olá a seguir ou desativar:

  - Atualização automática tooautomatically atualização hello Azure AD Connect Health toohello mais recente versão do agente: será automaticamente atualizada toohello versões mais recentes Olá agente do Azure AD Connect Health quando elas estiverem disponíveis. Isso é habilitado por padrão.
  - Permitir que os dados de integridade do diretório do Microsoft access tooyour AD do Azure para fins de solução de problemas: se isso estiver habilitado, a Microsoft pode ver Olá os mesmos dados que você vê. Essas informações podem ajudar na solução de problemas e a obter ajuda para problemas. Isso está desabilitado por padrão.

## <a name="related-links"></a>Links relacionados
* [Instalação do Agente do Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Operações de Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Usando o Azure AD Connect Health com o AD FS](active-directory-aadconnect-health-adfs.md)
* [Usando o Azure AD Connect Health para sincronização](active-directory-aadconnect-health-sync.md)
* [Usar o Azure AD Connect Health com o AD DS](active-directory-aadconnect-health-adds.md)
* [Perguntas frequentes do Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Histórico de versão do Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)
