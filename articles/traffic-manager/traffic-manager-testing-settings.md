---
title: "configurações do Azure Traffic Manager aaaVerify | Microsoft Docs"
description: "Este artigo ajudará você a verificar as configurações do Gerenciador de Tráfego"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 2180b640-596e-4fb2-be59-23a38d606d12
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: c670be6cf55e140c7ab63d5d526de08e14774d2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="verify-traffic-manager-settings"></a>Verificar as configurações do Gerenciador de Tráfego

tootest as configurações do Gerenciador de tráfego, você precisa toohave vários clientes, em vários locais, do qual você pode executar os testes. Em seguida, colocar pontos de extremidade de saudação em seu perfil do Traffic Manager um de cada vez.

* Baixo Olá valor de TTL do DNS para que as alterações se propagam rapidamente (por exemplo, 30 segundos).
* Conheça Olá endereços IP dos seus serviços de nuvem do Azure e sites no perfil de saudação que você está testando.
* Use as ferramentas que permitem resolver um endereço IP de tooan de nome DNS e exibem esse endereço.

Você está verificando toosee nomes DNS Olá resolver endereços tooIP de pontos de extremidade de saudação em seu perfil. nomes de saudação devem resolver de maneira consistente com o método de roteamento de tráfego do hello definido no perfil do Gerenciador de tráfego de saudação. Você pode usar ferramentas hello como **nslookup** ou **se aprofundar** tooresolve nomes DNS.

Olá exemplos a seguir ajudarão a testar seu perfil do Gerenciador de tráfego.

### <a name="check-traffic-manager-profile-using-nslookup-and-ipconfig-in-windows"></a>Verifique o perfil do Gerenciador de Tráfego usando nslookup e ipconfig no Windows

1. Abra um prompt de comando ou do Windows PowerShell como administrador.
2. Tipo `ipconfig /flushdns` tooflush Olá cache do resolvedor de DNS.
3. Digite `nslookup <your Traffic Manager domain name>`. Por exemplo, Olá Olá de verificações de nome de domínio com prefixo de saudação do comando a seguir *myapp.contoso*

        nslookup myapp.contoso.trafficmanager.net

    Um resultado típico mostra Olá informações a seguir:

    + Olá nome DNS e endereço IP do hello DNS server que está sendo acessado tooresolve esse nome de domínio do Traffic Manager.
    + nome de domínio do Traffic Manager Olá que você digitou na linha de comando Olá após "nslookup" e o domínio do hello IP endereço toowhich saudação do Traffic Manager resolve. Olá segundo endereço IP é Olá toocheck de um importante. Ele deve corresponder a um endereço IP (VIP) virtual público para um dos serviços de nuvem hello ou sites no hello perfil do Traffic Manager que você está testando.

## <a name="how-tootest-hello-failover-traffic-routing-method"></a>Como o método de roteamento de tráfego tootest Olá failover

1. Deixe todos os pontos de extremidade ativados.
2. Usando um único cliente, solicite a resolução de DNS para o nome de domínio da empresa usando nslookup ou um utilitário semelhante.
3. Certifique-se de que Olá resolvido endereço IP corresponde o ponto de extremidade primário hello.
4. Desativar o ponto de extremidade primário ou remova Olá monitoramento de arquivo para que o Traffic Manager pense que Olá aplicativo está inativo.
5. Aguarde Olá DNS Time-to-Live (TTL) do perfil do Traffic Manager hello mais mais dois minutos. Por exemplo, se a TTL do DNS for de 300 segundos (cinco minutos), você deverá aguardar por sete minutos.
6. Libere o cache de seu cliente DNS e solicite a resolução do DNS usando nslookup. No Windows, você pode liberar o cache DNS com o comando Olá ipconfig /flushdns.
7. Certifique-se de que Olá resolver o endereço IP corresponde a seu ponto de extremidade secundário.
8. Repita o processo de hello, interrompa a cada ponto de extremidade por sua vez. Verifique se que Olá DNS retorna o endereço IP de saudação do próximo ponto de extremidade de saudação na lista de saudação. Quando todos os pontos de extremidade estiverem desativados, você deverá obter o endereço IP de saudação do ponto de extremidade primário Olá novamente.

## <a name="how-tootest-hello-weighted-traffic-routing-method"></a>Como tootest Olá ponderada método de roteamento de tráfego

1. Deixe todos os pontos de extremidade ativados.
2. Usando um único cliente, solicite a resolução de DNS para o nome de domínio da empresa usando nslookup ou um utilitário semelhante.
3. Certifique-se de que Olá resolver o endereço IP corresponde a um dos seus pontos de extremidade.
4. Libere o cache do cliente DNS e repita as etapas 2 e 3 para cada ponto de extremidade. Você deverá ver diferentes endereços IP retornados para cada um de seus pontos de extremidade.

## <a name="how-tootest-hello-performance-traffic-routing-method"></a>Como método de roteamento de tráfego de desempenho de saudação tootest

tooeffectively teste um método de roteamento de tráfego de desempenho, você deve ter clientes localizados em diferentes partes do Olá, mundo. Você pode criar clientes em diferentes regiões do Azure que podem ser usado tootest seus serviços. Se você tiver uma rede global, você pode entrar tooclients em outras partes do Olá, mundo e executar os testes a partir daí remotamente.

Como alternativa, há serviços gratuitos e disponíveis de dig e pesquisa de DNS baseados na Web. Algumas dessas ferramentas permitem Olá capacidade toocheck nomes DNS de vários locais ao redor Olá, mundo. Pesquise "Pesquisa de DNS" para obter exemplos. Serviços de terceiros como, Gomez ou Keynote podem ser usado tooconfirm que os perfis estão distribuindo tráfego conforme o esperado.

## <a name="next-steps"></a>Próximas etapas

* [Sobre os métodos de roteamento de tráfego do Gerenciador de Tráfego](traffic-manager-routing-methods.md)
* [Considerações sobre desempenho do Gerenciador de Tráfego](traffic-manager-performance-considerations.md)
* [Solucionando problemas de estado degradado do Gerenciador de Tráfego](traffic-manager-troubleshooting-degraded.md)
