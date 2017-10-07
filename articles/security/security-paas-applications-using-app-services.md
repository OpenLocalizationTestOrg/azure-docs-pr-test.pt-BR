---
title: "aaaSecuring PaaS aplicativos web e móveis usando os serviços de aplicativo do Azure | Microsoft Docs"
description: " Saiba mais sobre os Serviços de Aplicativos do Azure e as melhores práticas de segurança para proteger aplicativos Web e móveis de PaaS. "
services: security
documentationcenter: na
author: techlake
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: terrylan
ms.openlocfilehash: 68a741c668efe2157cff114b649e0e287ef196f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-web-and-mobile-applications-using-azure-app-services"></a>Proteção dos aplicativos Web e móveis de PaaS usando os Serviços de Aplicativo do Azure

Neste artigo, discutiremos um conjunto de práticas recomendadas de segurança dos [Serviços de Aplicativo do Azure ](https://azure.microsoft.com/services/app-service/) para proteger seus aplicativos móveis e Web de PaaS. Essas práticas recomendadas são derivadas da nossa experiência com o Azure e experiências de saudação de clientes, como por conta própria.

## <a name="azure-app-services"></a>Serviços de Aplicativo do Azure
[Serviços de aplicativo do Azure](../app-service/app-service-value-prop-what-is.md) é uma oferta de PaaS que permite criar aplicativos web e móveis para qualquer plataforma ou dispositivo e conecte-se toodata em qualquer lugar, em nuvem hello ou local. Serviços de aplicativos inclui Olá web e móveis recursos que foram anteriormente entregues separadamente, como sites do Azure e serviços móveis do Azure. Ele também inclui novos recursos para automatizar processos empresariais e hospedagem de APIs de nuvem. Como um único serviço integrado, serviços de aplicativos oferece um conjunto avançado de recursos tooweb, móveis e integração de cenários.

toolearn mais, consulte visões gerais sobre [aplicativos móveis](../app-service-mobile/app-service-mobile-value-prop.md) e [aplicativos Web](../app-service-web/app-service-web-overview.md).

## <a name="best-practices"></a>Práticas recomendadas

Ao usar os Serviços de Aplicativo, siga estas práticas recomendadas:

- [Autenticar por meio do Azure Active Directory (AD)](../app-service-web/web-sites-authentication-authorization.md#authenticate-through-azure-active-directory). Os Serviços de Aplicativo fornecem um serviço OAuth 2.0 para seu provedor de identidade. O OAuth 2.0 se concentra na simplicidade de desenvolvedor do cliente, fornecendo fluxos de autorização específicos para aplicativos Web, aplicativos da área de trabalho e telefones celulares. AD do Azure usa OAuth 2.0 tooenable você tooauthorize acesso toomobile e aplicativos web.
- Restringir o acesso com base em Olá necessidade tooknow e princípios de segurança de privilégio mínimo. Restringir o acesso é fundamental para as organizações que desejam tooenforce políticas de segurança para acesso a dados. Controle de acesso baseado em função (RBAC) pode ser usado tooassign permissões toousers, grupos e aplicativos em um determinado escopo. toolearn mais sobre como conceder acessam a usuários tooapplications, consulte [Introdução ao gerenciamento de acesso](../active-directory/role-based-access-control-what-is.md).
- Proteja seus dados. Não importa a qualidade de sua segurança se você perder suas chaves de assinatura. O Cofre da Chave do Azure ajuda a proteger chaves criptográficas e segredos usados por aplicativos e serviços em nuvem. Usando o Cofre de Chaves, você pode criptografar chaves e segredos (como chaves de autenticação, chaves de conta de armazenamento, chaves de criptografia de dados, arquivos .PFX e senhas) usando chaves que são protegidas por HSMs (módulos de segurança de hardware). Para garantia extra, você pode importar ou gerar chaves em HSMs. Consulte [Azure Key Vault](../key-vault/key-vault-whatis.md) toolearn mais. Você também pode usar o Cofre de chaves toomanage seus certificados TLS com renovação automática.
- Restrinja os endereços IP de origem de entrada. O [Ambiente de Serviços de Aplicativos](../app-service-web/app-service-app-service-environment-intro.md) tem um recurso de integração de rede virtual que ajuda a restringir endereços IP de origem de entrada por meio dos NSGs (Grupos de Segurança de Rede). Se você estiver familiarizado com redes virtuais do Azure (VNETs), esse é um recurso que permite que você tooplace muitos dos recursos do Azure em uma rede roteável de não-internet que você controlar o acessem. mais, consulte toolearn [integrar seu aplicativo com uma rede Virtual do Azure](../app-service-web/web-sites-integrate-with-vnet.md).

## <a name="next-steps"></a>Próximas etapas
Este artigo introduzido coleção tooa das práticas recomendadas de segurança de serviços de aplicativos para proteger seu PaaS aplicativos web e móveis. toolearn mais sobre como proteger suas implantações de PaaS, consulte:

- [Proteção das implantações PaaS](security-paas-deployments.md)
- [Proteção de aplicativos Web e móveis de PaaS usando o Banco de Dados SQL do Azure e o SQL Data Warehouse](security-paas-applications-using-sql.md)
