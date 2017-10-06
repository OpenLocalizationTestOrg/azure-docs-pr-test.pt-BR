---
title: "tooauthentication aaaIntro na automação do Azure | Microsoft Docs"
description: "Este artigo fornece uma visão geral de segurança de automação e Olá diferentes métodos de autenticação disponíveis para contas de automação na automação do Azure."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
keywords: "segurança de automação, automação segura; autenticação de automação"
ms.assetid: 4a6bc2f5-c5a2-4dfb-b10d-7950d750dee8
ms.service: automation
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/01/2017
ms.author: magoedte
ROBOTS: NOINDEX
ms.openlocfilehash: 4b4409b5be010c16f7bf00a9a0f617e3617d4663
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooauthentication-in-azure-automation"></a>Introdução tooauthentication na automação do Azure  
Automação do Azure permite que você tooautomate tarefas com base nos recursos no Azure, no local e com outros provedores de nuvem, como serviços AWS (Amazon Web).  Para que um runbook tooperform suas ações requeridas, ele deve ter permissões toosecurely acessar Olá recursos com direitos mínimos do hello exigidos na assinatura de saudação.

Este artigo aborda Olá vários cenários de autenticação com suporte pela automação do Azure e mostrar a você como tooget iniciada com base no ambiente de saudação ou ambientes precisará toomanage.  

## <a name="automation-account-overview"></a>Visão geral da Conta de Automação
Quando você inicia automação do Azure para Olá primeira vez, você deve criar pelo menos uma conta de automação. Contas de automação permitem tooisolate seus recursos de automação (runbooks, ativos, configurações) do hello recursos contidos em outras contas de automação. Você pode usar os recursos de tooseparate de contas de automação em ambientes lógicos separados. Por exemplo, você pode usar uma conta para desenvolvimento, outra para produção e outra para seu ambiente local.  Uma conta de Automação do Azure é diferente de sua conta da Microsoft ou de contas criadas em sua assinatura do Azure.

recursos de automação Olá para cada conta de automação estão associados uma única região do Azure, mas as contas de automação podem gerenciar todos os recursos de saudação em sua assinatura. contas de automação de toocreate Olá motivo principal em regiões diferentes seria se você tivesse políticas que exigem dados e recursos toobe tooa isolado específico região.

> [!NOTE]
> Contas de automação e recursos Olá contiverem que são criados no hello portal do Azure, não pode ser acessado no hello portal clássico do Azure. Se você quiser toomanage essas contas ou seus recursos com o Windows PowerShell, você deve usar os módulos do Azure Resource Manager hello.
>

Todas as tarefas de saudação que podem ser executadas com base nos recursos usando o Gerenciador de recursos do Azure e hello cmdlets do Azure na automação do Azure devem autenticar tooAzure usando a autenticação baseada em credenciais do Active Directory do Azure identidade organizacional.  Autenticação baseada em certificado era Olá original método de autenticação com o modo de gerenciamento de serviços do Azure, mas era toosetup complicada.  Autenticando tooAzure com o usuário do AD do Azure foi introduzido novamente 2014 toonot somente simplificar Olá processo tooconfigure uma conta de autenticação, mas também suporte Olá capacidade toonon interativamente autenticar tooAzure com uma única conta de usuário que trabalhou com o Gerenciador de recursos do Azure e os recursos clássicos.   

Atualmente, quando você cria uma nova conta de automação em Olá portal do Azure, ele cria automaticamente:

* Conta executar como que cria uma nova entidade de serviço no Active Directory do Azure, um certificado e atribui o controle de acesso baseado em função hello colaborador (RBAC), que será usado toomanage recursos de Gerenciador de recursos usando o runbooks.
* Clássica conta executar como ao carregar um certificado de gerenciamento, que será a ser usado toomanage gerenciamento de serviços do Azure ou os recursos clássicos usando runbooks.  

Controle de acesso baseado em função está disponível com o Azure Resource Manager toogrant permitido a conta de usuário do AD do Azure de tooan de ações e conta executar como e autenticar essa entidade de serviço.  Leia [controle de acesso baseado em função no artigo de automação do Azure](automation-role-based-access-control.md) para obter mais informações toohelp desenvolver seu modelo para gerenciar permissões de automação.  

Runbooks em execução em um trabalho de Runbook híbrido em seu data center ou em serviços em AWS de computação não é possível usar Olá mesmo método que é normalmente usado para autenticar tooAzure recursos de runbooks.  Isso ocorre porque esses recursos estão em execução fora do Azure e, portanto, serão necessário suas próprias credenciais de segurança definidas em automação tooauthenticate tooresources que eles acessarão localmente.  

## <a name="authentication-methods"></a>Métodos de autenticação
Olá, tabela a seguir resume Olá diferentes métodos de autenticação para cada ambiente de automação do Azure e Olá artigo sobre suportada como autenticação toosetup para seus runbooks.

| Método | Ambiente | Artigo |
| --- | --- | --- |
| Conta de Usuário do Azure AD |Azure Resource Manager e o Gerenciamento de Serviços do Azure |[Autenticar Runbooks com uma conta de Usuário do Azure AD](automation-create-aduser-account.md) |
| Conta Executar como do Azure |Gerenciador de Recursos do Azure |[Autenticar Runbooks com uma conta Executar como do Azure](automation-sec-configure-azure-runas-account.md) |
| Conta Executar como do Azure Clássico |Gerenciamento do Serviço do Azure |[Autenticar Runbooks com uma conta Executar como do Azure](automation-sec-configure-azure-runas-account.md) |
| Autenticação do Windows |Datacenter local |[Autenticar Runbooks para Hybrid Runbook Workers](automation-hybrid-runbook-worker.md) |
| Credenciais do AWS |Amazon Web Services |[Autenticar Runbooks com o AWS (Amazon Web Services)](automation-config-aws-account.md) |
