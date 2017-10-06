---
title: aaaGetting iniciado com a CDN do Azure | Microsoft Docs
description: "Este tópico mostra como tooenable hello Azure Content Delivery Network (CDN). tutorial de saudação orienta na criação de saudação de um novo perfil CDN e o ponto de extremidade."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 4ca51224-5423-419b-98cf-89860ef516d2
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 0ce9802bfd7b60e70a9a62330f5593fc17ea07d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-cdn"></a>Introdução à CDN do Azure
Este tópico explica a habilitação do Azure CDN por meio da criação de um novo perfil e um ponto de extremidade CDN.

> [!IMPORTANT]
> Para um Introdução toohow o CDN works, bem como uma lista de recursos, consulte Olá [visão geral da CDN](cdn-overview.md).
> 
> 

## <a name="create-a-new-cdn-profile"></a>Criar um novo perfil CDN
Um perfil CDN é um conjunto de pontos de extremidade CDN.  Cada perfil contém um ou mais pontos de extremidade CDN.  Você poderá toouse tooorganize de vários perfis seus pontos de extremidade CDN, o domínio da internet, aplicativo web ou algum outro critério.

> [!NOTE]
> Por padrão, uma única assinatura do Azure é limitado tooeight perfis CDN. Cada perfil CDN é limitado tooten pontos de extremidade CDN.
> 
> Preços de CDN é aplicada no nível de perfil CDN hello. Se você desejar toouse uma mistura de CDN do Azure camadas de preços, você precisará vários perfis CDN.
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a>Criar um novo ponto final de CDN
**toocreate um novo ponto de extremidade CDN**

1. Em Olá [Portal do Azure](https://portal.azure.com), navegar tooyour perfil CDN.  Você pode ter-fixado toohello painel na etapa anterior hello.  Se você não, você pode encontrá-lo clicando **procurar**, em seguida, **perfis CDN**, e clicando no perfil Olá planejar tooadd seu ponto de extremidade.
   
    folha de perfil CDN Olá aparece.
   
    ![Perfil CDN][cdn-profile-settings]
2. Clique em Olá **Adicionar ponto de extremidade** botão.
   
    ![Adicionar botão de ponto de extremidade][cdn-new-endpoint-button]
   
    Olá **adicionar um ponto de extremidade** folha é exibida.
   
    ![Adicionar folha de ponto de extremidade][cdn-add-endpoint]
3. Insira um **Nome** para esse ponto de extremidade CDN.  Esse nome será usado tooaccess seus recursos armazenados em cache no domínio Olá `<endpointname>.azureedge.net`.
4. Em Olá **tipo de origem** lista suspensa, selecione o tipo de origem.  Selecione **Armazenamento** para uma conta de armazenamento do Azure, **Serviço de nuvem** para um Serviço de Nuvem do Azure, **Aplicativo Web** para um Aplicativo Web do Azure ou **Origem personalizada** para qualquer outra origem de servidor Web acessível publicamente (hospedado no Azure ou em outro lugar).
   
    ![Tipo de origem CDN](./media/cdn-create-new-endpoint/cdn-origin-type.png)
5. Em Olá **nome de host de origem** lista suspensa, selecione ou digite o domínio de origem.  Olá suspensa listará todas as origens disponíveis do tipo hello especificada na etapa 4.  Se você selecionou *origem personalizado* como seu **tipo de origem**, você digitará no domínio de saudação de sua origem personalizada.
6. Em Olá **caminho de origem** texto, digite Olá caminho toohello recursos desejados toocache ou deixe em branco tooallow cache qualquer recurso no domínio Olá especificado na etapa 5.
7. Em Olá **cabeçalho de host de origem**, insira o cabeçalho de host Olá deseja Olá CDN toosend com cada solicitação ou deixe o padrão de saudação.
   
   > [!WARNING]
   > Alguns tipos de origens, como o armazenamento do Azure e os aplicativos Web, exigem domínio Olá host cabeçalho toomatch Olá de origem hello. A menos que você tenha uma origem que requer um cabeçalho de host diferente do seu domínio, você deve deixar o valor padrão de saudação.
   > 
   > 
8. Para **protocolo** e **porta de origem**, especificar Olá protocolos e portas tooaccess usado seus recursos na origem de saudação.  É necessário selecionar pelo menos um protocolo (HTTP ou HTTPS).
   
   > [!NOTE]
   > Olá **porta de origem** afeta somente o ponto de extremidade de saudação de porta usa as informações de tooretrieve de origem hello.  Olá ponto de extremidade em si será apenas clientes tooend disponível em saudação padrão portas HTTP e HTTPS (80 e 443), independentemente de saudação **porta de origem**.  
   > 
   > **Azure CDN do Akamai** pontos de extremidade não permitem a gama porta TCP de saudação completa para origens.  Para obter uma lista das portas de origem que não são permitidas, confira [CDN do Azure das Portas de Origem Permitidas Akamai](https://msdn.microsoft.com/library/mt757337.aspx).  
   > 
   > Acessar o CDN conteúdo usando HTTPS tem Olá restrições a seguir:
   > 
   > * Você deve usar o certificado SSL Olá fornecido pelo Olá CDN. Não há suporte a certificados de terceiros.
   > * Você deve usar o domínio fornecido CDN de saudação (`<endpointname>.azureedge.net`) tooaccess conteúdo em HTTPS. Suporte ao protocolo HTTPS não está disponível para nomes de domínio personalizados (CNAMEs) como Olá CDN não oferece suporte a certificados personalizados no momento.
   > 
   > 
9. Clique em Olá **adicionar** toocreate botão Olá novo ponto de extremidade.
10. Depois que o ponto de extremidade de saudação é criado, ele aparece em uma lista de pontos de extremidade para o perfil de saudação. modo de exibição de lista Olá mostra Olá URL toouse tooaccess em cache o conteúdo, bem como domínio de origem de saudação.
    
    ![Ponto de extremidade CDN][cdn-endpoint-success]
    
    > [!IMPORTANT]
    > ponto de extremidade de saudação não estará disponível imediatamente para uso, como demora Olá toopropagate de registro por meio de saudação CDN.  Para <b>Azure CDN do Akamai</b> , a propagação geralmente é concluída em um minuto.  Para perfis da <b>CDN do Azure da Verizon</b>, a propagação geralmente é concluída em 90 minutos, mas em alguns casos pode levar mais tempo.
    > 
    > Os usuários que tentarem nome de domínio toouse Olá CDN antes de configuração de ponto de extremidade Olá propagou toohello POPs receberá códigos de resposta HTTP 404.  Se passaram várias horas desde que você criou o ponto de extremidade e ainda está recebendo respostas 404, consulte [Solucionando problemas dos pontos de extremidade CDN retornando status 404](cdn-troubleshoot-endpoint.md).
    > 
    > 

## <a name="see-also"></a>Consulte também
* [Controle do comportamento do cache de solicitações com cadeias de caracteres de consulta](cdn-query-string.md)
* [Como tooMap conteúdo CDN tooa domínio personalizado](cdn-map-content-to-custom-domain.md)
* [Pré-carregar ativos em um ponto de extremidade da CDN do Azure](cdn-preload-endpoint.md)
* [Limpar um ponto de extremidade CDN do Azure](cdn-purge-endpoint.md)
* [Solucionando problemas dos pontos de extremidade CDN retornando status 404](cdn-troubleshoot-endpoint.md)

[cdn-profile-settings]: ./media/cdn-create-new-endpoint/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-create-new-endpoint/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-create-new-endpoint/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-create-new-endpoint/cdn-endpoint-success.png
