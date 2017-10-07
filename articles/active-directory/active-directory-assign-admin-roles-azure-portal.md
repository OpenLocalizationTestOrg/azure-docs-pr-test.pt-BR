---
title: "funções de administrador de aaaAssigning no Active Directory do Azure | Microsoft Docs"
description: "Uma função de administrador pode criar ou editar usuários, atribuir funções administrativas tooothers, redefinir senhas de usuário, gerenciar licenças de usuário ou gerenciar domínios. Um usuário que é atribuído a uma função de administrador tem Olá mesmas permissões em todos os toowhich de serviços de nuvem sua organização tenha assinado."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7fc27e8e-b55f-4194-9b8f-2e95705fb731
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.reviewer: Vince.Smith
ms.custom: it-pro;
ms.openlocfilehash: 41cddbf311767d9995c99ee386e6d276745dad18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="assigning-administrator-roles-in-azure-active-directory"></a>Atribuindo funções de administrador no Azure Active Directory
> [!div class="op_single_selector"]
> * [Portal do Azure](active-directory-assign-admin-roles-azure-portal.md)
> * [Portal clássico do Azure](active-directory-assign-admin-roles.md)
>
>

Usando o Azure Active Directory (AD do Azure), você pode designar administradores separados tooserve diferentes funções. Esses administradores terão acesso toovarious recursos em Olá portal do Azure ou portal clássico do Azure e, dependendo de sua função, será ser capaz de toocreate ou editar usuários, atribuir funções administrativas tooothers, redefinir senhas de usuário, gerenciar licenças de usuário, e Gerencie domínios, entre outras coisas. Um usuário que é atribuído a uma função de administrador terá Olá mesmas permissões em todos os serviços de nuvem Olá que sua organização tenha assinado, independentemente de você atribuir Olá função no portal do Office 365 de saudação ou Olá no hello portal clássico do Azure, ou usando Módulo do AD do Azure para o Windows PowerShell.

Olá, funções de administrador a seguir está disponível:

* **Administrador de Cobrança**: faz compras, gerencia as assinaturas, gerencia tíquetes de suporte e monitora a integridade do serviço.

