- add please

old:

cmd paste %{{
    start_time=$(date +'%s')
    load=$(lf -remote 'load')
    mode="$(echo "$load" | sed -n '1p')"
    load="$(echo "$load" | sed '1d')"
    [ -z $load ] && exit 1
    srcF=$(mktemp)
    echo "$load" > "$srcF"
    please='' && [ ! -w . ] && please='sudo'
    case "$mode" in
        copy) cmd='cp-p'; copying=copying;;
        move) cmd='mv-p'; copying=moving;;
    esac
    cmd="$cmd --new-line --backup=numbered -F"
    $please sh -c  "$cmd \"$srcF\" . | while read -r line
      do
        lf -remote \"send $id echo \$line\"
      done &&
        lf -remote 'send load' && rm -f \"$srcF\" &"
    lf -remote 'send load'
    lf -remote 'send clear'
    #wait $! && end_time=$(date +'%s')
    #interval=$(($(date +'%s')-$start_time))
    #[ $interval -gt 6 ] &&
    #notify-send "done $copying files" "\"$(<$srcf)\"\nto\n\"$(realpath .)/\""
}}
