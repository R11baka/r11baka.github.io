# git cannot lock ref
Выскочила мне недавно ошибка
```
error: cannot lock ref 'refs/remotes/origin/test': is at c21593dc62042d39efc044f366579667e but expected 3d0e5b15fc558cd447fb475a8ecd999
```

Починилось запуском в консоли
`git gc --prune=now`