# Machine Setup

1. `brew install goenv`
1. Add `eval "$(goenv init -)"` to shell file
1. `goenv global $(goenv install --list | tail -1 | awk '{$1=$1};1')`
