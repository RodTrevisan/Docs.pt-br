---
uid: mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-cs
title: Exibindo uma tabela de banco de dados (c#) | Microsoft Docs
author: microsoft
description: "Neste tutorial, demonstrarei dois métodos de exibição de um conjunto de registros do banco de dados. Mostrar dois métodos de formatação de um conjunto de registros do banco de dados em um HTML ta..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/07/2008
ms.topic: article
ms.assetid: d6e758b6-6571-484d-a132-34ee6c47747a
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-cs
msc.type: authoredcontent
ms.openlocfilehash: 37ea081df2ee26e186669b815a4d769e1976ae9c
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/10/2017
---
<a name="displaying-a-table-of-database-data-c"></a><span data-ttu-id="e7703-104">Exibindo uma tabela de banco de dados (c#)</span><span class="sxs-lookup"><span data-stu-id="e7703-104">Displaying a Table of Database Data (C#)</span></span>
====================
<span data-ttu-id="e7703-105">por [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="e7703-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="e7703-106">Baixar PDF</span><span class="sxs-lookup"><span data-stu-id="e7703-106">Download PDF</span></span>](http://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_11_CS.pdf)

> <span data-ttu-id="e7703-107">Neste tutorial, demonstrarei dois métodos de exibição de um conjunto de registros do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e7703-107">In this tutorial, I demonstrate two methods of displaying a set of database records.</span></span> <span data-ttu-id="e7703-108">Vou mostrar dois métodos de formatação de um conjunto de registros do banco de dados em uma tabela HTML.</span><span class="sxs-lookup"><span data-stu-id="e7703-108">I show two methods of formatting a set of database records in an HTML table.</span></span> <span data-ttu-id="e7703-109">Primeiro, vou mostrar como você pode formatar os registros de banco de dados diretamente dentro de um modo de exibição.</span><span class="sxs-lookup"><span data-stu-id="e7703-109">First, I show how you can format the database records directly within a view.</span></span> <span data-ttu-id="e7703-110">Em seguida, demonstrarei como você pode tirar proveito das existe meio-termo ao formatar os registros do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e7703-110">Next, I demonstrate how you can take advantage of partials when formatting database records.</span></span>


<span data-ttu-id="e7703-111">O objetivo deste tutorial é explicar como você pode exibir uma tabela HTML do banco de dados em um aplicativo ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="e7703-111">The goal of this tutorial is to explain how you can display an HTML table of database data in an ASP.NET MVC application.</span></span> <span data-ttu-id="e7703-112">Primeiro, você aprenderá a usar as ferramentas de scaffolding incluídas no Visual Studio para gerar uma exibição que exibe um conjunto de registros automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e7703-112">First, you learn how to use the scaffolding tools included in Visual Studio to generate a view that displays a set of records automatically.</span></span> <span data-ttu-id="e7703-113">Em seguida, você aprenderá a usar um parcial como um modelo quando os registros do banco de dados de formatação.</span><span class="sxs-lookup"><span data-stu-id="e7703-113">Next, you learn how to use a partial as a template when formatting database records.</span></span>

## <a name="create-the-model-classes"></a><span data-ttu-id="e7703-114">Criar as Classes de modelo</span><span class="sxs-lookup"><span data-stu-id="e7703-114">Create the Model Classes</span></span>

<span data-ttu-id="e7703-115">Vamos para exibir o conjunto de registros da tabela de banco de dados de filmes.</span><span class="sxs-lookup"><span data-stu-id="e7703-115">We are going to display the set of records from the Movies database table.</span></span> <span data-ttu-id="e7703-116">A tabela de banco de dados de filmes contém as seguintes colunas:</span><span class="sxs-lookup"><span data-stu-id="e7703-116">The Movies database table contains the following columns:</span></span>

<a id="0.3_table01"></a>


| <span data-ttu-id="e7703-117">**Nome da coluna**</span><span class="sxs-lookup"><span data-stu-id="e7703-117">**Column Name**</span></span> | <span data-ttu-id="e7703-118">**Tipo de dados**</span><span class="sxs-lookup"><span data-stu-id="e7703-118">**Data Type**</span></span> | <span data-ttu-id="e7703-119">**Permitir nulos**</span><span class="sxs-lookup"><span data-stu-id="e7703-119">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e7703-120">Id</span><span class="sxs-lookup"><span data-stu-id="e7703-120">Id</span></span> | <span data-ttu-id="e7703-121">int</span><span class="sxs-lookup"><span data-stu-id="e7703-121">Int</span></span> | <span data-ttu-id="e7703-122">False</span><span class="sxs-lookup"><span data-stu-id="e7703-122">False</span></span> |
| <span data-ttu-id="e7703-123">Título</span><span class="sxs-lookup"><span data-stu-id="e7703-123">Title</span></span> | <span data-ttu-id="e7703-124">Nvarchar (200)</span><span class="sxs-lookup"><span data-stu-id="e7703-124">Nvarchar(200)</span></span> | <span data-ttu-id="e7703-125">False</span><span class="sxs-lookup"><span data-stu-id="e7703-125">False</span></span> |
| <span data-ttu-id="e7703-126">Diretor</span><span class="sxs-lookup"><span data-stu-id="e7703-126">Director</span></span> | <span data-ttu-id="e7703-127">Nvarchar (50)</span><span class="sxs-lookup"><span data-stu-id="e7703-127">NVarchar(50)</span></span> | <span data-ttu-id="e7703-128">False</span><span class="sxs-lookup"><span data-stu-id="e7703-128">False</span></span> |
| <span data-ttu-id="e7703-129">DateReleased</span><span class="sxs-lookup"><span data-stu-id="e7703-129">DateReleased</span></span> | <span data-ttu-id="e7703-130">DateTime</span><span class="sxs-lookup"><span data-stu-id="e7703-130">DateTime</span></span> | <span data-ttu-id="e7703-131">False</span><span class="sxs-lookup"><span data-stu-id="e7703-131">False</span></span> |


<span data-ttu-id="e7703-132">Para representar a tabela de filmes em nosso aplicativo ASP.NET MVC, precisamos criar uma classe de modelo.</span><span class="sxs-lookup"><span data-stu-id="e7703-132">In order to represent the Movies table in our ASP.NET MVC application, we need to create a model class.</span></span> <span data-ttu-id="e7703-133">Neste tutorial, usamos o Entity Framework da Microsoft para criar nossas classes de modelo.</span><span class="sxs-lookup"><span data-stu-id="e7703-133">In this tutorial, we use the Microsoft Entity Framework to create our model classes.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="e7703-134">Neste tutorial, usamos o Entity Framework da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e7703-134">In this tutorial, we use the Microsoft Entity Framework.</span></span> <span data-ttu-id="e7703-135">No entanto, é importante entender que você pode usar uma variedade de tecnologias diferentes para interagir com um banco de dados de um aplicativo ASP.NET MVC incluindo LINQ to SQL, o NHibernate ou ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="e7703-135">However, it is important to understand that you can use a variety of different technologies to interact with a database from an ASP.NET MVC application including LINQ to SQL, NHibernate, or ADO.NET.</span></span>


<span data-ttu-id="e7703-136">Siga estas etapas para iniciar o Assistente de modelo de dados de entidade:</span><span class="sxs-lookup"><span data-stu-id="e7703-136">Follow these steps to launch the Entity Data Model Wizard:</span></span>

1. <span data-ttu-id="e7703-137">Clique na pasta de modelos na janela do Gerenciador de soluções e selecione a opção de menu **adicionar, o novo Item**.</span><span class="sxs-lookup"><span data-stu-id="e7703-137">Right-click the Models folder in the Solution Explorer window and the select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="e7703-138">Selecione o **dados** categoria e selecione o **modelo de dados de entidade ADO.NET** modelo.</span><span class="sxs-lookup"><span data-stu-id="e7703-138">Select the **Data** category and select the **ADO.NET Entity Data Model** template.</span></span>
3. <span data-ttu-id="e7703-139">Forneça o nome de seu modelo de dados *MoviesDBModel.edmx* e clique no **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="e7703-139">Give your data model the name *MoviesDBModel.edmx* and click the **Add** button.</span></span>

<span data-ttu-id="e7703-140">Depois de clicar no botão Adicionar, o Assistente de modelo de dados de entidade é exibida (consulte a Figura 1).</span><span class="sxs-lookup"><span data-stu-id="e7703-140">After you click the Add button, the Entity Data Model Wizard appears (see Figure 1).</span></span> <span data-ttu-id="e7703-141">Siga estas etapas para concluir o Assistente:</span><span class="sxs-lookup"><span data-stu-id="e7703-141">Follow these steps to complete the wizard:</span></span>

1. <span data-ttu-id="e7703-142">No **escolher o modelo de conteúdo** etapa, selecione o **gerar do banco de dados** opção.</span><span class="sxs-lookup"><span data-stu-id="e7703-142">In the **Choose Model Contents** step, select the **Generate from database** option.</span></span>
2. <span data-ttu-id="e7703-143">No **escolha sua Conexão de dados** etapa, use o *MoviesDB.mdf* conexão de dados e o nome *MoviesDBEntities* para as configurações de conexão.</span><span class="sxs-lookup"><span data-stu-id="e7703-143">In the **Choose Your Data Connection** step, use the *MoviesDB.mdf* data connection and the name *MoviesDBEntities* for the connection settings.</span></span> <span data-ttu-id="e7703-144">Clique o **próximo** botão.</span><span class="sxs-lookup"><span data-stu-id="e7703-144">Click the **Next** button.</span></span>
3. <span data-ttu-id="e7703-145">No **escolher seus objetos de banco de dados** etapa, expanda o nó tabelas, selecione a tabela de filmes.</span><span class="sxs-lookup"><span data-stu-id="e7703-145">In the **Choose Your Database Objects** step, expand the Tables node, select the Movies table.</span></span> <span data-ttu-id="e7703-146">Insira o namespace *modelos* e clique no **concluir** botão.</span><span class="sxs-lookup"><span data-stu-id="e7703-146">Enter the namespace *Models* and click the **Finish** button.</span></span>


<span data-ttu-id="e7703-147">[![Criando LINQ para classes do SQL](displaying-a-table-of-database-data-cs/_static/image1.jpg)](displaying-a-table-of-database-data-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e7703-147">[![Creating LINQ to SQL classes](displaying-a-table-of-database-data-cs/_static/image1.jpg)](displaying-a-table-of-database-data-cs/_static/image1.png)</span></span>

<span data-ttu-id="e7703-148">**Figura 01**: Criando classes LINQ to SQL ([clique para exibir a imagem em tamanho normal](displaying-a-table-of-database-data-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="e7703-148">**Figure 01**: Creating LINQ to SQL classes ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image2.png))</span></span>


<span data-ttu-id="e7703-149">Depois de concluir o Assistente de modelo de dados de entidade, abre o Designer de modelo de dados de entidade.</span><span class="sxs-lookup"><span data-stu-id="e7703-149">After you complete the Entity Data Model Wizard, the Entity Data Model Designer opens.</span></span> <span data-ttu-id="e7703-150">O Designer deve exibir a entidade de filmes (consulte a Figura 2).</span><span class="sxs-lookup"><span data-stu-id="e7703-150">The Designer should display the Movies entity (see Figure 2).</span></span>


<span data-ttu-id="e7703-151">[![O Designer de modelo de dados de entidade](displaying-a-table-of-database-data-cs/_static/image2.jpg)](displaying-a-table-of-database-data-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="e7703-151">[![The Entity Data Model Designer](displaying-a-table-of-database-data-cs/_static/image2.jpg)](displaying-a-table-of-database-data-cs/_static/image3.png)</span></span>

<span data-ttu-id="e7703-152">**Figura 02**: O Designer de modelo de dados de entidade ([clique para exibir a imagem em tamanho normal](displaying-a-table-of-database-data-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="e7703-152">**Figure 02**: The Entity Data Model Designer ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image4.png))</span></span>


<span data-ttu-id="e7703-153">É preciso fazer uma alteração antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="e7703-153">We need to make one change before we continue.</span></span> <span data-ttu-id="e7703-154">O Assistente de dados de entidade gera uma classe de modelo chamada *filmes* que representa a tabela de banco de dados de filmes.</span><span class="sxs-lookup"><span data-stu-id="e7703-154">The Entity Data Wizard generates a model class named *Movies* that represents the Movies database table.</span></span> <span data-ttu-id="e7703-155">Como vamos usar a classe de filmes para representar um filme específico, é preciso modificar o nome da classe a ser *filme* em vez de *filmes* (singular em vez de no plural).</span><span class="sxs-lookup"><span data-stu-id="e7703-155">Because we'll use the Movies class to represent a particular movie, we need to modify the name of the class to be *Movie* instead of *Movies* (singular rather than plural).</span></span>

<span data-ttu-id="e7703-156">Clique duas vezes no nome da classe na superfície do designer e alterar o nome da classe de filmes para filme.</span><span class="sxs-lookup"><span data-stu-id="e7703-156">Double-click the name of the class on the designer surface and change the name of the class from Movies to Movie.</span></span> <span data-ttu-id="e7703-157">Depois de fazer essa alteração, clique no **salvar** botão (o ícone de disquete) para gerar a classe de filme.</span><span class="sxs-lookup"><span data-stu-id="e7703-157">After making this change, click the **Save** button (the icon of the floppy disk) to generate the Movie class.</span></span>

## <a name="create-the-movies-controller"></a><span data-ttu-id="e7703-158">Criar o controlador de filmes</span><span class="sxs-lookup"><span data-stu-id="e7703-158">Create the Movies Controller</span></span>

<span data-ttu-id="e7703-159">Agora que temos uma maneira de representar nossos registros do banco de dados, podemos criar um controlador que retorna a coleção de filmes.</span><span class="sxs-lookup"><span data-stu-id="e7703-159">Now that we have a way to represent our database records, we can create a controller that returns the collection of movies.</span></span> <span data-ttu-id="e7703-160">Dentro da janela do Gerenciador de soluções do Visual Studio, clique na pasta controladores e selecione a opção de menu **adicionar, controlador** (consulte a Figura 3).</span><span class="sxs-lookup"><span data-stu-id="e7703-160">Within the Visual Studio Solution Explorer window, right-click the Controllers folder and select the menu option **Add, Controller** (see Figure 3).</span></span>


<span data-ttu-id="e7703-161">[![O Menu do controlador de adição](displaying-a-table-of-database-data-cs/_static/image3.jpg)](displaying-a-table-of-database-data-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="e7703-161">[![The Add Controller Menu](displaying-a-table-of-database-data-cs/_static/image3.jpg)](displaying-a-table-of-database-data-cs/_static/image5.png)</span></span>

<span data-ttu-id="e7703-162">**Figura 03**: Adicionar controlador Menu ([clique para exibir a imagem em tamanho normal](displaying-a-table-of-database-data-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="e7703-162">**Figure 03**: The Add Controller Menu ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image6.png))</span></span>


<span data-ttu-id="e7703-163">Quando o **Adicionar controlador** caixa de diálogo for exibida, insira o nome do controlador MovieController (consulte a Figura 4).</span><span class="sxs-lookup"><span data-stu-id="e7703-163">When the **Add Controller** dialog appears, enter the controller name MovieController (see Figure 4).</span></span> <span data-ttu-id="e7703-164">Clique o **adicionar** botão para adicionar o novo controlador.</span><span class="sxs-lookup"><span data-stu-id="e7703-164">Click the **Add** button to add the new controller.</span></span>


<span data-ttu-id="e7703-165">[![A caixa de diálogo Adicionar controlador](displaying-a-table-of-database-data-cs/_static/image4.jpg)](displaying-a-table-of-database-data-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="e7703-165">[![The Add Controller dialog](displaying-a-table-of-database-data-cs/_static/image4.jpg)](displaying-a-table-of-database-data-cs/_static/image7.png)</span></span>

<span data-ttu-id="e7703-166">**Figura 04**: caixa de diálogo a adicionar controlador ([clique para exibir a imagem em tamanho normal](displaying-a-table-of-database-data-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="e7703-166">**Figure 04**: The Add Controller dialog([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image8.png))</span></span>


<span data-ttu-id="e7703-167">É preciso modificar a ação de Index () exposta pelo controlador de filme, de forma que ele retorna o conjunto de registros do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e7703-167">We need to modify the Index() action exposed by the Movie controller so that it returns the set of database records.</span></span> <span data-ttu-id="e7703-168">Modificar o controlador para que ele se parece com o controlador na listagem 1.</span><span class="sxs-lookup"><span data-stu-id="e7703-168">Modify the controller so that it looks like the controller in Listing 1.</span></span>

<span data-ttu-id="e7703-169">**Listando 1 – Controllers\MovieController.cs**</span><span class="sxs-lookup"><span data-stu-id="e7703-169">**Listing 1 – Controllers\MovieController.cs**</span></span>

[!code-csharp[Main](displaying-a-table-of-database-data-cs/samples/sample1.cs)]

<span data-ttu-id="e7703-170">Na listagem 1, a classe MoviesDBEntities é usada para representar o banco de dados MoviesDB.</span><span class="sxs-lookup"><span data-stu-id="e7703-170">In Listing 1, the MoviesDBEntities class is used to represent the MoviesDB database.</span></span> <span data-ttu-id="e7703-171">Para usar essa classe, você precisa importar o namespace MvcApplication1.Models como este:</span><span class="sxs-lookup"><span data-stu-id="e7703-171">To use this class, you need to import the MvcApplication1.Models namespace like this:</span></span>

<span data-ttu-id="e7703-172">usando MvcApplication1.Models;</span><span class="sxs-lookup"><span data-stu-id="e7703-172">using MvcApplication1.Models;</span></span>

<span data-ttu-id="e7703-173">A expressão *entidades. MovieSet.ToList()* retorna o conjunto de todos os filmes da tabela de banco de dados de filmes.</span><span class="sxs-lookup"><span data-stu-id="e7703-173">The expression *entities.MovieSet.ToList()* returns the set of all movies from the Movies database table.</span></span>

## <a name="create-the-view"></a><span data-ttu-id="e7703-174">Criar o modo de exibição</span><span class="sxs-lookup"><span data-stu-id="e7703-174">Create the View</span></span>

<span data-ttu-id="e7703-175">É a maneira mais fácil de exibir um conjunto de registros do banco de dados em uma tabela HTML aproveitar o scaffolding fornecido pelo Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e7703-175">The easiest way to display a set of database records in an HTML table is to take advantage of the scaffolding provided by Visual Studio.</span></span>

<span data-ttu-id="e7703-176">Criar seu aplicativo, selecionando a opção de menu **criar, compilar solução**.</span><span class="sxs-lookup"><span data-stu-id="e7703-176">Build your application by selecting the menu option **Build, Build Solution**.</span></span> <span data-ttu-id="e7703-177">Você deve criar seu aplicativo antes de abrir o **adicionar exibição** suas classes de dados ou de caixa de diálogo não aparecerão na caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e7703-177">You must build your application before opening the **Add View** dialog or your data classes won't appear in the dialog.</span></span>

<span data-ttu-id="e7703-178">A ação Index () e selecione a opção de menu **adicionar exibição** (consulte a Figura 5).</span><span class="sxs-lookup"><span data-stu-id="e7703-178">Right-click the Index() action and select the menu option **Add View** (see Figure 5).</span></span>


<span data-ttu-id="e7703-179">[![Adicionando uma exibição](displaying-a-table-of-database-data-cs/_static/image5.jpg)](displaying-a-table-of-database-data-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="e7703-179">[![Adding a view](displaying-a-table-of-database-data-cs/_static/image5.jpg)](displaying-a-table-of-database-data-cs/_static/image9.png)</span></span>

<span data-ttu-id="e7703-180">**Figura 05**: adicionando uma exibição ([clique para exibir a imagem em tamanho normal](displaying-a-table-of-database-data-cs/_static/image10.png))</span><span class="sxs-lookup"><span data-stu-id="e7703-180">**Figure 05**: Adding a view ([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image10.png))</span></span>


<span data-ttu-id="e7703-181">No **adicionar exibição** caixa de diálogo, marque a caixa de seleção **criar uma exibição fortemente tipada**.</span><span class="sxs-lookup"><span data-stu-id="e7703-181">In the **Add View** dialog, check the checkbox labeled **Create a strongly-typed view**.</span></span> <span data-ttu-id="e7703-182">Selecione a classe de filme como o **exibir dados de classe**.</span><span class="sxs-lookup"><span data-stu-id="e7703-182">Select the Movie class as the **view data class**.</span></span> <span data-ttu-id="e7703-183">Selecione *lista* como o **exibir conteúdo** (veja a Figura 6).</span><span class="sxs-lookup"><span data-stu-id="e7703-183">Select *List* as the **view content** (see Figure 6).</span></span> <span data-ttu-id="e7703-184">Selecionar essas opções irá gerar uma exibição fortemente tipada que exibe uma lista de filmes.</span><span class="sxs-lookup"><span data-stu-id="e7703-184">Selecting these options will generate a strongly-typed view that displays a list of movies.</span></span>


<span data-ttu-id="e7703-185">[![A caixa de diálogo Adicionar modo de exibição](displaying-a-table-of-database-data-cs/_static/image6.jpg)](displaying-a-table-of-database-data-cs/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="e7703-185">[![The Add View dialog](displaying-a-table-of-database-data-cs/_static/image6.jpg)](displaying-a-table-of-database-data-cs/_static/image11.png)</span></span>

<span data-ttu-id="e7703-186">**Figura 06**: caixa de diálogo Adicionar exibir ([clique para exibir a imagem em tamanho normal](displaying-a-table-of-database-data-cs/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="e7703-186">**Figure 06**: The Add View dialog([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image12.png))</span></span>


<span data-ttu-id="e7703-187">Depois de clicar no **adicionar** botão, o modo de exibição na lista 2 é gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e7703-187">After you click the **Add** button, the view in Listing 2 is generated automatically.</span></span> <span data-ttu-id="e7703-188">Essa exibição contém o código necessário para iterar pela coleção de filmes e exibir cada uma das propriedades de um filme.</span><span class="sxs-lookup"><span data-stu-id="e7703-188">This view contains the code required to iterate through the collection of movies and display each of the properties of a movie.</span></span>

<span data-ttu-id="e7703-189">**A listagem 2 – Views\Movie\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="e7703-189">**Listing 2 – Views\Movie\Index.aspx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample2.aspx)]

<span data-ttu-id="e7703-190">Você pode executar o aplicativo, selecionando a opção de menu **depurar, iniciar depuração** (ou pressionar a tecla F5).</span><span class="sxs-lookup"><span data-stu-id="e7703-190">You can run the application by selecting the menu option **Debug, Start Debugging** (or hitting the F5 key).</span></span> <span data-ttu-id="e7703-191">Executando o aplicativo inicia o Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="e7703-191">Running the application launches Internet Explorer.</span></span> <span data-ttu-id="e7703-192">Se você navegar para a URL de /Movie, em seguida, você verá a página na Figura 7.</span><span class="sxs-lookup"><span data-stu-id="e7703-192">If you navigate to the /Movie URL then you'll see the page in Figure 7.</span></span>


<span data-ttu-id="e7703-193">[![Uma tabela de filmes](displaying-a-table-of-database-data-cs/_static/image7.jpg)](displaying-a-table-of-database-data-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="e7703-193">[![A table of movies](displaying-a-table-of-database-data-cs/_static/image7.jpg)](displaying-a-table-of-database-data-cs/_static/image13.png)</span></span>

<span data-ttu-id="e7703-194">**Figura 07**: uma tabela de filmes ([clique para exibir a imagem em tamanho normal](displaying-a-table-of-database-data-cs/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="e7703-194">**Figure 07**: A table of movies([Click to view full-size image](displaying-a-table-of-database-data-cs/_static/image14.png))</span></span>


<span data-ttu-id="e7703-195">Se você não gosta nada sobre a aparência da grade de registros do banco de dados na Figura 7, em seguida, você simplesmente pode modificar a exibição do índice.</span><span class="sxs-lookup"><span data-stu-id="e7703-195">If you don't like anything about the appearance of the grid of database records in Figure 7 then you can simply modify the Index view.</span></span> <span data-ttu-id="e7703-196">Por exemplo, você pode alterar o *DateReleased* cabeçalho para *data de lançamento* modificando a exibição do índice.</span><span class="sxs-lookup"><span data-stu-id="e7703-196">For example, you can change the *DateReleased* header to *Date Released* by modifying the Index view.</span></span>

## <a name="create-a-template-with-a-partial"></a><span data-ttu-id="e7703-197">Criar um modelo com um parcial</span><span class="sxs-lookup"><span data-stu-id="e7703-197">Create a Template with a Partial</span></span>

<span data-ttu-id="e7703-198">Quando uma exibição é muito complicada, é recomendável iniciar invadir o modo de exibição existe meio-termo.</span><span class="sxs-lookup"><span data-stu-id="e7703-198">When a view gets too complicated, it is a good idea to start breaking the view into partials.</span></span> <span data-ttu-id="e7703-199">Usar existe meio-termo torna mais fácil de entender e manter seus modos de exibição.</span><span class="sxs-lookup"><span data-stu-id="e7703-199">Using partials makes your views easier to understand and maintain.</span></span> <span data-ttu-id="e7703-200">Vamos criar um parcial que podemos usar como modelo para formatar cada um dos registros de banco de dados do filme.</span><span class="sxs-lookup"><span data-stu-id="e7703-200">We'll create a partial that we can use as a template to format each of the movie database records.</span></span>

<span data-ttu-id="e7703-201">Siga estas etapas para criar o parcial:</span><span class="sxs-lookup"><span data-stu-id="e7703-201">Follow these steps to create the partial:</span></span>

1. <span data-ttu-id="e7703-202">Clique na pasta Views\Movie e selecione a opção de menu **adicionar exibição**.</span><span class="sxs-lookup"><span data-stu-id="e7703-202">Right-click the Views\Movie folder and select the menu option **Add View**.</span></span>
2. <span data-ttu-id="e7703-203">Marque a caixa de seleção *criar uma exibição parcial (. ascx)*.</span><span class="sxs-lookup"><span data-stu-id="e7703-203">Check the checkbox labeled *Create a partial view (.ascx)*.</span></span>
3. <span data-ttu-id="e7703-204">Nomeie o parcial *MovieTemplate*.</span><span class="sxs-lookup"><span data-stu-id="e7703-204">Name the partial *MovieTemplate*.</span></span>
4. <span data-ttu-id="e7703-205">Marque a caixa de seleção **criar uma exibição fortemente tipada**.</span><span class="sxs-lookup"><span data-stu-id="e7703-205">Check the checkbox labeled **Create a strongly-typed view**.</span></span>
5. <span data-ttu-id="e7703-206">Selecione um filme, como o *exibir dados de classe*.</span><span class="sxs-lookup"><span data-stu-id="e7703-206">Select Movie as the *view data class*.</span></span>
6. <span data-ttu-id="e7703-207">Selecione vazio como o *exibir conteúdo*.</span><span class="sxs-lookup"><span data-stu-id="e7703-207">Select Empty as the *view content*.</span></span>
7. <span data-ttu-id="e7703-208">Clique o **adicionar** botão para adicionar o parcial para seu projeto.</span><span class="sxs-lookup"><span data-stu-id="e7703-208">Click the **Add** button to add the partial to your project.</span></span>

<span data-ttu-id="e7703-209">Depois de concluir essas etapas, modifique o MovieTemplate parcial para se parecer com a listagem 3.</span><span class="sxs-lookup"><span data-stu-id="e7703-209">After you complete these steps, modify the MovieTemplate partial to look like Listing 3.</span></span>

<span data-ttu-id="e7703-210">**A listagem 3 – Views\Movie\MovieTemplate.ascx**</span><span class="sxs-lookup"><span data-stu-id="e7703-210">**Listing 3 – Views\Movie\MovieTemplate.ascx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample3.aspx)]

<span data-ttu-id="e7703-211">Parcial na listagem 3 contém um modelo para uma única linha de registros.</span><span class="sxs-lookup"><span data-stu-id="e7703-211">The partial in Listing 3 contains a template for a single row of records.</span></span>

<span data-ttu-id="e7703-212">O modo de exibição do índice modificado na listagem 4 usa o MovieTemplate parcial.</span><span class="sxs-lookup"><span data-stu-id="e7703-212">The modified Index view in Listing 4 uses the MovieTemplate partial.</span></span>

<span data-ttu-id="e7703-213">**A listagem 4 – Views\Movie\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="e7703-213">**Listing 4 – Views\Movie\Index.aspx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample4.aspx)]

<span data-ttu-id="e7703-214">O modo de exibição na listagem 4 contém um loop foreach que itera por meio de todos os filmes.</span><span class="sxs-lookup"><span data-stu-id="e7703-214">The view in Listing 4 contains a foreach loop that iterates through all of the movies.</span></span> <span data-ttu-id="e7703-215">Para cada filme, o MovieTemplate parcial é usado para formatar o filme.</span><span class="sxs-lookup"><span data-stu-id="e7703-215">For each movie, the MovieTemplate partial is used to format the movie.</span></span> <span data-ttu-id="e7703-216">O MovieTemplate é renderizado, chamando o método auxiliar RenderPartial().</span><span class="sxs-lookup"><span data-stu-id="e7703-216">The MovieTemplate is rendered by calling the RenderPartial() helper method.</span></span>

<span data-ttu-id="e7703-217">O modo de exibição do índice modificado renderiza a mesma tabela HTML de registros do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e7703-217">The modified Index view renders the very same HTML table of database records.</span></span> <span data-ttu-id="e7703-218">No entanto, o modo de exibição foi bastante simplificado.</span><span class="sxs-lookup"><span data-stu-id="e7703-218">However, the view has been greatly simplified.</span></span>


<span data-ttu-id="e7703-219">O método RenderPartial() é diferente do que a maioria dos outros métodos auxiliares porque ele não retorna uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="e7703-219">The RenderPartial() method is different than most of the other helper methods because it does not return a string.</span></span> <span data-ttu-id="e7703-220">Portanto, você deve chamar o método RenderPartial() usando &lt;% % Html.RenderPartial();&gt; em vez de &lt;% = Html.RenderPartial(); %&gt;.</span><span class="sxs-lookup"><span data-stu-id="e7703-220">Therefore, you must call the RenderPartial() method using &lt;% Html.RenderPartial(); %&gt; instead of &lt;%= Html.RenderPartial(); %&gt;.</span></span>


## <a name="summary"></a><span data-ttu-id="e7703-221">Resumo</span><span class="sxs-lookup"><span data-stu-id="e7703-221">Summary</span></span>

<span data-ttu-id="e7703-222">O objetivo deste tutorial era explicam como você pode exibir um conjunto de registros do banco de dados em uma tabela HTML.</span><span class="sxs-lookup"><span data-stu-id="e7703-222">The goal of this tutorial was to explain how you can display a set of database records in an HTML table.</span></span> <span data-ttu-id="e7703-223">Primeiro, você aprendeu como retornar um conjunto de registros do banco de dados de uma ação do controlador, aproveitando o Entity Framework da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e7703-223">First, you learned how to return a set of database records from a controller action by taking advantage of the Microsoft Entity Framework.</span></span> <span data-ttu-id="e7703-224">Em seguida, você aprendeu a usar scaffolding do Visual Studio para gerar uma exibição que exibe uma coleção de itens automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e7703-224">Next, you learned how to use Visual Studio scaffolding to generate a view that displays a collection of items automatically.</span></span> <span data-ttu-id="e7703-225">Por fim, você aprendeu a simplificar a exibição aproveitando um parcial.</span><span class="sxs-lookup"><span data-stu-id="e7703-225">Finally, you learned how to simplify the view by taking advantage of a partial.</span></span> <span data-ttu-id="e7703-226">Você aprendeu a usar um parcial como um modelo para que você pode formatar cada registro do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e7703-226">You learned how to use a partial as a template so that you can format each database record.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="e7703-227">[Anterior](creating-model-classes-with-linq-to-sql-cs.md)
[Próximo](performing-simple-validation-cs.md)</span><span class="sxs-lookup"><span data-stu-id="e7703-227">[Previous](creating-model-classes-with-linq-to-sql-cs.md)
[Next](performing-simple-validation-cs.md)</span></span>