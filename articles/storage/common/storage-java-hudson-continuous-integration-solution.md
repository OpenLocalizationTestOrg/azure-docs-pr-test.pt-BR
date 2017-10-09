---
title: aaaHow toouse Hudson com armazenamento de Blob | Microsoft Docs
description: "Descreve como toouse Hudson com o armazenamento de BLOBs do Azure como um repositório de artefatos de compilação."
services: storage
documentationcenter: java
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 119becdd-72c4-4ade-a439-070233c1e1ac
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 02/28/2017
ms.author: seguler
ms.openlocfilehash: 196b5d014b0318c5972a052f7822b568cfcc23df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-storage-with-a-hudson-continuous-integration-solution"></a>Usando o Armazenamento do Azure com uma solução Hudson Continuous Integration
## <a name="overview"></a>Visão geral
Olá informações a seguir mostram como o armazenamento de Blob toouse como um repositório de artefatos de compilação criado por uma solução Hudson CI (integração contínua) ou como uma fonte de arquivos para download toobe usados em um processo de compilação. Um dos cenários de saudação em que isso poderia ser útil é quando você estar codificando em um ambiente de desenvolvimento ágil (usando Java ou outras linguagens), compilações são executados com base em integração contínua e você precisa de um repositório para seus artefatos de compilação, para que você poderia , por exemplo, compartilhá-los com outros membros da organização, os clientes, ou mantenha um arquivamento.  Outro cenário é quando o seu próprio trabalho de compilação requer outros arquivos, por exemplo, toodownload de dependências, como parte da saudação entrada de construção.

Neste tutorial você usará plug-in do armazenamento do Azure Olá para CI Hudson disponibilizados pela Microsoft.

## <a name="introduction-toohudson"></a>Introdução tooHudson
Habilita a integração contínua Hudson de um projeto de software, permitindo que os desenvolvedores tooeasily integrar as alterações de código e ter cria gerado automaticamente e com frequência, aumentando a produtividade Olá de desenvolvedores de saudação. Compilações têm controle de versão e artefatos de compilação podem ser carregado toovarious repositórios. Este artigo mostra como toouse armazenamento de BLOBs do Azure como repositório de saudação do hello criar artefatos. Ele também mostra como dependências toodownload do armazenamento de BLOBs do Azure.

