# Terminal

## Font Resizing
| Keystroke | Action |
| - | - |
| `<CTRL><SHIFT>=` | Increase font size |
| `<CTRL>-` | Decrease Font Size |

**Note:** `<SHIFT>=` is `+`, hence `<CTRL><SHIFT>=` is really `<CTRL>+`.

## tmux

A helpful tmux cheatsheet can be found [here](https://tmuxcheatsheet.com/).

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