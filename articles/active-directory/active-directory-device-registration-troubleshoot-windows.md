---
title: "aaaTroubleshooting Olá o registro automático de domínio do AD do Azure em computadores ingressados para Windows 10 e Windows Server 2016 | Microsoft Docs"
description: "Solucionando problemas de registro automático de saudação do domínio do AD do Azure em computadores ingressados para Windows 10 e Windows Server 2016."
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
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 3795323ce9392368b412b3e1208868431e59a74b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad--windows-10-and-windows-server-2016"></a>Solucionando problemas de registro automático de domínio Unido computadores tooAzure AD – Windows 10 e Windows Server 2016

Este tópico é aplicável toohello clientes a seguir:

-   Windows 10
-   Windows Server 2016

Para outros clientes do Windows, consulte [Solucionando problemas de registro automático de domínio Unido computadores tooAzure AD para clientes de nível inferior do Windows](active-directory-device-registration-troubleshoot-windows-legacy.md).

Este tópico pressupõe que você tenha configurado o registro automático de dispositivos que ingressaram no domínio conforme descrito em descrito em [como tooconfigure o registro automático do Windows ingressado no domínio dispositivos com o Active Directory do Azure](active-directory-device-registration-get-started.md) Olá toosupport os seguintes cenários:

- [Acesso condicional com base em dispositivo](active-directory-conditional-access-automatic-device-registration-setup.md)

- [Roaming corporativo de configurações](active-directory-windows-enterprise-state-roaming-overview.md)

- [Configurar o Hello for Business](active-directory-azureadjoin-passport-deployment.md)


Este documento fornece orientação para solução de problemas sobre como tooresolve potenciais problemas. 

Olá registro tem suporte no Windows hello atualização 10 de novembro de 2015 e superior.  
É recomendável usar saudação da atualização de aniversário para habilitar cenários de saudação acima.

## <a name="step-1-retrieve-hello-registration-status"></a>Etapa 1: Recuperar o status de registro de saudação 

**status do registro Olá tooretrieve:**

1. Olá abrir o prompt de comando como administrador.

2. Digite **dsregcmd /status**



    +----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+
    
        AzureAdJoined : YES
     EnterpriseJoined: Nenhum DeviceId: impressão digital de 5820fbe9-60c8-43b0-bb11-44aee233e4e7: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: TpmProtected de provedor de criptografia da plataforma Microsoft: Sim KeySignTest:: deve executar com privilégios elevados tootest.
                  Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO
    
    +----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+
    
                 NgcSet : YES
               NgcKeyId : {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined : NO
          WamDefaultSet : YES
    WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES



## <a name="step-2-evaluate-hello-registration-status"></a>Etapa 2: Avaliar o status de registro de saudação 

Examine Olá campos a seguir e certifique-se de que eles têm valores esperados de saudação:

### <a name="azureadjoined--yes"></a>AzureAdJoined : YES  

Este campo mostra se o dispositivo de saudação é registrado no AD do Azure. Se o valor de saudação mostra como 'Não', o registro não foi concluída. 

**Possíveis causas:**

- Falha na autenticação de computador Olá para o registro.

- Há um proxy HTTP na organização Olá que não pode ser descoberta pelo computador Olá

- computador Olá não pode chegar Azure AD para autenticação ou do Azure DRS para registro

- Olá computador podem não estar na rede interna da organização hello ou em VPN com a linha direta de visão tooan controlador de domínio do AD local.

- Se o computador Olá tem um TPM, é possível em um estado inválido.

- Pode haver um erro de configuração nos serviços observado anteriormente no documento de saudação que você precisará tooverify novamente. Alguns exemplos comuns são:

    - O servidor de Federação não tem pontos de extremidade WS-Trust habilitados

    - O servidor de federação pode não permitir a autenticação de entrada de computadores na rede usando a Autenticação Integrada do Windows.

    - Não há nenhum objeto de ponto de Conexão de serviço que aponta para o nome de domínio verificado tooyour no AD do Azure na floresta Olá AD qual pertence o computador de saudação

---

### <a name="domainjoined--yes"></a>DomainJoined : YES  

Este campo mostra se o dispositivo Olá é tooan ingressado no Active Directory local ou não. Se o valor de saudação mostra como **não**, dispositivo Olá não é automaticamente o registro com o Azure AD. Verifique primeiro toohello de associações de dispositivo que Olá local do Active Directory para que ele possa registrar com o Azure AD. Se você estiver procurando unindo Olá computador tooAzure AD diretamente, vá tooLearn sobre recursos de junção do Azure Active Directory.

---

### <a name="workplacejoined--no"></a>WorkplaceJoined : NO  

Este campo mostra se o dispositivo de saudação está registrado com o AD do Azure, mas como um dispositivo pessoal (marcado como 'Ingressou no local de trabalho'). Se esse valor deve aparecer como 'Não' para um computador ingressado no domínio registrado com o Azure AD, porém se ele mostra como Sim, isso significa que uma conta corporativa ou escolar foi concluído o registro do computador adicionado toohello anterior. Nesse caso a conta de saudação será ignorada se usando a versão de atualização de aniversário de saudação do Windows 10 (1607 quando executar comando de WinVer Olá em Olá janela 'Executar' ou em uma janela de prompt de comando).

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a>WamDefaultSet : YES e AzureADPrt : YES
  
Esses campos mostram que o usuário Olá foi autenticado com êxito tooAzure AD ao fazer logon no dispositivo toohello. Se elas mostram 'Nenhum' hello seguem as possíveis causas:

- Chave de armazenamento incorreta (STK) no TPM associado Olá dispositivo após o registro (seleção Olá KeySignTest durante a execução com privilégios elevados).

- ID de logon alternativo

- Proxy HTTP não encontrado

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações, consulte Olá [perguntas frequentes sobre o registro de dispositivo automático](active-directory-device-registration-faq.md) 
