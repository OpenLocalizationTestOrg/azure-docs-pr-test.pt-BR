---
title: "faz com que o aaaCommon de reciclagem de funções de serviço de nuvem | Microsoft Docs"
description: "Uma função de serviço de nuvem que é reciclada repentinamente pode causar um tempo de inatividade significativo. Aqui estão alguns problemas comuns que causam funções toobe reciclado, o que pode ajudar a reduzir o tempo de inatividade."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 533930d1-8035-4402-b16a-cf887b2c4f85
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 8fa152b33d2b22a8a02f834d4bc38519b4272f7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="common-issues-that-cause-roles-toorecycle"></a>Problemas comuns que causam toorecycle funções
Este artigo aborda algumas das causas comuns de saudação de problemas de implantação e fornece dicas de solução de problemas toohelp resolver esses problemas. Uma indicação de que existe um problema com um aplicativo é quando a instância de função hello falha toostart ou circula entre os estados inicializando, ocupado e parando de saudação.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-runtime-dependencies"></a>Dependências de tempo de execução ausentes
Se uma função em seu aplicativo depende de qualquer assembly que não faz parte da saudação biblioteca gerenciada do .NET Framework ou saudação do Azure, você deve incluir explicitamente esse assembly no pacote de aplicativo hello. Tenha em mente que outras estruturas da Microsoft não estão disponíveis no Azure por padrão. Se sua função depender de tal estrutura, você deve adicionar o pacote de aplicativo de toohello desses assemblies.

Antes que você compile e empacote seu aplicativo, verifique se a seguir hello:

* Se usando o Visual studio, verifique se Olá **Copy Local** propriedade for definida muito**True** para cada assembly referenciada no seu projeto que não faz parte de saudação do SDK do Azure ou Olá do .NET Framework.
* Verifique se o arquivo Web. config de saudação não faz referência aos assemblies não usados no elemento de compilação de saudação.
* Olá **ação de compilação** de cada. cshtml arquivo está definido muito**conteúdo**. Isso garante que os arquivos de saudação sejam exibidos corretamente no pacote de saudação e permite tooappear outros arquivos referenciados no pacote de saudação.

## <a name="assembly-targets-wrong-platform"></a>Plataforma incorreta de destinos de assembly
O Azure é um ambiente de 64 bits. Portanto, os assemblies do .NET compilados para um destino de 32 bits não funcionarão no Azure.

## <a name="role-throws-unhandled-exceptions-while-initializing-or-stopping"></a>A função gera exceções sem tratamento durante a inicialização ou interrupção
Todas as exceções que são geradas pelos métodos de saudação da saudação [RoleEntryPoint] classe, que inclui a saudação [OnStart], [OnStop], e [executar]os métodos são exceções sem tratamento. Se uma exceção não tratada ocorrer em um desses métodos, a função hello reciclará. Se a função hello estiver Reciclando repetidamente, ela poderá lançar uma exceção sem tratamento toda vez que ele tenta toostart.

## <a name="role-returns-from-run-method"></a>A função é retornada do método Run
Olá [executar] método é pretendido toorun indefinidamente. Se seu código substituir Olá [executar] método, ele deverá ser suspendo indefinidamente. Se hello [executar] método retorna, Olá função se reciclar.

## <a name="incorrect-diagnosticsconnectionstring-setting"></a>Configuração incorreta de DiagnosticsConnectionString
Se o aplicativo usa o diagnóstico do Azure, o arquivo de configuração do serviço deve especificar Olá `DiagnosticsConnectionString` configuração. Essa configuração deve especificar uma conta de armazenamento do tooyour de conexão HTTPS no Azure.

tooensure que seu `DiagnosticsConnectionString` configuração está correta antes de implantar seu tooAzure do pacote de aplicativo, verifique se a seguinte hello:  

* Olá `DiagnosticsConnectionString` definindo pontos de conta de armazenamento válida tooa no Azure.  
  Por padrão, essa configuração aponta toohello emulado conta de armazenamento, portanto você precisa alterar explicitamente essa configuração antes de implantar seu pacote de aplicativo. Se você não alterar essa configuração, uma exceção é lançada quando a instância de função hello tentativas de monitor de diagnóstico toostart hello. Isso pode causar toorecycle de instância de função hello indefinidamente.
* Olá cadeia de caracteres de conexão é especificada no seguinte Olá [formato](../storage/common/storage-configure-connection-string.md). (protocolo de saudação deve ser especificado como HTTPS). Substituir *MyAccountName* com o nome de saudação da sua conta de armazenamento e *MyAccountKey* com sua chave de acesso:    

        DefaultEndpointsProtocol=https;AccountName=MyAccountName;AccountKey=MyAccountKey

  Se você estiver desenvolvendo seu aplicativo usando ferramentas do Azure para Microsoft Visual Studio, você pode usar tooset de páginas de propriedade Olá esse valor.

## <a name="exported-certificate-does-not-include-private-key"></a>O certificado exportado não inclui a chave privada
toorun uma função web no SSL, você deve garantir que seu certificado de gerenciamento exportado inclui a chave privada hello. Se você usar o hello *Gerenciador de certificados do Windows* tooexport certificado do hello, ser tooselect se **Sim** para Olá **chave privada de saudação de exportação** opção. certificado Olá deve ser exportado em formato PFX hello, o que é Olá formato só tem suportado no momento.

## <a name="next-steps"></a>Próximas etapas
Confira mais [artigos sobre solução de problemas](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) para serviços de nuvem.

Veja mais cenários de reciclagem da função na [Série de blogs de Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).

[RoleEntryPoint]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx
[OnStart]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx
[OnStop]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx
[executar]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx
