---
title: "tipo de aaaWhat de coleção que você precisa para o Azure RemoteApp? | Microsoft Docs"
description: "Saiba mais sobre os tipos de saudação de coleções disponíveis com o Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: c13ec78d-07e9-4646-8194-cf3efafc1760
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: f00b5fe41af597cf75e26300bf7842c3a8ff94fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-kind-of-collection-do-you-need-for-azure-remoteapp"></a>Que tipo de coleção é necessária para o Azure RemoteApp?
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

O Azure RemoteApp permite que você compartilhe aplicativos e recursos com usuários em qualquer dispositivo. Podemos fazer isso criando coleções toohold Olá aplicativos e recursos e, em seguida, compartilhar essas coleções com usuários. Há duas opções diferentes de coleção, com opções de rede e de autenticação – qual é a ideal para você?

Vamos examinar considerações diferentes Olá e opções que você toomake tooget hello mais precisa fora de sua coleção do RemoteApp. 

## <a name="quick-differences-between-hello-collection-types"></a>Rápido diferenças entre tipos de coleção Olá
|  | Nuvem | Híbrido |
| --- | --- | --- |
| Usa uma VNET existente |Sim |Sim |
| Requer contas conectadas ao AD (DirSync) |Não |Sim |
| Requer o ingresso no domínio |Não |Sim |
| Requer tooVNET acessível do controlador de domínio |Não |Sim |

## <a name="cloud-collections"></a>Coleções na nuvem
* Toocreate rápido - coleção Olá rapidamente é fornecida, que significa que seus aplicativos obtém toousers mais rápido.
* Traga seus próprios aplicativos ou compartilhe os nossos. Você pode usar uma imagem personalizada (criado a partir de uma VM do Azure) ou uma das imagens de saudação incluídas com sua assinatura.
* Você não precisa tooconfigure uma conexão entre seu domínio local e de sua coleção.
* Mas você também pode usar o acesso de tooprovide sua própria rede virtual do Azure em seu ambiente local de compartilhamento ou toouse não-Windows para autenticação de dados em recursos como o SQL Server (usando a autenticação do banco de dados).

OK, como posso criar uma?

* Somente nuvem? Criar com hello **criação rápida** opção no portal de saudação.
* Nuvem + VNET? Criar usando Olá **criar com uma rede virtual** opção mas não escolha toojoin um domínio.

## <a name="hybrid-collections"></a>Coleções híbridas
* Fornece acesso completo a rede de local tooon + VNET do Azure.
* Inclui o acesso ao ingresso no domínio para aplicativos e dados. Os aplicativos remotos podem fazer a autenticação em seu Active Directory local – em seguida, eles poderão acessar os recursos em seu domínio.
* Habilitar o monitoramento e gerenciamento avançados com soluções existentes do System Center e Políticas de Grupo do Windows (por meio de uma imagem personalizada criada no Windows Server 2012 R2)
* Suporte [ExpressRoute](https://azure.microsoft.com/services/expressroute/) tooconnect tooyour sua rede virtual do Azure redes locais.

Criar usando Olá **criar com uma rede virtual** opção e escolha toojoin um domínio.

## <a name="authentication-options"></a>Opções de autenticação
O Azure RemoteApp dá suporte a contas da Microsoft e a contas do Active Directory do Azure, mas nem todas as coleções dão suporte a todos os métodos. 

| Tipo de conta |  | Nuvem | Nuvem + VNET | Híbrido |
| --- | --- | --- | --- | --- |
| Conta da Microsoft | |Sim |Sim |Não |
| Active Directory do Azure (Azure AD) | | | | |
| Somente AD do Azure |Sim |Sim |Não | |
| AD Connect com sincronização de senha |Sim |Sim |Sim | |
| AD Connect sem sincronização de senha |Sim |Sim |Não | |
| AD Connect com o AD FS |Sim |Sim |Sim | |
| Provedores de identidade terceiros com suporte do Azure (por exemplo, Ping) |Sim |Sim |Sim | |
| Multi-Factor Authentication | |Sim |Sim |Sim |

### <a name="cloud-and-cloud--vnet"></a>Nuvem e Nuvem + VNET
Com coleções de nuvem, você pode usar contas da Microsoft, contas do AD do Azure ou uma mistura de saudação dois. Use contas de saudação que funcionam melhor para seus usuários.

Não há nenhum requisito específico para o uso das contas da Microsoft. 

Se você quiser toouse contas de AD do Azure, você precisa toomake certeza de que seu locatário do AD do Azure corresponde Olá associado à sua assinatura. Quando você criar a assinatura do Azure RemoteApp, locatário do AD do Azure Olá que você estava usando foi automaticamente associado à sua assinatura. Qualquer usuário do AD do Azure você concede permissão tooneeds toobe mesmo locatário. Se necessário, você pode [alterar locatário Olá AD do Azure](remoteapp-changetenant.md) associado à sua assinatura.

### <a name="hybrid-or-cloud--azure-ad--ad"></a>Híbrido (ou nuvem + AD do Azure + AD)
Usar o AD do Azure + Active Directory local é um pré-requisito para uma coleção híbrida. É necessário toouse AD Connect toointegrate Olá dois diretórios. Mas você tem algumas opções quando se trata de toohow configurar AD Connect. 

Há dois cenários do AD Connect – usar a sincronização de senha ou a federação do AD. Check-out Olá [informações de conexão do AD](../active-directory/active-directory-aadconnect.md) toofigure qual delas funciona melhor para você.

Você também pode usar o AD do Azure + AD com uma coleção na nuvem. Certifique-se de que seguir as mesmas etapas de configuração de saudação.

Check-out [AD do Azure + requisitos do Active Directory do Azure RemoteApp](remoteapp-ad.md) para tooconfigure necessário de etapas de saudação do AD do Azure e o Active Directory.

## <a name="go-create-your-collection"></a>Crie sua coleção!
Okey, acho que já descobrimos-lo agora, há apenas uma coisa e esquerda toodo - criar sua primeira coleção do RemoteApp.

[Criar uma coleção na nuvem](remoteapp-create-cloud-deployment.md) ou [criar uma coleção híbrida](remoteapp-create-hybrid-deployment.md) – basta começar a criar.

