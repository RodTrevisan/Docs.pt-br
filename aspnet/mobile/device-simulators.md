---
uid: mobile/device-simulators
title: Simular dispositivos móveis populares para teste | Microsoft Docs
author: rick-anderson
description: Você pode baixar os emuladores de dispositivos móveis populares e navegadores seguindo estes links
ms.author: aspnetcontent
ms.date: 01/28/2011
ms.assetid: bfb5612e-c3ec-4f28-b43b-63d781aa2272
msc.legacyurl: /mobile/device-simulators
msc.type: content
ms.openlocfilehash: 092186a48a304c1b9e3e140e74f65dbe5a035e66
ms.sourcegitcommit: b28cd0313af316c051c2ff8549865bff67f2fbb4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37833679"
---
<a name="simulate-popular-mobile-devices-for-testing"></a>Simular dispositivos móveis populares para teste
====================
> Você pode baixar os emuladores de dispositivos móveis populares e navegadores seguindo estes links


| Dispositivo ou navegador | Emulador / Simulator |
| --- | --- |
| Navegador de virtualização hospedada no BrowserStack ![Navegador de virtualização hospedada no BrowserStack](device-simulators/_static/image1.png) | [Virtualização do BrowserStack hospedada no navegador](http://browserstack.com) testar seu ambiente local ou de produção em qualquer navegador em qualquer plataforma. Você pode criar um túnel entre seu computador e a rede de BrowserStack em sua própria máquina virtual hospedada. Certifique-se de obter o [extensão do Visual Studio BrowserStack](https://visualstudiogallery.msdn.microsoft.com/2dfa32b1-3c47-439d-b1c5-9e28be18b81c) para uma experiência ainda mais transparente. |
| Windows Phone | [Downloads do Windows Phone SDK](https://dev.windowsphone.com/downloadsdk) o Windows Phone Software Development Kit (SDK) inclui todas as ferramentas que você precisa para desenvolver aplicativos e jogos para Windows Phone |
| iPhone / iPod / iPad | [Electric Plum](http://www.electricplum.com/studio.aspx) iPhone e iPad simuladores para Windows, bem como uma responsiva ferramenta de design. Pode integrar-se a opção "Procurar com..." do VS 2012. |
| Android | [Home page do Android SDK](https://developer.android.com/sdk) |
| Opera Mobile / Opera Mini | Versões mais recentes: [ferramentas de desenvolvedor Opera doméstica](http://www.opera.com/developer/tools/) Opera Mini 4.2: [simulador baseado em Java Online](http://www.opera.com/mobile/demo/?ver=4) |
| Windows Mobile 6.5.3 | [Kit de ferramentas de desenvolvedor do Windows Mobile 6.5.3](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=c0213f68-2e01-4e5c-a8b2-35e081dcf1ca&amp;displaylang=en) Observe que para conceder o acesso à rede de telefone, você também precisa o adaptador de rede do VPC incluídos no [Virtual PC 2007](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=04d26402-3199-48a3-afa2-2dc0b40a73b6&amp;DisplayLang=en). Para conectar-se o IE no telefone para seu servidor de desenvolvimento do Visual Studio, consulte [postagem do blog de Kiran Patil](http://kiranpatils.wordpress.com/2009/11/19/access-internetlocal-website-from-your-windows-mobile-device-emulators/). |
| Windows Mobile 6.1 | [Imagens do emulador do Visual Studio 2005/2008](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=3d6f581e-c093-4b15-ab0c-a2ce5bffdb47) |

Observe que, se você quiser exibir seu aplicativo em um dispositivo móvel real (que é a única opção para testar totalmente o iPhone ou iPad, já que não há nenhum verdadeiro emulador para Windows) será necessário hospedar seu aplicativo no IIS ou IIS Express. Você não pode facilmente usar servidor de web interno do Visual Studio para isso, porque ele não responderá às solicitações de outros computadores.
