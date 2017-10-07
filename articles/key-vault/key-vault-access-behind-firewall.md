---
title: "Cofre de chaves de aaaAccess atrás de um firewall | Microsoft Docs"
description: Saiba como tooaccess chave do Azure Cofre de um aplicativo protegido por um firewall
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 50d21774-2ee1-4212-8995-570c9de603c5
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: ambapat
ms.openlocfilehash: ab4bb0c27a41fef878a20dace6cab203df04e579
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="access-azure-key-vault-behind-a-firewall"></a>Acessar o Cofre de Chaves do Azure por trás de um firewall
### <a name="q-my-key-vault-client-application-needs-toobe-behind-a-firewall-what-ports-hosts-or-ip-addresses-should-i-open-tooenable-access-tooa-key-vault"></a>P: o aplicativo de cliente do Cofre de chaves precisa toobe atrás de um firewall. Quais portas, hosts ou endereços IP deve abrir Cofre de chaves acesso tooa tooenable?
tooaccess um cofre de chaves, o aplicativo de cliente do Cofre de chaves tem a tooaccess vários pontos de extremidade para várias funcionalidades:

* Autenticação via Azure AD (Azure Active Directory)
* Gerenciamento do Cofre de Chaves do Azure. Isso inclui criar, ler, atualizar, excluir e definir políticas de acesso por meio do Azure Resource Manager.
* Acessar e gerenciar objetos (chaves e segredos) armazenados no cofre de chaves em si, passando por Olá ponto de extremidade específico de Cofre de chave (por exemplo, [https://yourvaultname.vault.azure.net](https://yourvaultname.vault.azure.net)).  

Dependendo do ambiente e configuração, há algumas variações.   

## <a name="ports"></a>Portas
Todos os tráfego tooa Cofre de chaves para todas as três funções (acesso de plano de dados, gerenciamento e autenticação) vai via HTTPS: porta 443. No entanto, ocasionalmente, haverá tráfego HTTP (porta 80) para CRL. Os clientes que dão suporte a OCSP não devem chegar a CRL, mas ocasionalmente podem chegar a [http://cdp1.public-trust.com/CRL/Omniroot2025.crl](http://cdp1.public-trust.com/CRL/Omniroot2025.crl).  

## <a name="authentication"></a>Autenticação
Aplicativos de cliente do Cofre de chaves precisará tooaccess pontos de extremidade do Azure Active Directory para autenticação. ponto de extremidade de saudação usado depende de Olá configuração de locatário do AD do Azure, o tipo de saudação do principal (UPN ou entidade de serviço) e hello tipo de conta – por exemplo, uma conta da Microsoft ou um trabalho ou conta escolar.  

| Tipo de entidade | Ponto de extremidade:porta |
| --- | --- |
| Usuário usando a conta da Microsoft<br> (por exemplo, user@hotmail.com) |**Global:**<br> login.microsoftonline.com:443<br><br> **Azure China:**<br> login.chinacloudapi.cn:443<br><br>**Azure Governo dos EUA:**<br> login-us.microsoftonline.com:443<br><br>**Azure Alemanha:**<br> login.microsoftonline.de:443<br><br> e <br>login.live.com:443 |
| Usuário ou entidade de serviço usando uma conta corporativa ou de Estudante com o Azure AD (por exemplo, user@contoso.com) |**Global:**<br> login.microsoftonline.com:443<br><br> **Azure China:**<br> login.chinacloudapi.cn:443<br><br>**Azure Governo dos EUA:**<br> login-us.microsoftonline.com:443<br><br>**Azure Alemanha:**<br> login.microsoftonline.de:443 |
| Usuário ou entidade de serviço usando um trabalho ou conta de estudante, além de serviços de Federação do Active Directory (AD FS) ou outro ponto de extremidade federado (por exemplo, user@contoso.com) |Todos os pontos de extremidade de uma conta corporativa ou de estudante, além do AD FS ou outros pontos de extremidade federados |

Há outros cenários complexos possíveis. Consulte também[fluxo do Azure Active Directory autenticação](/documentation/articles/active-directory-authentication-scenarios/), [integrando aplicativos com o Active Directory do Azure](/documentation/articles/active-directory-integrating-applications/), e [protocolos de autenticação do Active Directory](https://msdn.microsoft.com/library/azure/dn151124.aspx) Para obter informações adicionais.  

## <a name="key-vault-management"></a>Gerenciamento do Cofre de Chaves
Para o gerenciamento de Cofre de chaves (CRUD e configuração de política de acesso), o aplicativo de cliente do Cofre de chaves de saudação precisa tooaccess um ponto de extremidade do Gerenciador de recursos do Azure.  

| Tipo de operação | Ponto de extremidade:porta |
| --- | --- |
| Operações do plano de controle do cofre de chaves<br> por meio do Azure Resource Manager |**Global:**<br> management.azure.com:443<br><br> **Azure China:**<br> management.chinacloudapi.cn:443<br><br> **Azure Governo dos EUA:**<br> management.usgovcloudapi.net:443<br><br> **Azure Alemanha:**<br> management.microsoftazure.de:443 |
| Graph API do Active Directory do Azure |**Global:**<br> graph.windows.net:443<br><br> **Azure China:**<br> graph.chinacloudapi.cn:443<br><br> **Azure Governo dos EUA:**<br> graph.windows.net:443<br><br> **Azure Alemanha:**<br> graph.cloudapi.de:443 |

## <a name="key-vault-operations"></a>Operações do cofre de chaves
Para todas as operações de criptografia e gerenciamento de Cofre de chaves de objeto (chaves e segredos), o cliente do Cofre de chaves de saudação precisa ponto de extremidade do tooaccess Olá Cofre de chaves. sufixo DNS do ponto de extremidade Olá varia dependendo do local de saudação do seu Cofre de chaves. o ponto de extremidade do Hello Cofre de chaves está em formato de saudação *nome do cofre*. *região---o sufixo dns específico*, conforme descrito em Olá a tabela a seguir.  

| Tipo de operação | Ponto de extremidade:porta |
| --- | --- |
| Operações, incluindo operações criptográficas em chaves; criar, ler, atualizar e excluir chaves e segredos; definir ou obter marcas e outros atributos em objetos de cofre de chaves (chaves ou segredos) |**Global:**<br> &lt;vault-name&gt;.vault.azure.net:443<br><br> **Azure China:**<br> &lt;vault-name&gt;.vault.azure.cn:443<br><br> **Azure Governo dos EUA:**<br> &lt;vault-name&gt;.vault.usgovcloudapi.net:443<br><br> **Azure Alemanha:**<br> &lt;vault-name&gt;.vault.microsoftazure.de:443 |

## <a name="ip-address-ranges"></a>Intervalos de endereços IP
Olá serviço de Cofre de chaves usa outros recursos do Azure como a infraestrutura de PaaS. Portanto, não é possível tooprovide um específico intervalo de endereços IP que o Cofre de chaves terão pontos de extremidade de serviço a qualquer momento determinado. Se o firewall oferece suporte a apenas os intervalos de endereços IP, consulte toohello [intervalos de IP de Datacenter do Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653) documento. Autenticação e identidade (Active Directory do Azure), seu aplicativo deve ser capaz de tooconnect toohello pontos de extremidade descritos em [endereços de autenticação e identidade](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

## <a name="next-steps"></a>Próximas etapas
Se você tiver dúvidas sobre o Cofre de chaves, visite Olá [fóruns do Azure Key Vault](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).

