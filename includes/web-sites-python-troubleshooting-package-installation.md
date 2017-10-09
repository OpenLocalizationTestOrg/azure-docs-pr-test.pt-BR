<span data-ttu-id="129ca-101">Alguns pacotes podem não ser instalados usando pip durante a execução do Azure.</span><span class="sxs-lookup"><span data-stu-id="129ca-101">Some packages may not install using pip when run on Azure.</span></span>  <span data-ttu-id="129ca-102">Pode ser simplesmente que pacote hello não está disponível no hello índice de pacote do Python.</span><span class="sxs-lookup"><span data-stu-id="129ca-102">It may simply be that hello package is not available on hello Python Package Index.</span></span>  <span data-ttu-id="129ca-103">É possível que um compilador é necessário (um compilador não está disponível em Olá máquina executando Olá aplicativo web do serviço de aplicativo do Azure).</span><span class="sxs-lookup"><span data-stu-id="129ca-103">It could be that a compiler is required (a compiler is not available on hello machine running hello web app in Azure App Service).</span></span>

<span data-ttu-id="129ca-104">Nesta seção, vamos examinar maneiras toodeal com esse problema.</span><span class="sxs-lookup"><span data-stu-id="129ca-104">In this section, we'll look at ways toodeal with this issue.</span></span>

### <a name="request-wheels"></a><span data-ttu-id="129ca-105">Solicitar discos</span><span class="sxs-lookup"><span data-stu-id="129ca-105">Request wheels</span></span>
<span data-ttu-id="129ca-106">Se a instalação do pacote de saudação requer um compilador, você deve tentar entrar em contato com toorequest de proprietário do pacote hello rodas ficar disponível para o pacote de saudação.</span><span class="sxs-lookup"><span data-stu-id="129ca-106">If hello package installation requires a compiler, you should try contacting hello package owner toorequest that wheels be made available for hello package.</span></span>

<span data-ttu-id="129ca-107">Com a disponibilidade recente saudação do [compilador do Microsoft Visual C++ para Python 2.7][Microsoft Visual C++ Compiler for Python 2.7], agora é mais fácil pacotes toobuild com código nativo para Python 2.7.</span><span class="sxs-lookup"><span data-stu-id="129ca-107">With hello recent availability of [Microsoft Visual C++ Compiler for Python 2.7][Microsoft Visual C++ Compiler for Python 2.7], it is now easier toobuild packages that have native code for Python 2.7.</span></span>

### <a name="build-wheels-requires-windows"></a><span data-ttu-id="129ca-108">Compilar discos(requires Windows)</span><span class="sxs-lookup"><span data-stu-id="129ca-108">Build wheels (requires Windows)</span></span>
<span data-ttu-id="129ca-109">Observação: Ao usar essa opção, certifique-se de pacote de saudação toocompile usando um ambiente do Python que corresponde a saudação/arquitetura/versão da plataforma que é usado no aplicativo web de saudação do serviço de aplicativo do Azure (Windows/32-bit/2.7 ou 3.4).</span><span class="sxs-lookup"><span data-stu-id="129ca-109">Note: When using this option, make sure toocompile hello package using a Python environment that matches hello platform/architecture/version that is used on hello web app in Azure App Service (Windows/32-bit/2.7 or 3.4).</span></span>

<span data-ttu-id="129ca-110">Se não instalar o pacote hello porque requer que um compilador, pode instalar o compilador Olá em seu computador local e criar um disco para o pacote de saudação, que, em seguida, você incluirá em seu repositório.</span><span class="sxs-lookup"><span data-stu-id="129ca-110">If hello package doesn't install because it requires a compiler, you can install hello compiler on your local machine and build a wheel for hello package, which you will then include in your repository.</span></span>

