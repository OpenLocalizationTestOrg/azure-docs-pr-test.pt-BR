---
title: "aaaLicensing Microsoft® Smooth Streaming Client Porting Kit"
description: "Saiba mais sobre como toolicensing Olá Microsoft® Smooth Streaming Client Porting Kit."
services: media-services
documentationcenter: 
author: xpouyat
manager: cfowler
editor: 
ms.assetid: e3b488e7-8428-4c10-a072-eb3af46c82ad
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: xpouyat
ms.openlocfilehash: 56c3dccda73dd02207bb4dbe8109ba6fda917a6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-microsoft-smooth-streaming-client-porting-kit"></a>Licenciamento do kit de portabilidade de cliente do Microsoft® Smooth Streaming
## <a name="overview"></a>Visão geral
Microsoft Smooth Streaming Client Porting Kit (**SSPK** abreviada) é uma implementação de cliente de Smooth Streaming otimizada toohelp inserido os fabricantes de dispositivo, cabo e operadoras móveis, provedores de serviço de conteúdo, fone fabricantes, fornecedores de software independentes (ISVs) e produtos de toocreate de provedores de soluções e serviços para streaming de conteúdo adaptável em formato Smooth Streaming. SSPK é uma implementação independente dispositivo e plataforma de cliente de Smooth Streaming que pode ser movido por plataforma e o dispositivo de tooany licenciado hello. 

Incluída abaixo é uma arquitetura de alto nível e caixa IIS Smooth Streaming Porting Kit é Olá Smooth Streaming Client implementação fornecida pela Microsoft e inclui toda a lógica de núcleo Olá para reprodução de conteúdo de Smooth Streaming. Em seguida, isso será portado por parceiros para um dispositivo ou plataforma específicos, implementando interfaces apropriadas. 

![SSPK](./media/media-services-sspk/sspk-arch.png)

## <a name="description"></a>Descrição
O SSPK é licenciado em termos que oferecem excelente valor comercial. Licença SSPK fornece setor Olá com:

* a fonte do Kit de Portabilidade de Smooth Streaming em C++ 
  * implementa a funcionalidade de Cliente do Smooth Streaming
  * adiciona a análise de formato, heurística, lógica de buffer etc.
* APIs do aplicativo Player 
  * interfaces de programação para interação com um aplicativo de player de mídia
* Interface da Camada de Abstração de Plataforma (PAL) 
  * interfaces de programação para interação com o sistema operacional de saudação (threads, soquetes)
* Interface da Camada de Abstração de Hardware (HAL) 
  * interfaces de programação para interação com decodificadores A/V de hardware (decodificação, renderização)
* Interface de Gerenciamento de Direitos Digitais (DRM) 
  * interfaces de programação para lidar com DRM por meio de saudação DRM abstração DAL (camada)
  * O Kit de Portabilidade do Microsoft PlayReady é fornecido separadamente, mas se integra por meio dessa interface. Para saber mais sobre o licenciamento do Dispositivo Microsoft PlayReady, clique [aqui](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).
* Amostras de implementação 
  * implementação de amostra de PAL para Linux
  * implementação de amostra de HAL para GStreamer

## <a name="licensing-options"></a>Opções de Licenciamento
Microsoft Smooth Streaming Client Porting Kit é feita toolicensees disponível em dois contratos de licença distintas: uma para o desenvolvimento de Smooth Streaming Client provisória produtos e outro para a distribuição de usuários de tooend Smooth Streaming Final produtos de cliente.

* Kit de toodevelop provisória produtos, um Microsoft Smooth Streaming Client Porting Kit para fabricantes de chipset, integradores de sistema ou software independente ISVs (fornecedores) que exigem uma movimentação de código fonte **licença do produto provisória** deve ser executado.
* Para os fabricantes de dispositivo ou ISVs que precisam de direitos de distribuição para os usuários tooend de Smooth Streaming Final produtos de cliente, Olá Microsoft Smooth Streaming Client Porting Kit **Final de licenças de produto** devem ser executados.

### <a name="microsoft-smooth-streaming-client-porting-kit-interim-product-license"></a>Licença de Produto Provisório do Kit de Portabilidade de Cliente do Microsoft Smooth Streaming
Sob esta licença Microsoft oferece um Smooth Streaming Client Porting Kit Olá toodevelop de direitos de propriedade intelectual necessários e distribuir licenciados de dispositivo do Smooth Streaming Client provisória produtos tooother Smooth Streaming Client Porting Kit que Distribua Smooth Streaming Final produtos de cliente.

#### <a name="fee-structure"></a>Estrutura de taxa
Uma taxa de licença única de US $50.000 fornece acesso toohello Smooth Streaming Client Porting Kit. 

