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
# <a name="troubleshooting-guide-for-live-streaming"></a><span data-ttu-id="ab142-103">Guia de solução de problemas da transmissão ao vivo</span><span class="sxs-lookup"><span data-stu-id="ab142-103">Troubleshooting guide for live streaming</span></span>
<span data-ttu-id="ab142-104">Este tópico fornece sugestões sobre como tootroubleshoot alguns live streaming problemas.</span><span class="sxs-lookup"><span data-stu-id="ab142-104">This topic gives suggestions on how tootroubleshoot some live streaming problems.</span></span>

## <a name="issues-related-tooon-premises-encoders"></a><span data-ttu-id="ab142-105">Problemas relacionados codificadores tooon locais</span><span class="sxs-lookup"><span data-stu-id="ab142-105">Issues related tooon-premises encoders</span></span>
<span data-ttu-id="ab142-106">Esta seção fornece sugestões sobre como codificadores locais tooon relacionados do tootroubleshoot problemas que estão configurados toosend um canais de tooAMS de fluxo de taxa de bits única que são habilitados para codificação ao vivo.</span><span class="sxs-lookup"><span data-stu-id="ab142-106">This section gives suggestions on how tootroubleshoot problems related tooon-premises encoders that are configured toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span>

### <a name="problem-would-like-toosee-logs"></a><span data-ttu-id="ab142-107">Problema: Gostaria que os logs de toosee</span><span class="sxs-lookup"><span data-stu-id="ab142-107">Problem: Would like toosee logs</span></span>
* <span data-ttu-id="ab142-108">**Problema potencial**: não é possível localizar os logs do codificador que poderiam ajudar na depuração de problemas.</span><span class="sxs-lookup"><span data-stu-id="ab142-108">**Potential issue**: Can't find encoder logs that might help in debugging issues.</span></span>
  
  * <span data-ttu-id="ab142-109">**Telestream Wirecast**: normalmente, você pode encontrar os logs em C:\Users\{nome_do_usuário\AppData\Roaming\Wirecast\\</span><span class="sxs-lookup"><span data-stu-id="ab142-109">**Telestream Wirecast**: You can usually find logs under C:\Users\{username}\AppData\Roaming\Wirecast\\</span></span> 
  * <span data-ttu-id="ab142-110">**Live elementar**: você pode encontrar tem links toologs no portal de gerenciamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="ab142-110">**Elemental Live**: You can find has links toologs on hello management portal.</span></span> <span data-ttu-id="ab142-111">Clique em **Estatísticas** e em **Logs**.</span><span class="sxs-lookup"><span data-stu-id="ab142-111">Click on **Stats**, then **Logs**.</span></span> <span data-ttu-id="ab142-112">Em Olá **arquivos de Log** página, você verá uma lista dos logs para todos os Olá LiveEvent itens; selecione Olá uma correspondência de sua sessão atual.</span><span class="sxs-lookup"><span data-stu-id="ab142-112">On hello **Log Files** page, you will see a list of logs for all hello LiveEvent items; select hello one matching your current session.</span></span> 
  * <span data-ttu-id="ab142-113">**Codificador de mídia ao vivo de Flash**: você pode encontrar hello **diretório de Log...**  navegando toohello **Log codificação** guia.</span><span class="sxs-lookup"><span data-stu-id="ab142-113">**Flash Media Live Encoder**: You can find hello **Log Directory...** by navigating toohello **Encoding Log** tab.</span></span>

### <a name="problem-there-is-no-option-for-outputting-a-progressive-stream"></a><span data-ttu-id="ab142-114">Problema: não há nenhuma opção para gerar uma transmissão progressiva</span><span class="sxs-lookup"><span data-stu-id="ab142-114">Problem: There is no option for outputting a progressive stream</span></span>
* <span data-ttu-id="ab142-115">**Possível problema**: codificador hello está sendo usado não desentrelaçamento automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ab142-115">**Potential issue**: hello encoder being used doesn't automatically deinterlace.</span></span> 
  
    <span data-ttu-id="ab142-116">**Etapas de solução de problemas**: procure uma opção desentrelaçamento na interface de codificador hello.</span><span class="sxs-lookup"><span data-stu-id="ab142-116">**Troubleshooting steps**: Look for a de-interlacing option within hello encoder interface.</span></span> <span data-ttu-id="ab142-117">Depois de habilitar o desentrelaçamento, verifique novamente as configurações de saída progressiva.</span><span class="sxs-lookup"><span data-stu-id="ab142-117">Once de-interlacing is enabled, check again for progressive output settings.</span></span> 

### <a name="problem-tried-several-encoder-output-settings-and-still-unable-tooconnect"></a><span data-ttu-id="ab142-118">Problema: Tentativa de várias configurações de saída de codificador e tooconnect ainda não é possível.</span><span class="sxs-lookup"><span data-stu-id="ab142-118">Problem: Tried several encoder output settings and still unable tooconnect.</span></span>
* <span data-ttu-id="ab142-119">**Possível problema**: o canal de codificação do Azure não foi redefinido corretamente.</span><span class="sxs-lookup"><span data-stu-id="ab142-119">**Potential issue**: Azure encoding channel was not properly reset.</span></span> 
  
    <span data-ttu-id="ab142-120">**Etapas de solução de problemas**: Certifique-se de codificador de Olá não está fazendo com que tooAMS, pare e redefinir o canal de saudação.</span><span class="sxs-lookup"><span data-stu-id="ab142-120">**Troubleshooting steps**: Make sure hello encoder is no longer pushing tooAMS, stop and reset hello channel.</span></span> <span data-ttu-id="ab142-121">Quando em execução novamente, tente conectar-se o seu codificador com novas configurações de saudação.</span><span class="sxs-lookup"><span data-stu-id="ab142-121">Once running again, try connecting your encoder with hello new settings.</span></span> <span data-ttu-id="ab142-122">Se isso ainda não corrigir o problema de saudação, tente criar um novo canal inteiramente, às vezes canais podem ser corrompidos após várias tentativas com falha.</span><span class="sxs-lookup"><span data-stu-id="ab142-122">If this still does not correct hello issue, try creating a new channel entirely, sometimes channels can become corrupt after several failed attempts.</span></span>  
* <span data-ttu-id="ab142-123">**Possível problema**: tamanho de GOP hello ou configurações de quadro-chave não forem ideais.</span><span class="sxs-lookup"><span data-stu-id="ab142-123">**Potential issue**: hello GOP size or key frame settings are not optimal.</span></span> 
  
    <span data-ttu-id="ab142-124">**Etapas de solução de problemas**: o intervalo recomendado de tamanho do GOP ou de quadro-chave é de 2 segundos.</span><span class="sxs-lookup"><span data-stu-id="ab142-124">**Troubleshooting steps**: Recommended GOP size or keyframe interval is 2 seconds.</span></span> <span data-ttu-id="ab142-125">Alguns codificadores calculam essa configuração em número de quadros, enquanto que outras usam segundos.</span><span class="sxs-lookup"><span data-stu-id="ab142-125">Some encoders calculate this setting in number of frames, while others use seconds.</span></span> <span data-ttu-id="ab142-126">Por exemplo: quando a saída de 30fps, Olá tamanho GOP seria 60 quadros, que é o equivalente too2 segundos.</span><span class="sxs-lookup"><span data-stu-id="ab142-126">For example: When outputting 30fps, hello GOP size would be 60 frames, which is equivalent too2 seconds.</span></span>  
* <span data-ttu-id="ab142-127">**Possível problema**: portas fechadas estão bloqueando o fluxo de saudação.</span><span class="sxs-lookup"><span data-stu-id="ab142-127">**Potential issue**: Closed ports are blocking hello stream.</span></span> 
  
    <span data-ttu-id="ab142-128">**Etapas de solução de problemas**: quando a transmissão por RTMP, verifique firewall e/ou tooconfirm de configurações de proxy que as portas de saída 1935 e 1936 estão abertas.</span><span class="sxs-lookup"><span data-stu-id="ab142-128">**Troubleshooting steps**: When streaming via RTMP, check firewall and/or proxy settings tooconfirm that outbound ports 1935 and 1936 are open.</span></span> <span data-ttu-id="ab142-129">Ao usar a transmissão RTP, confirme que a porta de saída 2010 está aberta.</span><span class="sxs-lookup"><span data-stu-id="ab142-129">When using RTP streaming, confirm that outbound port 2010 is open.</span></span> 

### <a name="problem-when-configuring-hello-encoder-toostream-with-hello-rtp-protocol-there-is-no-place-tooenter-a-host-name"></a><span data-ttu-id="ab142-130">Problema: Quando configurar Olá codificador toostream com hello protocolo RTP, há nenhum lugar tooenter um nome de host.</span><span class="sxs-lookup"><span data-stu-id="ab142-130">Problem: When configuring hello encoder toostream with hello RTP protocol, there is no place tooenter a host name.</span></span>
* <span data-ttu-id="ab142-131">**Possível problema**: não permitir codificadores RTP muitos nomes de host e um endereço IP será necessário toobe adquirido.</span><span class="sxs-lookup"><span data-stu-id="ab142-131">**Potential issue**: Many RTP encoders do not allow for host names, and an IP address will need toobe acquired.</span></span>  
  
    <span data-ttu-id="ab142-132">**Etapas de solução de problemas**: toofind Olá endereço IP, abra um prompt de comando em qualquer computador.</span><span class="sxs-lookup"><span data-stu-id="ab142-132">**Troubleshooting steps**: toofind hello IP address, open a command prompt on any computer.</span></span> <span data-ttu-id="ab142-133">toodo isso no Windows, abra Olá iniciador de execução (WIN + R) e digite "cmd" tooopen.</span><span class="sxs-lookup"><span data-stu-id="ab142-133">toodo this in Windows, open hello Run launcher (WIN + R) and type “cmd” tooopen.</span></span>  
  
    <span data-ttu-id="ab142-134">Após abrir o prompt de comando hello, digite "Ping [nome do Host de AMS]".</span><span class="sxs-lookup"><span data-stu-id="ab142-134">Once hello command prompt is open, type "Ping [AMS Host Name]".</span></span> 
  
    <span data-ttu-id="ab142-135">nome do host Olá pode ser derivado, omitindo o número de porta de saudação de saudação URL de ingestão do Azure, como destacado no hello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ab142-135">hello host name can be derived by omitting hello port number from hello Azure Ingest URL, as highlighted in hello following example:</span></span> 
  
    <span data-ttu-id="ab142-136">rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/</span><span class="sxs-lookup"><span data-stu-id="ab142-136">rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/</span></span> 
  
    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle10.png)

> [!NOTE]
> <span data-ttu-id="ab142-138">Se depois de seguir as etapas de solução de problemas de saudação que você ainda não é possível com êxito de fluxo, envie um tíquete de suporte usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab142-138">If after following hello troubleshooting steps you still cannot successfully stream, submit a support ticket using hello Azure portal.</span></span>
> 
> 

## <a name="media-services-learning-paths"></a><span data-ttu-id="ab142-139">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="ab142-139">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ab142-140">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="ab142-140">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

