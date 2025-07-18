# Windows 10 Tips

### Cyrillic problem in `cmd`:
```CMD
> psql -h localhost -U postgres
postgres=# \du
                                    ╤яшёюъ Ёюыхщ
 ╚ь  Ёюыш |                                └ЄЁшсєЄ√
----------+-------------------------------------------------------------------------
 postgres | ╤єяхЁяюы№чютрЄхы№, ╤ючфр╕Є Ёюыш, ╤ючфр╕Є ┴─, ╨хяышърЎш , ╧ЁюяєёърЄ№ RLS

# fix in PowerShell (admin)
Set-ItemProperty 'HKLM:\Software\Microsoft\Command Processor' AutoRun '@chcp 1251 >NUL'

# rerun `cmd`
> psql -h localhost -U postgres
postgres=# \du
                                    Список ролей
 Имя роли |                                Атрибуты
----------+-------------------------------------------------------------------------
 postgres | Суперпользователь, Создаёт роли, Создаёт БД, Репликация, Пропускать RLS

```


### Set new $PATH value permanently (not only current cmd session)
```CMD
# set user side $PATH
setx path "%path%;C:\path\to\portable\git"

# set system side $PATH
setx /M path "%path%;C:\path\to\portable\git"
```
