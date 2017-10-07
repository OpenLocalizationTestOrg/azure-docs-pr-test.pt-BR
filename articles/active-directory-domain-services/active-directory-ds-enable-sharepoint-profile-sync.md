---
title: "Azure Active Directory Domain Services: Habilitar o suporte para o Serviço de Perfil de Usuário do SharePoint | Microsoft Docs"
description: "Configurar a sincronização de perfil do Azure Active Directory Domain Services domínios gerenciados toosupport para o SharePoint Server"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 9de4f810380309e8f6436fc24412701645978f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-managed-domain-toosupport-profile-synchronization-for-sharepoint-server"></a>Configurar a sincronização de perfil do domínio gerenciado toosupport para o SharePoint Server
O SharePoint Server inclui um Serviço de Perfil de Usuário que é usado para sincronização de perfil do usuário. tooset backup Olá serviço de perfil de usuário, as permissões apropriadas necessário toobe concedida em um domínio do Active Directory. Para saber mais, consulte [conceder permissões do Active Directory Domain Services para sincronização de perfil no SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).

Este artigo explica como você pode configurar o serviço de sincronização de perfil de usuário do servidor do SharePoint do serviços de domínio do AD do Azure domínios gerenciados toodeploy hello.

## <a name="hello-aad-dc-service-accounts-group"></a>grupo de 'Contas de serviço de controlador de domínio do AAD' Hello
Um grupo de segurança chamado '**contas de serviço de controlador de domínio do AAD**' está disponível na unidade organizacional do hello 'Usuários' em seu domínio gerenciado. Você pode ver esse grupo em Olá **computadores e usuários do Active Directory** snap-in do MMC no seu domínio gerenciado.

![Grupo de segurança Contas de Serviço do Controlador de Domínio do AAD](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts.png)

Os membros desse grupo de segurança são delegada Olá privilégios a seguir:
- privilégio de 'Replicar alterações de diretório' Hello na raiz de saudação DSE de saudação gerenciadas de domínio.
- Olá privilégio 'Replicar alterações de diretório' no contexto de nomenclatura de configuração de saudação (cn = contêiner de configuração) do hello gerenciados no domínio.

Esse grupo de segurança também é um membro do grupo interno Olá **acesso compatível do Windows 2000**.

![Grupo de segurança Contas de Serviço do Controlador de Domínio do AAD](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-properties.png)


## <a name="enable-your-managed-domain-toosupport-sharepoint-server-user-profile-sync"></a>Habilitar toosupport seu domínio gerenciado sincronização de perfil de usuário do SharePoint Server
Você pode adicionar a conta de serviço de saudação usada para toohello de sincronização de perfil de usuário do SharePoint **contas de serviço de controlador de domínio do AAD** grupo. Como resultado, conta de sincronização de saudação obtém o diretório de toohello privilégios adequados tooreplicate alterações. Essa etapa de configuração permite que o SharePoint Server toowork de sincronização de perfil de usuário corretamente.

![Contas de Serviço do Controlador de Domínio do AAD - adicionar membros](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member.png)

![Contas de Serviço do Controlador de Domínio do AAD - adicionar membros](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member2.png)

## <a name="related-content"></a>Conteúdo relacionado
* [Referência técnica - Conceder permissões do Active Directory Domain Services para sincronização de perfil no SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx)