* **Administrador de conformidade**: os usuários com essa função tem permissões de gerenciamento em Olá segurança do Office 365 e o Centro de conformidade e Centro de administração do Exchange. Mais informações em “[Sobre funções de administrador do Office 365](https://support.office.com/en-us/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d)”.

* **Administrador de serviço do CRM**: os usuários com essa função tem permissões globais no Microsoft CRM Online, quando o serviço de saudação estiver presente, bem como Olá capacidade toomanage tíquetes de suporte e monitorar a integridade do serviço. Mais informações em [Sobre funções de administrador do Office 365](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

* **Administradores do dispositivo**: os usuários com essa função se tornar os administradores de computador local em todos os dispositivos Windows 10 que estão unida tooAzure do Active Directory. Eles não têm objetos de dispositivos Olá capacidade toomanage no Active Directory do Azure.

* **Leitores de diretório**: esta é uma função herdada que é tooapplications toobe atribuído que não dão suporte a saudação [estrutura de consentimento](active-directory-integrating-applications.md). Ele não deve ser atribuído tooany usuários.

* **Contas de Sincronização de Diretório**: não use. Essa função recebe automaticamente o serviço do toohello AD do Azure Connect e não é destinada ou suporte para qualquer outro uso.

* **Gravadores de diretório**: esta é uma função herdada que é tooapplications toobe atribuído que não dão suporte a saudação [estrutura de consentimento](active-directory-integrating-applications.md). Ele não deve ser atribuído tooany usuários.

* **Administrador de serviço do Exchange**: os usuários com essa função tem permissões globais no Microsoft Exchange Online, quando o serviço hello está presente. Mais informações em [Sobre funções de administrador do Office 365](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

* **Administrador global / administrador da empresa**: os usuários com essa função têm acesso tooall administrativas recursos no Azure Active Directory, bem como serviços que agrupe tooAzure do Active Directory como o Exchange Online, SharePoint Online, e Skype for Business Online. Olá quem se inscreve para o locatário do Active Directory do Azure Olá torna-se um administrador global. Somente os administradores globais podem atribuir outras funções de administrador. Pode haver mais de um administrador global na sua empresa. Os administradores globais podem redefinir a senha de saudação para qualquer usuário e todos os outros administradores.

  > [!NOTE]
  > Na API do Graph da Microsoft, na API do Graph do Azure AD e no Azure AD PowerShell, essa função é identificada como "Administrador da Empresa". É "Administrador Global" hello [portal do Azure](https://portal.azure.com).
  >
  >

* **Emissor do convite convidado**: os usuários nesta função podem gerenciar convites de usuário convidado do Azure Active Directory B2B quando configuração de usuário de "Membros podem convidar" hello é definida tooNo. Para obter mais informações sobre a colaboração B2B em [sobre a visualização de colaboração de saudação do Azure AD B2B](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b). Ela não inclui nenhuma outra permissão.

* **Administrador do serviço Intune**: usuários com essa função tem permissões globais no Microsoft Intune on-line, quando o serviço hello está presente. Além disso, essa função contém Olá capacidade toomanage os usuários e dispositivos na política de tooassociate ordem, bem como criar e gerenciar grupos.

* **Administrador de Caixa de Correio**: essa função é usada somente como parte do suporte por email do Exchange Online para dispositivos RIM Blackberry. Se sua organização não usar o email do Exchange Online em dispositivos RIM Blackberry, não use essa função.

* **Suporte ao parceiro de Nível 1**: não use. Essa função foi substituída e será removida do AD do Azure no hello futuras. Essa função é destinada a um pequeno número de parceiros de revenda da Microsoft e não se destina ao uso geral.

* **Suporte ao parceiro de Nível 2**: não use. Essa função foi substituída e será removida do AD do Azure no hello futuras. Essa função é destinada a um pequeno número de parceiros de revenda da Microsoft e não se destina ao uso geral.

* **Administrador de Senha/Administrador de Assistência Técnica**: usuários com essa função podem redefinir senhas, gerenciar solicitações de serviço e monitorar a integridade do serviço. Administradores de senha podem redefinir senhas somente para os usuários e outros administradores de senha.

  > [!NOTE]
  > Na API do Graph da Microsoft, na API do Graph do Azure AD e no Azure AD PowerShell, essa função é identificada como "Administrador da Assistência Técnica". É "administrador de senha" hello [portal do Azure](https://portal.azure.com/).
  >
  >
  
* **Administrador de serviço do Power BI**: os usuários com essa função têm permissões globais no Microsoft Power BI, quando o serviço de saudação estiver presente, bem como Olá capacidade toomanage tíquetes de suporte e monitorar a integridade do serviço. Mais informações em [Sobre funções de administrador do Office 365](https://support.office.com/en-us/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d?ui=en-US&rs=en-001&ad=US).

* **Administrador da função com privilégios**: os usuários com essa função podem gerenciar atribuições de função no Azure Active Directory, bem como dentro do Azure AD Privileged Identity Management. Além disso, essa função permite o gerenciamento de todos os aspectos do Privileged Identity Management.

* **Administrador de segurança**: os usuários com essa função têm todas as permissões de somente leitura de saudação da função de leitor de segurança hello, além de configuração de toomanage Olá capacidade para serviços relacionados à segurança: Azure Active Directory Identity Protection Gerenciamento de identidades com privilégios e segurança do Office 365 & Centro de conformidade. Para obter mais informações sobre as permissões do Office 365 estão disponíveis em [permissões no Centro de conformidade e Olá Office 365 segurança](https://support.office.com/en-us/article/Permissions-in-the-Office-365-Security-Compliance-Center-d10608af-7934-490a-818e-e68f17d0e9c1).

* **Leitor de segurança**: os usuários com essa função têm acesso somente leitura global, incluindo todas as informações no Active Directory do Azure, proteção de identidade, gerenciamento de identidades com privilégios, bem como Olá capacidade tooread Active Directory do Azure entrar os relatórios e logs de auditoria. função Hello também concede permissão somente leitura no Centro de conformidade e segurança do Office 365. Para obter mais informações sobre as permissões do Office 365 estão disponíveis em [permissões no Centro de conformidade e Olá Office 365 segurança](https://support.office.com/en-us/article/Permissions-in-the-Office-365-Security-Compliance-Center-d10608af-7934-490a-818e-e68f17d0e9c1).

* **Administrador de suporte do serviço**: os usuários com essa função podem abrir solicitações de suporte com a Microsoft para serviços do Azure e o Office 365 e modos de exibição Olá Centro de painel e a mensagem de serviço no hello portal do Azure e o portal de administração do Office 365. Mais informações em [Sobre funções de administrador do Office 365](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

* **Administrador de serviço do SharePoint**: os usuários com essa função tem permissões globais no Microsoft SharePoint Online, quando o serviço de saudação estiver presente, bem como Olá capacidade toomanage tíquetes de suporte e monitorar a integridade do serviço. Mais informações em [Sobre funções de administrador do Office 365](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

* **Skype for Business / administrador de serviço do Lync**: os usuários com essa função tem permissões globais no Microsoft Skype for Business, quando o serviço hello está presente, bem como gerenciar atributos de usuário do Skype específicos no Active Directory do Azure. Além disso, essa função concede Olá capacidade toomanage tíquetes e monitor de integridade do serviço. Mais informações em [Sobre funções de administrador do Office 365](https://support.office.com/article/About-Office-365-admin-roles-da585eea-f576-4f55-a1e0-87090b6aaa9d).

  > [!NOTE]
  > Na API do Graph da Microsoft, na API do Graph do Azure AD e no Azure AD PowerShell, essa função é identificada como "Administrador de Serviços do Lync". É "Skype para o administrador de serviço do negócio" hello [portal do Azure](https://portal.azure.com/).
  >
  >

* **Administrador da Conta de Usuário**: os usuários com essa função podem criar e gerenciar todos os aspectos de usuários e grupos. Além disso, essa função inclui tíquetes de suporte do hello capacidade toomanage e monitores de integridade do serviço. Algumas restrições se aplicam. Por exemplo, essa função não permite a exclusão de um administrador global e, embora permita a alteração de senhas para não administradores, ela não permite a alteração de senhas para os administradores globais ou outros administradores com privilégios.

## <a name="administrator-permissions"></a>Permissões de administrador

### <a name="billing-administrator"></a>Administrador de cobrança

| O que ele pode fazer | O que não pode fazer |
| --- | --- |
|<p>Exibir informações da empresa e do usuário</p><p>Gerenciar tíquetes de suporte do Office</p><p>Executar operações de cobrança e compra de produtos do Office</p> |<p>Redefinir senhas de usuário</p><p>Criar e gerenciar modos de exibição do usuário</p><p>Criar, editar e excluir usuários e grupos e gerenciar licenças de usuário</p><p>Gerenciar domínios</p><p>Editar informações da empresa</p><p>Delegar funções administrativas tooothers</p><p>Usar sincronização de diretório</p><p>Exibir logs de auditoria</p>|

### <a name="global-administrator"></a>Administrador global
| O que ele pode fazer | O que não pode fazer |
| --- | --- |
| <p>Exibir informações da empresa e do usuário</p><p>Gerenciar tíquetes de suporte do Office</p><p>Executar operações de cobrança e compra de produtos do Office</p><p>Redefinir senhas de usuário</p>
<p>Redefinir senhas de outro administrador</p> <p>Criar e gerenciar modos de exibição do usuário</p><p>Criar, editar e excluir usuários e grupos e gerenciar licenças de usuário</p><p>Gerenciar domínios</p><p>Editar informações da empresa</p><p>Delegar funções administrativas tooothers</p><p>Usar sincronização de diretório</p><p>Habilitar ou desabilitar autenticação multifator</p><p>Exibir logs de auditoria</p> |N/D |

### <a name="password-administrator"></a>Administrador de senha
| O que ele pode fazer | O que não pode fazer |
| --- | --- |
| <p>Exibir informações da empresa e do usuário</p><p>Gerenciar tíquetes de suporte do Office</p><p>Redefinir senhas de usuário</p> <p>Redefinir senhas de outro administrador</p>|<p>Executar operações de cobrança e compra de produtos do Office</p><p>Criar e gerenciar modos de exibição do usuário</p><p>Criar, editar e excluir usuários e grupos e gerenciar licenças de usuário</p><p>Gerenciar domínios</p><p>Editar informações da empresa</p><p>Delegar funções administrativas tooothers</p><p>Usar sincronização de diretório</p><p>Exibir relatórios</p>|

### <a name="service-administrator"></a>Administrador de serviço
| O que ele pode fazer | O que não pode fazer |
| --- | --- |
| <p>Exibir informações da empresa e do usuário</p><p>Gerenciar tíquetes de suporte do Office</p> |<p>Redefinir senhas de usuário</p><p>Executar operações de cobrança e compra de produtos do Office</p><p>Criar e gerenciar modos de exibição do usuário</p><p>Criar, editar e excluir usuários e grupos e gerenciar licenças de usuário</p><p>Gerenciar domínios</p><p>Editar informações da empresa</p><p>Delegar funções administrativas tooothers</p><p>Usar sincronização de diretório</p><p>Exibir logs de auditoria</p> |

### <a name="user-administrator"></a>Administrador de usuários
| O que ele pode fazer | O que não pode fazer |
| --- | --- |
| <p>Exibir informações da empresa e do usuário</p><p>Gerenciar tíquetes de suporte do Office</p><p>Redefinir senhas de usuário, com limitações.</p><p>Redefinir senhas de outro administrador</p><p>Redefinir senhas de outros usuários</p><p>Criar e gerenciar modos de exibição do usuário</p><p>Criar, editar e excluir usuários e grupos e gerenciar licenças de usuário, com limitações. Eles não podem excluir um administrador global ou criar outros administradores.</p> |<p>Executar operações de cobrança e compra de produtos do Office</p><p>Gerenciar domínios</p><p>Editar informações da empresa</p><p>Delegar funções administrativas tooothers</p><p>Usar sincronização de diretório</p><p>Habilitar ou desabilitar autenticação multifator</p><p>Exibir logs de auditoria</p> |

### <a name="security-reader"></a>Leitor de segurança
| Nesse | O que ele pode fazer |
| --- | --- |
| Identity Protection Center |Ler todos os relatórios de segurança e informações de configurações para recursos de segurança<ul><li>Anti-spam<li>Criptografia<li>Prevenção de perda de dados<li>Antimalware<li>Proteção avançada contra ameaças<li>Antiphishing<li>Regras de fluxo de mensagens |
| Privileged Identity Management |<p>Tem acesso somente leitura tooall informações apresentadas no Azure AD PIM: as políticas e relatórios para atribuições de função do AD do Azure, as revisões de segurança e no hello futuro ler toopolicy de acessar dados e relatórios para cenários além da atribuição de função do AD do Azure.<p>**Não é possível** inscrever-se no Azure AD PIM ou fazer quaisquer alterações tooit. No portal do PIM ou por meio do PowerShell, alguém nesta função pode ativar funções adicionais (por exemplo, Administrador Global ou administrador com privilégios de função), se o usuário Olá é um candidato para eles. |
| <p>Monitorar a integridade do serviço Office 365</p><p>Centro de Conformidade e Segurança do Office 365</p> |<ul><li>Ler e gerenciar alertas<li>Ler políticas de segurança<li>Ler informações sobre inteligência contra ameaças, Cloud App Discovery e quarentena em Pesquisar e Investigar<li>Ler todos os relatórios |

### <a name="security-administrator"></a>Administrador de segurança
| Nesse | O que ele pode fazer |
| --- | --- |
| Identity Protection Center |<ul><li>Todas as permissões da função de leitor de segurança de saudação.<li>Além disso, Olá capacidade tooperform todas as operações de IPC com exceção de redefinição de senhas. |
| Privileged Identity Management |<ul><li>Todas as permissões da função de leitor de segurança de saudação.<li>**Não é possível** gerenciar associações de função ou configurações do Azure AD. |
| <p>Monitorar a integridade do serviço Office 365</p><p>Centro de Conformidade e Segurança do Office 365 |<ul><li>Todas as permissões da função de leitor de segurança de saudação.<li>Pode configurar todas as configurações no recurso de proteção avançada contra ameaças de saudação (proteção contra malware e vírus mal-intencionado configuração de URL, rastreamento de URL, etc.). |

## <a name="details-about-hello-global-administrator-role"></a>Detalhes sobre a função de administrador global Olá
administrador global Olá tem recursos administrativos do acesso tooall. Por padrão, Olá quem se inscreve para uma assinatura do Azure é atribuído a função de administrador global Olá para o diretório de saudação. Somente os administradores globais podem atribuir outras funções de administrador.

### <a name="tooadd-a-colleague-as-a-global-administrator"></a>tooadd uma colega de trabalho como um administrador global

1. Entrar toohello [Centro de administração do Azure Active Directory](https://aad.portal.azure.com) com uma conta que seja um administrador global para o diretório do locatário hello.

   ![Como abrir o Centro de administração do Azure AD](./media/active-directory-assign-admin-roles-azure-portal/active-directory-admin-center.png)

2. Selecione **Usuários e grupos &gt; Todos os usuários**

3. Localize usuário Olá toodesignate como um administrador global e abra a folha de saudação para esse usuário.

4. Na folha de usuário hello, selecione **função de diretório**.
 
5. Na folha de função de diretório hello, selecione Olá **Administrador Global** função e salve.

## <a name="assign-or-remove-administrator-roles"></a>Atribuir ou remover funções de administrador
toolearn como usuário de tooa tooassign funções administrativas no Active Directory do Azure, consulte [atribuir um usuário tooadministrator funções na visualização do Azure Active Directory](active-directory-users-assign-role-azure-portal.md).

## <a name="deprecated-roles"></a>Funções preteridas

Olá funções a seguir não deve ser usado. Ele foi substituído e será removido do AD do Azure no hello futuras.

* Administrador de Licenças AdHoc
* Criador de Usuário Verificado por Email
* Ingresso de Dispositivo
* Gerenciadores de Dispositivo
* Usuários de Dispositivo
* Ingresso no Dispositivo no Local de Trabalho

## <a name="next-steps"></a>Próximas etapas

* toolearn mais sobre como os administradores de toochange para uma assinatura do Azure, consulte [como tooadd ou alterar funções de administrador do Azure](../billing-add-change-azure-subscription-administrator.md)
* toolearn mais sobre como o acesso aos recursos é controlado no Microsoft Azure, consulte [Noções básicas sobre o acesso a recursos no Azure](active-directory-understanding-resource-access.md)
* Para obter mais informações sobre como o Active Directory do Azure se relaciona tooyour assinatura do Azure, consulte [assinaturas do Azure como estão associadas com o Active Directory do Azure](active-directory-how-subscriptions-associated-directory.md)
* [Gerenciar usuários](active-directory-create-users.md)
* [Gerenciar senhas](active-directory-manage-passwords.md)
* [Gerenciar grupos](active-directory-manage-groups.md)
