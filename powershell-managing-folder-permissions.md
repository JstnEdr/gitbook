---
description: >-
  https://petri.com/how-to-use-powershell-to-manage-folder-permissionsAdd ways
  to manage folder permissions to share
---

# Powershell managing folder permissions

## Exploring NTFS File and Folder Permissions

Becoming a super hero is a fairly straight forward process:

{% tabs %}
{% tab title="Get Permissions" %}
```bash
$ACL = Get-ACL -Path "Test1.txt"
$AccessRule = New-Object System.Security.AccessControl.FileSystemAccessRule("TestUser1","Read","Allow")
$ACL.SetAccessRule($AccessRule)
$ACL | Set-Acl -Path "Test1.txt"
(Get-ACL -Path "Test1.txt").Access | Format-Table IdentityReference,FileSystemRights,AccessControlType,IsInherited,InheritanceFlags -AutoSize Super-powers are granted randomly so please submit an issue if you're not happy with yours.
```
{% endtab %}
{% endtabs %}

Once you're strong enough, save the world by creating a super smart shell script:

{% code title="setupFolderPermissions.sh" %}
```bash
# Ain't no code for that yet, sorry
echo 'You got to trust me on this, I saved the world'
```
{% endcode %}

## See Options

```bash

```

