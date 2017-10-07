---
title: "aaaConfigure um nome de domínio personalizado no serviço de aplicativo do Azure (GoDaddy)"
description: "Saiba como toouse um domínio nome do GoDaddy com aplicativos Web do Azure"
services: app-service
documentationcenter: 
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 33233e30-5846-488f-83f3-b32e5c114564
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 48158ee752f9833249bbf85adf80f572d1c68486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-custom-domain-name-in-azure-app-service-purchased-directly-from-godaddy"></a>Configurar um nome de domínio personalizado no Serviço de Aplicativo do Azure (adquirido diretamente do GoDaddy)
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro.md)]

Se você tiver adquirido por meio de aplicativos de Web do serviço de aplicativo do Azure, consulte a etapa final toohello do [comprar o domínio para aplicativos Web](custom-dns-web-site-buydomains-web-app.md).

Este artigo fornece instruções sobre como usar um nome de domínio personalizado adquirido diretamente de [GoDaddy](https://godaddy.com) com [Aplicativos Web do Serviço de Aplicativo](http://go.microsoft.com/fwlink/?LinkId=529714).

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a>Compreendendo os registros DNS
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-raw.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a>Adicionar um registro DNS a seu domínio personalizado
tooassociate seu domínio personalizado com um aplicativo web no serviço de aplicativo, você deve adicionar uma nova entrada na tabela DNS Olá para seu domínio personalizado usando as ferramentas fornecidas pelo GoDaddy. Olá uso seguindo as etapas toolocate Olá DNS ferramentas para GoDaddy.com

1. Fazer logon na conta tooyour com GoDaddy.com e selecione **minha conta** e **gerenciar Meus domínios**. Menu suspenso de seleção Olá Olá nome de domínio que você deseja toouse com seu aplicativo web do Azure e selecione **gerenciar DNS**.
   
    ![página de domínio personalizado para GoDaddy](./media/web-sites-godaddy-custom-domain-name/godaddy-customdomain.png)
2. De saudação **detalhes do domínio** página, role toohello **arquivo de zona DNS** guia. Isso é usada para adicionar e modificar os registros DNS para seu nome de domínio da seção de saudação.
   
    ![Guia Arquivo de Zona DNS](./media/web-sites-godaddy-custom-domain-name/godaddy-zonetab.png)
   
    Selecione **adicionar registro** tooadd um registro existente.
   
    muito**editar** um registro existente, o ícone de caneta e papel Olá select ao lado de registro de saudação.
   
   > [!NOTE]
   > Antes de adicionar os novos registros, observe que o GoDaddy já criou os registros DNS para subdomínios populares (chamados **Host** no editor), como **email**, **arquivos**, **correio** e outros. Se nome hello desejar toouse já existir, modifique o registro existente do hello em vez de criar um novo.
   > 
   > 
3. Ao adicionar um registro, você deve primeiro selecionar tipo de registro de saudação.
   
    ![selecione o tipo de registro](./media/web-sites-godaddy-custom-domain-name/godaddy-selectrecordtype.png)
   
    Em seguida, você deve fornecer Olá **Host** (Olá domínio personalizado ou subdomínio) e o que ele **aponta para**.
   
    ![adicionar um registro de zona](./media/web-sites-godaddy-custom-domain-name/godaddy-addzonerecord.png)
   
   * Ao adicionar um **um registro (host)** -você deve definir Olá **Host** campo tooeither  **@**  (isso representa o nome do domínio raiz, como  **Contoso.com**,) * (curinga para correspondência de vários subdomínios,) ou subdomínio de saudação desejar toouse (por exemplo, **www**.) Você deve definir Olá **aponta para** campo toohello endereço IP de seu aplicativo web do Azure.
   * Ao adicionar um **registro CNAME (alias)** -você deve definir Olá **Host** campo toohello subdomínio desejar toouse. Por exemplo, **www**. Você deve definir Olá **aponta para** campo toohello **. azurewebsites.net** nome de domínio do seu aplicativo web do Azure. Por exemplo, **contoso.azurewebsites.net**.
4. Clique em **Adicionar Outro**.
5. Selecione **TXT** como o tipo de registro hello, em seguida, especifique um **Host** valor  **@**  e um **aponta para** valor  **&lt;yourwebappname&gt;. azurewebsites.net**.
   
   > [!NOTE]
   > Esse registro TXT é usado pelo toovalidate do Azure que você possui o domínio Olá descrito pelo Olá um registro TXT de primeiro do registro ou hello. Depois que o domínio de saudação foi mapeada toohello aplicativo web hello Portal do Azure, essa entrada de registro TXT pode ser removida.
   > 
   > 
6. Quando você terminar de adicionar ou modificar registros, clique em **concluir** toosave alterações.

<a name="enabledomain"></a>

## <a name="enable-hello-domain-name-on-your-web-app"></a>Habilitar o nome de domínio de saudação em seu aplicativo web
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-web-site.md)]

> [!NOTE]
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo. Nenhum cartão de crédito é exigido, sem compromissos.
> 
> 

## <a name="whats-changed"></a>O que mudou
* Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