Mais informações sobre o Hudson podem ser encontradas em [Conheça o Hudson (a página pode estar em inglês)](http://wiki.eclipse.org/Hudson-ci/Meet_Hudson).

## <a name="benefits-of-using-hello-blob-service"></a>Benefícios do uso do serviço Blob Olá
Benefícios do uso de toohost de serviço Blob Olá seus artefatos de compilação de desenvolvimento ágil incluem:

* Alta disponibilidade de seus artefatos de compilação e/ou dependências baixáveis.
* O desempenho quando sua solução Hudson CI carrega seus artefatos de compilação.
* Desempenho quando seus clientes e parceiros baixam seus artefatos de compilação.
* O controle sobre as políticas de acesso do usuário, com uma opção entre acesso anônimo, acesso compartilhado com base em expiração, acesso de assinatura, acesso particular, etc.

## <a name="prerequisites"></a>Pré-requisitos
Você será necessário Olá seguintes toouse Olá serviço Blob com sua solução CI Hudson:

* Uma solução Hudson Continuous Integration.
  
    Se você atualmente não tem uma solução CI Hudson, você pode executar uma solução CI Hudson usando Olá técnica a seguir:
  
  1. Em um computador habilitado para Java, download Olá Hudson WAR do <http://hudson-ci.org/>.
  2. No prompt de comando é aberto toohello pasta que contém a saudação Hudson WAR, execute Olá Hudson WAR. Por exemplo, se você baixou a versão 3.1.2:
     
      `java -jar hudson-3.1.2.war`

  3. No seu navegador, abra `http://localhost:8080/`. Isso abrirá Olá painel Hudson.
  4. No primeiro uso do Hudson, concluir a instalação inicial do hello no `http://localhost:8080/`.
  5. Depois de concluir a configuração inicial hello, cancelar Olá executando a instância do hello Hudson WAR, iniciar Olá Hudson WAR novamente e reabra Olá painel Hudson, `http://localhost:8080/`, que você usará tooinstall e configurar o plug-in do armazenamento do Azure hello.
     
      Enquanto uma solução típica de CI Hudson será configurada toorun como um serviço, executar Olá war Hudson na linha de comando Olá será suficiente para este tutorial.
* Uma conta do Azure. Você pode criar uma conta do Azure em <http://www.azure.com>.
* Uma conta de armazenamento do Azure. Se você ainda não tiver uma conta de armazenamento, você pode criar um usando as etapas de saudação em [criar uma conta de armazenamento](../common/storage-create-storage-account.md#create-a-storage-account).
* Familiaridade com a solução de CI Hudson Olá é recomendável, mas não é necessário, como hello conteúdo a seguir usará um tooshow exemplo básico Olá etapas necessárias ao usar o serviço de Blob hello como um repositório para o IC Hudson compilar artefatos.

## <a name="how-toouse-hello-blob-service-with-hudson-ci"></a>Como toouse Olá serviço Blob com Hudson CI
serviço de Blob toouse Olá com Hudson, você precisará tooinstall Olá plug-in do armazenamento do Azure, configurar Olá plug-in toouse sua conta de armazenamento e, em seguida, crie uma ação de pós-compilação que carrega sua conta de armazenamento de tooyour de artefatos de compilação. Essas etapas são descritas nas seções a seguir de saudação.

## <a name="how-tooinstall-hello-azure-storage-plugin"></a>Como tooinstall Olá plug-in do armazenamento do Azure
1. No painel Hudson do hello, clique em **Hudson gerenciar**.
2. Em Olá **Hudson gerenciar** , clique em **gerenciar plug-ins**.
3. Clique em Olá **disponível** guia.
4. Clique em **Others**.
5. Em Olá **artefato Uploaders** seção, selecione **plug-in de armazenamento do Microsoft Azure**.
6. Clique em **Instalar**.
7. Após a conclusão da instalação hello, reinicie Hudson.

## <a name="how-tooconfigure-hello-azure-storage-plugin-toouse-your-storage-account"></a>Como tooconfigure Olá toouse de plug-in do armazenamento do Azure sua conta de armazenamento
1. No painel Hudson do hello, clique em **Hudson gerenciar**.
2. Em Olá **Hudson gerenciar** , clique em **Configurar sistema**.
3. Em Olá **configuração de conta de armazenamento do Microsoft Azure** seção:
   
    a. Insira seu nome de conta de armazenamento, você pode obter de saudação [Portal do Azure](https://portal.azure.com).
   
    b. Insira a chave de conta de armazenamento, também alcançável de saudação [Portal do Azure](https://portal.azure.com).
   
    c. Usar o valor padrão Olá **URL de ponto de extremidade de serviço Blob** se você estiver usando a nuvem do Azure públicos de saudação. Se você estiver usando uma nuvem do Azure diferente, use o ponto de extremidade de hello como especificado no hello [Portal do Azure](https://portal.azure.com) para sua conta de armazenamento.
   
    d. Clique em **validar as credenciais de armazenamento** toovalidate sua conta de armazenamento.
   
    e. [Opcional] Se você tiver contas de armazenamento adicional que você deseja tooyour feita disponível Hudson CI, clique em **adicionar mais contas de armazenamento**.
   
    f. Clique em **salvar** toosave suas configurações.

## <a name="how-toocreate-a-post-build-action-that-uploads-your-build-artifacts-tooyour-storage-account"></a>Como toocreate uma ação de pós-compilação que carrega sua conta de armazenamento de tooyour de artefatos de compilação
Para fins de instrução, primeiro vamos precisar toocreate um trabalho que criará vários arquivos e, em seguida, adicionar conta de armazenamento Olá ação pós-compilação tooupload Olá arquivos tooyour.

1. No painel Hudson do hello, clique em **novo trabalho**.
2. Nome do trabalho Olá **MyJob**, clique em **criar um trabalho de software livre de estilo**e, em seguida, clique em **Okey**.
3. Em Olá **criar** seção de configuração de trabalho hello, clique em **adicionar a etapa de compilação** e escolha **Windows executar comando de lote**.
4. Em **comando**, use Olá comandos a seguir:

    ```   
        md text
        cd text
        echo Hello Azure Storage from Hudson > hello.txt
        date /t > date.txt
        time /t >> date.txt
    ```

5. Em Olá **ações de pós-compilação** seção de configuração de trabalho hello, clique em **carregar o armazenamento de Blob do Azure artefatos tooMicrosoft**.
6. Para **nome da conta de armazenamento**, selecione Olá toouse da conta de armazenamento.
7. Para **nome do contêiner**, especifique o nome do contêiner de saudação. (Olá contêiner será criado se ele ainda não existir quando são carregados artefatos de compilação hello.) Você pode usar variáveis de ambiente, então para este exemplo, digite **${JOB_NAME}** como nome do contêiner de saudação.
   
    **Dica**
   
    Abaixo Olá **comando** seção em que você inseriu um script para **Windows executar comando de lote** é um link de variáveis de ambiente toohello reconhecidas pelo Hudson. Clique em que se vinculam a nomes de variável de ambiente toolearn hello e descrições. Observe que o ambiente de variáveis que contêm caracteres especiais, como Olá **BUILD_URL** variável de ambiente, não são permitidos como um nome de contêiner ou o caminho virtual comum.
8. Clique em **Tornar o novo contêiner público por padrão** para este exemplo. (Se você quiser toouse um contêiner privado, você precisará toocreate um acesso de tooallow de assinatura de acesso compartilhado. Que está além do escopo deste artigo hello. Você pode saber mais sobre assinaturas de acesso compartilhado em [Uso de SAS (Assinaturas de Acesso Compartilhado)](../storage-dotnet-shared-access-signature-part-1.md).
9. [Opcional] Clique em **contêiner limpa antes de carregar** se você quiser Olá contêiner toobe apagados do conteúdo para artefatos de compilação são carregados (deixá-la desmarcada se você não quiser tooclean conteúdo de saudação do contêiner de saudação).
10. Para **tooupload de lista de artefatos**, digite  **texto /*. txt**.
11. Em **Common virtual path for uploaded artifacts**, digite **${BUILD\_ID}/${BUILD\_NUMBER}**.
12. Clique em **salvar** toosave suas configurações.
13. No painel Hudson do hello, clique em **criar agora** toorun **MyJob**. Examine a saída de console de saudação status. Mensagens de status para o armazenamento do Azure serão incluídas na saída do console Olá início da ação de pós-compilação Olá artefatos de compilação tooupload.
14. Após a conclusão bem-sucedida do trabalho hello, você pode examinar artefatos de compilação Olá abrindo blob público hello.
    
    a. Entrar toohello [Portal do Azure](https://portal.azure.com).
    
    b. Clique em **Armazenamento**.
    
    c. Clique no nome de conta de armazenamento Olá que você usou para Hudson.
    
    d. Clique em **Contêineres**.
    
    e. Clique em contêiner Olá denominado **myjob**, Olá a versão em minúsculas do nome do trabalho Olá que você atribuiu ao criar hello trabalho Hudson. Os nomes de contêineres e de blob são escritos em letra minúscula (e diferenciam maiúsculas de minúsculas) no Armazenamento do Azure. Na lista de saudação de blobs para contêiner Olá denominado **myjob** , você verá **hello.txt** e **date.txt**. Copiar URL de saudação para qualquer um desses itens e abri-lo no seu navegador. Você verá o arquivo de texto de saudação que foi carregado como um artefato de compilação.

Somente uma ação de pós-compilação que carrega os artefatos tooAzure armazenamento de Blob pode ser criada por trabalho. Observe que o armazenamento de Blob Olá única ação de pós-compilação tooupload artefatos tooAzure pode especificar diferentes arquivos (incluindo caracteres curinga) e caminhos toofiles em **tooupload de lista de artefatos** usando um ponto e vírgula como separador. Por exemplo, se seu Hudson compilar produz arquivos JAR e arquivos TXT no seu espaço de trabalho **criar** pasta e você deseja tooupload ambos tooAzure armazenamento de Blob, use o seguinte de saudação para Olá **tooupload de lista de artefatos** valor: **criar /\*. jar; compilação /\*. txt**. Você também pode usar a sintaxe de dois-pontos duplo toospecify toouse um caminho em nome do blob hello. Por exemplo, se você quiser Olá JARs tooget carregado usando **binários** no caminho de blob hello e Olá TXT arquivos tooget carregados usando **avisos** no caminho de blob Olá, use o seguinte de Olá para Olá  **Lista de tooupload artefatos** valor: **criar /\*. jar::binaries; compilação /\*. txt::notices**.

## <a name="how-toocreate-a-build-step-that-downloads-from-azure-blob-storage"></a>Como uma etapa de compilação de toocreate downloads do armazenamento de BLOBs do Azure
Olá, as etapas a seguir mostra como tooconfigure uma compilação etapa itens toodownload do armazenamento de BLOBs do Azure. Isso pode ser útil se você quiser tooinclude itens em sua criação, por exemplo, JARs manter no armazenamento de BLOBs do Azure.

1. Em Olá **criar** seção de configuração de trabalho hello, clique em **adicionar a etapa de compilação** e escolha **Download do armazenamento de BLOBs do Azure**.
2. Para **nome da conta de armazenamento**, selecione Olá toouse da conta de armazenamento.
3. Para **nome do contêiner**, especificar nome de saudação do contêiner de saudação que tem blobs Olá deseja toodownload. É possível usar variáveis de ambiente.
4. Para **nome do Blob**, especifique o nome do blob hello. É possível usar variáveis de ambiente. Além disso, você pode usar um asterisco como um caractere curinga depois que você especificar letras de saudação inicial do nome do blob hello. Por exemplo, **project\*** deve especificar todos os blobs cujos nomes começam com **project**.
5. [Opcional] Para **caminho de Download**, especifique o caminho de saudação em Olá máquina Hudson onde deseja toodownload arquivos do armazenamento de BLOBs do Azure. Também é possível usar variáveis de ambiente. (Se você não fornecer um valor para **caminho de Download**, arquivos de saudação do armazenamento de BLOBs do Azure será o espaço de trabalho do trabalho toohello baixado.)

Se você tiver itens adicionais que você deseja toodownload do armazenamento de BLOBs do Azure, você pode criar etapas de compilação adicionais.

Depois de executar uma compilação, você pode verificar Olá compilar saída do console de histórico ou examinar seu local de download, toosee se Olá blobs esperado foram baixados com êxito.

## <a name="components-used-by-hello-blob-service"></a>Componentes usados pelo serviço Blob da saudação
a seguir Olá fornece uma visão geral dos componentes de serviço Blob hello.

* **Conta de armazenamento**: todos os acessos tooAzure armazenamento é feito por meio de uma conta de armazenamento. Este é o nível mais alto de saudação do namespace Olá para acessar blobs. Uma conta pode conter um número ilimitado de contêineres, desde que seu tamanho total seja inferior a 100 TB.
* **Contêiner**: o contêiner fornece um agrupamento de conjunto de blobs. Todos os blobs devem ter um contêiner. Uma conta pode conter um número ilimitado de contêineres. Um contêiner pode armazenar um número ilimitado de blobs.
* **Blob**: um arquivo de qualquer tipo e tamanho. Existem dois tipos de blobs que podem ser armazenados no Armazenamento do Azure: blobs de blocos e de páginas. A maioria dos arquivos são blobs de bloco. Um blob de bloco único pode ser a too200 GB de tamanho. Este tutorial usa blobs de bloco. Blobs de página, outro tipo de blob, podem ser até too1 TB de tamanho e são mais eficiente quando os intervalos de bytes em um arquivo são alterados com frequência. Para obter mais informações sobre os blobs, consulte [Compreendendo os Blobs de Bloco, Blobs de Anexo e Blobs de Página](http://msdn.microsoft.com/library/azure/ee691964.aspx).
* **Formato de URL**: Blobs são endereçados através de Olá formato de URL a seguir:
  
    `http://storageaccount.blob.core.windows.net/container_name/blob_name`
  
    (formato de saudação acima se aplica toohello nuvem pública do Azure. Se você estiver usando uma nuvem do Azure diferente, use pontos de extremidade Olá Olá [Portal do Azure](https://portal.azure.com) toodetermine seu ponto de extremidade de URL.)
  
    No formato de saudação acima, `storageaccount` representa Olá nome da sua conta de armazenamento, `container_name` representa Olá nome do seu contêiner e `blob_name` representa Olá nome de seu blob, respectivamente. Em nome do contêiner de saudação, você pode ter vários caminhos, separados por uma barra invertida,  **/** . nome do contêiner de exemplo Hello neste tutorial foi **MyJob**, e **${COMPILAR\_ID} / ${BUILD\_número}** foi usado para comuns caminho virtual hello, resultando em Olá blob tem um URL da saudação formulário a seguir:
  
    `http://example.blob.core.windows.net/myjob/2014-05-01_11-56-22/1/hello.txt`

## <a name="next-steps"></a>Próximas etapas
* [Conheça o Hudson](http://wiki.eclipse.org/Hudson-ci/Meet_Hudson)
* [SDK de Armazenamento do Azure para Java](https://github.com/azure/azure-storage-java)
* [Referência de SDK do Cliente de Armazenamento do Azure](http://dl.windowsazure.com/storage/javadoc/)
* [API REST de serviços de armazenamento do Azure](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Blog da equipe de Armazenamento do Azure](http://blogs.msdn.com/b/windowsazurestorage/)

Para saber mais, visite [Azure para desenvolvedores Java](/java/azure).