---
title: "Como migrar de uma coleção híbrida de uma VNET RemoteApp para uma VNET do Azure | Microsoft Docs"
description: "Aprenda como migrar de uma coleção híbrida de uma VNET RemoteApp para uma VNET do Azure"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: baea5d29-353b-48f8-b47f-806f2163e067
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 10b5f4844a38fe97852dee8634e8cf54f1a23a1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-migrate-a-hybrid-collection-from-a-remoteapp-vnet-to-an-azure-vnet"></a>Como migrar uma coleção híbrida de um VNET RemoteApp para uma VNET do Azure
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Leia o [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Boas notícias! Habilitamos você para implantar as coleções híbridas de RemoteApp diretamente para as redes virtuais (VNETs) do Azure existentes em vez de criar VNETs específicas do RemoteApp. Isso permite a você aproveitar os recursos mais recentes do VNET (como ExpressRoute) e dar a suas coleções híbridas acesso direto de rede a outros serviços do Azure e máquinas virtuais implantadas nessa VNET.  (Isso apresenta um desempenho melhor e mais fácil instalação que configurações de VNET para VNET).

Digamos que você já criou uma coleção híbrida de RemoteApp chamada *ColeçãoOriginal* com uma VNET do RemoteApp chamada *RemoteAppVNET*. Aqui estão as etapas para migrá-la para uma nova VNET do Azure chamada *AzureVNET*.

1. Na guia **Redes** do [Portal de Gerenciamento](http://manage.windowsazure.com/), crie uma VNET chamada *AzureVNET*, usando o mesmo local, a configuração do DNS e espaço de endereço (para pelo menos uma das sub-redes do *AzureVNET*) que você usou para a *RemoteAppVNET*.
2. Configure *AzureVNET* para hospedar ou ter conectividade de rede para a implantação do Active Directory ao qual o domínio *ColeçãoOriginal* é integrado.
3. Na guia **RemoteApps** , crie uma nova coleção de RemoteApp chamada *NovaColeção*. (Use a opção **Criar com VNET**, e não **Criação rápida**.)
4. Configure *NovaColeção* para ser implantada em uma sub-rede em *AzureVNET*.
5. Configure *NovaColeção* para usar as mesmas informações de imagem e ingresso no domínio que as usadas para *ColeçãoOriginal*.
6. Após algumas horas, *NovaColeção* aparecerá na sua lista de coleções com um estado Ativo.

Agora, se você NÃO precisa migrar informações do usuário da coleção original para a nova coleção, siga estas etapas:

1. Exclua *ColeçãoOriginal*.
2. Exclua *RemoteAppVNET*.

E pronto!

Alternativamente, se você PRECISA migrar informações do usuário da coleção original para a nova coleção, siga estas etapas:

1. Envie um email para [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) com sua ID de assinatura do Azure, o nome de sua coleção original e o nome da nova coleção e peça-lhes para migrarem suas informações de usuário.
2. Em 2 dias úteis a equipe RemoteApp moverá a lista de acesso de usuário e todos os documentos e configurações de usuário da coleção original para a nova coleção.
3. Exclua *ColeçãoOriginal*.
4. Exclua *RemoteAppVNET*.

E pronto!

Se você tiver dúvidas ou precisar de ajuda especial, envie um email para [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).

