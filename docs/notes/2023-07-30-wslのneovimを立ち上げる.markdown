title: WSLのneovimを立ち上げる
==========
date: 2023-07-30 08:42
tags: []
categories: []
- - -

https://vim-jp.slack.com/archives/C011WE9V2R1/p1689073591862879
```
function nvim-qt() {
    true
    while [ $? -ne 1 ]; do
        RANDOM_PORT=$(( ( RANDOM % 10000 ) + 50000 ))
        nc -z 127.0.0.1 $RANDOM_PORT
    done
    echo "Using port $RANDOM_PORT"
    cat - <<CMD | parallel
      /mnt/c/windows/system32/cmd.exe /c "nvim-qt --server 127.0.0.1:$RANDOM_PORT" 2> /dev/null &
      nvim --listen "0.0.0.0:$RANDOM_PORT" --headless "$@" &
CMD
```
