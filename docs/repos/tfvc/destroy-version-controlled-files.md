---
title: Destroy Version Controlled Files
titleSuffix: Azure Repos
description: Destroy Version Controlled Files
ms.assetid: 9be4d796-b448-4084-a102-a0e95e7b0053
ms.technology: devops-code-tfvc
ms.topic: conceptual
ms.date: 06/30/2022
monikerRange: '<= azure-devops'
---


# Destroy Version Controlled Files

[!INCLUDE [version-lt-eq-azure-devops](../../includes/version-lt-eq-azure-devops.md)]
[!INCLUDE [version-vs-gt-2013](../../includes/version-vs-gt-2013.md)]

Over time, a version control server acquires a growing number of files and folders. This can cause problems as you try to manage disk space requirements. You might be forced to remove all the projects and their hierarchies from version control. For example, a project might be created for learning purposes only, or perhaps some files are contaminated with a virus. Therefore, as a Team Foundation administrator, occasionally you may have to destroy files and folders that are under version control.

The following procedure shows you how to destroy files and folders by using the **tf** **destroy** command. Although the files are permanently removed, you can retain the history associated with them. For more information about the options and arguments available for **tf destroy**, see [Destroy Command (Team Foundation Version Control)](destroy-command-team-foundation-version-control.md).

> [!NOTE]
> This operation is available only from the command-line.

## Prerequisites

To use the **destroy** command, you must be a member of the **Team Foundation Administrators** security group. For more information, see [Default TFVC permissions](../../organizations/security/default-tfvc-permissions.md).
## Prerequisites for Running tf destroy
Before you run **tf destroy** without the **/keephistory** option, we recommend that you first delete the files you want to destroy. For more information, see [Delete Files and Folders from Version Control](delete-restore-files-folders.md). After you delete a file, its file name now includes a deletion ID. For example, if a file name is aFile.cs, after deletion the file name is aFile.cs;x123, where x123 is the deletion ID.

After you delete the files, you can synchronize the Team Foundation warehouse. Otherwise the warehouse will not be synchronized with the destroyed items.

### To permanently destroy version-controlled files

-   Click **Start**, click **All Programs**, click **Microsoft Visual Studio 2008**, click **Visual Studio Tools**, and then click **Visual Studio Command Prompt**.

    -   To preview the file aFile.cs without destroying it, type at the command prompt:

        ```
        >tf destroy /preview /i $/MyTeamProject/aFile.cs
        ```

        > [!NOTE]
        > The text in the Command Prompt window displays &quot;Destroyed: $/MyTeamProject/aFile.cs&quot;, but the file is not actually destroyed when you use the **/preview** option.

    -   To destroy the file, aFile.cs, type at the command prompt:

        ```
        >tf destroy /i $/MyTeamProject/aFile.cs
        ```

        This command displays information about possible pending changes and shelvesets in the Command Prompt window. Because you specified **/i** (non-interactive), you are not prompted with a **Yes**, **No**, **Yes to all** dialog box before the files are permanently removed.

    -   To destroy all the files in aFolder and, at the same time, retain their history, type:

        ```
        >tf destroy /keephistory $/MyTeamProject/aFolder
        ```

        > [!NOTE]
        > **/preview** cannot be specified with **/keephistory**.

        This action retains the historical information about all the files in aFolder. You can use the **tf history** command to view the history of a file. You can also view the history in Source Control Explorer. For more information, see [History Command](history-command.md) and [Get the history of an item](get-history-item.md).

    -   Use the **/stopat** option to retain the historical information up to and including a *versionSpec* value. The *versionSpec* value can be the latest version, a specific changeset, or a date. For more information about *versionspec* values, see [Use Team Foundation version control commands](use-team-foundation-version-control-commands.md).

        To destroy all the files in the project MyTeamProject and, at the same time, retain the history for the files up to and including 10/23/2005, type:

        ```
        >tf destroy $/MyTeamProject /keephistory /stopat:D10/23/2005
        ```

    -   Use the **/startcleanup** option to immediately clean up the TFVC metadata of the files that are no longer referenced by Team Foundation Server. Without this option, those metadata are removed when the database is maintained by a SQL process that runs every 5 days. Seven days after the TFVC metadata deletion, the content of the destroyed files will be deleted by another SQL process.

        To immediately destroy all the files in aFolder, type:

        ```
        >tf destroy /startcleanup $/MyTeamProject/aFolder
        ```

## Related articles

- [Move, Rename, and Delete Version-Controlled Files and Folders](rename-move-files-folders.md)
- [Destroy Command (Team Foundation Version Control)](destroy-command-team-foundation-version-control.md)
- [What is TFVC?, Operations available only from the tf command-line](what-is-tfvc.md#command-line-only)
- [Team Foundation Version Control Command-Line Reference](use-team-foundation-version-control-commands.md)