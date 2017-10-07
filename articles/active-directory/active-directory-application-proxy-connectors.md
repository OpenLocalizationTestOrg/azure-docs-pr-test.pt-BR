---
title: conectores de Proxy de aplicativo do AD do Azure portais aaaClassic | Microsoft Docs
description: Aborda como toocreate e gerenciar grupos de conectores no Proxy de aplicativo do Azure AD.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b283796a-9679-4c79-b703-802bb850f65d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 43559b0f4ffc3c7dbbf00901e89ac276d01796e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a>Publicar aplicativos em redes e locais separados usando grupos de conectores
> [!div class="op_single_selector"]
> * [Portal do Azure](active-directory-application-proxy-connectors-azure-portal.md)
> * [Portal clássico do Azure](active-directory-application-proxy-connectors.md)
>
>

Os grupos de conectores são úteis para diversos cenários, incluindo:

* Sites com vários datacenters interconectados. Nesse caso, você deseja tookeep como a quantidade de tráfego dentro do datacenter Olá possível porque os links entre data centers são caros e lentos. Você pode implantar conectores em cada datacenter tooserve somente Olá aplicativos que residem dentro do datacenter hello. Essa abordagem minimiza os links entre data centers e fornece uma experiência totalmente transparente tooyour usuários.
* Gerenciamento de aplicativos instalados em redes isoladas que não fazem parte da rede corporativa principal de saudação. É possível usar conectores de tooinstall dedicado de grupos de conector em redes isoladas tooalso isolar aplicativos toohello de rede.
* Para aplicativos instalados para o acesso à nuvem IaaS, grupos de conector fornecem um comuns toosecure Olá acesso tooall Olá os aplicativos de serviço. Grupos de conector não criar dependências adicionais em sua rede corporativa ou fragmento de experiência de saudação do aplicativo. Conectores podem ser instalados em cada datacenter na nuvem e servir apenas os aplicativos que residem nessa rede. Você pode instalar vários conectores tooachieve alta disponibilidade.
* Suporte para ambientes de várias florestas em que os conectores específicos podem ser implantados por floresta e definir aplicativos específicos tooserve.
* Grupos de conector podem ser usados em sites de recuperação de desastres tooeither detectar failover ou como backup para Olá principal site.
* Grupos de conector também podem ser usado tooserve várias empresas de um único locatário.

## <a name="prerequisite-create-your-connectors"></a>Pré-requisito: criar seus conectores
toogroup seus conectores, [instalar vários conectores](active-directory-application-proxy-enable.md), em seguida, nome e agrupá-los. Finalmente tiver tooassign-los toospecific aplicativos.

## <a name="step-1-create-connector-groups"></a>Etapa 1: Criar grupos de conectores
Você pode criar quantos grupos de conectores desejar. Criação de grupo do conector é realizada em Olá portal clássico do Azure.

1. Escolha o diretório e clique em **Configurar**.  
    ![Captura de tela da configuração do proxy de aplicativo - clique em gerenciar grupos de conectores](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)
2. Em Proxy de aplicativo, clique em **gerenciar grupos de conector** e criar um grupo, fornecendo um nome de grupo hello.  
    ![Captura de tela dos grupos de conectores do proxy de aplicativo - nomeie o novo grupo](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)

## <a name="step-2-assign-connectors-tooyour-groups"></a>Etapa 2: Atribuir conectores tooyour grupos
Após a criação de grupos de conector Olá, mova o grupo apropriado do hello conectores toohello.

1. Em **Proxy de Aplicativo**, clique em **Gerenciar Conectores**.
2. Em **grupo**, selecione grupo Olá desejado para cada conector. Pode levar conectores Olá backup too10 minutos toobecome ativos no novo grupo de saudação.  
    ![Captura de tela dos conectores do proxy de aplicativo - selecione o grupo no menu suspenso](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)

## <a name="step-3-assign-applications-tooyour-connector-groups"></a>Etapa 3: Atribuir grupos de conector tooyour de aplicativos
última etapa de saudação é tooset cada grupo de conector toohello de aplicativos que atende.

1. Em Olá portal clássico do Azure, em seu diretório, selecione Olá aplicativo deseja tooassign toohello grupo e clique em **configurar**.
2. Em **grupo**, selecione grupo Olá deseja Olá toouse de aplicativo. A alteração é aplicada imediatamente.  
    ![Captura de tela do grupo de conectores do proxy de aplicativo - selecione o grupo no menu suspenso](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)

## <a name="see-also"></a>Confira também
* [Habilitar Proxy de aplicativo](active-directory-application-proxy-enable.md)
* [Habilitar o logon único](active-directory-application-proxy-sso-using-kcd.md)
* [Habilitar o acesso condicional](active-directory-application-proxy-conditional-access.md)
* [Solucionar problemas que surgirem com o Proxy de Aplicativo](active-directory-application-proxy-troubleshoot.md)

Para Olá últimas notícias e atualizações, confira Olá [blog de Proxy de aplicativo](http://blogs.technet.com/b/applicationproxyblog/)
