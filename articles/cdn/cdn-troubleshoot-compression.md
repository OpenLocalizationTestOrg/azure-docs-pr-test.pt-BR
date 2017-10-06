---
title: "compactação de arquivo aaaTroubleshooting no Azure CDN | Microsoft Docs"
description: "Solucione problemas com a compactação de arquivo da CDN do Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: a6624e65-1a77-4486-b473-8d720ce28f8b
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f00b98beaf6b3b3cd30108ece65a8191edc06ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-cdn-file-compression"></a>Solucionando problemas de compactação de arquivo CDN
Este artigo ajuda você a solucionar problemas com a [compactação de arquivo CDN](cdn-improve-performance.md).

Se você precisar de mais ajuda a qualquer momento neste artigo, você pode contatar hello Azure especialistas em [hello Azure MSDN e Olá fóruns de estouro de pilha](https://azure.microsoft.com/support/forums/). Como alternativa, você também pode registrar um incidente de suporte do Azure. Vá toohello [site de suporte do Azure](https://azure.microsoft.com/support/options/) e clique em **suporte**.

## <a name="symptom"></a>Sintoma
A compactação do ponto de extremidade está habilitada, mas os arquivos estão sendo retornados descompactados.

> [!TIP]
> toocheck se os arquivos estão sendo retornados compactados, você precisa toouse uma ferramenta como [Fiddler](http://www.telerik.com/fiddler) ou seu navegador [ferramentas de desenvolvedor](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).  Cabeçalhos de resposta HTTP de saudação seleção retornado com a CDN em cache conteúdos.  Se houver um cabeçalho chamado `Content-Encoding` com um valor **gzip**, **bzip2** ou **deflate**, seu conteúdo será compactado.
> 
> ![Cabeçalho Content-Encoding](./media/cdn-troubleshoot-compression/cdn-content-header.png)
> 
> 

## <a name="cause"></a>Causa
Há várias causas possíveis, incluindo:

* Olá solicitou o conteúdo não está qualificado para compactação.
* A compactação não está habilitada para Olá tipo de arquivo solicitado.
* solicitação HTTP Olá não incluir um cabeçalho solicitando um tipo de compactação inválido.

## <a name="troubleshooting-steps"></a>Etapas para solucionar problemas
> [!TIP]
> Assim como a implantação de novos pontos de extremidade, as alterações de configuração de CDN levar alguns toopropagate tempo por meio da rede de saudação.  Normalmente, as alterações são aplicadas dentro de 90 minutos.  Se esse for Olá pela primeira vez que você definiu a compactação para o ponto de extremidade CDN, você deve considerar a espera-se de que as configurações de compactação Olá tenham se propagado toohello POPs de toobe de 1 a 2 horas. 
> 
> 

### <a name="verify-hello-request"></a>Verifique se a solicitação de saudação
Primeiro, devemos fazer uma verificação de integridade rápido na solicitação de saudação.  Você pode usar o navegador [ferramentas de desenvolvedor](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) tooview Olá solicitações feitas.

* Verifique se a solicitação hello está sendo enviada a URL de ponto de extremidade tooyour, `<endpointname>.azureedge.net`e não sua origem.
* Verifique se a solicitação Olá contém um **Accept-Encoding** cabeçalho e hello valor para esse cabeçalho contém **gzip**, **deflate**, ou **bzip2** .

> [!NOTE]
> Os perfis da **CDN do Azure da Akamai** suportam somente a codificação **gzip**.
> 
> 

![Cabeçalhos da solicitação CDN](./media/cdn-troubleshoot-compression/cdn-request-headers.png)

### <a name="verify-compression-settings-standard-cdn-profile"></a>Verificar as configurações de compactação (perfil CDN Standard)
> [!NOTE]
> Essa etapa se aplica somente se o seu perfil de CDN é um perfil da **CDN Standard do Azure da Verizon** ou **CDN Standard do Azure do Akamai**. 
> 
> 

Navegue de ponto de extremidade tooyour no hello [portal do Azure](https://portal.azure.com) e clique em Olá **configurar** botão.

* Verifique se a compactação está habilitada.
* Verifique se o tipo MIME Olá Olá conteúdo toobe compactado está incluído na lista de saudação dos formatos compactados.

![Configurações de compactação CDN](./media/cdn-troubleshoot-compression/cdn-compression-settings.png)

### <a name="verify-compression-settings-premium-cdn-profile"></a>Verificar as configurações de compactação (perfil CDN Premium)
> [!NOTE]
> Essa etapa se aplica somente se o seu perfil de CDN é um perfil da **CDN Premium do Azure da Verizon** .
> 
> 

Navegue de ponto de extremidade tooyour no hello [portal do Azure](https://portal.azure.com) e clique em Olá **gerenciar** botão.  portal suplementar Olá será aberto.  Passe o mouse sobre Olá **HTTP grande** guia, em seguida, passe o mouse sobre Olá **as configurações de Cache** flutuante.  Clique em **Compactação**. 

* Verifique se a compactação está habilitada.
* Verifique se Olá **tipos de arquivo** lista contém uma lista separada por vírgulas (sem espaços) dos tipos MIME.
* Verifique se o tipo MIME Olá Olá conteúdo toobe compactado está incluído na lista de saudação dos formatos compactados.

![Configurações de compactação premium CDN](./media/cdn-troubleshoot-compression/cdn-compression-settings-premium.png)

### <a name="verify-hello-content-is-cached"></a>Verifique se o conteúdo de saudação é armazenado em cache
> [!NOTE]
> Essa etapa se aplica somente se o seu perfil de CDN é um perfil da **CDN do Azure da Verizon** (Standard ou Premium).
> 
> 

Usando ferramentas de desenvolvedor do navegador, verifique se o arquivo de saudação do hello resposta cabeçalhos tooensure é armazenado em cache na região Olá onde ele está sendo solicitado.

* Verificar Olá **Server** cabeçalho de resposta.  cabeçalho Olá deve ter o formato de saudação **plataforma (ID do servidor/POP)**, como mostrado no exemplo a seguir de saudação.
* Verificar Olá **X Cache** cabeçalho de resposta.  deve ler o cabeçalho de saudação **ocorrências**.  

![Cabeçalhos de resposta CDN](./media/cdn-troubleshoot-compression/cdn-response-headers.png)

### <a name="verify-hello-file-meets-hello-size-requirements"></a>Verifique se o arquivo hello atende aos requisitos de tamanho de saudação
> [!NOTE]
> Essa etapa se aplica somente se o seu perfil de CDN é um perfil da **CDN do Azure da Verizon** (Standard ou Premium).
> 
> 

toobe qualificada para compactação, um arquivo deve atender Olá seguindo os requisitos de tamanho:

* Maior que 128 bytes.
* Menor que 1 MB.

### <a name="check-hello-request-at-hello-origin-server-for-a-via-header"></a>Verificar Olá solicitação no servidor de origem Olá para um **Via** cabeçalho
Olá **Via** cabeçalho HTTP indica o servidor de web toohello que Olá solicitação está sendo passado por um servidor proxy.  Servidores de web Microsoft IIS por padrão não compactar respostas quando Olá solicitação contém um **Via** cabeçalho.  toooverride esse comportamento, execute Olá seguinte:

* **IIS 6**: [definir HcNoCompressionForProxies = "FALSE" nas propriedades de Metabase do IIS Olá](https://msdn.microsoft.com/library/ms525390.aspx)
* **IIS 7 e superior**: [tanto **noCompressionForHttp10** e **noCompressionForProxies** tooFalse na configuração do servidor de saudação](http://www.iis.net/configreference/system.webserver/httpcompression)

