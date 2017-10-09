---
title: aaaAzure AD + requisitos do Active Directory do Azure RemoteApp | Microsoft Docs
description: Saiba como tooset backup toowork do Active Directory com o Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 66366b25-6012-45fa-a4f6-da0ddfe0b486
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: c1c4a7ad6fb96ec4d479fdc231f03d81b58b2b71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad--active-directory-requirements-for-azure-remoteapp"></a>Requisitos do AD do Azure + Active Directory para o Azure RemoteApp
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Para sua coleção do RemoteApp híbrida ou para uma coleção de nuvem que você deseja toofederate usando AD Connect, é necessário a seguir Olá toodo.

### <a name="connect-azure-ad-and-active-directory"></a>Conecte o AD do Azure e o Active Directory
Se você quiser tooconnect seu locatário do AD do Azure e seus ambientes do Active Directory local, use AD Connect. Levará apenas [4 cliques](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) tooconnect Olá dois diretórios.

Observação - a sincronização de diretórios é necessária para coleções híbridas.

### <a name="make-sure-your-domaincom-match"></a>Certifique-se de que o "@domain.com" corresponda
Antes de começar, certifique-se que hello UPN para o sufixo de saudação do local floresta correspondências de seu domínio do AD do Azure. 

Depois de configurar o sufixo de domínio do UPN Olá no AD do Azure, todos os usuários que fizerem logon no Azure RemoteApp fará logon como "usuário @<hello suffix you set up>." Certifique-se de que os usuários podem também fazer logon com hello mesmo user@suffix no domínio local de saudação. Em alguns casos você pode configurar um nome de domínio no AD do Azure ao especificar um sufixo de domínio diferente para Olá usuário-local. Nesse caso, os usuários não será capaz de tooconnect tooany computadores do domínio ou os recursos por meio do Azure RemoteApp.

Por exemplo, se você configurar o sufixo de domínio do UPN no AAD como contoso.com, mas alguns usuários no local/AD toolog configurado com @contoso.uk, em seguida, os usuários não será capaz de toocorrectly log em Olá coleção ARA. Os usuários que deve ser UPN no AAD e AD hello mesmo para possíveis de toobe logon hello"

### <a name="create-objects-for-azure-remoteapp"></a>Criar objetos para o Azure RemoteApp
Você também precisa Olá toocreate objetos do Active Directory no local a seguir:

* Uma conta de serviço tooprovide acesso toodomain recursos para os programas RemoteApp unindo o domínio de local de toohello RDSH pontos de extremidade.
* Objetos de computador uma UO (unidade organizacional) toocontain RemoteApp. Uso de saudação UO é recomendado (mas não obrigatório) tooisolate Olá contas e políticas que você usará com o RemoteApp.

Você precisará de ambos esses objetos ao criar sua coleção do RemoteApp, portanto, ser toodo-se de que essas etapas primeiro.

