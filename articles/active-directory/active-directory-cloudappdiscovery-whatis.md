---
title: "aplicativos de nuvem com o Cloud App Discovery não gerenciado aaaFinding | Microsoft Docs"
description: "Fornece informações sobre como localizar e gerenciar aplicativos com o Cloud App Discovery, quais são os benefícios de saudação e como ele funciona."
services: active-directory
keywords: cloud app discovery, gerenciamento de aplicativos
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: db968bf5-22ae-489f-9c3e-14df6e1fef0a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 50c24af9bb400e4be11f4ad2d1de13d26f5467bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="finding-unmanaged-cloud-applications-with-cloud-app-discovery"></a>Encontrando aplicativos em nuvem não gerenciados com o Cloud App Discovery
## <a name="overview"></a>Visão geral
Nas empresas modernas, os departamentos de TI geralmente não estão cientes de todos os aplicativos de nuvem Olá que membros de sua organização usam toodo seu trabalho. É fácil toosee por que os administradores terão preocupações sobre dados de toocorporate de acesso não autorizado, perda de dados e outros riscos de segurança. Essa falta de reconhecimento pode fazer com que a criação de um plano para lidar com esses riscos de segurança pareça assustadora.

Cloud App Discovery é um recurso Premium do Azure AD (Active Directory) que permite que você toodiscover aplicativos em nuvem que estão sendo usados por pessoas de saudação em sua organização.

**Com o Cloud App Discovery é possível:**

* Localizar aplicativos em nuvem hello está sendo usados e que o uso de medidas por número de usuários, volume de tráfego ou número de solicitações toohello aplicativo.
* Identificar usuários Olá que estão usando um aplicativo.
* Exporte os dados para a análise offline.
* Coloque esses aplicativos sob controle da TI e habilite o logon único para o gerenciamento de usuário.

## <a name="how-it-works"></a>Como ele funciona
1. Os agentes de uso dos aplicativos são instalados nos computadores dos usuários.
2. informações de uso do aplicativo Hello capturadas por agentes de saudação são enviadas por um serviço do canal seguro, criptografado toohello cloud app discovery.
3. Olá serviço Cloud App Discovery avalia Olá dados e gera relatórios.

![Diagrama do Cloud App Discovery](./media/active-directory-cloudappdiscovery/cad01.png)

tooget Introdução ao Cloud App Discovery, consulte [guia de Introdução ao Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)

## <a name="related-articles"></a>Artigos relacionados
* [Considerações de privacidade e segurança no Cloud App Discovery](active-directory-cloudappdiscovery-security-and-privacy-considerations.md)  
* [Guia de Implantação da Política de Grupo do Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)
* [Guia de Implantação do System Center do Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)
* [Configurações de Registro do Cloud App Discovery para Servidores Proxy com Portas Personalizadas](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md)
* [Cloud App Discovery - Log de Alteração de Agente ](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx)
* [Cloud App Discovery - Perguntas Frequentes](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx)
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)

