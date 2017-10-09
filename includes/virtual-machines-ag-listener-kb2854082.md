Em seguida, se todos os servidores no cluster Olá estiver executando o Windows Server 2008 R2 ou Windows Server 2012, você deve verificar esse hotfix Olá [KB2854082](http://support.microsoft.com/kb/2854082) é instalado em cada um dos servidores de locais de saudação ou máquinas virtuais do Azure que fazem parte do cluster hello. Qualquer servidor ou VM que está em cluster hello, mas não no grupo de disponibilidade hello, também deverá ter esse hotfix instalado.

Na Olá sessão de área de trabalho remota para cada um de nós de cluster de saudação, baixe [KB2854082](http://support.microsoft.com/kb/2854082) tooa diretório de local. Em seguida, instale o hotfix de Olá em cada nó de cluster, em sequência. Se o serviço de cluster hello está sendo executado no nó de cluster Olá, servidor de saudação será reiniciado no final de saudação da instalação do hotfix hello.

> [!WARNING]
> Parar o serviço de cluster hello ou reiniciar o servidor de saudação afeta a integridade do quorum de saudação do seu grupo de disponibilidade do cluster e hello e pode causar o toogo de cluster offline. toomaintain Olá alta disponibilidade do seu cluster durante a instalação, verifique se:
> 
> * cluster de saudação está na integridade de quorum ideal. 
> * Antes de instalar o hotfix hello em qualquer nó, todos os nós de cluster estão online.
> * Antes de instalar o hotfix hello em qualquer outro nó no cluster hello, permitir Olá hotfix instalação toorun toocompletion em um nó, incluindo reinicialização completa Olá servidor.
> 
> 

