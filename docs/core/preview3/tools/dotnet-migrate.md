---
title: "dotnet-migrate 명령 | Microsoft 문서"
description: "dotnet-migrate 명령은 프로젝트와 모든 종속성을 마이그레이션합니다."
keywords: "dotnet-migrate, CLI, CLI 명령, .NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 11/13/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 0da07253-5ae1-42e9-9455-bffee9950952
translationtype: Human Translation
ms.sourcegitcommit: 796df1549a7553aa93158598d62338c02d4df73e
ms.openlocfilehash: 57ae01419c6f7a75970816e1245094c38c5247fa

---

#<a name="dotnet-migrate"></a>dotnet-migrate

[!INCLUDE[preview-warning](../../../includes/warning.md)]

## <a name="name"></a>이름 
dotnet-migrate - Preview 2 .NET Core 프로젝트를 RC4 .NET Core 프로젝트로 마이그레이션

## <a name="synopsis"></a>개요

`dotnet migrate [--help] [--template-file]  
    [--sdk-package-version] [--xproj-file]  
    [--skip-project-references]  [--report-file] [--format-report-file-json]
    [--skip-backup]
    [<arguments>]`

## <a name="description"></a>설명
`dotnet migrate` 명령은 유효한 Preview 2 `project.json` 기반 프로젝트를 유효한 RC4 `csproj` 프로젝트로 마이그레이션합니다. 기본적으로 이 명령은 루트 프로젝트와, 루트 프로젝트에 포함된 모든 프로젝트 참조를 마이그레이션합니다. 이 동작은 런타임에 `--skip-project-references` 옵션을 사용하여 사용하지 않도록 설정할 수 있습니다. 

마이그레이션은 다음 위치에서 수행할 수 있습니다.

* 마이그레이션할 `project.json` 파일을 지정하는 단일 프로젝트
* `global.json` 파일로 경로를 전달하여 `global.json` 파일에 지정된 모든 디렉터리
* 지정된 디렉터의 모든 하위 디렉터리(재귀적) 

migrate 명령은 마이그레이션된 `project.json` 파일을 `backup` 디렉터리에서 유지합니다. 이 디렉터리는 없는 경우 생성됩니다. `--skip-backup` 옵션을 사용하여 재정의할 수 있습니다. 

기본적으로 마이그레이션 작업은 표준 출력(STDOUT)에 마이그레이션 프로세스의 상태를 출력합니다. `--report-file` 옵션을 사용하는 경우 출력은 지정한 파일에도 저장됩니다. 

RC4부터 `dotnet migrate` 명령은 유효한 Preview 2 `project.json` 파일만 지원합니다. 즉, 오래된 DNX 또는 Preview 1 `project.json` 파일을 직접 csproj로 마이그레이션하는 데 사용할 수 없습니다. 먼저 Preview 2 project.json 파일로 마이그레이션한 다음 csproj 파일로 마이그레이션해야 합니다. 나중에 Preview 1 프로젝트에 대한 지원이 추가될 예정입니다. 

## <a name="options"></a>옵션

`-h|--help`

명령에 대한 간단한 도움말을 출력합니다.  

`-t|--template-file <TEMPLATE_FILE>`

마이그레이션에 사용할 템플릿 csproj 파일입니다. 기본적으로 `dotnet new`에서 삭제한 것과 동일한 템플릿이 사용됩니다. 

`-v|--sdk-package-version <VERSION>`

마이그레이션된 앱에서 참조할 sdk 패키지의 버전입니다. 기본값은 새 dotnet의 sdk 버전입니다.

`-x|--xproj-file <FILE>`

사용할 xproj 파일에 대한 경로입니다. 프로젝트 디렉터리에 둘 이상의 xproj 있을 때 필요합니다.

`-s|--skip-project-references [Debug|Release]`

마이그레이션 프로젝트 참조를 건너뜁니다. 기본적으로 프로젝트 참조는 재귀적으로 마이그레이션됩니다.

`-r|--report-file <REPORT_FILE>`

마이그레이션 보고서를 콘솔 외에도 파일에 출력합니다.

`--format-report-file-json <REPORT_FILE>`

사용자 메시지가 아닌 json으로 마이그레이션 보고서 파일을 출력합니다.

`--skip-backup`

마이그레이션을 완료한 후 project.json, global.json, 및 \*.xproj를 `backup` 디렉터리로 이동하는 작업을 건너뜁니다.

## <a name="examples"></a>예제

현재 디렉터리의 프로젝트와 해당하는 모든 프로젝트를 프로젝트 종속성으로 마이그레이션합니다.

`dotnet migrate`

`global.json` 파일에서 가리키는 프로젝트를 모두 마이그레이션합니다.

`dotnet migrate path/to/global.json`

현재 프로젝트만 마이그레이션하고 프로젝트 간 종속성은 마이그레이션하지 않으며, 특정 SDK 버전을 사용합니다.

`dotnet migrate -s -v 1.0.0-preview4`


<!--HONumber=Feb17_HO2-->


