---
title: pontos de extremidade do Azure CDN aaaTroubleshooting retornando status 404 | Microsoft Docs
description: "Solucione problemas nos códigos de resposta 404 com pontos de extremidade da CDN do Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: b588a1eb-ab69-4fc7-ae4d-157c3e46f4a8
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 450bfbd641c869cfd88169a12c4b69819eaa7c26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-cdn-endpoints-returning-404-statuses"></a>Solucionando problemas de pontos de extremidade CDN que retornam o status 404
Este artigo ajuda a solucionar problemas com [pontos de extremidade CDN](cdn-create-new-endpoint.md) que retornam erros 404.

Se você precisar de mais ajuda a qualquer momento neste artigo, você pode contatar hello Azure especialistas em [hello Azure MSDN e Olá fóruns de estouro de pilha](https://azure.microsoft.com/support/forums/). Como alternativa, você também pode registrar um incidente de suporte do Azure. Vá toohello [site de suporte do Azure](https://azure.microsoft.com/support/options/) e clique em **suporte**.

## <a name="symptom"></a>Sintoma
Você criou um perfil CDN e um ponto de extremidade, mas seu conteúdo não parece estar toobe disponível em Olá CDN.  Usuários que tentam tooaccess seu conteúdo por meio de saudação URL CDN receber códigos de status HTTP 404. 

## <a name="cause"></a>Causa
Há várias causas possíveis, incluindo:

* origem do arquivo Hello não está visível toohello CDN
* ponto de extremidade Hello está configurado incorretamente, causando Olá CDN toolook no local errado Olá
* host de saudação está rejeitando o cabeçalho de host de saudação do hello CDN
* ponto de extremidade de saudação não teve tempo toopropagate durante saudação CDN

## <a name="troubleshooting-steps"></a>Etapas para solucionar problemas
> [!IMPORTANT]
> Depois de criar um ponto de extremidade CDN, ele não estará disponível imediatamente para uso, como demora Olá toopropagate de registro por meio de saudação CDN.  Para perfis da <b>CDN do Azure da Akamai</b> , a propagação normalmente é concluída em um minuto.  Para perfis da <b>CDN do Azure da Verizon</b>, a propagação geralmente é concluída em 90 minutos, mas em alguns casos pode levar mais tempo.  Se você concluir as etapas de saudação neste documento e ainda obter 404 respostas, considere aguardar alguns toocheck de horas antes de abrir um tíquete de suporte.
> 
> 

### <a name="check-hello-origin-file"></a>Verifique o arquivo de origem Olá
Primeiro, deve verificar Olá arquivo hello queremos em cache está disponível em nosso origem e é acessível publicamente.  Olá toodo de maneira mais rápida que está tooopen um navegador em uma sessão em particular ou Incognito e navegar diretamente toohello arquivo.  Apenas digite ou cole a URL de saudação na caixa de endereço de hello e ver se que os resultados no arquivo hello esperado.  Neste exemplo, vou toouse um arquivo existente em uma conta de armazenamento do Azure, acessível no `https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`.  Como você pode ver, ele passa com êxito o teste de saudação.

![Sucesso!](./media/cdn-troubleshoot-endpoint/cdn-origin-file.png)

> [!WARNING]
> Enquanto isso é hello mais rápida e tooverify de maneira mais fácil o arquivo está disponível publicamente, algumas configurações de rede na sua organização podem dar a você Olá ilusão que esse arquivo está publicamente disponível quando é, na verdade, apenas visíveis toousers de sua rede ( mesmo se ele estiver hospedado no Azure).  Se você tiver um navegador externo do qual você pode testar, como um dispositivo móvel que não está conectado a rede da organização tooyour ou uma máquina virtual no Azure, que seria melhor.
> 
> 

### <a name="check-hello-origin-settings"></a>Verifique as configurações de origem de saudação
Agora que verificamos arquivo hello está disponível publicamente na internet de Olá, deve verificar as configurações de origem.  Em Olá [Portal do Azure](https://portal.azure.com), navegue perfil CDN tooyour e clique em ponto de extremidade de saudação estiver solucionando problemas.  Em Olá resultante **ponto de extremidade** folha, clique em origem hello.  

![Folha do ponto de extremidade com a origem realçada](./media/cdn-troubleshoot-endpoint/cdn-endpoint.png)

Olá **origem** folha é exibida. 

![Folha da origem](./media/cdn-troubleshoot-endpoint/cdn-origin-settings.png)

#### <a name="origin-type-and-hostname"></a>Tipo e nome do host da origem
Verifique se Olá **tipo de origem** está correto e verifique se Olá **nome de host de origem**.  No exemplo, `https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`, porção hostname de saudação do hello URL é `cdndocdemo.blob.core.windows.net`.  Como você pode ver na captura de tela hello, isso está correto.  Para o armazenamento do Azure, Web App e origens de serviço de nuvem, Olá **nome de host de origem** campo é uma lista suspensa, portanto, não precisamos tooworry sobre ortografia-la corretamente.  No entanto, se você estiver usando uma origem personalizada, será *importantíssimo* escrever o nome do host corretamente.

#### <a name="http-and-https-ports"></a>Portas HTTP e HTTPS
Olá outros toocheck coisa aqui é o **HTTP** e **portas HTTPS**.  Na maioria dos casos, as portas 80 e 443 estão corretas e não será necessária nenhuma alteração.  No entanto, se o servidor de origem hello está escutando em uma porta diferente, que será necessário toobe representada aqui.  Se você não tiver certeza, examine apenas Olá URL para o arquivo de origem.  Olá HTTP e especificações de HTTPS especificam portas 80 e 443 como Olá padrões. Na minha URL `https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`, uma porta não for especificada, portanto, Olá padrão de 443 será considerado e Minhas configurações estão corretas.  

No entanto, diga Olá URL para o arquivo de origem que você testou anteriormente é `http://www.contoso.com:8080/file.txt`.  Saudação de Observação `:8080` final de saudação do segmento de nome de host de saudação.  Que informa a porta do hello navegador toouse `8080` toohello de tooconnect para o servidor web, na `www.contoso.com`, portanto, você precisará tooenter 8080 no hello **porta HTTP** campo.  É importante toonote que essas configurações de porta afetam apenas o ponto de extremidade de saudação de porta usa as informações de tooretrieve de origem hello.

> [!NOTE]
> **Azure CDN do Akamai** pontos de extremidade não permitem a gama porta TCP de saudação completa para origens.  Para obter uma lista das portas de origem que não são permitidas, confira [CDN do Azure das Portas de Origem Permitidas Akamai](https://msdn.microsoft.com/library/mt757337.aspx).  
> 
> 

### <a name="check-hello-endpoint-settings"></a>Verifique as configurações de ponto de extremidade de saudação
Em Olá **ponto de extremidade** folha, clique em Olá **configurar** botão.

![Folha do ponto de extremidade com o botão Configurar realçado](./media/cdn-troubleshoot-endpoint/cdn-endpoint-configure-button.png)

Olá do ponto de extremidade **configurar** folha é exibida.

![Configurar folha](./media/cdn-troubleshoot-endpoint/cdn-configure.png)

#### <a name="protocols"></a>Protocolos
Para **protocolos**, verifique se está sendo usado por clientes de saudação do protocolo de saudação é selecionado.  Olá mesmo protocolo usado pelo cliente Olá será Olá um usado origem de saudação tooaccess, portanto, é importante toohave portas de origem de Olá configuradas corretamente na seção anterior hello.  ponto de extremidade Olá apenas ouve saudação padrão portas HTTP e HTTPS (80 e 443), independentemente das portas de origem hello.

Vamos retornar tooour de exemplo hipotético com `http://www.contoso.com:8080/file.txt`.  Como você se lembrará, a Contoso especificou `8080` como sua porta HTTP, mas suponhamos também que eles especificaram `44300` como sua porta HTTPS.  Se eles tiverem criado um ponto de extremidade chamado `contoso`, seu nome de host do ponto de extremidade de CDN será `contoso.azureedge.net`.  Uma solicitação para `http://contoso.azureedge.net/file.txt` é uma solicitação HTTP para o ponto de extremidade Olá usaria HTTP na porta 8080 tooretrieve-o de origem hello.  Uma solicitação segura por HTTPS, `https://contoso.azureedge.net/file.txt`, causaria Olá toouse de ponto de extremidade HTTPS na porta 44300 quando recuperar Olá arquivo de origem de saudação.

#### <a name="origin-host-header"></a>Cabeçalho de host de origem
Olá **cabeçalho de host de origem** é o valor do cabeçalho de host de saudação enviada toohello origem com cada solicitação.  Na maioria dos casos, isso deve ser Olá mesmo como Olá **nome de host de origem** verificamos anteriormente.  Um valor incorreto no campo geralmente não causará 404 status, mas é provável toocause outros status 4xx, dependendo de qual origem Olá espera.

#### <a name="origin-path"></a>Caminho de origem
Por fim, devemos verificar nosso **Caminho de origem**.  Por padrão, ele está em branco.  Você deve usar esse campo apenas se você quiser que o escopo de saudação toonarrow de recursos de host de origem Olá você deseja toomake disponível em Olá CDN.  

Por exemplo, no meu ponto de extremidade, queria que todos os recursos em meu toobe da conta de armazenamento disponível, portanto, à esquerda **caminho de origem** em branco.  Isso significa que uma solicitação muito`https://cdndocdemo.azureedge.net/publicblob/lorem.txt` resulta em uma conexão do meu ponto de extremidade muito`cdndocdemo.core.windows.net` que solicita `/publicblob/lorem.txt`.  Da mesma forma, uma solicitação para `https://cdndocdemo.azureedge.net/donotcache/status.png` resulta na solicitação de ponto de extremidade Olá `/donotcache/status.png` origem hello.

Mas e se eu não quero toouse Olá CDN para cada caminho em minha origem?  Dizer I apenas quisesse Olá tooexpose `publicblob` caminho.  Se inserir */publicblob* na minha **caminho de origem** campo, o que fará com que tooinsert de ponto de extremidade Olá */publicblob* antes de cada solicitação que está sendo feita toohello origem.  Isso significa que essa solicitação Olá para `https://cdndocdemo.azureedge.net/publicblob/lorem.txt` agora levará realmente Olá solicitação porção de saudação URL, `/publicblob/lorem.txt`e acrescente `/publicblob` toohello início. Isso resulta em uma solicitação de `/publicblob/publicblob/lorem.txt` origem hello.  Se esse caminho não resolver tooan real do arquivo, origem Olá retorna um status 404.  Olá correto URL tooretrieve lorem.txt neste exemplo, na verdade, seria `https://cdndocdemo.azureedge.net/lorem.txt`.  Observe que não incluímos Olá */publicblob* caminho, como parte da solicitação de saudação do hello URL é `/lorem.txt` e o ponto de extremidade Olá adiciona `/publicblob`, resultando em `/publicblob/lorem.txt` sendo solicitação Olá passado toohello origem .

