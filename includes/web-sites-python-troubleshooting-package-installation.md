Alguns pacotes podem não ser instalados usando pip durante a execução do Azure.  Pode ser simplesmente que pacote hello não está disponível no hello índice de pacote do Python.  É possível que um compilador é necessário (um compilador não está disponível em Olá máquina executando Olá aplicativo web do serviço de aplicativo do Azure).

Nesta seção, vamos examinar maneiras toodeal com esse problema.

### <a name="request-wheels"></a>Solicitar discos
Se a instalação do pacote de saudação requer um compilador, você deve tentar entrar em contato com toorequest de proprietário do pacote hello rodas ficar disponível para o pacote de saudação.

Com a disponibilidade recente saudação do [compilador do Microsoft Visual C++ para Python 2.7][Microsoft Visual C++ Compiler for Python 2.7], agora é mais fácil pacotes toobuild com código nativo para Python 2.7.

### <a name="build-wheels-requires-windows"></a>Compilar discos(requires Windows)
Observação: Ao usar essa opção, certifique-se de pacote de saudação toocompile usando um ambiente do Python que corresponde a saudação/arquitetura/versão da plataforma que é usado no aplicativo web de saudação do serviço de aplicativo do Azure (Windows/32-bit/2.7 ou 3.4).

Se não instalar o pacote hello porque requer que um compilador, pode instalar o compilador Olá em seu computador local e criar um disco para o pacote de saudação, que, em seguida, você incluirá em seu repositório.

Os usuários do Mac/Linux: Se você não tiver acessar tooa o computador Windows, consulte [criar uma máquina Virtual executando o Windows] [ Create a Virtual Machine Running Windows] como toocreate uma VM no Azure.  Pode usá-lo toobuild rodas de saudação, adicioná-los toohello repositório e descartar Olá VM se desejar. 

Para Python 2.7, você pode instalar [compilador do Microsoft Visual C++ para Python 2.7][Microsoft Visual C++ Compiler for Python 2.7].

Para Python 3.4, você pode instalar [Microsoft Visual C++ 2010 Express][Microsoft Visual C++ 2010 Express].

toobuild rodas, você precisará pacote de roda hello:

    env\scripts\pip install wheel

Você usará `pip wheel` toocompile uma dependência:

    env\scripts\pip wheel azure==0.8.4

Isso cria um arquivo de .whl na pasta de \wheelhouse hello.  Adicione pasta de \wheelhouse hello e repositório de tooyour de arquivos do disco.

Editar a saudação de tooadd requirements.txt `--find-links` opção na parte superior da saudação. Isso informa o pip toolook uma correspondência exata na pasta local do hello antes do índice de pacote vai toohello python.

    --find-links wheelhouse
    azure==0.8.4

Se você quiser tooinclude todas as suas dependências em Olá \wheelhouse pasta e não use Olá python pacote em todos os índice, você pode forçar o índice de pacote de saudação do pip tooignore adicionando `--no-index` toohello superior de sua requirements.txt.

    --no-index

### <a name="customize-installation"></a>Personalizar a instalação
Você pode personalizar tooinstall de script de implantação de saudação um pacote no ambiente virtual hello, usando um instalador alternativo, como fácil\_instalar.  Consulte deploy.cmd para obter um exemplo que é comentado.  Certifique-se de que esses pacotes não são listados em requirements.txt, tooprevent pip de instalá-los.

Adicione este script de implantação toohello:

    env\scripts\easy_install somepackage

Você também pode ser capaz de toouse fácil\_instalar tooinstall de um instalador exe (alguns são compatíveis, tão fáceis de zip\_instalação oferece suporte a eles).  Adicionar Olá instalador tooyour repositório e invocar fácil\_instalar passando Olá toohello de caminho executável.

Adicione este script de implantação toohello:

    env\scripts\easy_install "%DEPLOYMENT_SOURCE%\installers\somepackage.exe"

### <a name="include-hello-virtual-environment-in-hello-repository-requires-windows"></a>Incluir o ambiente virtual Olá no repositório de saudação (requer o Windows)
Observação: Ao usar essa opção, certifique-se de que toouse um ambiente virtual que corresponde a saudação/arquitetura/versão da plataforma que é usado no aplicativo web de saudação do serviço de aplicativo do Azure (Windows/32-bit/2.7 ou 3.4).

Se você incluir o ambiente virtual Olá no repositório de hello, você pode impedir que o script de implantação Olá fazendo o gerenciamento do ambiente virtual no Azure, criando um arquivo vazio:

    .skipPythonDeployment

É recomendável que você exclua o ambiente virtual existente do hello no aplicativo hello, arquivos de tooprevent deixados de quando o ambiente virtual Olá foi gerenciado automaticamente.

[Create a Virtual Machine Running Windows]: http://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/
[Microsoft Visual C++ Compiler for Python 2.7]: http://aka.ms/vcpython27
[Microsoft Visual C++ 2010 Express]: http://go.microsoft.com/?linkid=9709949
