---
title: problemas de armazenamento de arquivo do Azure aaaTroubleshoot no Linux | Microsoft Docs
description: "Solução de problemas de armazenamento de Arquivos do Azure no Linux"
services: storage
documentationcenter: 
author: genlin
manager: willchen
editor: na
tags: storage
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: genli
ms.openlocfilehash: 4bdc3c6ed2e48f245060a03632fca9bd14d33545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-linux"></a>Solucionar problemas de armazenamento de Arquivos do Azure no Linux

Este artigo lista os problemas comuns que estão relacionada tooMicrosoft armazenamento de arquivo do Azure durante a conexão de clientes do Linux. Também fornece as possíveis causas e resoluções para esses problemas.

<a id="permissiondenied"></a>
## <a name="permission-denied-disk-quota-exceeded-when-you-try-tooopen-a-file"></a>"cota de disco [permissão negada] excedida" ao tentar tooopen um arquivo

No Linux, você recebe uma mensagem de erro semelhante a seguinte hello:

**<filename> [permissão negada] Cota de disco excedida**

### <a name="cause"></a>Causa

Você atingiu o limite superior de saudação de identificadores abertos simultâneos permitidas para um arquivo.

### <a name="solution"></a>Solução

Reduza o número de saudação de identificadores abertos simultâneos fechando alguns identificadores e, em seguida, repita a operação de saudação. Para obter mais informações, consulte [Lista de verificação de desempenho e escalabilidade do Armazenamento do Microsoft Azure](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-linux"></a>Arquivos lenta copiando tooand do armazenamento de arquivo do Azure no Linux

-   Se você não tiver um requisito de tamanho de e/s mínimo específico, é recomendável que você use 1 MB como Olá tamanho de e/s para o desempenho ideal.
-   Se você conhece Olá o tamanho final de um arquivo que você estiver estendendo usando gravações, e o software não ter problemas de compatibilidade quando uma final não gravada no arquivo hello contém zeros, em seguida, definir o tamanho do arquivo de Olá antecipadamente, em vez de fazer cada gravação uma extensão gravação.
-   Use o método de cópia de direito de saudação:
    -   Use o [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) para todas as transferências entre dois compartilhamentos de arquivo.
    -   Use o [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) entre compartilhamentos de arquivos e um computador local.

<a id="error112"></a>
## <a name="mount-error112-host-is-down-because-of-a-reconnection-time-out"></a>“Erro de montagem (112): o host está inativo” devido a um tempo limite de reconexão

Ocorrerá um erro de montagem "112" no cliente do Linux hello quando o cliente Olá ficar ocioso por um longo tempo. Após um longo tempo ocioso, Olá cliente se desconecta e conexão Olá expire.  

### <a name="cause"></a>Causa

conexão Olá pode ficar ociosa para Olá motivos a seguir:

-   Falhas de comunicação de rede que impedem a estabelecer novamente um servidor de toohello de conexão TCP quando a opção de montagem "soft" hello padrão é usada
-   Correções de reconexão recentes que não estão presentes nos kernels mais antigos

### <a name="solution"></a>Solução

Esse problema de reconexão do kernel do Linux Olá agora é fixo como parte da saudação as seguintes alterações:

- [Correção de reconexão toonot adiar smb3 sessão reconectar depois reconectar-se do soquete](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/fs/cifs?id=4fcd1813e6404dd4420c7d12fb483f9320f0bf93)
-   [Chamar o serviço de eco imediatamente após a reconexão do soquete](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7)
-   [CIFS: corrigir uma possível corrupção de memória durante a reconexão](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b)
-   [CIFS: corrigir um possível bloqueio duplo de mutex durante a reconexão (para kernel v4.9 e posterior)](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183)

No entanto, essas alterações não podem ser movidas ainda tooall Olá distribuições do Linux. Essa correção e outras correções de reconexão são feitas no hello populares kernels do Linux a seguir: 4.4.40, 4.8.16 e 4.9.1. Você pode obter essa correção atualizando tooone dessas versões de kernel recomendado.

### <a name="workaround"></a>Solução alternativa

Resolva esse problema especificando uma montagem rígida. Isso força Olá cliente toowait até que uma conexão seja estabelecida ou até que ela seja interrompida explicitamente e pode ser usado tooprevent erros devido a tempos limite de rede. No entanto, essa solução alternativa pode causar esperas indefinidas. Ser preparados toostop conexões conforme o necessário.

Se você não pode atualizar versões mais recentes de kernel toohello, você pode contornar esse problema mantendo um arquivo em um compartilhamento de arquivo do Azure Olá gravar tooevery 30 segundos ou menos. Isso deve ser uma operação de gravação, como reconfiguração Olá criado ou data de modificação no arquivo hello. Caso contrário, você pode obter resultados em cache e a operação não pode disparar a reconexão hello.

<a id="error115"></a>
## <a name="mount-error115-operation-now-in-progress-when-you-mount-azure-file-storage-by-using-smb-30"></a>“Erro de montagem (115): operação em andamento” durante a montagem do armazenamento de Arquivos do Azure usando o SMB 3.0

### <a name="cause"></a>Causa

Algumas distribuições do Linux não ainda dão suporte a recursos de criptografia do SMB 3.0 e os usuários podem receber uma mensagem de erro "115" se tentarem toomount armazenamento de arquivo do Azure usando o SMB 3.0 devido a um recurso ausente.

### <a name="solution"></a>Solução

O recurso de criptografia do SMB 3.0 para Linux foi introduzido no kernel 4.11. Este recurso permite a montagem do Compartilhamento de Arquivos do Azure do local ou de uma região diferente do Azure. Em tempo de saudação da publicação, essa funcionalidade foi backported tooUbuntu 17.04 e 16.10 do Ubuntu. Se o cliente SMB Linux não dá suporte à criptografia, montar o armazenamento de arquivo do Azure usando o SMB 2.1 de uma VM do Linux do Azure que está em Olá mesmo data center como Olá conta de armazenamento de arquivo.

<a id="slowperformance"></a>
## <a name="slow-performance-on-an-azure-file-share-mounted-on-a-linux-vm"></a>Desempenho lento em um compartilhamento de arquivos do Azure montado em uma VM Linux

### <a name="cause"></a>Causa

Uma possível causa da lentidão no desempenho é o cache desabilitado.

### <a name="solution"></a>Solução

toocheck se o cache é desabilitado, procure Olá **cache =** entrada. 

**Cache=none** indica que o cache está desabilitado.  Remontagem Olá compartilhamento usando o comando de montagem saudação padrão ou adicione explicitamente Olá **cache = estrito** opção toohello montagem comando tooensure padrão cache ou "estrito" modo de cache está habilitado.

Em alguns cenários, Olá **serverino** a opção de montagem pode causar Olá **ls** stat no comando toorun em cada entrada de diretório. Esse comportamento resulta na degradação do desempenho quando você está listando um diretório grande. Você pode verificar as opções de montagem de saudação em seu **/etc/fstab** entrada:

`//azureuser.file.core.windows.net/cifs /cifs cifs vers=3.0,serverino,username=xxx,password=xxx,dir_mode=0777,file_mode=0777`

Você também pode verificar se as opções corretas de saudação estão sendo usadas executando Olá **sudo montagem | grep cifs** comando e a verificação de sua saída, como Olá saída de exemplo a seguir:

`//mabiccacifs.file.core.windows.net/cifs on /cifs type cifs (rw,relatime,vers=3.0,sec=ntlmssp,cache=strict,username=xxx,domain=X,uid=0,noforceuid,gid=0,noforcegid,addr=192.168.10.1,file_mode=0777, dir_mode=0777,persistenthandles,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,actimeo=1)`

Se hello **cache = estrito** ou **serverino** opção é não apresentar, desmontar e montar o armazenamento de arquivo do Azure novamente, executando o comando de montagem de saudação do hello [documentação](../storage-how-to-use-files-linux.md). Em seguida, verificar que Olá **/etc/fstab** entrada tem opções corretas de saudação.

<a id="timestampslost"></a>
## <a name="time-stamps-were-lost-in-copying-files-from-windows-toolinux"></a>Os carimbos de hora foram perdidos ao copiar arquivos do Windows tooLinux

Em plataformas Unix/Linux, Olá **cp -p** comando falhará se o arquivo 1 e 2 pertencentes a diferentes usuários.

### <a name="cause"></a>Causa

Olá sinalizador force **f** em COPYFILE resulta em execução **cp -p -f** em Unix. Este comando também falha toopreserve Olá carimbo de data do arquivo hello que você não possui.

### <a name="workaround"></a>Solução alternativa

Use o usuário da conta de armazenamento Olá para copiar arquivos de saudação:

- `Useadd : [storage account name]`
- `Passwd [storage account name]`
- `Su [storage account name]`
- `Cp -p filename.txt /share`

## <a name="need-help-contact-support"></a>Precisa de ajuda? Entre em contato com o suporte.

Se você ainda precisar de Ajuda, [entre em contato com o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget o problema foi resolvido rapidamente.
