---
title: aaaCreate uma imagem do RemoteApp do Azure | Microsoft Docs
description: "Saber mais sobre opções de saudação disponíveis para a criação de imagens do Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: cb0f9424-6185-45a1-abe9-c23f1edf34f2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 54e63b6fa13addfcda96ce581910e1ac48d91e70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-remoteapp-image"></a>Criar uma imagem de RemoteApp do Azure
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

O Azure RemoteApp usa imagens toohold Olá aplicativos que você compartilha com os usuários. (É capturar sua imagem e usá-lo VMs toocreate - do qual os usuários de saudação acessam quando entrarem no Azure RemoteApp.) toocreate uma coleção do RemoteApp do Azure com sua escolha de aplicativos, seja nuvem ou híbrida, comece criando uma imagem com os aplicativos instalados. Em seguida, crie uma coleção que usa essa imagem, atribuir usuários a coleção de toohello e publicar os usuários toothose de aplicativos.

Você tem várias opções para criar ou usar as imagens. Olá básico [requisito](remoteapp-imagereqs.md) para uma imagem que executam o Windows Server 2012 R2 e função de Host de sessão de área de trabalho remota (RDSH) Olá instalada. Como você obtém isso é onde as coisas ficam interessantes.

Você tem as opções a seguir quando se trata de tooimages de saudação:

* Você pode importar e usar uma [imagem com base em uma máquina virtual do Azure](remoteapp-image-on-azurevm.md). Isso é bom para aplicativos de linha de negócios que requerem configurações personalizadas. Você pode personalizar Olá toowork de imagem para o aplicativo hello.
* Você pode [criar e carregar uma imagem personalizada](remoteapp-create-custom-image.md). Isso é bom se você já tiver uma imagem que use para sua implantação de Serviços de Área de Trabalho Remota local.
* Você pode usar uma saudação [imagens de modelo](remoteapp-images.md) incluído na sua assinatura do RemoteApp. Essas imagens são criadas e mantido pela equipe do RemoteApp hello e contêm alguns aplicativos padrão (como Olá Office suite) que você pode criar usuários tooyour disponíveis. Observe que Olá Office 365 Pro Plus a imagem somente pode ser usada em um ambiente de produção.

Independentemente de onde obter sua imagem ou como criá-lo, você desejará toomake-se de que entendeu Olá [requisitos do aplicativo](remoteapp-appreqs.md) tooensure que o aplicativo funciona bem no RemoteApp. Em seguida, a próxima etapa de saudação é toocreate uma [nuvem](remoteapp-create-cloud-deployment.md) ou [híbrida](remoteapp-create-hybrid-deployment.md) coleção.

