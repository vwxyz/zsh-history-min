#zsh-history-min


.zsh_history


A CLI tool for minimizing `.zsh_history`. Delete repeated entries, Keep all entries unique



slimmed down `.zsh_history` works pretty well when combined with **[peco](https://github.com/peco/peco)-assisted backward search**


##installation


```
npm install -g zsh-history-min
```

##usage


- simply run `zsh-history-min`



## Note1: **peco**-assisted backward search


- install peco
- copy and pasted this snippet below into your `.zshrc`


```bash
# copied from:
# http://qiita.com/uchiko/items/f6b1528d7362c9310da0
function peco-select-history() {
    local tac
    if which tac > /dev/null; then
        tac="tac"
    else
        tac="tail -r"
    fi
    BUFFER=$(\history -n 1 | \
        eval $tac | \
        peco --query "$LBUFFER")
    CURSOR=$#BUFFER
    zle clear-screen
}
zle -N peco-select-history
bindkey '^r' peco-select-history
```

##Note2: format of `.zsh_history`


I dont't find any **spec** about `.zsh_history`, but each entry has rules like below:



|colon| unixtime | colon | repeated time|semicolon | command|
|---|---|---|---|---|---|---|
|:|1413905231|:|0|;|~/my/padding|
|:|1413905285|:|0|;|npm version|
|:|1413905304|:|0|;|npm help|
|:|1413905341|:|0|;|npm i padding|
|:|1413905517|:|0|;|git commit -m "modify callback message in cli mode"|


```shell:.zsh_history
#ex
: 1413905231:0;~/my/padding
: 1413905285:0;npm version
: 1413905304:0;npm help
: 1413905341:0;npm i padding
: 1413905517:0;git commit -m "modify callback message in cli mode"
```

##Note3 some inspiring resources

- [noodle.clj](https://gist.github.com/r00k/7948384)

- [nsue/zshist](https://github.com/nsue/zshist)


##Licence

MIT





