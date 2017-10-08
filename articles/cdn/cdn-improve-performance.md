---
title: aaaImprove desempenho compactando arquivos no Azure CDN | Microsoft Docs
description: "Saiba como o arquivo tooimprove transferir velocidade e aumentos de desempenho de carregamento de página por compactar os arquivos no Azure CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: af1cddff-78d8-476b-a9d0-8c2164e4de5d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 9a1698b6c29233c2e2e6fb17cdd8e919ae8bfa1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="improve-performance-by-compressing-files-in-azure-cdn"></a>Melhorar o desempenho compactando os arquivos na CDN do Azure
A compactação é uma velocidade de transferência de arquivo do método simples e eficaz tooimprove e aumento de desempenho de carregamento de página, reduzindo o tamanho do arquivo antes de ele é enviado do servidor de saudação. Ela reduz os custos de largura de banda e oferece uma experiência mais responsiva para os seus usuários.

Há duas maneiras de compactação tooenable:

* Você pode habilitar a compactação no servidor de origem, caso em que hello CDN passe Olá arquivos compactados e entregar tooclients arquivos compactados que fazem a solicitação.
* Você pode habilitar a compactação diretamente nos servidores de borda CDN, na qual o caso Olá CDN compacta Olá arquivos e servi-los tooend usuários, mesmo se eles não são compactados com o servidor de origem de saudação.

> [!IMPORTANT]
> Alterações de configuração de CDN levar alguns toopropagate tempo por meio da rede de saudação.  Para perfis <b>CDN do Azure do Akamai</b> , a propagação normalmente é concluída em menos de um minuto.  Para perfis <b>CDN do Azure da Verizon</b> , você geralmente verá suas alterações serem aplicadas em 90 minutos.  Se esse for Olá pela primeira vez que você definiu a compactação para o ponto de extremidade CDN, você deve considerar a espera-se de que as configurações de compactação Olá tenham se propagado POPs toohello antes de solucionar problemas de toobe de 1 a 2 horas
> 
> 

## <a name="enabling-compression"></a>Habilitando a compactação
> [!NOTE]
> Olá camadas Standard e Premium CDN fornecem Olá a mesma funcionalidade de compactação, mas hello interface de usuário diferente.  Para obter mais informações sobre as diferenças de saudação entre camadas Standard e Premium CDN, consulte [visão geral do Azure CDN](cdn-overview.md).
> 
> 

### <a name="standard-tier"></a>Camada padrão
> [!NOTE]
> Esta seção aplica-se muito**Azure CDN padrão da Verizon** e **padrão do Azure CDN do Akamai** perfis.
> 
> 

1. Na página de perfil CDN hello, clique em ponto de extremidade CDN Olá desejar toomanage.
   
    ![Pontos de extremidade da página de perfil da CDN](./media/cdn-file-compression/cdn-endpoints.png)
   
    Abre a página de ponto de extremidade CDN Hello.
2. Clique em Olá **configurar** botão.
   
    ![Botão de gerenciamento de página de perfil da CDN](./media/cdn-file-compression/cdn-config-btn.png)
   
    Abre a página de configuração de CDN Hello.
3. Habilitar **Compactação**.
   
    ![Opções de compactação da CDN](./media/cdn-file-compression/cdn-compress-standard.png)
4. Use tipos de padrão de hello, ou modificar a lista de hello, removendo ou adicionando tipos de arquivo.
   
   > [!TIP]
   > Embora possível, não é recomendável tooapply compactação toocompressed formatos, como ZIP, MP3, MP4, JPG, etc.
   > 
   > 
5. Depois de fazer suas alterações, clique em Olá **salvar** botão.

### <a name="premium-tier"></a>Camada premium
> [!NOTE]
> Esta seção aplica-se muito**Premium do Azure CDN da Verizon** perfis.
> 
> 

1. Na página de perfil CDN hello, clique em Olá **gerenciar** botão.
   
    ![Botão de gerenciamento de página de perfil da CDN](./media/cdn-file-compression/cdn-manage-btn.png)
   
    portal de gerenciamento de CDN Olá é aberto.
2. Passe o mouse sobre Olá **HTTP grande** guia, em seguida, passe o mouse sobre Olá **as configurações de Cache** flutuante.  Clique em **Compactação**.

    ![Seleção de compactação de arquivos](./media/cdn-file-compression/cdn-compress-select.png)
   
    As opções de compactação são exibidas.
   
    ![Compactação de arquivos](./media/cdn-file-compression/cdn-compress-files.png)
