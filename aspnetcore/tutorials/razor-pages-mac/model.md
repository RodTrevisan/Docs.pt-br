---
title: Adicionar um modelo a um aplicativo Páginas Razor do ASP.NET Core com o Visual Studio para Mac
author: rick-anderson
description: Saiba como adicionar um modelo para um aplicativo Páginas Razor no ASP.NET Core usando o Visual Studio para Mac.
monikerRange: '>= aspnetcore-2.0'
ms.author: riande
ms.date: 08/27/2017
uid: tutorials/razor-pages-mac/model
ms.openlocfilehash: 3ca6c9b9988b8335116b7248c6c4a89997d02b14
ms.sourcegitcommit: a1afd04758e663d7062a5bfa8a0d4dca38f42afc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36273268"
---
# <a name="add-a-model-to-an-aspnet-core-razor-pages-app-with-visual-studio-for-mac"></a>Adicionar um modelo a um aplicativo Páginas Razor do ASP.NET Core com o Visual Studio para Mac

[!INCLUDE [model1](../../includes/RP/model1.md)]

## <a name="add-a-data-model"></a>Adicionar um modelo de dados

* No Gerenciador de Soluções, clique com o botão direito do mouse no projeto **RazorPagesMovie** e então selecione **Adicionar** > **Nova Pasta**. Nomeie a pasta *Models*.
* Clique com o botão direito do mouse na pasta *Modelos* e, em seguida, selecione **Adicionar** > **Novo Arquivo**.
* Na caixa de diálogo **Novo Arquivo**:

  * Selecione **Geral** no painel esquerdo.
  * Selecione **Classe Vazia** no painel central.
  * Nomeie a classe **Movie** e selecione **Novo**.

[!INCLUDE [model 2](../../includes/RP/model2.md)]

[!INCLUDE [model 2a](../../includes/RP/model2a.md)]

[!code-csharp[](../../tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie/Startup.cs?name=snippet_ConfigureServices2&highlight=3-6)]

Clique com o botão direito do mouse em uma linha curvada vermelha, por exemplo, `MovieContext` na linha `services.AddDbContext<MovieContext>(options =>`. Selecione **Correção Rápida > using RazorPagesMovie.Models;**. O Visual studio adiciona a instrução using.

Compile o projeto para verificar se não há erros.

![Criar página](model/red.png)

### <a name="entity-framework-core-nuget-packages-for-migrations"></a>Pacotes NuGet do Entity Framework Core para migrações

As ferramentas do EF para a CLI (interface de linha de comando) são fornecidas em [Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet). Clique no link [Microsoft.EntityFrameworkCore.Tools.DotNet](https://www.nuget.org/packages/Microsoft.EntityFrameworkCore.Tools.DotNet) para obter o número de versão a ser usado. Para instalar esse pacote, adicione-o à coleção `DotNetCliToolReference` no arquivo *.csproj*. **Observação:** é necessário instalar este pacote editando o arquivo *.csproj*; não é possível usar o comando `install-package` ou a GUI do Gerenciador de Pacotes.

Para editar um arquivo *.csproj*:

* Selecione **Arquivo** > **Abrir**, e, em seguida, selecione o arquivo *.csproj*.
* Selecione **Opções**.
* Alterar **Abrir com** para **Editor de código-fonte**.

![Editar o arquivo csproj](model/csproj.png)

Adicione a referência da ferramenta `Microsoft.EntityFrameworkCore.Tools.DotNet` para o segundo **\<ItemGroup>**.:

[!code-xml[](../../tutorials/razor-pages/razor-pages-start/snapshot_cli_sample/RazorPagesMovie/RazorPagesMovie.cli.csproj?highlight=10)]

Os números de versão mostrados no código a seguir estavam corretos no momento da gravação.

[!INCLUDE [model3](../../includes/RP/model3.md)]

[!INCLUDE [model 4x](../../includes/RP/model4x.md)]

[!INCLUDE [model 4 exit](../../includes/RP/model4exit.md)]

[!INCLUDE [model 4](../../includes/RP/model4.md)]

### <a name="add-the-pagesmovies-files-to-the-project"></a>Adicionar os arquivos de páginas/filmes ao projeto

* No Visual Studio, clique com o botão direito do mouse na pasta *Páginas* e selecione **Adicionar > Adicionar Pasta Existente**.
* Selecione a pasta *Filmes*.
* Na caixa de diálogo *Escolher arquivos para incluir no projeto*, selecione **Incluir Todos**.

O tutorial a seguir explica os arquivos criados por scaffolding.

> [!div class="step-by-step"]
> [Anterior: Introdução](xref:tutorials/razor-pages-mac/razor-pages-start)
> [Próximo: Páginas Razor geradas por scaffolding](xref:tutorials/razor-pages-mac/page)