<span data-ttu-id="129ca-111">Os usuários do Mac/Linux: Se você não tiver acessar tooa o computador Windows, consulte [criar uma máquina Virtual executando o Windows] [ Create a Virtual Machine Running Windows] como toocreate uma VM no Azure.</span><span class="sxs-lookup"><span data-stu-id="129ca-111">Mac/Linux Users: If you don't have access tooa Windows machine, see [Create a Virtual Machine Running Windows][Create a Virtual Machine Running Windows] for how toocreate a VM on Azure.</span></span>  <span data-ttu-id="129ca-112">Pode usá-lo toobuild rodas de saudação, adicioná-los toohello repositório e descartar Olá VM se desejar.</span><span class="sxs-lookup"><span data-stu-id="129ca-112">You can use it toobuild hello wheels, add them toohello repository, and discard hello VM if you like.</span></span> 

<span data-ttu-id="129ca-113">Para Python 2.7, você pode instalar [compilador do Microsoft Visual C++ para Python 2.7][Microsoft Visual C++ Compiler for Python 2.7].</span><span class="sxs-lookup"><span data-stu-id="129ca-113">For Python 2.7, you can install [Microsoft Visual C++ Compiler for Python 2.7][Microsoft Visual C++ Compiler for Python 2.7].</span></span>

<span data-ttu-id="129ca-114">Para Python 3.4, você pode instalar [Microsoft Visual C++ 2010 Express][Microsoft Visual C++ 2010 Express].</span><span class="sxs-lookup"><span data-stu-id="129ca-114">For Python 3.4, you can install [Microsoft Visual C++ 2010 Express][Microsoft Visual C++ 2010 Express].</span></span>

<span data-ttu-id="129ca-115">toobuild rodas, você precisará pacote de roda hello:</span><span class="sxs-lookup"><span data-stu-id="129ca-115">toobuild wheels, you'll need hello wheel package:</span></span>

    env\scripts\pip install wheel

<span data-ttu-id="129ca-116">Você usará `pip wheel` toocompile uma dependência:</span><span class="sxs-lookup"><span data-stu-id="129ca-116">You'll use `pip wheel` toocompile a dependency:</span></span>

    env\scripts\pip wheel azure==0.8.4

<span data-ttu-id="129ca-117">Isso cria um arquivo de .whl na pasta de \wheelhouse hello.</span><span class="sxs-lookup"><span data-stu-id="129ca-117">This creates a .whl file in hello \wheelhouse folder.</span></span>  <span data-ttu-id="129ca-118">Adicione pasta de \wheelhouse hello e repositório de tooyour de arquivos do disco.</span><span class="sxs-lookup"><span data-stu-id="129ca-118">Add hello \wheelhouse folder and wheel files tooyour repository.</span></span>

<span data-ttu-id="129ca-119">Editar a saudação de tooadd requirements.txt `--find-links` opção na parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="129ca-119">Edit your requirements.txt tooadd hello `--find-links` option at hello top.</span></span> <span data-ttu-id="129ca-120">Isso informa o pip toolook uma correspondência exata na pasta local do hello antes do índice de pacote vai toohello python.</span><span class="sxs-lookup"><span data-stu-id="129ca-120">This tells pip toolook for an exact match in hello local folder before going toohello python package index.</span></span>

    --find-links wheelhouse
    azure==0.8.4

<span data-ttu-id="129ca-121">Se você quiser tooinclude todas as suas dependências em Olá \wheelhouse pasta e não use Olá python pacote em todos os índice, você pode forçar o índice de pacote de saudação do pip tooignore adicionando `--no-index` toohello superior de sua requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="129ca-121">If you want tooinclude all your dependencies in hello \wheelhouse folder and not use hello python package index at all, you can force pip tooignore hello package index by adding `--no-index` toohello top of your requirements.txt.</span></span>

    --no-index

