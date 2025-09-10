# Terminal

## Font Resizing
- `<CTRL><SHIFT>=` (i.e., `<CTRL>+`): Increase font size
- `<CTRL>-`: Decrease Font Size

## tmux

[Here](https://tmuxcheatsheet.com/) is a helpful tmux cheatsheet.

### Kill Tmux Server
From within tmux session:
```
<CTRL>b
:kill-server
```

Detach tmux session and kill from command line:
```
<CTRL>b
d
tmux kill-server
```