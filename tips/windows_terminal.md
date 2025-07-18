# Terminal tips

### Windows 10 cmd buffer problem - max size is 9999
##### The problem in CMD
```Cmd
> python -c "[print(i) for i in range(20000)]"
10003
10004
10005
...
```
##### The problem in Terminal
```Terminal
> python -c '[print(i) for i in range(20000)]'
10970
10971
10972
...
```
#### New config for Terminal
```Config
{
    ...
    "profiles":
    {
        "defaults":
        {
            "historySize" : 32765
        },
        ...
    },
    ...
}
```
##### Terminal with new config
```Terminal
> python -c '[print(i) for i in range(32766)]'
0
1
2
...
```