3. Habilitar a compactação clicando Olá **compactação habilitada** botão de opção.  Inserir tipos MIME Olá desejar toocompress como uma lista delimitada por vírgulas (sem espaços) em Olá **tipos de arquivo** caixa de texto.
   
   > [!TIP]
   > Embora possível, não é recomendável tooapply compactação toocompressed formatos, como ZIP, MP3, MP4, JPG, etc. 
   > 
   > 
4. Depois de fazer suas alterações, clique em Olá **atualização** botão.

## <a name="compression-rules"></a>Regras de compactação
Essas tabelas descrevem o comportamento de compactação CDN do Azure para cada cenário.

> [!IMPORTANT]
> Para o **CDN do Azure da Verizon** (Standard e Premium), só os arquivos elegíveis são compactados.  toobe qualificada para compactação, um arquivo necessário:
> 
> * Ser maior que 128 bytes.
> * Ser menor que 1 MB.
> 
> Para o **CDN do Azure do Akamai**, todos os arquivos estão qualificados para compactação.
> 
> Para todos os produtos de CDN do Azure, um arquivo deve ser um tipo MIME que foi [configurado para compactação](#enabling-compression).
> 
> Os perfis da **CDN do Azure da Verizon** (Standard e Premium) oferecem suporte à codificação **gzip** (GNU zip), **deflate**, **bzip2** ou **br** (Brotli). Para codificação Brotli, compactação de saudação é feita apenas na borda de saudação. Olá cliente/navegador deve enviar a solicitação de saudação para codificação Brotli e ativo compactado Olá deve tiverem sido compactado no lado de origem Olá primeiro. 
>
>Os perfis da **CDN do Azure da Akamai** oferecem suporte somente á codificação **gzip**.
> 
> **Azure CDN do Akamai** pontos de extremidade sempre solicitar **gzip** codificada em arquivos de origem hello, independentemente de solicitação de saudação do cliente. 

### <a name="compression-disabled-or-file-is-ineligible-for-compression"></a>Compactação desabilitada ou arquivo não qualificado para compactação
| Formato solicitado pelo cliente (por meio do cabeçalho Accept-Encoding) | Formato de arquivo armazenado em cache | Cliente de toohello de resposta CDN | Observações |
| --- | --- | --- | --- |
| Compactado |Compactado |Compactado | |
| Compactado |Não compactado |Não compactado | |
| Compactado |Não armazenado em cache |Compactada ou descompactada |Depende da resposta de origem |
| Não compactado |Compactado |Não compactado | |
| Não compactado |Não compactado |Não compactado | |
| Não compactado |Não armazenado em cache |Não compactado | |

### <a name="compression-enabled-and-file-is-eligible-for-compression"></a>Compactação habilitada ou arquivo qualificado para compactação
| Formato solicitado pelo cliente (por meio do cabeçalho Accept-Encoding) | Formato de arquivo armazenado em cache | Cliente de toohello de resposta CDN | Observações |
| --- | --- | --- | --- |
| Compactado |Compactado |Compactado |CDN transcodifica entre os formatos com suporte |
| Compactado |Não compactado |Compactado |CDN executa compactação |
| Compactado |Não armazenado em cache |Compactado |O CDN executará compactação se a origem for retornada descompactada.  **A CDN do Azure da Verizon** passa Olá arquivo não compactado na primeira solicitação de saudação e, em seguida, compacta e caches Olá arquivo para solicitações subsequentes.  Os arquivos com o cabeçalho `Cache-Control: no-cache` nunca serão compactados. |
| Não compactado |Compactado |Não compactado |CDN executa descompactação |
| Não compactado |Não compactado |Não compactado | |
| Não compactado |Não armazenado em cache |Não compactado | |

## <a name="media-services-cdn-compression"></a>Compactação de CDN dos Serviços de Mídia
Para CDN de serviços de mídia habilitado pontos de extremidade de streaming, a compactação é habilitada por padrão para os seguintes tipos de conteúdo de saudação: application/vnd.ms-sstr + xml, application/dash+xml,application/vnd.apple.mpegurl, application/f4m + xml. Você não pode habilitar/desabilitar a compactação para Olá mencionado tipos usando Olá portal do Azure.  

## <a name="see-also"></a>Consulte também
* [Solucionando problemas de compactação de arquivo CDN](cdn-troubleshoot-compression.md)    

