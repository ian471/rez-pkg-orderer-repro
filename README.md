# rez [#1683](https://github.com/AcademySoftwareFoundation/rez/issues/1683) test case

Examples use PowerShell.

Repro:
```powershell
$env:REZ_PACKAGE_ORDERERS_JSON = '{"type":"per_family","orderers":[{"type":"version_split","packages":["A"],"first_version":"1"}]}'

rez env -vvv --no-implicit --no-local --paths packages C -- rez context
```

Should print:
```
resolved packages:
A-1  d:\projects\ct-891\packages\A\1
C-4  d:\projects\ct-891\packages\C\4\A-1
```

Does print:
```
resolved packages:
A-2  d:\projects\ct-891\packages\A\2
C-4  d:\projects\ct-891\packages\C\4\A-2
```

## Run with debugging

`pdb` commands are loaded from `.pdbrc`.

```powershell
& "C:\rez\Scripts\python.exe" -m pdb -m rez.cli._main env -vvv --no-implicit --no-local --paths packages C -- rez context
```
