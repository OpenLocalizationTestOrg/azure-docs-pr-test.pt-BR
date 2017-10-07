---
title: licenciamento de RemoteApp aaaAzure | Microsoft Docs
description: Saiba como funciona o licenciamento no RemoteApp do Azure.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: ff8ebd20-61a1-4f10-87a6-234a170534c9
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: dfa808a65ea6b1a78bf74f3daddb9a84e186eebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-licensing-work-in-azure-remoteapp"></a>Como o licenciamento funciona no RemoteApp do Azure?
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Portanto, você configurou seu serviço RemoteApp do Azure, criado seus modelos e está pronto toopublish aplicativos tooyour usuários. Mas ainda há uma última toofigure de coisa out: licenciamento. Assim como funciona o licenciamento para o RemoteApp e para aplicativos de saudação que compartilhar por meio do RemoteApp?

O RemoteApp não requer quaisquer licenças do Windows ou CALs de Área de Trabalho Remota. Sua assinatura se encarrega de saudação do lado do RemoteApp em si. (Verifique os detalhes de saudação do hello [planos de preços](https://azure.microsoft.com/pricing/details/remoteapp).)

Se você usar uma das imagens de saudação que está incluído na sua assinatura, você pode compartilhar qualquer Olá aplicativos instalados na imagem sem a necessidade de uma licença separada. Por exemplo, se você usar toobuild de imagem de modelo de Windows Server 2012 R2 Olá sua coleção, você pode compartilhar o System Center Endpoint Protection com os usuários. Olá somente as regras de toothis exceções são Office 365 ProPlus, que requer uma assinatura separada, e Office 2013, que não podem ser compartilhados em uma coleção de produção.

Se desejar que a imagem de modelo do toouse Olá Office 365 que vem com o RemoteApp, você deve ter uma *existente* Office 365 ProPlus plano. Olá que mesmo é verdadeiro para qualquer aplicativo do Office 365 que você publicar usando um modelo personalizado. Você precisa tooactivate Olá aplicativos com sua própria assinatura. Isso é verdadeiro para as assinaturas de avaliação e pagas. Se você quiser imagem de modelo Olá Office 365 toouse durante a avaliação de saudação *e você ainda não tiver uma assinatura*, acesse a página toohello Office 365 muito[inscrever-se](https://go.microsoft.com/fwlink/p/?LinkID=403802) para uma assinatura de avaliação. Consulte [Como o RemoteApp e o Office funcionam juntos?](remoteapp-o365.md) para obter mais informações.

Se, durante o período de avaliação hello, você não deseja assinatura de avaliação tooget um Office 365, use a imagem de modelo do Office 2013 Professional Plus Olá vem com o RemoteApp. Essa imagem de modelo só pode ser usada por 30 dias e não pode ser convertida em uma coleção paga.

Para outros aplicativos, você precisa toomake tenha Olá licença tooshare Olá aplicativo.

Isso faz sentido, certo? Você pode publicar qualquer aplicativo que você tem direito legal tooshare. E você precisa toomake-se de que você realmente é intitulado tooshare seus programas.

Observe que você não pode usar um contrato de licença de Volume ou CAL em uma coleção na nuvem. Você *pode* usar aplicativos de tooactivate de contrato de licença de Volume em sua coleção híbrida (com exceção do Office). Basta tooinstall-los em seu modelo de imagem de saudação mídia de licença de Volume. Siga as informações de saudação do licenças de tooinstall de fornecedor Olá aplicativos em um ambiente de área de trabalho remota.

