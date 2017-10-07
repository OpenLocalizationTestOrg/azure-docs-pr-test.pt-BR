---
title: "domínio personalizado do conteúdo tooa aaaMap CDN do Azure | Microsoft Docs"
description: "Saiba como o domínio personalizado tooa de conteúdo toomap CDN do Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 289f8d9e-8839-4e21-b248-bef320f9dbfc
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: d3ee77297f1dd7dbf31a9391191cc2910fbd2cee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="map-azure-cdn-content-tooa-custom-domain"></a>Mapear o domínio personalizado do Azure CDN tooa conteúdo
Você pode mapear um ponto de extremidade CDN do domínio personalizado tooa em ordem toouse seu próprio nome de domínio em URLs toocached conteúdo em vez de usar um subdomínio de azureedge.net.

Há toomap de duas maneiras de domínio personalizado tooa ponto de extremidade CDN:

1. [Crie um registro CNAME com seu registrador de domínio e mapear seu domínio e subdomínio toohello CDN ponto de extremidade personalizado](#register-a-custom-domain-for-an-azure-cdn-endpoint).
   
    Um registro CNAME é um recurso DNS que mapeia um domínio de origem, como `www.contosocdn.com` ou `cdn.contoso.com`, tooa domínio de destino. Nesse caso, o domínio de origem de saudação é seu domínio e subdomínio personalizados (um subdomínio, como **www** ou **cdn** é sempre necessário). domínio de destino Olá é o ponto de extremidade CDN.  
   
    processo de saudação do mapeamento de domínio personalizado tooyour ponto de extremidade CDN no entanto, pode resultar em um breve período de tempo de inatividade para o domínio de saudação enquanto você estiver registrando o domínio de saudação em Olá Portal do Azure.
2. [Adicionar uma etapa de registro intermediária com **cdnverify**](#register-a-custom-domain-for-an-azure-cdn-endpoint-using-the-intermediary-cdnverify-subdomain)
   
    Se seu domínio personalizado no momento está dando suporte a um aplicativo com um contrato de nível de serviço (SLA) que não requer que não haja nenhum tempo de inatividade, você pode usar o hello Azure **cdnverify** tooprovide subdomínio um registro intermediário etapa para que os usuários serão tooaccess capaz de seu domínio durante Olá DNS mapeando ocorra.  

Depois de registrar seu domínio personalizado usando uma saudação acima procedimentos, você desejará muito[verificar esse subdomínio personalizado Olá faz referência a seu ponto de extremidade CDN](#verify-that-the-custom-subdomain-references-your-cdn-endpoint).

> [!NOTE]
> Você deve criar um registro CNAME com seu toomap do registrador de domínio domínio toohello ponto de extremidade CDN. Os registros CNAME mapeiam subdomínios específicos como `www.contoso.com` ou `cdn.contoso.com`. Não é possível toomap um domínio de raiz de tooa registro CNAME, como `contoso.com`.
> 
> Um subdomínio só pode ser associado a um ponto de extremidade da CDN. Olá registro CNAME que você cria roteará todo o tráfego endereçado toohello subdomínio toohello especificado o ponto de extremidade.  Por exemplo, se você associar `www.contoso.com` ao ponto de extremidade da sua CDN, não poderá associá-lo a outros pontos de extremidade do Azure, como um ponto de extremidade de conta de armazenamento ou um ponto de extremidade de serviço de nuvem. No entanto, você pode usar outros subdomínios de saudação mesmo domínio para pontos de extremidade de serviço diferente. Você também pode mapear outros subdomínios toohello mesmo ponto de extremidade CDN.
> 
> Para **CDN do Azure da Verizon** pontos de extremidade (Standard e Premium), observe que está ocupando muito**90 minutos** nós de borda tooCDN toopropagate alterações de domínio personalizado.
> 
> 

## <a name="register-a-custom-domain-for-an-azure-cdn-endpoint"></a>Registrar um domínio personalizado para um ponto de extremidade da CDN do Azure
1. Faça logon no hello [Portal do Azure](https://portal.azure.com/).
2. Clique em **procurar**, em seguida, **CDN perfis**, Olá, em seguida, o perfil CDN com ponto de extremidade Olá você deseja que o domínio personalizado do toomap tooa.  
3. Em Olá **perfil CDN** folha, clique em ponto de extremidade CDN Olá com a qual você deseja que o subdomínio de saudação tooassociate.
4. Na parte superior de saudação da folha de ponto de extremidade de saudação, clique em Olá **adicionar um domínio personalizado** botão.  Em Olá **adicionar um domínio personalizado** folha, você verá nome de host do ponto de extremidade hello, derivado do ponto de extremidade CDN, toouse na criação de um novo registro CNAME. formato de saudação do endereço de nome de host Olá aparecerá como  **&lt;EndpointName >. azureedge.net**.  Você pode copiar este toouse de nome de host na criação de registro CNAME hello.  
5. Navegue de site do registrador de domínio tooyour e localize a seção Olá para criar registros DNS. Você pode encontrá-lo em uma seção como **Nome de Domínio**, **DNS** ou **Gerenciamento de Servidor de Nomes**.
6. Localize seção Olá para gerenciar CNAMEs. Você pode ter a página de configurações avançadas de tooan toogo e procure palavras Olá CNAME, Alias ou subdomínios.
7. Criar um novo registro CNAME que mapeie o subdomínio escolhido (por exemplo, **www** ou **cdn**) toohello nome do host fornecido no hello **adicionar um domínio personalizado** folha. 
8. Retornar toohello **adicionar um domínio personalizado** folha e insira seu domínio personalizado, incluindo o subdomínio hello, na caixa de diálogo de saudação. Por exemplo, digite o nome de domínio Olá no formato de saudação `www.contoso.com` ou `cdn.contoso.com`.   
   
   Azure verificará a existência de registro de CNAME Olá Olá nome de domínio inserido. Se Olá CNAME estiver correto, seu domínio personalizado será validado.  Para **CDN do Azure da Verizon** pontos de extremidade (Standard e Premium), pode levar até too90 minutos para nós de borda do CDN tooall do domínio personalizado configurações toopropagate, no entanto.  
   
   Observe que, em alguns casos, ele pode levar tempo para Olá CNAME toopropagate registro tooname servidores em Olá Internet. Se o domínio não for validado imediatamente, e você acredita Olá registro CNAME está correto, em seguida, aguarde alguns minutos e tente novamente.

## <a name="register-a-custom-domain-for-an-azure-cdn-endpoint-using-hello-intermediary-cdnverify-subdomain"></a>Registrar um domínio personalizado para um ponto de extremidade CDN do Azure usando o subdomínio intermediário cdnverify de saudação
1. Faça logon no hello [Portal do Azure](https://portal.azure.com/).
2. Clique em **procurar**, em seguida, **CDN perfis**, Olá, em seguida, o perfil CDN com ponto de extremidade Olá você deseja que o domínio personalizado do toomap tooa.  
3. Em Olá **perfil CDN** folha, clique em ponto de extremidade CDN Olá com a qual você deseja que o subdomínio de saudação tooassociate.
4. Na parte superior de saudação da folha de ponto de extremidade de saudação, clique em Olá **adicionar um domínio personalizado** botão.  Em Olá **adicionar um domínio personalizado** folha, você verá nome de host do ponto de extremidade hello, derivado do ponto de extremidade CDN, toouse na criação de um novo registro CNAME. formato de saudação do endereço de nome de host Olá aparecerá como  **&lt;EndpointName >. azureedge.net**.  Você pode copiar este toouse de nome de host na criação de registro CNAME hello.
5. Navegue de site do registrador de domínio tooyour e localize a seção Olá para criar registros DNS. Você pode encontrá-lo em uma seção como **Nome de Domínio**, **DNS** ou **Gerenciamento de Servidor de Nomes**.
6. Localize seção Olá para gerenciar CNAMEs. Você pode ter a página de configurações avançadas de tooan toogo e procurar palavras Olá **CNAME**, **Alias**, ou **subdomínios**.
7. Criar um novo registro CNAME e forneça um alias de subdomínio que inclui a saudação **cdnverify** subdomínio. Por exemplo, o subdomínio de saudação que você especificar estará no formato de saudação **cdnverify.www** ou **cdnverify.cdn**. Forneça o nome de host hello, que é o ponto de extremidade CDN, no formato de saudação **cdnverify.&lt; EndpointName >. azureedge.net**. O mapeamento de DNS deve ser parecido com: `cdnverify.www.consoto.com   CNAME   cdnverify.consoto.azureedge.net`  
8. Retornar toohello **adicionar um domínio personalizado** folha e insira seu domínio personalizado, incluindo o subdomínio hello, na caixa de diálogo de saudação. Por exemplo, digite o nome de domínio Olá no formato de saudação `www.contoso.com` ou `cdn.contoso.com`. Observe que, nesta etapa, você precisa não subdomínio Olá toopreface **cdnverify**.  
   
    Azure verificará a existência de registro de CNAME Olá Olá cdnverify nome de domínio inserido.
9. Neste ponto, seu domínio personalizado foi verificado pelo Azure, mas o domínio tooyour do tráfego ainda não está sendo roteado tooyour ponto de extremidade CDN. Depois de aguardar longo o suficiente toopropagate de configurações de domínio personalizado de saudação tooallow toohello CDN borda nós (90 minutos para **CDN do Azure da Verizon**, 1 a 2 minutos para **Azure CDN do Akamai**), retornar tooyour DNS site do registrador e criar outro registro CNAME que mapeie o subdomínio tooyour ponto de extremidade CDN. Por exemplo, especifique o subdomínio Olá **www** ou **cdn**, e Olá hostname como  **&lt;EndpointName >. azureedge.net**. Com essa etapa, o registro de saudação do seu domínio personalizado está concluído.
10. Por fim, você pode excluir o registro CNAME Olá criado usando **cdnverify**, pois ele foi necessário apenas como uma etapa intermediária.  

## <a name="verify-that-hello-custom-subdomain-references-your-cdn-endpoint"></a>Verifique se que esse subdomínio personalizado Olá referencia seu ponto de extremidade CDN
* Depois de concluir o registro de saudação do seu domínio personalizado, você pode acessar o conteúdo armazenado em cache no ponto de extremidade CDN usando o domínio personalizado hello.
  Primeiro, certifique-se de que você tem conteúdo público armazenado em cache no ponto de extremidade de saudação. Por exemplo, se o ponto de extremidade CDN estiver associado uma conta de armazenamento, Olá CDN armazene conteúdo em cache em contêineres de blob público. domínio personalizado do tootest hello, certifique-se de que o contêiner está definido acesso público de tooallow e que ele contém pelo menos um blob.
* No seu navegador, navegue toohello endereço de blob hello usando o domínio personalizado hello. Por exemplo, se seu domínio personalizado é `cdn.contoso.com`, blob armazenado em cache do tooa Olá URL será semelhante toohello URL a seguir: http://cdn.contoso.com/mypubliccontainer/acachedblob.jpg

## <a name="see-also"></a>Consulte também
[Como tooEnable Olá Content Delivery Network (CDN) do Azure](cdn-create-new-endpoint.md)  

