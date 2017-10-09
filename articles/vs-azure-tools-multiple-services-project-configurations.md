---
title: "aaaConfiguring seu projeto do Azure usando várias configurações de serviço | Microsoft Docs"
description: "Saiba como tooconfigure um Azure nuvem projeto de serviço alterando arquivos de saudação servicedefinition. Csdef e ServiceConfiguration. cscfg."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: a4fb79ed-384f-4183-9f74-5cac257206b9
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 14222266093eb876db0ac9ce8d3d17a04c65d1a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-your-azure-project-using-multiple-service-configurations"></a>Configurando seu projeto do Azure usando várias configurações de serviço
Um projeto de serviço de nuvem do Azure inclui dois arquivos de configuração: ServiceDefinition.csdef e ServiceConfiguration.cscfg. Esses arquivos são empacotados com o aplicativo de serviço de nuvem do Azure e implantados tooAzure.

* Olá **servicedefinition. Csdef** arquivo contém os metadados de saudação que é exigido pelo Olá ambiente Azure para requisitos de saudação do seu aplicativo de serviço de nuvem, incluindo as funções que ele contém. Esse arquivo também contém configurações que se aplicam a instâncias de tooall. Essas configurações podem ser lidos em tempo de execução usando Olá hospedagem API de tempo de execução de serviço do Azure. Esse arquivo não pode ser atualizado enquanto o serviço está em execução no Azure.
* Olá **ServiceConfiguration** arquivo define valores hello as definições de configuração definidas no arquivo de definição de serviço hello e especifica Olá número de instâncias toorun para cada função. Esse arquivo pode ser atualizado enquanto o serviço de nuvem está em execução no Azure.

Olá ferramentas do Azure para Microsoft Visual Studio fornece páginas de propriedades que você pode usar configurações tooset armazenadas nesses arquivos. tooaccess Olá páginas de propriedades, clique duas vezes em referência à função hello sob o projeto de serviço de nuvem do Azure Olá no Gerenciador de soluções, ou com o botão direito referência à função hello e escolha **propriedades**, conforme mostrado na figura a seguir de saudação.

![VS_Solution_Explorer_Roles_Properties](./media/vs-azure-tools-multiple-services-project-configurations/IC784076.png)

