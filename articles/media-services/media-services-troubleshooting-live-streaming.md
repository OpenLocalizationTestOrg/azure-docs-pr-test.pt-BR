---
title: "Guia de aaaTroubleshooting para transmissão ao vivo | Microsoft Docs"
description: "Este tópico fornece sugestões sobre como tootroubleshoot live streaming problemas."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 3a7f6c1d-ce57-4fa4-a7a6-edb526b3ffbf
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 8549bae947ff3b225ce624220d1e48b63f90208c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-live-streaming"></a>Guia de solução de problemas da transmissão ao vivo
Este tópico fornece sugestões sobre como tootroubleshoot alguns live streaming problemas.

## <a name="issues-related-tooon-premises-encoders"></a>Problemas relacionados codificadores tooon locais
Esta seção fornece sugestões sobre como codificadores locais tooon relacionados do tootroubleshoot problemas que estão configurados toosend um canais de tooAMS de fluxo de taxa de bits única que são habilitados para codificação ao vivo.

### <a name="problem-would-like-toosee-logs"></a>Problema: Gostaria que os logs de toosee
* **Problema potencial**: não é possível localizar os logs do codificador que poderiam ajudar na depuração de problemas.
  
  * **Telestream Wirecast**: normalmente, você pode encontrar os logs em C:\Users\{nome_do_usuário\AppData\Roaming\Wirecast\ 
  * **Live elementar**: você pode encontrar tem links toologs no portal de gerenciamento de saudação. Clique em **Estatísticas** e em **Logs**. Em Olá **arquivos de Log** página, você verá uma lista dos logs para todos os Olá LiveEvent itens; selecione Olá uma correspondência de sua sessão atual. 
  * **Codificador de mídia ao vivo de Flash**: você pode encontrar hello **diretório de Log...**  navegando toohello **Log codificação** guia.

### <a name="problem-there-is-no-option-for-outputting-a-progressive-stream"></a>Problema: não há nenhuma opção para gerar uma transmissão progressiva
* **Possível problema**: codificador hello está sendo usado não desentrelaçamento automaticamente. 
  
    **Etapas de solução de problemas**: procure uma opção desentrelaçamento na interface de codificador hello. Depois de habilitar o desentrelaçamento, verifique novamente as configurações de saída progressiva. 

### <a name="problem-tried-several-encoder-output-settings-and-still-unable-tooconnect"></a>Problema: Tentativa de várias configurações de saída de codificador e tooconnect ainda não é possível.
* **Possível problema**: o canal de codificação do Azure não foi redefinido corretamente. 
  
    **Etapas de solução de problemas**: Certifique-se de codificador de Olá não está fazendo com que tooAMS, pare e redefinir o canal de saudação. Quando em execução novamente, tente conectar-se o seu codificador com novas configurações de saudação. Se isso ainda não corrigir o problema de saudação, tente criar um novo canal inteiramente, às vezes canais podem ser corrompidos após várias tentativas com falha.  
* **Possível problema**: tamanho de GOP hello ou configurações de quadro-chave não forem ideais. 
  
    **Etapas de solução de problemas**: o intervalo recomendado de tamanho do GOP ou de quadro-chave é de 2 segundos. Alguns codificadores calculam essa configuração em número de quadros, enquanto que outras usam segundos. Por exemplo: quando a saída de 30fps, Olá tamanho GOP seria 60 quadros, que é o equivalente too2 segundos.  
* **Possível problema**: portas fechadas estão bloqueando o fluxo de saudação. 
  
    **Etapas de solução de problemas**: quando a transmissão por RTMP, verifique firewall e/ou tooconfirm de configurações de proxy que as portas de saída 1935 e 1936 estão abertas. Ao usar a transmissão RTP, confirme que a porta de saída 2010 está aberta. 

### <a name="problem-when-configuring-hello-encoder-toostream-with-hello-rtp-protocol-there-is-no-place-tooenter-a-host-name"></a>Problema: Quando configurar Olá codificador toostream com hello protocolo RTP, há nenhum lugar tooenter um nome de host.
* **Possível problema**: não permitir codificadores RTP muitos nomes de host e um endereço IP será necessário toobe adquirido.  
  
    **Etapas de solução de problemas**: toofind Olá endereço IP, abra um prompt de comando em qualquer computador. toodo isso no Windows, abra Olá iniciador de execução (WIN + R) e digite "cmd" tooopen.  
  
    Após abrir o prompt de comando hello, digite "Ping [nome do Host de AMS]". 
  
    nome do host Olá pode ser derivado, omitindo o número de porta de saudação de saudação URL de ingestão do Azure, como destacado no hello exemplo a seguir: 
  
    rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/ 
  
    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle10.png)

> [!NOTE]
> Se depois de seguir as etapas de solução de problemas de saudação que você ainda não é possível com êxito de fluxo, envie um tíquete de suporte usando Olá portal do Azure.
> 
> 

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

