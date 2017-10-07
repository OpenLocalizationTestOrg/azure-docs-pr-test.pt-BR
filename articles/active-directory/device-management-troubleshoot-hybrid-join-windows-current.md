---
title: "aaaTroubleshooting híbrida do Active Directory do Azure associado a dispositivos Windows 10 e Windows Server 2016 | Microsoft Docs"
description: "Solução de problemas do Azure Active Directory híbrido ingressado em dispositivos do Windows 10 e do Windows Server 2016."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: cc252d1d0684d6632694afc8a367327794228c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-windows-10-and-windows-server-2016-devices"></a>Solução de problemas do Azure Active Directory híbrido ingressado em dispositivos do Windows 10 e do Windows Server 2016 

Este tópico é aplicável toohello clientes a seguir:

-   Windows 10
-   Windows Server 2016

Para outros clientes do Windows, consulte [Solução de problemas do Azure Active Directory híbrido ingressado em dispositivos de nível inferior](device-management-troubleshoot-hybrid-join-windows-legacy.md).

Este tópico pressupõe que você tenha [dispositivos ingressados no configurado híbrida do Active Directory do Azure](device-management-hybrid-azuread-joined-devices-setup.md) Olá toosupport os seguintes cenários:

- Acesso condicional com base em dispositivo

- [Roaming corporativo de configurações](active-directory-windows-enterprise-state-roaming-overview.md)

- [Configurar o Hello for Business](active-directory-azureadjoin-passport-deployment.md)


Este documento fornece orientação para solução de problemas sobre como tooresolve potenciais problemas. 


Para Windows 10 e Windows Server 2016, híbrido do Azure Active Directory junção dá suporte a saudação Windows 10 de novembro de 2015 atualizar e acima. Recomendamos o uso da atualização de aniversário hello.

## <a name="step-1-retrieve-hello-join-status"></a>Etapa 1: Recuperar o status de junção Olá 

**status de junção de saudação tooretrieve:**

1. Olá abrir o prompt de comando como administrador

2. Digite **dsregcmd /status**



    +----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+
    
        AzureAdJoined: YES
     EnterpriseJoined: Nenhum DeviceId: impressão digital de 5820fbe9-60c8-43b0-bb11-44aee233e4e7: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: TpmProtected de provedor de criptografia da plataforma Microsoft: Sim KeySignTest:: deve executar com privilégios elevados tootest.
                  Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO
    
    +----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+
    
                 NgcSet: YES
               NgcKeyId: {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined: NO
          WamDefaultSet: YES
    WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: YES



## <a name="step-2-evaluate-hello-join-status"></a>Etapa 2: Avaliar o status de junção Olá 

Examine Olá campos a seguir e certifique-se de que eles têm valores esperados de saudação:

### <a name="azureadjoined--yes"></a>AzureAdJoined : YES  

Este campo indica se o dispositivo de saudação é associado com o Azure AD. Se o valor de saudação é **não**, Olá tooAzure junção AD ainda não foi concluída. 

**Possíveis causas:**

- Falha na autenticação de computador Olá para uma junção.

- Há um proxy HTTP na organização Olá que não pode ser descoberta pelo computador Olá

- computador Olá não pode chegar tooauthenticate do AD do Azure ou Azure DRS para registro

- Olá computador podem não estar na rede interna da organização hello ou em VPN com a linha direta de visão tooan controlador de domínio do AD local.

- Se o computador de saudação tiver um TPM, ele pode ser em um estado inválido.

- Pode haver um erro de configuração nos serviços de saudação observado anteriormente no documento de saudação que você precisará tooverify novamente. Alguns exemplos comuns são:

    - O servidor de Federação não tem pontos de extremidade WS-Trust habilitados

    - O servidor de federação não permite a autenticação de entrada de computadores em sua rede usando a Autenticação Integrada do Windows.

    - Não há nenhum objeto de ponto de Conexão de serviço que aponta para o nome de domínio verificado tooyour no AD do Azure na floresta Olá AD qual pertence o computador de saudação

---

### <a name="domainjoined--yes"></a>DomainJoined : YES  

Este campo indica se o dispositivo Olá é associado tooan local do Active Directory ou não. Se o valor de saudação é **não**, dispositivo Olá não é possível executar uma junção híbrido do AD do Azure.  

---

### <a name="workplacejoined--no"></a>WorkplaceJoined : NO  

Este campo indica se o dispositivo hello está registrado com o Azure AD como um dispositivo pessoal (marcados como *ingressado no local de trabalho*). Esse valor deve ser **NO** para um computador ingressado no domínio, que também é ingressado no Azure AD híbrido. Se o valor de saudação é **Sim**, uma conta corporativa ou escolar foi adicionada conclusão toohello anterior de junção do hello híbrido do AD do Azure. Nesse caso, a conta de Olá é ignorada ao usar a versão de atualização de aniversário de saudação do Windows 10 (1607).

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a>WamDefaultSet : YES e AzureADPrt : YES
  
Esses campos indicam se o usuário Olá foi autenticado com êxito tooAzure AD ao entrarem no dispositivo toohello. Se os valores hello são **não**, ele pode ter ocorrido:

- Chave de armazenamento incorreta (STK) no TPM associado Olá dispositivo após o registro (seleção Olá KeySignTest durante a execução com privilégios elevados).

- ID de logon alternativo

- Proxy HTTP não encontrado

## <a name="next-steps"></a>Próximas etapas

Para perguntas, consulte Olá [perguntas frequentes sobre o gerenciamento de dispositivos](device-management-faq.md) 
