---
title: "aaaLog tíquete de suporte para a série StorSimple 8000 | Microsoft Docs"
description: "Saiba como toocreate suporte à solicitação e iniciar uma sessão de suporte em seu dispositivo StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 2ebc20fe-f490-4749-8e43-c9fac86f1676
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli;anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e1a3aa3c56e036c782c4fb502c477dc0feaa0ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="contact-microsoft-support-for-your-storsimple"></a>Contate o Suporte da Microsoft para obter ajuda com seu StorSimple
Se tiver problemas com sua solução Microsoft Azure StorSimple, você poderá criar uma solicitação de serviço de suporte técnico. Em uma sessão online com seu engenheiro de suporte, talvez seja necessário também toostart uma sessão de suporte em seu dispositivo StorSimple. Este artigo orienta você sobre:

* Como solicitar toocreate de suporte.
* Como toostart uma sessão de suporte na Olá a interface do Windows PowerShell de seu dispositivo StorSimple.

Saudação de revisão [SLAs de suporte de série StorSimple 8000 e informações](https://msdn.microsoft.com/library/mt433077.aspx) antes de criar uma solicitação de suporte.

## <a name="create-a-support-request"></a>Criar uma solicitação de suporte
Execute Olá etapas toocreate uma solicitação de suporte a seguir:

#### <a name="toocreate-a-support-request"></a>toocreate uma solicitação de suporte
1. Em Olá [portal clássico do Azure](https://manage.windowsazure.com/), no Olá no canto superior direito, clique em seu nome de conta e, em seguida, clique em **entre em contato com o suporte da Microsoft**.
   
    ![Contate o Suporte da MS por meio do Portal de Gerenciamento](./media/storsimple-contact-microsoft-support/Ibiza1.png)
2. Você será redirecionado toohello novo portal do Azure (portal.azure.com). Clique em Olá **nova solicitação de suporte** lado a lado.
   
    ![Contate o Suporte da MS por meio do novo portal](./media/storsimple-contact-microsoft-support/Ibiza2.png)
   
    Olá direita da tela hello, Olá **nova solicitação de suporte** painel é exibido. 
   
    ![Painel de nova solicitação de suporte](./media/storsimple-contact-microsoft-support/Ibiza3a.png)
3. Em Olá **Noções básicas de** caixa de diálogo, Olá completo a seguir:                                
   
   1. De saudação **emitir tipo** lista suspensa, selecione **técnico**.
   2. Selecione um **assinatura** da lista suspensa de saudação.
   3. De saudação **Service** lista suspensa, selecione **StorSimple**. 
   4. Selecione um **plano de suporte** da lista suspensa de saudação. É necessário um tooenable do plano de suporte pago suporte técnico.
4. Clique em **Avançar**. Olá **problema** caixa de diálogo é exibida.
   
    ![Painel de nova solicitação de suporte](./media/storsimple-contact-microsoft-support/Ibiza5a.png) 
5. Em Olá **problema** caixa de diálogo, Olá completo a seguir:
   
   1. Selecione um **severidade** nível na lista suspensa de saudação.
   2. Selecione um **tipo de problema** da lista suspensa de saudação.
   3. Selecione um **categoria** da lista suspensa de saudação. 
   4. Em Olá **detalhes** caixa, descreva brevemente seu problema.
   5. Em Olá **período** caixa, indique Olá data, hora e fuso horário que corresponde a toohello de ocorrência mais recente do seu problema.
   6. Em **carregamento do arquivo**, clique em pacote de suporte do hello pasta ícone toobrowse tooyour.
   7. Selecione Olá **compartilhar informações de diagnóstico** caixa de seleção.
6. Clique em **Avançar**. Olá **informações de contato** caixa de diálogo é exibida.
   
    ![Painel de nova solicitação de suporte](./media/storsimple-contact-microsoft-support/Ibiza6a.png) 
7. Insira suas informações de contato e selecione um método de contato (telefone ou email). 
8. Selecione Olá **salvar alterações de contato para futuras solicitações de suporte** caixa de seleção.
9. Clique em **Criar**.

Depois que você enviou a solicitação, um engenheiro de suporte entrará em contato com você assim que possível tooproceed com sua solicitação.

## <a name="start-a-support-session-in-windows-powershell-for-storsimple"></a>Iniciar uma sessão de suporte no Windows PowerShell para StorSimple
tootroubleshoot quaisquer problemas que você pode experimentar com o dispositivo StorSimple hello, você precisará tooengage com a equipe do Microsoft Support hello. Talvez seja necessário toouse um toolog de sessão de suporte no dispositivo tooyour Microsoft Support. 

Executar o seguinte Olá etapas toostart uma sessão de suporte:

#### <a name="toostart-a-support-session"></a>toostart uma sessão de suporte
1. Dispositivo de saudação do acesso diretamente usando o console serial hello ou através de uma sessão telnet de um computador remoto. toodo etapas seguir, Olá [console serial do dispositivo Use PuTTY tooconnect toohello](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).
2. Na sessão de saudação que é aberta, pressione Olá **Enter** tooget chave um prompt de comando.
3. No menu do console serial hello, selecione a opção 1, **entrar com acesso completo**.
4. No prompt de hello, digite Olá senha a seguir: 
   
    `Password1`
5. No prompt de hello, digite Olá comando a seguir:
   
    `Enable-HcsSupportAccess`
6. Uma cadeia de caracteres criptografada será apresentada tooyou. Copie a cadeia de caracteres para um editor de texto como o Bloco de Notas.
7. Salve esta cadeia de caracteres e enviá-los em uma mensagem de email tooMicrosoft suporte. 

> [!IMPORTANT]
> Você pode desabilitar o acesso ao suporte executando `Disable-HcsSupportAccess`. o dispositivo StorSimple Olá também tentará toodisable o acesso ao suporte 8 horas após Olá sessão foi iniciada. É um toochange de prática recomendada credenciais depois de iniciar uma sessão de suporte de seu dispositivo StorSimple.
> 
> 

