
<!--
includes/sql-database-include-ip-address-22-v12portal.md

Latest Freshness check:  2016-03-21 , daleche.

As of circa 2015-09-04, hello following topics might include this include:
articles/sql-database/sql-database-configure-firewall-settings.md
articles/sql-database/sql-database-connect-query.md


## Server-level firewall rules

### Add a server-level firewall rule through hello new Azure portal
-->


1. <span data-ttu-id="b3de8-101">Faça logon no toohello [portal do Azure](https://portal.azure.com/) em http://portal.azure.com/.</span><span class="sxs-lookup"><span data-stu-id="b3de8-101">Log in toohello [Azure portal](https://portal.azure.com/) at http://portal.azure.com/.</span></span>
2. <span data-ttu-id="b3de8-102">Na faixa de saudação à esquerda, clique em **procurar todas as**.</span><span class="sxs-lookup"><span data-stu-id="b3de8-102">In hello left banner, click **BROWSE ALL**.</span></span> <span data-ttu-id="b3de8-103">Olá **procurar** folha é exibida.</span><span class="sxs-lookup"><span data-stu-id="b3de8-103">hello **Browse** blade is displayed.</span></span>
3. <span data-ttu-id="b3de8-104">Role e clique em **servidores SQL**.</span><span class="sxs-lookup"><span data-stu-id="b3de8-104">Scroll and click **SQL servers**.</span></span> <span data-ttu-id="b3de8-105">Olá **servidores SQL** folha é exibida.</span><span class="sxs-lookup"><span data-stu-id="b3de8-105">hello **SQL servers** blade is displayed.</span></span>
   
    ![Localize o servidor de banco de dados SQL no portal de saudação][b21-FindServerInPortal]
4. <span data-ttu-id="b3de8-107">Para sua conveniência, clique em Olá minimizar controle Olá anteriormente **procurar** folha.</span><span class="sxs-lookup"><span data-stu-id="b3de8-107">For convenience, click hello minimize control on hello earlier **Browse** blade.</span></span>
5. <span data-ttu-id="b3de8-108">Na caixa de texto de filtro Olá, comece a digitar o nome de saudação do servidor.</span><span class="sxs-lookup"><span data-stu-id="b3de8-108">In hello filter text box, start typing hello name of your server.</span></span> <span data-ttu-id="b3de8-109">A linha é exibida.</span><span class="sxs-lookup"><span data-stu-id="b3de8-109">Your row is displayed.</span></span>
6. <span data-ttu-id="b3de8-110">Clique em linha de saudação do servidor.</span><span class="sxs-lookup"><span data-stu-id="b3de8-110">Click hello row for your server.</span></span> <span data-ttu-id="b3de8-111">Uma folha do servidor é exibida.</span><span class="sxs-lookup"><span data-stu-id="b3de8-111">A blade for your server is displayed.</span></span>
7. <span data-ttu-id="b3de8-112">Na folha do seu servidor, clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="b3de8-112">On your server blade, click **Settings**.</span></span> <span data-ttu-id="b3de8-113">Olá **configurações** folha é exibida.</span><span class="sxs-lookup"><span data-stu-id="b3de8-113">hello **Settings** blade is displayed.</span></span>
8. <span data-ttu-id="b3de8-114">Clique em **Firewall**.</span><span class="sxs-lookup"><span data-stu-id="b3de8-114">Click **Firewall**.</span></span> <span data-ttu-id="b3de8-115">Olá **as configurações do Firewall** folha é exibida.</span><span class="sxs-lookup"><span data-stu-id="b3de8-115">hello **Firewall Settings** blade is displayed.</span></span>
   
    ![Clique em Configurações > Firewall][b31-SettingsFirewallNavig]
9. <span data-ttu-id="b3de8-117">Clique em **Adicionar Cliente IP**.</span><span class="sxs-lookup"><span data-stu-id="b3de8-117">Click **Add Client IP**.</span></span> <span data-ttu-id="b3de8-118">Digite um nome para a nova regra na primeira caixa de texto de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3de8-118">Type in a name for your new rule into hello first text box.</span></span>
10. <span data-ttu-id="b3de8-119">Valores de intervalo de saudação desejado de endereços IP tipo no hello baixa e alta tooenable.</span><span class="sxs-lookup"><span data-stu-id="b3de8-119">Type in hello low and high IP address values for hello range you want tooenable.</span></span>
    
    * <span data-ttu-id="b3de8-120">Ele pode ser útil toohave Olá baixo valor final com **.0** e hello alta com **.255**.</span><span class="sxs-lookup"><span data-stu-id="b3de8-120">It can be handy toohave hello low value end with **.0** and hello high with **.255**.</span></span>
    
    ![Adicionar um tooallow de intervalo de endereço IP][b41-AddRange]
11. <span data-ttu-id="b3de8-122">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="b3de8-122">Click **Save**.</span></span>

<!-- Image references. -->

[b21-FindServerInPortal]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b21-v12portal-findsvr.png

[b31-SettingsFirewallNavig]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b31-v12portal-settingsfirewall.png

[b41-AddRange]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b41-v12portal-addrange.png



<!--
These includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-ip-address-22-v12portal.md
? includes/sql-database-include-ip-address-*.md
-->
