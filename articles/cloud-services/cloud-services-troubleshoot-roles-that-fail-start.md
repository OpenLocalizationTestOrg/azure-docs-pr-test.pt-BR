---
title: "funções de aaaTroubleshoot que falham toostart | Microsoft Docs"
description: "Aqui estão algumas razões comuns por que uma função de serviço de nuvem pode falhar toostart. Problemas de toothese soluções também são fornecidos."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 674b2faf-26d7-4f54-99ea-a9e02ef0eb2f
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: e2fbecb08a10984add79dfc74e73de6869bb314f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-service-roles-that-fail-toostart"></a>Solucionar problemas de funções de serviço de nuvem que falham toostart
Aqui estão alguns problemas comuns e funções de serviços de nuvem de tooAzure relacionados soluções que não toostart.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-dlls-or-dependencies"></a>DLLs ou dependências ausentes
Funções sem resposta e funções que alternam entre os estados **Inicializando**, **Ocupado** e **Parando** podem ser causadas por DLLs ou assemblies ausentes.

Os sintomas de DLLs ou assemblies ausentes podem ser:

* A instância de função está alternando entre os estados **Inicializando**, **Ocupado** e **Parando**.
* A instância de função foi movido muito**pronto** , mas se você navegar tooyour aplicativo de web, a página de saudação não será exibida.

Há vários métodos recomendados para investigar esses problemas.

## <a name="diagnose-missing-dll-issues-in-a-web-role"></a>Como diagnosticar problemas de DLL ausente em uma função Web
Quando você navegar pelo site de tooa que é implantado em uma função web e navegador Olá exibe a seguinte toohello semelhante do erro de servidor, isso pode indicar que uma DLL está ausente.

![Erro de servidor no aplicativo '/'.](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503388.png)

## <a name="diagnose-issues-by-turning-off-custom-errors"></a>Diagnosticar problemas desativando erros personalizados
Informações de erro mais completas podem ser exibidas Configurando Olá Web. config para Olá web função tooset Olá erro personalizado modo tooOff e reimplantar o serviço de saudação.

tooview mais concluído erros sem usar a área de trabalho remota:

1. Abra a solução de saudação do Microsoft Visual Studio.
2. Em Olá **Solution Explorer**, localize o arquivo Web. config de saudação e abri-lo.
3. No arquivo Web. config de hello, localize a seção System. Web hello e adicione Olá seguinte linha:

    ```xml
    <customErrors mode="Off" />
    ```
4. Salve o arquivo hello.
5. Empacote novamente e reimplante o serviço de saudação.

Depois que o serviço Olá é reimplantado, você verá uma mensagem de erro com nome Olá Olá assembly ou DLL ausente.

## <a name="diagnose-issues-by-viewing-hello-error-remotely"></a>Diagnosticar problemas exibindo erros Olá remotamente
Você pode usar a função de saudação do tooaccess de área de trabalho remota e exibir informações de erro mais completas remotamente. Use Olá erros de saudação do tooview as etapas a seguir usando a área de trabalho remota:

1. Verifique se o Azure SDK 1.3 ou posterior está instalado.
2. Durante a implantação de saudação da solução hello usando o Visual Studio, escolha muito "Conexões configurar área de trabalho remota …". Para obter mais informações sobre como configurar a conexão de área de trabalho remota hello, consulte [usando a área de trabalho remota com funções do Azure](../vs-azure-tools-remote-desktop-roles.md).
3. No portal clássico Olá Microsoft Azure, depois que a instância de saudação mostra um status de **pronto**, clique em uma das instâncias de função hello.
4. Clique em Olá **conectar** ícone Olá **acesso remoto** área da faixa de opções de saudação.
5. Entre na máquina virtual de toohello usando credenciais de saudação que foram especificadas durante a configuração da área de trabalho remota hello.
6. Abra uma janela de comando.
7. Digite `IPconfig`.
8. Observe o valor do endereço IPV4 hello.
9. Abra o Internet Explorer.
10. Digite o endereço de saudação e nome de saudação do aplicativo da web hello. Por exemplo: `http://<IPV4 Address>/default.aspx`.

Navegando toohello site agora irá retornar mensagens de erro mais explícitas:

