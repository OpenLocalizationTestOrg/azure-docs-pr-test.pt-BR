---
title: "aaaAzure aplicativo de serviço Web aplicativo nas perguntas frequentes sobre o Linux | Microsoft Docs"
description: "Perguntas frequentes sobre o Aplicativo Web do Serviço de Aplicativo do Azure no Linux."
keywords: "serviço de aplicativo do azure, aplicativo web, perguntas frequentes, linux, oss"
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: c7798d9144d936eecdc0e191fc870b0ee0b220c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-web-app-on-linux-faq"></a>Perguntas frequentes sobre o Aplicativo Web do Serviço de Aplicativo do Azure no Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


Com a versão de saudação do aplicativo Web no Linux, estamos trabalhando para adicionar recursos e fazer melhorias tooour plataforma. Aqui estão algumas perguntas frequentes (FAQ) que nossos clientes têm solicitado conosco sobre Olá última meses.
Se você tiver uma pergunta, o comentário sobre o artigo hello e responderemos-lo assim que possível.

## <a name="built-in-images"></a>Imagens internas

**P:** desejo toofork Olá internos contêineres do Docker que Olá plataforma fornece. Onde posso encontrar esses arquivos?

**R:** É possível encontrar todos os arquivos do Docker no [GitHub](https://github.com/azure-app-service). É possível encontrar todos os contêineres do Docker no [Hub do Docker](https://hub.docker.com/u/appsvc/).

**P:** quais são os valores esperados de saudação para Olá seção do arquivo de inicialização quando configura o pilha de tempo de execução de saudação?

**R:** para Node.Js, especifique o arquivo de configuração Olá PM2 ou o arquivo de script. Para o .NET Core, especifique o nome da DLL compilada. Para Ruby, você pode especificar Olá Ruby script que você deseja tooinitialize seu aplicativo com.

## <a name="management"></a>Gerenciamento

**P:** o que acontece quando eu pressionar o botão de reinicialização de saudação em Olá portal do Azure?

**R:** isso é Olá equivalente de reinicialização do Docker.

**P:** posso usar o Secure Shell (SSH) tooconnect toohello aplicativo contêiner VM (máquina virtual)?

**R:** Sim, você pode fazer que através do site SCM hello, seleção seguinte de saudação do artigo para obter mais informações [suporte SSH para o aplicativo Web no Linux](./app-service-linux-ssh-support.md)

**P:** desejo toocreate um plano de Linux App Service através do SDK ou um modelo do ARM, como fazer isso?

**R:** necessário Olá tooset `reserved` campo do aplicativo hello serviço muito`true`.

## <a name="continuous-integrationdeployment"></a>Integração/implantação contínua

**P:** meu aplicativo web ainda usa uma imagem de contêiner do Docker antiga depois de atualizar a imagem Olá no Hub do Docker. Há suporte para implantação/integração contínua de contêineres personalizados?

**R:** tooset integração/implantação contínua para imagens de registro de contêiner do Azure ou DockerHub por seleção Olá artigo a seguir [implantação contínua com o aplicativo Web do Azure no Linux](./app-service-linux-ci-cd.md). Para registros privados, você pode atualizar o contêiner de saudação ao parar e iniciar o seu aplicativo web. Ou você pode alterar ou adicionar um aplicativo fictício configuração tooforce uma atualização do seu contêiner.

**P:** Há suporte para ambientes de preparo?

**R:** Sim.

**P:** posso usar **implantação da web** toodeploy meu aplicativo web?

**R:** Sim, você precisa tooset um aplicativo chamada `WEBSITE_WEBDEPLOY_USE_SCM` muito`false`.

## <a name="language-support"></a>Suporte ao idioma

**P:** Há suporte para aplicativos .NET Core não compilados?

**R:** Sim.

**P:** Há suporte para o Criador como um gerenciador de dependências para aplicativos PHP?

**R:** Sim. Durante a implantação de Git, Kudu deve detectar que você está implantando um aplicativo PHP (obrigado a presença de toohello de um arquivo de composer.json) e disparará uma instalação de criador para você.

## <a name="custom-containers"></a>Contêineres personalizados

**P:** Estou usando meu próprio contêiner personalizado. Meu aplicativo reside no hello `\home\` diretório, mas não é possível localizar Meus arquivos quando navegar conteúdo hello usando Olá [site SCM](https://github.com/projectkudu/kudu) ou um cliente de FTP. Onde estão meus arquivos?

**R:** montamos uma toohello de compartilhamento SMB `\home\` directory. Isso substituirá todo o conteúdo existente nele.

**P:** Estou usando meu próprio contêiner personalizado. Não quero Olá plataforma toomount um toohello de compartilhamento SMB `\home\`.

**R:** você pode fazer isso por configuração Olá `WEBSITES_ENABLE_APP_SERVICE_STORAGE` aplicativo configuração muito`false`.

**P:** meu contêiner personalizado leva um tempo longo toostart e conclusão contêiner de saudação do hello plataforma reinicialização antes que ele for iniciado.

**R:** você pode configurar o tempo de saudação plataforma Olá aguardará antes de reiniciar seu contêiner. Isso pode ser feito por configuração Olá `WEBSITES_CONTAINER_START_TIME_LIMIT` toohello de configuração de aplicativo o valor desejado em segundos. padrão de saudação é 230 segundos e Olá máximo é de 600 segundos.

**P:** o que é o formato de saudação para url do servidor de registro privada?

**R:** necessárias tooprovide Olá registro completo url incluindo `http://` ou `https://`.

**P:** o que é o formato de saudação para nome da imagem Olá na opção do registro privada?

**R:** você precisa de nome de imagem completa Olá tooadd incluindo Olá url de registro particular (por exemplo. myacr.azurecr.io/dotnet:latest)

**P:** desejada tooexpose mais de uma porta na minha imagem de contêiner personalizado. Isso é possível?

**R:** No momento, não há suporte para esse recurso.

**P:** posso colocar meu próprio armazenamento?

**R:** No momento, não há suporte para esse recurso.

**P:** não é possível navegar os processos do meu contêiner personalizado execução ou sistema de arquivos do site SCM Olá. Por que isso acontece?

**R:** site SCM Olá é executado em um contêiner separado. Não é possível verificar o sistema de arquivos de saudação ou executando processos do contêiner do aplicativo hello.

**P:** meu contêiner personalizado escuta tooa porta diferente da porta 80. Como posso configurar meu aplicativo tooroute Olá solicitações toothat porta?

**R:** temos a detecção automática porta, também é possível especificar um aplicativo de chamada **WEBSITES_PORT**e dê a ele valor de saudação do número de porta Olá esperado. Plataforma Olá foi usando previamente `PORT` aplicativo configuração, podemos estiver planejando toodeprecate Olá use essa configuração de aplicativo e mover toousing `WEBSITES_PORT` exclusivamente.

**P:** necessário tooimplement HTTPS no meu contêiner personalizado.

**R:** não, plataforma Olá manipula a terminação HTTPS no front-ends Olá compartilhado.

## <a name="pricing-and-sla"></a>Preço e SLA

**P:** o que é Olá preços enquanto você estiver usando a visualização pública Olá?

**R:** você é cobrado pelo número de saudação metade de horas que seu aplicativo é executado, com preços do saudação normal do serviço de aplicativo do Azure. Isso significa que você obtém um desconto de 50% sobre o preço normal do Serviço de Aplicativo do Azure.

## <a name="other"></a>outro

**P:** o que são caracteres hello suportado em nomes de configurações do aplicativo?

**R:** você só pode usar A-Z, a-z, 0-9 e Olá sublinhado para configurações de aplicativo.

**P:** onde solicitar novos recursos?

**R:** poderá enviar sua ideia no hello [Fórum de comentários de aplicativos Web](https://aka.ms/webapps-uservoice). Adicione "[Linux]" toohello título de sua ideia.

## <a name="next-steps"></a>Próximas etapas
* [O que é um Aplicativo Web do Azure no Linux?](app-service-linux-intro.md)
* [Suporte de SSH para o Aplicativo Web do Azure no Linux](./app-service-linux-ssh-support.md)
* [Configurar ambientes de preparo no Serviço de Aplicativo do Azure](./web-sites-staged-publishing.md)
* [Implantação contínua com o Aplicativo Web do Azure no Linux](./app-service-linux-ci-cd.md)