Para obter informações sobre Olá subjacente esquemas de definição de serviço hello e arquivos de configuração de serviço, consulte Olá [referência de esquema](https://msdn.microsoft.com/library/azure/dd179398.aspx). Para obter mais informações sobre a configuração de serviço, consulte [como serviços em nuvem tooConfigure](cloud-services/cloud-services-how-to-configure.md).

## <a name="configuring-role-properties"></a>Configurando propriedades da função
páginas de propriedade Olá para uma função web e uma função de trabalho são semelhantes, embora haja algumas diferenças, indicadas nas seções a seguir de saudação.

De saudação **cache** página, você pode configurar Olá serviços de cache do Azure.

### <a name="configuration-page"></a>Página Configuração
Em Olá **configuração** página, você pode definir essas propriedades:

**Instâncias**

Saudação de conjunto **instância** contar propriedade toohello número de instâncias de serviço Olá deve ser executado para esta função.

Saudação de conjunto **tamanho da VM** propriedade muito**Extra pequeno**, **pequeno**, **médio**, **grande**, ou **Extra grande**.  Para saber mais, veja [Tamanhos dos Serviços de Nuvem](cloud-services/cloud-services-sizes-specs.md).

**Ação de inicialização** (somente função web)

Defina este toospecify de propriedade que o Visual Studio deve iniciar um navegador da web para pontos de extremidade Olá HTTP ou pontos de extremidade HTTPS hello ou ambos, quando você iniciar a depuração.

Olá opção do ponto de extremidade HTTPS está disponível somente se você já definiu um ponto de extremidade HTTPS para sua função. Você pode definir um ponto de extremidade HTTPS em Olá **pontos de extremidade** página de propriedades.

Se você já tiver adicionado um ponto de extremidade HTTPS, Olá opção do ponto de extremidade HTTPS é habilitado por padrão e o Visual Studio iniciará um navegador para este ponto de extremidade quando você iniciar a depuração, além de navegador tooa para seu ponto de extremidade HTTP. Isso pressupõe que ambas as opções de inicialização estão habilitadas.

**Diagnostics**

Por padrão, o diagnóstico está habilitado para função de Web hello. Olá projeto de serviço de nuvem do Azure e a conta de armazenamento são definidas toouse emulador de armazenamento local de saudação. Quando você estiver pronto toodeploy tooAzure, você pode selecionar o botão do construtor de saudação (**...** ) toouse de conta de armazenamento do tooupdate Olá armazenamento do Azure na nuvem hello. Você pode transferir a conta de armazenamento Olá diagnóstico dados toohello sob demanda ou em intervalos agendados automaticamente. Para saber mais sobre o diagnóstico do Azure, veja [Habilitando o Diagnóstico nos Serviços de Nuvem do Azure e nas Máquinas Virtuais](cloud-services/cloud-services-dotnet-diagnostics.md).

## <a name="settings-page"></a>Página Configurações
Em Olá **configurações** página, você pode adicionar parâmetros de configuração para o serviço. Definições de configuração são pares nome-valor. Código em execução na função hello pode ler os valores de saudação de suas definições de configuração em tempo de execução usando classes fornecidas pela Olá [biblioteca gerenciada do Azure](http://go.microsoft.com/fwlink?LinkID=171026). Especificamente, Olá [GetConfigurationSettingValue](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getconfigurationsettingvalue.aspx) método retorna o valor de saudação de uma definição de configuração nomeado em tempo de execução.

### <a name="configuring-a-connection-string-tooa-storage-account"></a>Configurando uma conta de armazenamento de tooa de cadeia de caracteres de conexão
Uma cadeia de caracteres de conexão é uma configuração que fornece informações de conexão e autenticação para o emulador de armazenamento hello, ou para uma conta de armazenamento do Azure. Sempre que o código precisar acessar os dados de serviços de armazenamento do Azure – ou seja, blob, fila ou dados da tabela – do código em execução em uma função, você terá que toodefine uma cadeia de caracteres de conexão para essa conta de armazenamento.

Uma cadeia de caracteres de conexão que aponta tooan conta de armazenamento do Azure deve usar um formato definido. Para obter informações sobre como toocreate cadeias de caracteres de conexão, consulte [configurar cadeias de Conexão de armazenamento do Azure](storage/common/storage-configure-connection-string.md).

Quando você está pronto tootest seu serviço em relação aos serviços de armazenamento do Azure hello, ou quando você estiver pronto toodeploy seu tooAzure de serviço de nuvem, você pode alterar o valor de saudação de qualquer tooyour de toopoint de cadeias de caracteres de conexão conta de armazenamento do Azure. Escolha (**...**) e **Inserir credenciais da conta de armazenamento**. Insira as informações de sua conta que incluem o nome da conta e a chave de conta. Em Olá **cadeia de Conexão da conta de armazenamento** caixa de diálogo, você também pode indicar se deseja toouse Olá HTTPS pontos de extremidade padrão (opção padrão de saudação), pontos de extremidade saudação padrão HTTP ou pontos de extremidade personalizados. Você pode decidir toouse pontos de extremidade personalizados se você tiver registrado um nome de domínio personalizado para seu serviço, conforme descrito em [configurar um nome de domínio personalizado para dados blob em uma conta de armazenamento do Azure](storage/blobs/storage-custom-domain-name.md).

> [!IMPORTANT]
> Você deve modificar seu tooan de toopoint de cadeias de caracteres de conexão conta de armazenamento do Azure antes de implantar seu serviço. Falha toodo, isso pode causar sua função não toostart ou toocycle por meio de Olá estados inicializando, ocupados e parando.
> 
> 

## <a name="endpoints-page"></a>Página Pontos de Extremidade
Uma função de trabalho pode ter qualquer número de pontos de extremidade HTTP, HTTPS ou TCP. Pontos de extremidade podem ser pontos de extremidade de entrada, que são clientes tooexternal disponível, ou pontos de extremidade internos, que são funções de tooother disponíveis que estão em execução no serviço de saudação.

* os clientes tooexternal disponíveis de ponto de extremidade toomake um HTTP e navegadores da Web, altere Olá tooinput de tipo de ponto de extremidade e especifique um nome e um número de porta pública.
* toomake um HTTPS clientes do ponto de extremidade tooexternal disponíveis e navegadores da Web, alterar tipo de ponto de extremidade de saudação muito**entrada**e especifique um nome, um número de porta pública e um nome de certificado de gerenciamento.
  
    Observe que, antes de você pode especificar um certificado de gerenciamento, você deve definir certificado Olá em Olá **certificados** página de propriedades.
* toomake um ponto de extremidade disponível para acesso interno por outras funções no serviço de nuvem hello, altere Olá toointernal de tipo de ponto de extremidade e especifique um nome e possíveis portas privadas para esse ponto de extremidade.

## <a name="local-storage-page"></a>Página Armazenamento Local
Você pode usar o hello **armazenamento Local** tooreserve de página de propriedade um ou mais recursos de armazenamento local para uma função. Um recurso de armazenamento local é um diretório reservado no sistema de arquivos de saudação do hello máquina virtual do Azure no qual uma instância de uma função está sendo executado.

## <a name="certificates-page"></a>Página Certificados
Em Olá **certificados** página, você pode associar certificados com sua função. certificados de saudação que você adicionar pode ser usado tooconfigure seus pontos de extremidade HTTPS no hello **pontos de extremidade** página de propriedades.

Olá **certificados** página de propriedade adiciona informações sobre a configuração de serviço tooyour certificados. Observe que os certificados não são compactados com o serviço; Você deve carregá-los separadamente tooAzure por meio de saudação [portal clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885).

tooassociate um certificado com sua função, forneça um nome para o certificado de saudação. Use este certificado toohello toorefer quando você configura um ponto de extremidade HTTPS no hello **pontos de extremidade** página de propriedades. Em seguida, especifique se o repositório de certificados de saudação é **Máquina Local** ou **usuário atual** e o nome de saudação do repositório hello. Finalmente, insira a impressão digital do certificado hello. Se certificado Olá for no hello User\Personal atual (Meu), você pode inserir impressão digital do certificado hello, selecionando o certificado de saudação em uma lista populada. Se ele residir em qualquer outro local, insira o valor de impressão digital Olá manualmente.

Quando você adiciona um certificado do repositório de certificados hello, os certificados intermediários são adicionados automaticamente toohello definições de configuração para você. Esses certificados intermediários também devem ser carregados tooAzure em ordem toocorrectly configurar seu serviço para SSL.

Qualquer certificado de gerenciamento que você associar seu serviço se aplicam a tooyour serviço apenas quando ele está em execução na nuvem hello. Quando o serviço está em execução no ambiente de desenvolvimento local hello, ele usa um certificado padrão que é gerenciado pelo emulador de computação hello.

## <a name="configuring-hello-azure-cloud-service-project"></a>Configurando o projeto de serviço de nuvem do Azure Olá
tooconfigure configurações que se aplicam a tooan projeto de serviço de nuvem inteiro do Azure, você primeiro abra Olá menu de atalho desse nó do projeto e, em seguida, escolha Propriedades tooopen suas páginas de propriedades. Olá, a tabela a seguir mostra essas páginas de propriedades.

| Página de Propriedades | Descrição |
| --- | --- |
| Aplicativo |Nessa página, você pode exibir informações sobre Olá versão das ferramentas do Azure que usa este projeto de serviço de nuvem e você pode atualizar a versão atual toohello das ferramentas de saudação. |
| Eventos de compilação |Nessa página, você pode configurar eventos de pré e pós-compilação. |
| Desenvolvimento |Nessa página, você pode especificar instruções de configuração de compilação e as condições de saudação sob a qual os eventos de pós-compilação são executados. |
| Web |Nessa página, você pode configurar as configurações relacionadas toohello servidor de web. |

