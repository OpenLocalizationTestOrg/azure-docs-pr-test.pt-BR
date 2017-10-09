---
title: "aaaSetting a credenciais de autenticação de chamada | Microsoft Docs"
description: "Saiba como o serviço de nuvem tootooprovide credenciais que o Visual Studio pode usar tooauthenticate solicitações tooAzure toopublish tooAzure um aplicativo do Visual Studio ou toomonitor um existente. "
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 61570907-42a1-40e8-bcd6-952b21a55786
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/22/2017
ms.author: kraigb
ms.openlocfilehash: 3cc147a2f7a3e766293ca282f56078cf24281346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-named-authentication-credentials"></a>Configurando credenciais de autenticação nomeadas
toopublish tooAzure um aplicativo do Visual Studio ou toomonitor um serviço de nuvem existente, você deve fornecer credenciais que o Visual Studio pode usar tooauthenticate solicitações tooAzure. Há vários locais no Visual Studio, onde você pode entrar no tooprovide essas credenciais. Por exemplo, de Olá Gerenciador de servidores, você pode abrir o menu de atalho de saudação de saudação **Azure** nó e escolha **conectar tooMicrosoft assinatura do Azure...** . Quando você entrar, informações de assinatura de saudação associadas à sua conta do Azure estão disponíveis no Visual Studio, e nada mais que ter toodo.

Ferramentas do Azure também oferece suporte a uma maneira mais antiga de fornecer credenciais, Olá assinatura (arquivo. publishsettings). Este tópico descreve esse método, que ainda tem suporte no Azure SDK 2.2.

Olá itens a seguir é necessário para autenticação tooAzure:

* Sua ID de assinatura
* Um certificado X.509 v3 válido

> [!NOTE]
> comprimento de saudação da chave do certificado x. 509 v3 da saudação deve ser pelo menos 2048 bits. O Azure descartará qualquer certificado que não atenda a esse requisito ou que não seja válido.
>
>

O Visual Studio usa sua ID da assinatura junto com dados de certificado hello como credenciais. credenciais apropriadas Olá são referenciadas no arquivo de assinatura de saudação (arquivo. publishsettings), que contém uma chave pública para o certificado de saudação. arquivo de assinatura de saudação pode conter credenciais para mais de uma assinatura.

Você pode editar as informações de assinatura de saudação da saudação **nova assinatura/editar** caixa de diálogo, conforme explicado mais adiante neste tópico.

Se você quiser toocreate um certificado por conta própria, você pode consultar instruções toohello [criar e carregar um certificado de gerenciamento do Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) e, em seguida, carregar manualmente Olá certificado toohello [portal clássico do Azure ](http://go.microsoft.com/fwlink/?LinkID=213885).

> [!NOTE]
> Essas credenciais que o Visual Studio requer toomanage que seus serviços de nuvem não são Olá mesmas credenciais que são necessária tooauthenticate uma solicitação nos serviços de armazenamento do Azure hello.
>
>

## <a name="import-set-up-or-edit-authentication-credentials-in-visual-studio"></a>Importar, configurar ou editar as credenciais de autenticação no Visual Studio
Você pode importar, configurar ou modificar suas credenciais de autenticação em Olá **nova assinatura** caixa de diálogo que aparece se você executar Olá ação a seguir:

* Em **Server Explorer**, abra menu de atalho de saudação de saudação **Azure** nó, escolha **gerenciar e assinaturas de filtro...** , escolha Olá **certificados** guia e siga um destes procedimentos hello:

    * Escolha **importar** tooopen Olá importar assinaturas do Microsoft Azure caixa de diálogo onde você pode baixar o arquivo assinaturas Olá Olá atualmente carregados assinatura, procurar tooits local de download e, em seguida, importá-lo para uso em autenticação.
    * Escolha **novo** tooopen Olá nova caixa de diálogo onde você pode configurar uma nova assinatura para uso na autenticação.
    * Escolha **editar** (depois de escolher sua assinatura ativa) tooopen Olá Editar caixa de diálogo onde você pode editar uma assinatura existente para uso na autenticação. 

Olá, procedimento a seguir supõe que Olá **nova assinatura** caixa de diálogo é aberta.

### <a name="tooset-up-authentication-credentials-in-visual-studio"></a>tooset as credenciais de autenticação no Visual Studio
1. Em Olá **selecionar um certificado existente** para lista de autenticação, selecione um certificado.
2. Escolha Olá **Copiar caminho completo do hello** link. Olá caminho certificado hello (arquivo. cer) é copiado toohello da área de transferência.

   > [!IMPORTANT]
   > toopublish seu aplicativo do Azure no Visual Studio, você deve carregar este certificado toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
   >
   >
3. tooupload Olá certificado toohello portal do Azure:

   1. Olá abrir [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
   2. Se solicitado, entre no portal de toohello e navegue muito**configurações**, **certificados de gerenciamento**.
   3. No painel de certificados de gerenciamento hello, escolha **carregar**.
   4. Selecione sua assinatura do Azure, cole o caminho completo de saudação do arquivo. cer de saudação que você acabou de criado e escolha **carregar**.
