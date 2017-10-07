---
title: "aaaLearn sobre opções de suporte de malha do serviço do Azure | Microsoft Docs"
description: "Versões de cluster do Service Fabric do Azure com suporte e links toofile tíquetes de suporte"
services: service-fabric
documentationcenter: .net
author: pkc
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: pkc
ms.openlocfilehash: 42394e2cd9dad2040d37d3a2ff3600ee040d8720
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-support-options"></a>Opções de suporte do Azure Service Fabric

suporte a toodeliver Olá apropriado para os clusters de malha do serviço que você está executando o trabalho de aplicativo carrega em, configuramos a várias opções para você. Dependendo de saudação nível de suporte necessários e gravidade de saudação do problema hello, você obterá toopick opções corretas de saudação. 


<a id="getlivesitesupportonazure"></a>

## <a name="report-production-or-live-site-issues-or-request-paid-support-for-azure"></a>Relatar problemas de produção ou de site ativo ou solicitar o suporte pago para o Azure

Para relatar problemas de site ativo no cluster do Service Fabric implantado no Azure, abra um tíquete de suporte profissional [no portal do Azure](https://ms.portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview) ou no [portal de suporte da Microsoft](http://support.microsoft.com/oas/default.aspx?prid=16146).

Saiba mais sobre:
 
- [Suporte Profissional da Microsoft para o Azure](https://azure.microsoft.com/en-us/support/plans/?b=16.44).
- [Suporte premier da Microsoft](https://support.microsoft.com/en-us/premier).

<a id="getlivesitesupportonprem"></a>

## <a name="report-production-or-live-site-issues-or-request-paid-support-for-standalone-service-fabric-clusters"></a>Relatar problemas de produção ou de site ativo ou solicitar o suporte pago para clusters independentes do Service Fabric

Para relatar problemas de site ativo no cluster do Service Fabric implantado localmente ou em outras nuvens, abra um tíquete para obter suporte profissional no [portal de suporte da Microsoft](http://support.microsoft.com/oas/default.aspx?prid=16146).

Saiba mais sobre:

- [Suporte Profissional da Microsoft para o local](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).
- [Suporte premier da Microsoft](https://support.microsoft.com/en-us/premier).


<a id="getsupportonissues"></a>
## <a name="report-azure-service-fabric-issues"></a>Relatar problemas do Azure Service Fabric 
Organizamos um repositório GitHub para relatar problemas do Service Fabric.  Estamos também ativamente monitorando Olá fóruns a seguir.

### <a name="github-repo"></a>Repositório GitHub 
Relate problemas do Azure Service Fabric no [repositório Git de problemas do Service Fabric](https://github.com/Azure/service-fabric-issues). Esse repositório destina-se a relatar e acompanhar problemas com o Azure Service Fabric e a ser usado para fazer pequenas solicitações de recursos. **Não use este tooreport live-site emite**.

### <a name="stackoverflow-and-msdn-forums"></a>StackOverflow e fóruns do MSDN

Olá [marca de malha do serviço em StackOverflow] [ stackoverflow] e hello [Fórum do Service Fabric no MSDN] [ msdn-forum] são melhor usado para fazer perguntas sobre como a plataforma de saudação funciona e como você pode realizar certas tarefas com ele.

### <a name="azure-feedback-forum"></a>Fórum de Comentários do Azure

Olá [Fórum de comentários do Azure para Service Fabric] [ uservoice-forum] é Olá melhor local para enviar ideias ótimo recurso você tem para o produto hello como examinamos solicitações mais populares Olá fazem parte de nosso prazo toolong médio planejamento. Recomendamos que você toorally suporte para suas sugestões na comunidade de saudação.


<a id="releasesuport"></a>
## <a name="supported-service-fabric-versions"></a>Versões do Service Fabric com suporte.

Verifique se o cluster sempre executa uma versão do Service Fabric com suporte. Como e quando é anunciar o lançamento de saudação de uma nova versão do Service Fabric, versão anterior do hello está marcado para o fim do suporte após um mínimo de 60 dias a partir dessa data. Olá novas versões são anunciadas [no blog da equipe do Service Fabric Olá](https://blogs.msdn.microsoft.com/azureservicefabric/).

Consulte toohello documentos a seguir detalhes sobre como tookeep o cluster executando uma versão com suporte do Service Fabric.

- [Atualizar a versão do Service Fabric em um cluster do Azure ](service-fabric-cluster-upgrade.md)
- [Atualizar a versão do Service Fabric em um cluster de servidores independente do Windows Server ](service-fabric-cluster-upgrade-windows-server.md)
 
Aqui estão lista Olá das versões do Service Fabric Olá que têm suporte e suas datas de término do suporte.

| **Cluster de tempo de execução do Service Fabric** | **Compatível com SDK/versões do pacote NuGet** | **Data de fim do suporte** |
| --- | --- | --- |
| Todos os too5.3.121 de versões anteriores do cluster |Menor que ou igual tooversion 2.3 |20 de janeiro de 2017 |
| 5.3.* |Menor que ou igual tooversion 2.3 |24 de fevereiro de 2017 |
| 5.4.* |Menor que ou igual tooversion 2.4 |10 de maio de 2017     |
| 5.5.* |Menor que ou igual tooversion 2.5 |10 de agosto de 2017    |
| 5.6.* |Menor que ou igual tooversion 2.6 |13 de outubro de 2017    |
| 5.7.* |Menor que ou igual tooversion 2.7 |Versão atual e, portanto, sem data de término

<a id="previewversion"></a>
## <a name="service-fabric-preview-versions---unsupported-for-production-use"></a>Versões prévias do Service Fabric – sem suporte para uso em produção.
De hora tootime, lançamos versões que têm recursos importantes que desejamos comentários, que são lançados como visualizações. Essas versões prévias devem ser usadas apenas para fins de teste. O cluster de produção sempre deve estar executando uma versão do Service Fabric estável e com suporte. Uma versão prévia sempre começa com um número de versão principal e secundária de 255. Por exemplo, se você vir uma malha de serviço versão 255.255.5703.949, essa versão é toobe somente usado em clusters de teste e está em visualização. Essas versões de visualização também sejam anunciados no hello [blog da equipe do Service Fabric](https://blogs.msdn.microsoft.com/azureservicefabric) e ter detalhes Olá recursos incluídos.

Não há nenhuma opção de suporte pago para essas versões prévias. Use uma das opções de saudação listadas em [problemas de relatório do Azure Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support#report-azure-service-fabric-issues) tooask perguntas ou comentários.

## <a name="next-steps"></a>Próximas etapas

- [Atualizar a versão do Service Fabric em um cluster do Azure ](service-fabric-cluster-upgrade.md)
- [Atualizar a versão do Service Fabric em um cluster de servidores independente do Windows Server ](service-fabric-cluster-upgrade-windows-server.md)

<!--references-->
[msdn-forum]: https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureServiceFabric
[stackoverflow]: http://stackoverflow.com/questions/tagged/azure-service-fabric
[uservoice-forum]: https://feedback.azure.com/forums/293901-service-fabric
[acom-docs]: http://aka.ms/servicefabricdocs
[sample-repos]: http://aka.ms/servicefabricsamples