* Erro de servidor no aplicativo '/'.
* Descrição: Uma exceção não tratada ocorreu durante a execução de saudação da solicitação da web atual de saudação. Analise o rastreamento de pilha de saudação para obter mais informações sobre o erro hello e onde ele foi originado no código de saudação.
* Detalhes da exceção: System.IO.FIleNotFoundException: não foi possível carregar o arquivo ou assembly ‘Microsoft.WindowsAzure.StorageClient, Version=1.1.0.0, Culture=neutral, PublicKeyToken=31bf856ad364e35’ ou uma de suas dependências. sistema Olá não é possível localizar o arquivo hello especificado.

Por exemplo:

![Erro de servidor explícito no aplicativo '/'](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503389.png)

## <a name="diagnose-issues-by-using-hello-compute-emulator"></a>Diagnosticar problemas usando o emulador de computação Olá
Você pode usar o hello Microsoft Azure compute emulator toodiagnose e solucionar problemas de dependências ausentes e erros de Web. config.

Para obter melhores resultados ao usar esse método de diagnóstico, você deve usar um computador ou uma máquina virtual com uma instalação limpa do Windows. toobest simular Olá ambiente do Azure, use o Windows Server 2008 R2 x64.

1. Instalar versão autônoma Olá Olá [SDK do Azure](https://azure.microsoft.com/downloads/).
2. No computador de desenvolvimento Olá, compile o projeto de serviço de nuvem hello.
3. No Windows Explorer, navegue toohello bin\debug pasta do projeto de serviço de nuvem hello.
4. Copiar a pasta hello. CSx e. cscfg toohello computador que você está usando toodebug problemas de saudação do arquivo.
5. No hello computador limpo, abra uma janela de Prompt de comando do SDK do Azure e digite `csrun.exe /devstore:start`.
6. No prompt de comando hello, digite `run csrun <path too.csx folder> <path too.cscfg file> /launchBrowser`.
7. Quando a função hello é iniciado, você verá informações detalhadas do erro no Internet Explorer. Você também pode usar ferramentas de solução de problemas padrão do Windows toofurther diagnosticar o problema de saudação.

## <a name="diagnose-issues-by-using-intellitrace"></a>Diagnosticar problemas usando o IntelliTrace
Para as funções Web e de trabalho que usam o .NET Framework 4, você pode usar o [IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx), que está disponível no Microsoft Visual Studio Enterprise.

Execute o serviço de saudação de toodeploy essas etapas com o IntelliTrace habilitado:

1. Confirme se o Azure SDK 1.3 ou posterior está instalado.
2. Implante solução de saudação usando o Visual Studio. Durante a implantação, verifique Olá **habilitar IntelliTrace para funções do .NET 4** caixa de seleção.
3. Depois de iniciada a instância hello, abra Olá **Server Explorer**.
4. Expanda Olá **Azure\\serviços de nuvem** nó e localize a implantação de saudação.
5. Expanda a implantação de saudação até que você veja instâncias de função hello. Clique em uma das instâncias de saudação.
6. Escolha **Exibir logs do IntelliTrace**. Olá **resumo do IntelliTrace** será aberto.
7. Localize a seção de exceções de saudação do hello resumo. Se houver exceções, seção hello será rotulada **dados de exceção**.
8. Expanda Olá **dados de exceção** e procure **System.IO. FileNotFoundException** a seguir toohello semelhante erros:

![Dados de exceção, arquivo ou assembly ausente](./media/cloud-services-troubleshoot-roles-that-fail-start/ic503390.png)

## <a name="address-missing-dlls-and-assemblies"></a>Lidar com DLLs e assemblies ausentes
tooaddress tem erros DLL e assembly, siga estas etapas:

1. Abra a solução de saudação no Visual Studio.
2. Em **Solution Explorer**, abra Olá **referências** pasta.
3. Clique em assembly hello identificado no erro hello.
4. Em Olá **propriedades** painel, localize **propriedade Copy Local** e defina o valor de saudação muito**True**.
5. Reimplante o serviço de nuvem hello.

Depois de ter verificado que todos os erros foram corrigidos, você pode implantar o serviço de saudação sem verificar Olá **habilitar IntelliTrace para funções do .NET 4** caixa de seleção.

## <a name="next-steps"></a>Próximas etapas
Confira mais [artigos sobre solução de problemas](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) para serviços de nuvem.

toolearn como função de serviço de nuvem tootroubleshoot problemas usando dados de diagnóstico do computador de PaaS do Azure, consulte [série do blog de Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).