### <a name="microsoft-smooth-streaming-client-porting-kit-final-product-license"></a>Licença de Produto Final do Kit de Portabilidade de Cliente do Microsoft Smooth Streaming
Sob esta licença, a Microsoft oferece todos os tooreceive de direitos de propriedade intelectual Smooth Streaming Client provisória produtos de outras licenças de Smooth Streaming Client Porting Kit e toodistribute da empresa com a marca Final de cliente Smooth Streaming Usuários tooend de produtos.

#### <a name="fee-structure"></a>Estrutura de taxa
Olá Smooth Streaming Client Final do produto é oferecido em um modelo de direitos autorais, como em:

* US$ 0,10 por implementação de dispositivo fornecida
* royalty Hello está limitado a r $50.000 por ano
* Nenhum royalty para as primeiras 10.000 implementações de dispositivo por ano 

## <a name="licensing-procedure-and-sspk-access"></a>Procedimento de licenciamento e acesso do SSPK
Caso tenha alguma dúvida sobre licenciamento, envie um email para [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) .

Olá [portal SSPK distribuição](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) é acessível tooregistered licenciados provisória.

Licenciados provisória e SSPK Final podem enviar perguntas técnicas muito[smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).

## <a name="microsoft-smooth-streaming-client-interim-product-agreement-licensees"></a>Licenciados do Contrato do Produto provisório do cliente do Microsoft Smooth Streaming
* Adroit Business Solutions, Inc
* Advanced Digital Broadcast SA
* AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.
* Albis Technologies Ltd.
* Alticast Corporation
* Amazon Digital Services, Inc.
* Arion Technology, Inc.
* AVC Multimedia Software Co., Ltd.
* Cavium, Inc.
* EchoStar Purchasing Corporation
* Enseo, Inc.
* Fluendo S.A.
* HANDAN BroadInfoCom Co., Ltd.
* Infomir GMBH
* Irdeto USA Inc.
* iWEDIA S.A. 
* Liberty Global Services BV
* MediaTek Inc.
* MStar Co, Ltd
* Nintendo Co., Ltd.
* OpenTV, Inc.
* Saffron Digital Limited
* Sichuan Changhong Electric Co., Ltd
* SoftAtHome
* Sony Corporation
* Tatung Technology Inc.
* TCL Technoly Electronics (Huizhou) Co., Ltd.
* Top Victory Investments, Ltd.
* Vestel Elektronik Sanayi ve Ticaret A.S.
* VisualOn, Inc.
* ZTE Corporation

## <a name="microsoft-smooth-streaming-client-final-product-agreement-licensees"></a>Licenciados do Contrato do Produto final do cliente do Microsoft Smooth Streaming
* Advanced Digital Broadcast SA
* AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.
* Albis Technologies Ltd.
* Amazon Digital Services, Inc.
* AmTRAN Technology Co., Ltd.
* Arcadyan Technology Corporation
* Arion Technology, Inc.
* ATMACA ELEKTRONİK SAN. VE TİC. A.Ş
* British Sky Broadcasting Limited
* CastPal Technology Inc., Shenzhen
* Compal eletrônicos, Inc.
* Dongguan Digital AV Technology Corp., Ltd.
* EchoStar Purchasing Corporation
* Enseo, Inc.
* Filmflex Movies Limited
* Fluendo S.A.
* Gibson Innovations Limited
* Haier Information Applicantion S.R.L
* HANDAN BroadInfoCom Co., Ltd.
* Hisense International Co., Ltd. 
* Homecast Co.,Ltd
* Hon Hai Precision Industry Co., Ltd.
* Infomir GMBH
* Kaonmedia Co., Ltd.
* KDDI Corporation
* Nintendo Co., Ltd.
* Orange SA
* Saffron Digital Limited
* Sagemcom Broadband SAS
* Shenzhen Coship Electronics CO., LTD
* Shenzhen Jiuzhou Electric Co.,Ltd
* Shenzhen Skyworth Digital Technology Co., Ltd
* Sichuan Changhong Electric Co., Ltd.
* Skardin Industrial Corp.
* Sky Deutschland Fernsehen GmbH & Co. KG
* SmarDTV S.A.
* SoftAtHome
* Sony Corporation
* TCL Overseas Marketing (Macao Commercial Offshore) Limited
* Technicolor Delivery Technologies, SAS
* Tongfang Global Ltd.
* Top Victory Investments, Ltd.
* Toshiba Lifestyle Products & Services Corporation
* Universal Media Corporation /Slovakia/ s.r.o.
* VIZIO, Inc.
* Wistron Corporation
* ZTE Corporation


## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