### <a name="customize-installation"></a><span data-ttu-id="129ca-122">Personalizar a instalação</span><span class="sxs-lookup"><span data-stu-id="129ca-122">Customize installation</span></span>
<span data-ttu-id="129ca-123">Você pode personalizar tooinstall de script de implantação de saudação um pacote no ambiente virtual hello, usando um instalador alternativo, como fácil\_instalar.</span><span class="sxs-lookup"><span data-stu-id="129ca-123">You can customize hello deployment script tooinstall a package in hello virtual environment using an alternate installer, such as easy\_install.</span></span>  <span data-ttu-id="129ca-124">Consulte deploy.cmd para obter um exemplo que é comentado.  Certifique-se de que esses pacotes não são listados em requirements.txt, tooprevent pip de instalá-los.</span><span class="sxs-lookup"><span data-stu-id="129ca-124">See deploy.cmd for an example that is commented out.  Make sure that such packages aren't listed in requirements.txt, tooprevent pip from installing them.</span></span>

<span data-ttu-id="129ca-125">Adicione este script de implantação toohello:</span><span class="sxs-lookup"><span data-stu-id="129ca-125">Add this toohello deployment script:</span></span>

    env\scripts\easy_install somepackage

<span data-ttu-id="129ca-126">Você também pode ser capaz de toouse fácil\_instalar tooinstall de um instalador exe (alguns são compatíveis, tão fáceis de zip\_instalação oferece suporte a eles).</span><span class="sxs-lookup"><span data-stu-id="129ca-126">You may also be able toouse easy\_install tooinstall from an exe installer (some are zip compatible, so easy\_install supports them).</span></span>  <span data-ttu-id="129ca-127">Adicionar Olá instalador tooyour repositório e invocar fácil\_instalar passando Olá toohello de caminho executável.</span><span class="sxs-lookup"><span data-stu-id="129ca-127">Add hello installer tooyour repository, and invoke easy\_install by passing hello path toohello executable.</span></span>

<span data-ttu-id="129ca-128">Adicione este script de implantação toohello:</span><span class="sxs-lookup"><span data-stu-id="129ca-128">Add this toohello deployment script:</span></span>

    env\scripts\easy_install "%DEPLOYMENT_SOURCE%\installers\somepackage.exe"

### <a name="include-hello-virtual-environment-in-hello-repository-requires-windows"></a><span data-ttu-id="129ca-129">Incluir o ambiente virtual Olá no repositório de saudação (requer o Windows)</span><span class="sxs-lookup"><span data-stu-id="129ca-129">Include hello virtual environment in hello repository (requires Windows)</span></span>
<span data-ttu-id="129ca-130">Observação: Ao usar essa opção, certifique-se de que toouse um ambiente virtual que corresponde a saudação/arquitetura/versão da plataforma que é usado no aplicativo web de saudação do serviço de aplicativo do Azure (Windows/32-bit/2.7 ou 3.4).</span><span class="sxs-lookup"><span data-stu-id="129ca-130">Note: When using this option, make sure toouse a virtual environment that matches hello platform/architecture/version that is used on hello web app in Azure App Service (Windows/32-bit/2.7 or 3.4).</span></span>

<span data-ttu-id="129ca-131">Se você incluir o ambiente virtual Olá no repositório de hello, você pode impedir que o script de implantação Olá fazendo o gerenciamento do ambiente virtual no Azure, criando um arquivo vazio:</span><span class="sxs-lookup"><span data-stu-id="129ca-131">If you include hello virtual environment in hello repository, you can prevent hello deployment script from doing virtual environment management on Azure by creating an empty file:</span></span>

    .skipPythonDeployment

<span data-ttu-id="129ca-132">É recomendável que você exclua o ambiente virtual existente do hello no aplicativo hello, arquivos de tooprevent deixados de quando o ambiente virtual Olá foi gerenciado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="129ca-132">We recommend that you delete hello existing virtual environment on hello app, tooprevent leftover files from when hello virtual environment was managed automatically.</span></span>

[Create a Virtual Machine Running Windows]: http://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/
[Microsoft Visual C++ Compiler for Python 2.7]: http://aka.ms/vcpython27
[Microsoft Visual C++ 2010 Express]: http://go.microsoft.com/?linkid=9709949
