---
title: "condições de mecanismo de correspondência de regras aaaAzure CDN | Microsoft Docs"
description: "Documentação de referência para recursos e condições de correspondência do mecanismo de regras da CDN do Azure."
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 5e79f8f0c75a646e13bf315c492b9f2a9defc396
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-match-conditions"></a>Condições de correspondência do mecanismo de regras da CDN do Azure
Este tópico lista descrições detalhadas Olá condições de correspondência disponíveis para o Azure Content Delivery Network (CDN) [mecanismo de regras](cdn-rules-engine.md).

Olá segunda parte de uma regra é condição de correspondência de saudação. Uma condição de correspondência identifica tipos específicos de solicitações para os quais um conjunto de recursos será executado.

Por exemplo, pode ser solicitações toofilter usado para o conteúdo em um local específico, solicitações geradas de um endereço IP ou o país específico, ou por informações de cabeçalho.

## <a name="always"></a>Sempre

Olá, condição de correspondência sempre é projetado tooapply definir um padrão de solicitações de tooall de recursos.

## <a name="device"></a>Dispositivo

condição de correspondência de dispositivo Olá identifica solicitações feitas em um dispositivo móvel com base em suas propriedades.  A detecção de dispositivos móveis é alcançada por meio de [WURFL](http://wurfl.sourceforge.net/).  Os recursos do WURFL e suas variáveis de mecanismo de regras de CDN estão listados abaixo.

> [!NOTE] 
> Olá variáveis abaixo têm suporte em Olá **cabeçalho de solicitação de cliente modificar** e **cabeçalho de resposta de cliente modificar** recursos.

Recurso | Variável | Descrição | Valor(es) de exemplo
-----------|----------|-------------|----------------
Nome da marca | %{wurfl_cap_brand_name} | Uma cadeia de caracteres que indica o nome da marca de saudação do dispositivo hello. | Samsung
SO do dispositivo | %{wurfl_cap_device_os} | Uma cadeia de caracteres que indica o sistema operacional de saudação instalado no dispositivo de saudação. | IOS
Versão do SO do dispositivo | %{wurfl_cap_device_os_version} | Uma cadeia de caracteres que indica o número de versão de saudação do hello SO instalado no dispositivo de saudação. | 1.0.1
Orientação dupla | %{wurfl_cap_dual_orientation} | Um booliano que indica se o dispositivo Olá suporta orientação dupla. | verdadeiro
DTD preferencial HTML | %{wurfl_cap_html_preferred_dtd} | Uma cadeia de caracteres que indica a definição de tipo do dispositivo móvel Olá preferencial de documento (DTD) para conteúdo HTML. | nenhum<br/>xhtml_basic<br/>html5
Inlining de Imagem | %{wurfl_cap_image_inlining} | Um valor booleano que indica se o dispositivo Olá suporta Base64 codificada em imagens. | false
É Android | %{wurfl_vcap_is_android} | Um booliano que indica se o dispositivo Olá usa Olá sistema operacional Android. | verdadeiro
É IOS | %{wurfl_vcap_is_ios} | Um booliano que indica se o dispositivo Olá usa iOS. | false
É Smart TV | %{wurfl_cap_is_smarttv} | Um booliano que indica se o dispositivo de saudação é uma TV inteligente. | false
É Smartphone | %{wurfl_vcap_is_smartphone} | Um booliano que indica se o dispositivo de saudação é um smartphone. | verdadeiro
É Tablet | %{wurfl_cap_is_tablet} | Um booliano que indica se o dispositivo de saudação é um tablet. Esta é uma descrição independente de sistema operacional. | verdadeiro
É dispositivo sem fio | %{wurfl_cap_is_wireless_device} | Um booliano que indica se o dispositivo de saudação é considerado um dispositivo sem fio. | verdadeiro
Nome de marketing | %{wurfl_cap_marketing_name} | Uma cadeia de caracteres que indica o nome de marketing do dispositivo hello. | BlackBerry 8100 Pearl
Navegador de dispositivo móvel | %{wurfl_cap_mobile_browser} | Uma cadeia de caracteres que indica o navegador Olá usado toorequest conteúdo de dispositivo de saudação. | Chrome
Versão do navegador móvel | %{wurfl_cap_mobile_browser_version} | Uma cadeia de caracteres que indica a versão de saudação do navegador Olá usado toorequest conteúdo de dispositivo de saudação. | 31
Nome do modelo | %{wurfl_cap_model_name} | Uma cadeia de caracteres que indica o nome do modelo do dispositivo hello. | s3
Download progressivo | %{wurfl_cap_progressive_download} | Um booliano que indica se o dispositivo Olá oferece suporte a reprodução de áudio/vídeo Olá enquanto ele ainda está sendo baixado. | verdadeiro
Data do lançamento | %{wurfl_cap_release_date} | Uma cadeia de caracteres que indica o ano de saudação e o mês no qual Olá dispositivo foi adicionado o banco de dados do toohello WURFL.<br/><br/>Formato: `yyyy_mm` | 2013_december
Altura de resolução | %{wurfl_cap_resolution_height} | Um inteiro que indica a altura do dispositivo Olá em pixels. | 768
Largura de resolução | %{wurfl_cap_resolution_width} | Um inteiro que indica a largura do dispositivo Olá em pixels. | 1024


## <a name="location"></a>Local

Eles correspondem condições solicitações tooidentify projetado com base na localização do solicitante hello.

Nome | Finalidade
-----|--------
Número AS | Identifica solicitações originadas de uma rede específica.
País | Identifica solicitações originadas de saudação especificada países.


## <a name="origin"></a>Origem

Eles coincidem com as condições são projetadas tooidentify solicitações que o armazenamento tooCDN ponto ou um servidor de origem do cliente.

Nome | Finalidade
-----|--------
Origem CDN | Identifica solicitações de conteúdo armazenado no armazenamento CDN.
Origem do Cliente | Identifica solicitações de conteúdo armazenado em um servidor de origem do cliente específico.


## <a name="request"></a>Solicitação

Eles coincidem com as condições são solicitações de tooidentify projetado com base em suas propriedades.

Nome | Finalidade
-----|--------
Endereço IP do Cliente | Identifica solicitações originadas de um endereço IP específico.
Parâmetro de Cookie | Verificações de Olá cookies associados a cada solicitação de saudação especificada valor.
Regex de Parâmetro de Cookie | Verifica cookies Olá associados com cada solicitação de saudação especificado de expressão regular.
Cname de Borda | Identifica solicitações de ponto de extremidade específico de tooa CNAME.
Domínio de Referência | Identifica as solicitações eram chamadas de saudação especificado hostname(s).
Literal de Cabeçalho de Solicitação | Identifica as solicitações que contenham Olá especificado tooa de conjunto de cabeçalho especificado valor (es).
Regex do Cabeçalho da Solicitação | Identifica as solicitações que contenham Olá especificado cabeçalho defina tooa o valor que corresponde a saudação especificado de expressão regular.
Curinga de Cabeçalho de Solicitação | Identifica as solicitações que contenham Olá especificado cabeçalho definido o valor de tooa que corresponda ao padrão especificado hello.
Método de Solicitação | Identifica solicitações pelo método HTTP.
Esquema de Solicitação | Identifica solicitações pelo protocolo HTTP.

## <a name="url"></a>URL

Eles correspondem condições solicitações tooidentify projetado com base em suas URLs.

Nome | Finalidade
-----|--------
Diretório do Caminho da URL | Identifica solicitações pelo caminho relativo.
Extensão do Caminho da URL | Identifica solicitações pela extensão de nome do arquivo.
Nome do Arquivo do Caminho da URL | Identifica solicitações pelo nome do arquivo
Literal do Caminho da URL | Compara uma solicitação do caminho relativo toohello valor especificado.
Regex do Caminho da URL | Compara uma solicitação do toohello de caminho relativo especificado expressão regular.
Curinga do Caminho da URL | Compara o padrão especificado do toohello da solicitação, um caminho relativo.
Literal da Consulta da URL | Compara uma solicitação do toohello de cadeia de caracteres de consulta valor especificado.
Parâmetro da Consulta da URL | Identifica as solicitações que contêm a consulta especificada hello, parâmetro de cadeia de caracteres definida tooa valor que corresponde a um padrão especificado.
Regex da consulta da URL | Identifica as solicitações que contêm a consulta especificada hello, parâmetro de cadeia de caracteres definido tooa valor que corresponde a uma expressão regular especificada.
Curinga da consulta da URL | Olá compara especificado valor (es) em relação a cadeia de caracteres de consulta da solicitação hello.


## <a name="next-steps"></a>Próximas etapas
* [Visão geral da CDN do Azure](cdn-overview.md)
* [Referência do Mecanismo de Regras](cdn-rules-engine-reference.md)
* [Expressões condicionais do Mecanismo de regras](cdn-rules-engine-reference-conditional-expressions.md)
* [Recursos do Mecanismo de regras](cdn-rules-engine-reference-features.md)
* [Substituindo o comportamento HTTP padrão usando o mecanismo de regras de saudação](cdn-rules-engine.md)

