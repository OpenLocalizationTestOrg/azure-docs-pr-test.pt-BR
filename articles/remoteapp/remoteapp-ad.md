---
title: Requisitos do Azure AD + Active Directory para o Azure RemoteApp | Microsoft Docs
description: Saiba como configurar o Active Directory para trabalhar com o Azure RemoteApp.
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
ms.openlocfilehash: 78008a032faa93795cc02b720d68a0c6f5f16e9a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad--active-directory-requirements-for-azure-remoteapp"></a>Requisitos do AD do Azure + Active Directory para o Azure RemoteApp
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Leia o [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Para a coleção híbrida do Azure RemoteApp ou para uma coleção na nuvem que você deseja federar usando o AD Connect, você precisa fazer o seguinte:

### <a name="connect-azure-ad-and-active-directory"></a>Conecte o AD do Azure e o Active Directory
Se desejar conectar seu locatário do AD do Azure e seus ambientes locais do Active Directory, use o AD Connect. Levará apenas [quatro cliques](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) para conectar os dois diretórios.

Observação - a sincronização de diretórios é necessária para coleções híbridas.

### <a name="make-sure-your-domaincom-match"></a>Certifique-se de que o "@domain.com" corresponda
Antes de começar, lembre-se de que o UPN da floresta local corresponde ao sufixo do seu domínio do AD do Azure. 

Depois de configurar o sufixo de domínio UPN no Azure AD, todos os usuários que fizerem logon no Azure RemoteApp farão logon como "user@<the suffix you set up>". Certifique-se de que os usuários também podem fazer logon com o mesmo user@suffix no domínio local. Em alguns casos, é possível configurar um nome de domínio no AD do Azure, ao mesmo tempo que você especifica um sufixo de domínio diferente para o usuário local. Nesse caso, seus usuários não poderão se conectar a nenhum computador ou recurso ingressado no domínio por meio do Azure RemoteApp.

Por exemplo, se você configurar o sufixo de domínio UPN no AAD como contoso.com mas alguns usuários locais/no AD estiverem configurados para fazer logon em @contoso.uk, esses usuários não poderão fazer logon corretamente na coleção ARA. Os UPNs dos usuários no AAD e no AD devem ser iguais para que o logon seja possível.

### <a name="create-objects-for-azure-remoteapp"></a>Criar objetos para o Azure RemoteApp
Você também precisará criar os seguintes objetos locais do Active Directory:

* Uma conta de serviço para fornecer acesso aos recursos do domínio para programas RemoteApp unindo os pontos de extremidade RDSH ao domínio local.
* Uma OU (unidade organizacional) para conter objetos de computador do RemoteApp. Uso da OU é recomendável (mas não obrigatório) para isolar as contas e as políticas que você usará com o RemoteApp.

Você precisa desses dois objetos ao criar sua coleção do RemoteApp, portanto lembre-se de realizar essas etapas primeiro.

