---
title: "lista de compatibilidade de Federação aaaAzure AD"
description: "Esta página contém não Microsoft provedores de identidade que podem ser usado tooimplement o logon único."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 22c8693e-8915-446d-b383-27e9587988ec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: ac2f9ad324c8ca6b587b73ea465426ad6b074b03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-federation-compatibility-list"></a>Lista de compatibilidade de federação do AD do Azure
O Azure Active Directory fornece logon único e segurança aprimorada de acesso ao aplicativo para o Office 365 e outros serviços do Microsoft Online para implementações híbridas e apenas de nuvem, sem a necessidade de qualquer solução de terceiros. O Office 365, como a maioria dos serviços online da Microsoft, é integrado ao Azure Active Directory para autorização, autenticação e serviços de diretório. Active Directory do Azure também fornece toothousands de logon único de aplicativos SaaS e aplicativos da web local. Consulte a Galeria de aplicativos do Active Directory do Azure Olá para aplicativos SaaS com suporte.

Para organizações que investiram em soluções de Federação não Microsoft, este tópico contém orientações para configurar o logon único para seus usuários do Active Directory do Windows Server com o Microsoft Online services por meio de provedores de identidade de terceiros Olá "Azure Active Directory federation compatibilidade lista" abaixo. 

![](./media/active-directory-aadconnect-federation-compatibility/oxford2.jpg)   
O [Oxford Computer Group](http://oxfordcomputergroup.com/), um terceiro, em nome da Microsoft, testou essas experiências de logon único usando provedores de identidade de terceiros com base em um conjunto de casos de uso comuns com o Azure Active Directory.

Para obter informações sobre como você pode obter o provedor de identidade do terceiro listado aqui, contate o Oxford Computer Group em [idp@oxfordcomputergroup.com](mailto:idp@oxfordcomputergroup.com).

> [!IMPORTANT]
> Grupo de computadores Oxford testado somente Olá funcionalidade de Federação desses cenários de logon único. Grupo de computadores Oxford não executou os testes de sincronização hello, autenticação de dois fatores, componentes etc. esses cenários de logon único.
> 
> Uso de entrada por ID alternativa tooUPN também não é testado neste programa.
> 
> 

* [Active Directory do Azure](#azure-active-directory)
* [AuthAnvil Single Sign On 4.5](#authanvil-single-sign-on-45)
* [BIG-IP com Access Policy Manager BIG-IP ver. 11.3x – 11.6x](#big-ip-with-access-policy-manager-big-ip-ver-113x--116x) 
* [BitGlass](#bitglass)
* [CA Secure Cloud](#ca-secure-cloud) 
* [CA SiteMinder 12.52](#ca-siteminder-1252-sp1-cumulative-release-4) 
* [Centrify](#centrify) 
* [Dell One Identity Cloud Access Manager v7.1](#dell-one-identity-cloud-access-manager-v71) 
* [Autenticação de composição DigitalPersona](#digitalpersona-composite-authentication)
* [IBM Tivoli Federated Identity Manager 6.2.2](#ibm-tivoli-federated-identity-manager-622) 
* [IceWall Federation versão 3.0](#icewall-federation-version-30) 
* [Memority](#memority)
* [NetIQ Access Manager 4.x](#netiq-access-manager-4x) 
* [Okta](#okta) 
* [OneLogin](#onelogin) 
* [Optimal IDM Virtual Identity Server Federation Services](#optimal-idm-virtual-identity-server-federation-services) 
* [PingFederate 6.11, 7.2, 8.x](#pingfederate-611-72-8x)
* [RadiantOne CFS 3.0](#radiantone-cfs-30) 
* [Sailpoint IdentityNow](#sailpoint-identitynow)
* [SecureAuth IdP 7.2.0](#secureauth-idp-720) 
* [Sign&go 5.3](#signgo-53) 
* [SoftBank Technology Online Service Gate](#softbank)
* [VMware Workspace One](#vmware-workspace-one)



> [!IMPORTANT]
> Como eles são produtos de terceiros, Microsoft não oferece suporte para implantação de saudação, configuração, solução de problemas, práticas práticas recomendadas, etc. problemas e perguntas sobre esses provedores de identidade. Suporte e perguntas sobre esses provedores de identidade, entre em contato com terceiros Olá suportada diretamente.
> 
> Esses provedores de identidade de terceiros foram testados quanto à interoperabilidade com os serviços de nuvem da Microsoft usando apenas os protocolos WS-Federation e WS-Trust. Os testes não incluíram usando o protocolo do SAML hello.
> 


## <a name="azure-active-directory"></a>Azure Active Directory

seguir Olá é a matriz de suporte de cenário Olá para esta experiência de logon: 

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, como o Exchange Web Access e o SharePoint Online |Suportado |Nenhum |
| Aplicativos de cliente avançados como o Lync, a assinatura do Office, o CRM |Suportado |Nenhum |
| Clientes de email avançados, como o Outlook e o ActiveSync |Suportado |Nenhum |
| Aplicativos modernos com ADAL, como Office 2016 |Suportado |Nenhum |

Para saber mais sobre como usar o Azure Active Directory com o AD FS, consulte [Serviços de Federação do Active Directory (ADFS)](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs).

Para saber mais sobre como usar o Azure Active Directory com sincronização de senha, confira [Azure AD Connect](active-directory-aadconnect.md).

## <a name="authanvil-single-sign-on-45"></a>AuthAnvil Single Sign On 4.5

seguir Olá é a matriz de suporte de cenário Olá para esta experiência de logon único:

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, como o Exchange Web Access e o SharePoint Online |Suportado |Não há suporte para a Autenticação Integrada do Windows |
| Aplicativos de cliente avançados como o Lync, a assinatura do Office, o CRM |Suportado |Não há suporte para a Autenticação Integrada do Windows |
| Clientes de email avançados, como o Outlook e o ActiveSync |Suportado |Nenhum |

Para obter mais informações, consulte [Logon único do AuthAnvil](https://help.scorpionsoft.com/entries/26538603-How-can-I-Configure-Single-Sign-On-for-Office-365-).


## <a name="big-ip-with-access-policy-manager-big-ip-ver-113x--116x"></a>BIG-IP com Access Policy Manager BIG-IP ver. 11.3x – 11.6x

seguir Olá é a matriz de suporte de cenário Olá para esta experiência de logon único: 

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, como o Exchange Web Access e o SharePoint Online |Suportado |Nenhum |
| Aplicativos de cliente avançados como o Lync, a assinatura do Office, o CRM |Sem suporte |Sem suporte |
| Clientes de email avançados, como o Outlook e o ActiveSync |Suportado |Nenhum |

Para saber mais sobre o BIG-IP Access Policy Manager, confira [BIG-IP Access Policy Manager.](https://f5.com/products/modules/access-policy-manager) 

Para obter instruções Olá BIG-IP Access Policy Manager sobre como tooconfigure este tooyour de experiência de logon único do STS tooprovide Olá usuários do Active Directory, baixe Olá pdf [BIG-IP](http://www.f5.com/pdf/deployment-guides/microsoft-office-365-idp-dg.pdf).

## <a name="bitglass"></a>BitGlass

seguir Olá é a matriz de suporte de cenário Olá para esta experiência de logon único:

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, como o Exchange Web Access e o SharePoint Online |Suportado |Não há suporte para a Autenticação Integrada do Windows |
| Aplicativos de cliente avançados como o Lync, a assinatura do Office, o CRM |Suportado |Não há suporte para a Autenticação Integrada do Windows |
| Clientes de email avançados, como o Outlook e o ActiveSync |Suportado |Nenhum |

Para obter mais informações sobre o BitGlass, veja [BitGlass](http://www.bitglass.com).

## <a name="ca-secure-cloud"></a>CA Secure Cloud

seguir Olá é a matriz de suporte de cenário Olá para esta experiência de logon único:

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, como o Exchange Web Access e o SharePoint Online |Suportado |Não há suporte para a Autenticação Integrada do Windows |
| Aplicativos de cliente avançados como o Lync, a assinatura do Office, o CRM |Suportado |Não há suporte para a Autenticação Integrada do Windows |
| Clientes de email avançados, como o Outlook e o ActiveSync |Suportado |Nenhum |

Para saber mais sobre o CA Secure Cloud, confira [CA Secure Cloud](http://www.ca.com/us/products/security-as-a-service.aspx).

## <a name="ca-siteminder-1252-sp1-cumulative-release-4"></a>Versão cumulativa 4 do CA SiteMinder 12.52 SP1

seguir Olá é a matriz de suporte de cenário Olá para esta experiência de logon único: 

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, como o Exchange Web Access e o SharePoint Online |Suportado |Nenhum |
| Aplicativos de cliente avançados como o Lync, a assinatura do Office, o CRM |Suportado |Nenhum |
| Clientes de email avançados, como o Outlook e o ActiveSync |Suportado |Nenhum |

Para saber mais sobre o CA SiteMinder, confira [Federação do CA SiteMinder](http://www.ca.com/us/products/ca-single-sign-on.html). 

## <a name="centrify"></a>Centrify

seguir Olá é a matriz de suporte de cenário Olá para esta experiência de logon único:

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, como o Exchange Web Access e o SharePoint Online |Suportado |Nenhum |
| Aplicativos de cliente avançados como o Lync, a assinatura do Office, o CRM |Suportado |Nenhum |
| Clientes de email avançados, como o Outlook e o ActiveSync |Suportado |Não há suporte para o Controle de Acesso do cliente |

Para saber mais sobre o Centrify, consulte [Centrify](http://www.centrify.com/cloud/apps/single-sign-on-for-office-365.asp).

## <a name="dell-one-identity-cloud-access-manager-v71"></a>Dell One Identity Cloud Access Manager v7.1

seguir Olá é a matriz de suporte de cenário Olá para esta experiência de logon único:

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, como o Exchange Web Access e o SharePoint Online |Suportado |Nenhum |
| Aplicativos de cliente avançados como o Lync, a assinatura do Office, o CRM |Suportado |Nenhum |
| Clientes de email avançados, como o Outlook e o ActiveSync |Suportado |Nenhum |

Para obter mais informações sobre o Dell One Identity Cloud Access Manager, confira [Dell One Identity Cloud Access Manager](http://software.dell.com/products/cloud-access-manager).

 Para obter instruções de saudação sobre como tooconfigure este tooyour de experiência de logon único do STS tooprovide Olá usuários do Office 365, consulte [configurar usuários do Office 365](http://documents.software.dell.com/dell-one-identity-cloud-access-manager/7.1/how-to-configure-microsoft-office-365). 

## <a name="digitalpersona-composite-authentication"></a>Autenticação de composição DigitalPersona  

seguir Olá é a matriz de suporte de cenário Olá para esta experiência de logon único:

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, como o Exchange Web Access e o SharePoint Online |Suportado |Não há suporte para a Autenticação Integrada do Windows|
| Aplicativos de cliente avançados como o Lync, a assinatura do Office, o CRM |Suportado |Não há suporte para a Autenticação Integrada do Windows|
| Clientes de email avançados, como o Outlook e o ActiveSync |Suportado |Nenhum |

Para obter mais informações, consulte [Autenticação de composição DigitalPersona](http://www.crossmatch.com/uploadedFiles/Support/Reference_Material/DigitalPersona-Office-365-Deployment-Guide.pdf).


## <a name="ibm-tivoli-federated-identity-manager-622"></a>IBM Tivoli Federated Identity Manager 6.2.2

seguir Olá é a matriz de suporte de cenário Olá para esta experiência de logon único: 

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, como o Exchange Web Access e o SharePoint Online |Suportado |Nenhum |
| Aplicativos de cliente avançados como o Lync, a assinatura do Office, o CRM |Suportado |Nenhum |
| Clientes de email avançados, como o Outlook e o ActiveSync |Suportado |Nenhum |

Para saber mais sobre o IBM Tivoli Federated Identity Manager, confira [IBM Security Access Manager para Aplicativos Microsoft](http://www-01.ibm.com/support/docview.wss?uid=swg24029517).

## <a name="icewall-federation-version-30"></a>IceWall Federation versão 3.0

seguir Olá é a matriz de suporte de cenário Olá para esta experiência de logon único:

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, como o Exchange Web Access e o SharePoint Online |Suportado |Não há suporte para a Autenticação Integrada do Windows |
| Aplicativos de cliente avançados como o Lync, a assinatura do Office, o CRM |Suportado |Não há suporte para a Autenticação Integrada do Windows |
| Clientes de email avançados, como o Outlook e o ActiveSync |Suportado |Nenhum |

Para obter mais informações sobre o IceWall Federation, consulte [IceWall Federation versão 3.0](http://h50146.www5.hp.com/products/software/security/icewall/eng/federation/) e [IceWall Federation com Office 365](http://h50146.www5.hp.com/products/software/security/icewall/federation/office365.html).

## <a name="memority"></a>Memority

seguir Olá é a matriz de suporte de cenário Olá para esta experiência de logon: 

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, como o Exchange Web Access e o SharePoint Online |Suportado |Nenhum |
| Aplicativos de cliente avançados como o Lync, a assinatura do Office, o CRM |Suportado |Nenhum |
| Clientes de email avançados, como o Outlook e o ActiveSync |Suportado |Nenhum |

Para obter mais informações sobre o uso do Memority, consulte [Memority](http://www.memority.com).


## <a name="netiq-access-manager-4x"></a>NetIQ Access Manager 4.x

seguir Olá é a matriz de suporte de cenário Olá para esta experiência de logon único:

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, como o Exchange Web Access e o SharePoint Online |Suportado |Nenhum|
| Aplicativos de cliente avançados como o Lync, a assinatura do Office, o CRM |Suportado |Nenhum|
| Clientes de email avançados, como o Outlook e o ActiveSync |Suportado |Nenhum |

Para obter mais informações, consulte [NetIQ Access Manager](https://www.netiq.com/documentation/access-manager-43/admin/data/b65ogn0.html#b12iqp0m).

## <a name="okta"></a>Okta

seguir Olá é a matriz de suporte de cenário Olá para esta experiência de logon único: 

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, como o Exchange Web Access e o SharePoint Online |Suportado |A Autenticação Integrada do Windows exige a instalação de um servidor Web adicional e do aplicativo Okta. |
| Aplicativos de cliente avançados como o Lync, a assinatura do Office, o CRM |Suportado |Autenticação Integrada do Windows |
| Clientes de email avançados, como o Outlook e o ActiveSync |Suportado |Nenhum |

Para saber mais sobre o Okta, confira [Okta](https://www.okta.com/).

## <a name="onelogin"></a>OneLogin

seguir Olá é a matriz de suporte de cenário Olá para esta experiência de logon único: 

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, como o Exchange Web Access e o SharePoint Online |Suportado |Autenticação Integrada do Windows |
| Aplicativos de cliente avançados como o Lync, a assinatura do Office, o CRM |Suportado |Autenticação Integrada do Windows |
| Clientes de email avançados, como o Outlook e o ActiveSync |Suportado |Nenhum |

Para saber mais sobre o OneLogin, confira [OneLogin](https://www.onelogin.com/).

## <a name="optimal-idm-virtual-identity-server-federation-services"></a>Optimal IDM Virtual Identity Server Federation Services

a seguir Olá é Olá matriz de suporte do cenário desta experiência de logon único:

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, como o Exchange Web Access e o SharePoint Online |Suportado |Nenhum |
| Aplicativos de cliente avançados como o Lync, a assinatura do Office, o CRM |Suportado |Autenticação Integrada do Windows |
| Clientes de email avançados, como o Outlook e o ActiveSync |Suportado |

Para obter mais informações sobre o cliente veja de políticas de acesso [tooOffice limitando o acesso 365 serviços com base em Olá local da saudação cliente](https://technet.microsoft.com/library/hh526961.aspx).





## <a name="pingfederate-611-72-8x"></a>PingFederate 6.11, 7.2, 8.x

seguir Olá é a matriz de suporte de cenário Olá para esta experiência de logon único:

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, como o Exchange Web Access e o SharePoint Online |Suportado |Nenhum |
| Aplicativos de cliente avançados como o Lync, a assinatura do Office, o CRM |Suportado |Nenhum |
| Clientes de email avançados, como o Outlook e o ActiveSync |Suportado |Nenhum |

Para obter instruções sobre como tooconfigure esse STS tooprovide Olá único experiência de logon PingFederate Olá tooyour usuários do Active Directory, consulte um dos seguintes hello: 

- [PingFederate 6.11](http://go.microsoft.com/fwlink/?LinkID=266321)
- [PingFederate 7.2](http://documentation.pingidentity.com/display/PF72/PingFederate+7.2)
- [PingFederate 8.x](http://documentation.pingidentity.com/display/PFS/SSO+to+Office+365+Introduction)

## <a name="radiantone-cfs-30"></a>RadiantOne CFS 3.0

seguir Olá é a matriz de suporte de cenário Olá para esta experiência de logon único: 

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, como o Exchange Web Access e o SharePoint Online |Suportado |Nenhum |
| Aplicativos de cliente avançados como o Lync, a assinatura do Office, o CRM |Suportado |Autenticação Integrada do Windows |
| Clientes de email avançados, como o Outlook e o ActiveSync |Suportado |Nenhum |

Para saber mais sobre o RadiantOne CFS, confira [RadiantOne CFS](http://www.radiantlogic.com/products/radiantone-cfs/).

## <a name="sailpoint-identitynow"></a>Sailpoint IdentityNow

seguir Olá é a matriz de suporte de cenário Olá para esta experiência de logon único:

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, como o Exchange Web Access e o SharePoint Online |Suportado |Não há suporte para a Autenticação Integrada do Windows |
| Aplicativos de cliente avançados como o Lync, a assinatura do Office, o CRM |Suportado |Não há suporte para a Autenticação Integrada do Windows |
| Clientes de email avançados, como o Outlook e o ActiveSync |Suportado |Nenhum |

Para saber mais, confira [Sailpoint IdentityNow](https://www.sailpoint.com/idaas-identity-as-a-service-identitynow/).

## <a name="secureauth-idp-720"></a>SecureAuth IdP 7.2.0

seguir Olá é a matriz de suporte de cenário Olá para esta experiência de logon único: 

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, como o Exchange Web Access e o SharePoint Online |Suportado |Nenhum |
| Aplicativos de cliente avançados como o Lync, a assinatura do Office, o CRM |Suportado |Nenhum |
| Clientes de email avançados, como o Outlook e o ActiveSync |Suportado |Nenhum |

Para saber mais sobre o SecureAuth, confira [SecureAuth IdP](http://go.microsoft.com/?linkid=9845293).














## <a name="signgo-53"></a>Sign&go 5.3

seguir Olá é a matriz de suporte de cenário Olá para esta experiência de logon único:

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, como o Exchange Web Access e o SharePoint Online |Suportado |Contratos Kerberos com suporte |
| Aplicativos de cliente avançados como o Lync, a assinatura do Office, o CRM |Suportado |Nenhum |
| Clientes de email avançados, como o Outlook e o ActiveSync |Suportado |Nenhum |

O Sign&go 5.3 oferece suporte à autenticação Kerberos por meio da configuração de um Kerberos Contract.  Para obter assistência com essa configuração, entre em contato com Ilex ou exibição de guia de instalação Olá [Sign & go](http://www.ilex-international.com/docs/sign&go_wsfederation_en.pdf)

## <a name="softbank-technology-online-service-gate"></a>SoftBank Technology Online Service Gate

seguir Olá é a matriz de suporte de cenário Olá para esta experiência de logon único:

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, como o Exchange Web Access e o SharePoint Online |Suportado |Não há suporte para a Autenticação Integrada do Windows |
| Aplicativos de cliente avançados como o Lync, a assinatura do Office, o CRM |Suportado |Não há suporte para a Autenticação Integrada do Windows |
| Clientes de email avançados, como o Outlook e o ActiveSync |Suportado |Nenhum |

Para obter mais informações sobre o SoftBank Technology Online Service Gate, consulte [Softbank](https://www.softbanktech.jp/service/list/osg-pro-ent/)

## <a name="vmware-workspace-one"></a>VMware Workspace One

seguir Olá é a matriz de suporte de cenário Olá para esta experiência de logon único:

| Cliente | Suporte | Exceções |
| --- | --- | --- |
| Clientes baseados na Web, como o Exchange Web Access e o SharePoint Online |Suportado |Não há suporte para a Autenticação Integrada do Windows |
| Aplicativos de cliente avançados como o Lync, a assinatura do Office, o CRM |Suportado |Não há suporte para a Autenticação Integrada do Windows |
| Clientes de email avançados, como o Outlook e o ActiveSync |Suportado |Nenhum |

Para obter mais informações, consulte [VMware Workspace One](http://www.vmware.com/pdf/vidm-office365-saml.pdf)

