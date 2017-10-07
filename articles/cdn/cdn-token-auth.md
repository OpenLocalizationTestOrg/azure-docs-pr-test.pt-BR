---
title: "ativos do Azure CDN aaaSecuring com autenticação de token | Microsoft Docs"
description: "Usando a autenticação de token toosecure acessar tooyour Azure CDN ativos."
services: cdn
documentationcenter: .net
author: zhangmanling
manager: zhangmanling
editor: 
ms.assetid: 837018e3-03e6-4f9c-a23e-4b63d5707a64
ms.service: cdn
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 11/11/2016
ms.author: mezha
ms.openlocfilehash: 5865bcb8eed7ced834970d52d30136252039265f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-azure-cdn-assets-with-token-authentication"></a>Proteger ativos da CDN do Azure com autenticação de token

[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

##<a name="overview"></a>Visão geral

Autenticação de token é um mecanismo que permite que você tooprevent CDN do Azure que serve o toounauthorized clientes ativos.  Isso geralmente é feito tooprevent "hotlinking" de conteúdo, em que um site diferente, geralmente um quadro de mensagens usa seus ativos sem permissão.  Isso pode ter um impacto sobre os custos de fornecimento de conteúdo. Ao ativar esse recurso em CDN, as solicitações serão autenticadas pela borda da CDN POPs antes de entregar conteúdo de saudação. 

## <a name="how-it-works"></a>Como ele funciona

Autenticação de token verifica solicitações são geradas por um site confiável, exigindo solicitações toocontain um valor de token que contém informações codificadas sobre solicitante hello. Conteúdo somente será servido toorequester Olá codificados requisitos de saudação atenda às informações, caso contrário solicitações serão negadas. Você pode configurar o requisito de saudação usando um ou vários parâmetros abaixo.

- País: permitir ou negar solicitações originadas de países especificados.  [Lista de códigos de país válidos.](https://msdn.microsoft.com/library/mt761717.aspx) 
- URL: apenas permita toorequest ativo ou o caminho especificado.  
- Host: permitir ou negar as solicitações de hosts especificados no cabeçalho de solicitação de saudação.
- Referenciador: permitir ou negar toorequest referenciador especificado.
- Endereço IP: permitir somente solicitações originadas de determinado endereço IP ou sub-rede IP.
- Protocolo: permitir ou bloquear solicitações com base no protocolo hello usado toorequest conteúdo de saudação.
- Tempo de expiração: atribuir uma data e hora tooensure período que um link só permanece válido por um período de tempo limitado.

Confira o exemplo de configuração detalhado de cada parâmetro.

## <a name="reference-architecture"></a>Arquitetura de referência

Veja abaixo uma arquitetura de referência de configuração de autenticação de token em toowork CDN com seu aplicativo Web.

![botão gerenciar da folha Perfil CDN](./media/cdn-token-auth/cdn-token-auth-workflow2.png)

## <a name="token-validation-logic-on-cdn-endpoint"></a>Lógica de validação de token no ponto de extremidade da CDN
    
Este gráfico descreve como a CDN do Azure valida a solicitação do cliente quando a autenticação de token é configurada no ponto de extremidade da CDN.

![botão gerenciar da folha Perfil CDN](./media/cdn-token-auth/cdn-token-auth-validation-logic.png)

## <a name="setting-up-token-authentication"></a>Configurar autenticação de token

1. De saudação [portal do Azure](https://portal.azure.com), navegue perfil CDN tooyour e, em seguida, clique em Olá **gerenciar** portal suplementar do botão toolaunch hello.

    ![botão gerenciar da folha Perfil CDN](./media/cdn-rules-engine/cdn-manage-btn.png)

2. Passe o mouse sobre **HTTP grande**e, em seguida, clique em **autenticação de Token** no submenu hello. Você definirá a chave de criptografia e os parâmetros de criptografia nessa guia.

    1. Insira uma chave de criptografia exclusiva para **Primary Key**.  Insira outra para **Chave de Backup**

        ![Chave de configuração de autenticação de token da CDN](./media/cdn-token-auth/cdn-token-auth-setupkey.png)
    
    2. Configure os parâmetros de criptografia com a ferramenta de criptografia (permitir ou negar solicitações com base no tempo de expiração, país, referenciador, protocolo, IP do cliente. Você pode usar qualquer combinação.)

        ![botão gerenciar da folha Perfil CDN](./media/cdn-token-auth/cdn-token-auth-encrypttool.png)

        - ec-expirer: atribui um tempo de expiração de um token após um período de tempo especificado. Solicitações enviadas depois que o tempo de expiração de saudação será negado. Esse parâmetro usa o carimbo de data/hora do Unix (com base em segundos desde a época padrão de 1/1/1970 00:00:00 GMT. Você pode usar conversão de tooprovide ferramentas online entre hora padrão e Unix.)  Por exemplo, se desejar tooset toobe token Olá expirou em 31/12/2016 12:00:00 GMT, use Olá Unix tempo: 1483185600 como abaixo:
    
        ![botão gerenciar da folha Perfil CDN](./media/cdn-token-auth/cdn-token-auth-expire2.png)
    
        - permitir a url de EC: permite que você ativo em particular tootailor tokens tooa ou caminho. Ela restringe o acesso toorequests cuja URL começar com um caminho relativo específico. Você pode inserir vários caminhos, separando cada caminho com uma vírgula. URLs diferenciam maiúsculas de minúsculas. Dependendo do requisito de saudação, você pode configurar diferentes valor tooprovide diferentes níveis de acesso. Abaixo estão alguns cenários:
        
            Se você tiver uma URL: http://www.mydomain.com/pictures/city/strasbourg.png. Confira o valor de entrada "" e o nível de acesso correspondente

            1. Valor de entrada "/": todas as solicitações serão permitidas
            2. Valor de entrada "/ imagens": Olá todas as solicitações a seguir permitirá
            
                - http://www.mydomain.com/pictures.png
                - http://www.mydomain.com/pictures/city/strasbourg.png
                - http://www.mydomain.com/picturesnew/city/strasbourgh.png
            3. Valor de entrada "/pictures/": somente as solicitações de /pictures/ serão permitidas
            4. Valor de entrada "/pictures/city/strasbourg.png": só permite a solicitação para este ativo
    
        ![botão gerenciar da folha Perfil CDN](./media/cdn-token-auth/cdn-token-auth-url-allow4.png)
    
        - ec-country-allow: permite somente solicitações originadas de um ou mais países especificados. Solicitações originadas em todos os outros países serão negadas. Use tooset de código de país parâmetros hello e separando cada código de país com uma vírgula. Por exemplo, se você desejar acesso de tooallow de Estados Unidos e França, entrada US, FR na coluna hello como abaixo.  
        
        ![botão gerenciar da folha Perfil CDN](./media/cdn-token-auth/cdn-token-auth-country-allow.png)

        - ec-country-deny: nega solicitações originadas de um ou mais países especificados. Solicitações originadas em todos os outros países serão permitidas. Use tooset de código de país parâmetros hello e separando cada código de país com uma vírgula. Por exemplo, se você desejar acesso de toodeny de Estados Unidos e França, entrada US, FR na coluna hello.
    
        - ec-ref-allow: permite solicitações da referência especificada. Uma referência identifica Olá URL da página da web de saudação que toohello recurso que está sendo solicitado vinculado. o valor do parâmetro Hello referenciador não deve incluir o protocolo de saudação. Você pode inserir um nome de host e/ou um caminho específico no nome do host. Você também pode adicionar vários referenciadores em um único parâmetro, separando cada um com uma vírgula. Se você especificou um valor de referência, mas Olá referenciador não são enviadas na solicitação Olá devido a configuração do navegador toosome, essas solicitações serão negadas por padrão. Você pode atribuir "Missing" ou um valor em branco no hello parâmetro tooallow essas solicitações com informações do referenciador ausentes. Você também pode usar "*. consoto.com" tooallow todos os subdomínios de consoto.com.  Por exemplo, se você desejar acesso de tooallow para solicitações de www.consoto.com, todos os subdomínios em consoto2.com e erquests com reffers em branco ou ausentes, valor de entrada abaixo:
        
        ![botão gerenciar da folha Perfil CDN](./media/cdn-token-auth/cdn-token-auth-referrer-allow2.png)
    
        - ec-ref-deny: nega solicitações da referência especificada. Consulte o exemplo no parâmetro "ec-ref-permitir" e toodetails.
         
        - ec-proto-allow: permite somente solicitações do protocolo especificado. Por exemplo, http ou https.
        
        ![botão gerenciar da folha Perfil CDN](./media/cdn-token-auth/cdn-token-auth-url-allow4.png)
            
        - ec-proto-deny: nega solicitações do protocolo especificado. Por exemplo, http ou https.
    
        - clientip EC: restringe o endereço IP do solicitante do acesso toospecified. Há suporte para IPV4 e IPV6. Você pode especificar o endereço IP de solicitação única ou sub-rede IP.
            
        ![botão gerenciar da folha Perfil CDN](./media/cdn-token-auth/cdn-token-auth-clientip.png)
        
    3. Você pode testar seu token com a ferramenta de descrição de saudação.

    4. Você também pode personalizar o tipo hello da resposta será retornado toouser quando a solicitação será negada. Por padrão, usamos 403.

3. Agora, clique na guia **Mecanismo de Regras** em **HTTP Grande**. Você será usar esse recurso de saudação do guia toodefine caminhos tooapply, habilitar o recurso de autenticação de token hello e habilitar autenticação de token adicional relacionadas a recursos.

    - Use caminho que deseja que a autenticação de token tooapply ou ativo de toodefine de coluna "IF". 
    - Clique em tooadd "Autenticação de Token" de autenticação de token do hello recurso suspensa tooenable.
        
    ![botão gerenciar da folha Perfil CDN](./media/cdn-token-auth/cdn-rules-engine-enable2.png)

4. Em Olá **mecanismo de regras** guia, há alguns recursos adicionais, você pode habilitar.
    
    - Código de negação de autenticação de token: determina o tipo de saudação da resposta será retornado toouser quando uma solicitação é negada. As regras definidas aqui substituirá a configuração de código de negação de saudação na guia de autenticação de token hello.
    - Autenticação de token ignorar: determina se o token de toovalidate URL usada será diferencia maiusculas de minúsculas.
    - O parâmetro de token de autenticação: renomear consulta de autenticação de token Olá URL do parâmetro de cadeia de caracteres mostrando Olá solicitado. 
        
    ![botão gerenciar da folha Perfil CDN](./media/cdn-token-auth/cdn-rules-engine2.png)

5. Você pode personalizar o token, que é um aplicativo que gera um token para recursos de autenticação com base em token. O código-fonte pode ser acessado aqui no [GitHub](https://github.com/VerizonDigital/ectoken).
Os idiomas disponíveis incluem:
    
    - C
    - C#
    - PHP
    - Perl
    - Java
    - Python    


## <a name="azure-cdn-features-and-provider-pricing"></a>Preços de provedor e recursos da Azure CDN

Consulte Olá [visão geral da CDN](cdn-overview.md) tópico.
