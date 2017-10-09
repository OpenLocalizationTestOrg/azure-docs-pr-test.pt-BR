---
title: status de aaaTroubleshooting degradado no Azure Traffic Manager
description: "Como perfis de Gerenciador de tráfego tootroubleshoot quando ele aparece como status degradado."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
ms.assetid: 8af0433d-e61b-4761-adcc-7bc9b8142fc6
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: kumud
ms.openlocfilehash: fd95697781472b52e98d856e66beb7b89dfeaf23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-degraded-state-on-azure-traffic-manager"></a>Solucionando problemas de status degradado do Gerenciador de Tráfego do Azure

Este artigo descreve como tootroubleshoot um perfil do Gerenciador de tráfego do Azure que está mostrando um estado degradado. Para este cenário, considere a possibilidade de que você tenha configurado um perfil do Gerenciador de tráfego apontando toosome de seus serviços hospedados de cloudapp.net. Se a integridade de saudação do seu Traffic Manager exibe um **degradado** status e status de saudação de um ou mais pontos de extremidade podem ser **degradado**:

![status do ponto de extremidade degradado](./media/traffic-manager-troubleshooting-degraded/traffic-manager-degradedifonedegraded.png)

Se a integridade de saudação do seu Traffic Manager exibe um **inativo** status e, em seguida, os dois pontos de extremidade podem ser **desabilitado**:

![Status do Gerenciador de Tráfego Inativo](./media/traffic-manager-troubleshooting-degraded/traffic-manager-inactive.png)

## <a name="understanding-traffic-manager-probes"></a>Noções básicas sobre as investigações do Gerenciador de Tráfego

* Gerenciador de tráfego considera um toobe de ponto de extremidade ONLINE somente quando o teste de saudação recebe uma resposta HTTP 200 fazer do caminho de investigação de saudação. Qualquer outra resposta diferente de 200 é uma falha.
* Um redirecionamento 30 x falha, mesmo se Olá redirecionado URL retorna uma resposta 200.
* Para investigações de HTTPs, os erros de certificado são ignorados.
* conteúdo real de saudação do caminho de investigação de saudação não importa, desde que uma resposta 200 é retornado. Um tipo de conteúdo estático do toosome URL de investigação "/ favicon.ico" é uma técnica comum. Conteúdo dinâmico, como as páginas ASP hello, talvez nem sempre retorna 200, mesmo quando o aplicativo hello está íntegro.
* Uma prática recomendada é tooset Olá investigação toosomething de caminho que tem suficiente toodetermine lógica que Olá site está ativa ou inativa. Em Olá exemplo anterior, definindo Olá caminho too"/favicon.ico", você está apenas testar essa w3wp.exe está respondendo. Essa investigação pode não indicar que o aplicativo Web está íntegro. Uma opção melhor seria tooset tooa um caminho algo como "/ Probe.aspx" que tem lógica de integridade de saudação de toodetermine do site de saudação. Por exemplo, você pode usar a utilização de tooCPU de contadores de desempenho ou medida Olá número de solicitações com falha. Ou, você poderá tentar tooaccess recursos de banco de dados ou toomake de estado de sessão-se de que o aplicativo da web hello está funcionando.
* Se todos os pontos de extremidade em um perfil estão degradados, o Traffic Manager tratará todos os pontos de extremidade como íntegro e rotas tráfego tooall pontos de extremidade. Esse comportamento garante que problemas com hello mecanismo de sondagem não resultam em uma falha completa do seu serviço.

## <a name="troubleshooting"></a>Solucionar problemas

tootroubleshoot uma falha de teste, você precisa de uma ferramenta que mostra o código de status HTTP Olá retorno da URL de investigação de saudação. Há muitas ferramentas disponíveis que mostram Olá bruta resposta HTTP.

* [Fiddler](http://www.telerik.com/fiddler)
* [curl](https://curl.haxx.se/)
* [wget](http://gnuwin32.sourceforge.net/packages/wget.htm)

Além disso, você pode usar o guia de rede de saudação do hello F12 ferramentas de depuração em respostas HTTP do Internet Explorer tooview hello.

Neste exemplo, queremos toosee resposta de saudação do nosso URL de investigação: http://watestsdp2008r2.cloudapp.net:80/investigação. Olá PowerShell de exemplo a seguir ilustra o problema de saudação.

```powershell
Invoke-WebRequest 'http://watestsdp2008r2.cloudapp.net/Probe' -MaximumRedirection 0 -ErrorAction SilentlyContinue | Select-Object StatusCode,StatusDescription
```

Saída de exemplo:

    StatusCode StatusDescription
    ---------- -----------------
           301 Moved Permanently

Observe que recebemos uma resposta de redirecionamento. Como mencionamos anteriormente, qualquer StatusCode diferente de 200 é considerado uma falha. Alterações de Gerenciador de tráfego Olá tooOffline de status do ponto de extremidade. problema de saudação tooresolve, seleção Olá site configuração tooensure que Olá StatusCode adequada pode ser retornado do caminho de investigação de saudação. Reconfigure Olá Traffic Manager investigação toopoint tooa caminho que retorna uma resposta 200.

Se o teste é usando Olá protocolo HTTPS, talvez seja necessário certificado toodisable verificação de erros SSL/TLS tooavoid durante o teste. Olá, instruções a seguir do PowerShell desabilitar validação de certificado para a sessão atual do PowerShell hello:

```powershell
add-type @"
using System.Net;
using System.Security.Cryptography.X509Certificates;
public class TrustAllCertsPolicy : ICertificatePolicy {
    public bool CheckValidationResult(
    ServicePoint srvPoint, X509Certificate certificate,
    WebRequest request, int certificateProblem) {
    return true;
    }
}
"@
[System.Net.ServicePointManager]::CertificatePolicy = New-Object TrustAllCertsPolicy
```

## <a name="next-steps"></a>Próximas etapas

[Sobre os métodos de roteamento de tráfego do Gerenciador de Tráfego](traffic-manager-routing-methods.md)

[O que é o Gerenciador de Tráfego](traffic-manager-overview.md)

[Serviços de Nuvem](http://go.microsoft.com/fwlink/?LinkId=314074)

[Aplicativos Web do Azure](https://azure.microsoft.com/documentation/services/app-service/web/)

[Operações no Gerenciador de Tráfego (referência de API REST)](http://go.microsoft.com/fwlink/?LinkId=313584)

[Cmdlets do Gerenciador de Tráfego do Azure][1]

[1]: https://msdn.microsoft.com/library/mt125941(v=azure.200).aspx
