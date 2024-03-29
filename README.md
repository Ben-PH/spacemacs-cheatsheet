Originally copied from [this gist](https://gist.github.com/robphoenix/9e4db767ab5c912fb558)

New issues and pull requests to improve for general community highly encouraged.

## Useful Spacemacs commands

- `SPC q q` - quit

#### windowing

| Binding   | Description               |
| --:       | :--                       |
| `SPC w /` | split window vertically   |
| `SPC w -` | split window horizontally |
| `SPC 1`   | switch to window 1        |
| `SPC 2`   | switch to window 2        |
| `SPC w d` | delete current window     |
| `SPC TAB` | switch to previous buffer |

#### buffer/file/project juggling


| Binding     | Description                             |
| --:         | :--                                     |
| `SPC b b`   | switch buffers                          |
| `SPC f f`   | find a file                             |
| `SPC f s`   | save a file (:w also works)             |
| `SPC b d`   | kill current buffer                     |
| `SPC p p`   | open project                            |
| `SPC p f`   | find a file in current project          |
| `SPC p h`   | switch buffers within current project   |
| `SPC b 0-9  | move buffer to numbered window          |
| `SPC v`     | enter expand-region mode                |
| `SPC b b`   | Helm mini; lists buffers & recent files |
|             | - `CTRL SPC` Mark Items                 |
|             | - `CTRL z` Actions                      |
| `SPC b B`   | ibuffer                                 |
| `SPC f f`   | open files                              |
|             | - `CTRL h` up a folder                  |
|             | - `CTRL l` open a folder                |
|             | - `CTRL j` up                           |
|             | - `CTRL k` down                         |
| `SPC p p`   | switch projects                         |
| `SPC /`     | searches through project                |
|  /          | search in a file                        |
| `SPC s s`   | interactive search in a file            |
| `SPC h d`   | help describe                           |
| `SPC h d f` | help describe functions                 |
| `SPC h d v` | help describe variables                 |
| `SPC f e h` | help                                    |
| `ALT /`     | snippet completion                      |
| `SPC t s`   | toggle syntax checking                  |
| `SPC e`     | syntax checking options                 |
| `SPC a d`   | dired                                   |

#### region/highlighting

| Binding | Description          |
| --:     | :--                  |
| `SPC v` | expand region        |
| `SPC V` | contract region      |
| `v`     | set visual char mode |
| `V`     | set visual line mode |
| `C-v`       | block visual mode          |
| `s (`       | put parens around a region |

#### Unimpaired

| Binding  | Description              |
| :--      | :--                      |
| `[e`     | Move line up             |
| `]e`     | Move line down           |
| `[SPACE` | Insert space above       |
| `]SPACE` | Insert space below       |
| `[p`     | Paste above current line |
| `]p`     | Paste below current line |

## evil-mc

[`evil-mc`](https://github.com/gabesoft/evil-mc) is a multi-cursor
implementation available in `spacemacs` by default 
in the `develop` branch, optionally enabled in the main. 

| Binding | Description                |
| --:     | :--                        |
| `grm`   | make-all-cursors           |
| `gru`   | undo-all-cursors           |
| `grs`   | pause-cursors              |
| `grr`   | resume-cursors             |
| `grf`   | make-and-goto-first-cursor |
| `grl`   | make-and-goto-last-cursor  |
| `grh`   | make-cursor-here           |
| `M-n`   | make-and-goto-next-cursor  |
| `grN`   | skip-and-goto-next-cursor  |
| `M-p`   | make-and-goto-prev-cursor  |
| `grP`   | skip-and-goto-prev-cursor  |
| `C-n`   | make-and-goto-next-match   |
| `grn`   | skip-and-goto-next-match   |
| `C-t`   | skip-and-goto-next-match   |
| `C-p`   | make-and-goto-prev-match   |
| `grp`   | skip-and-goto-prev-match   |

### 2.1 Quick Guide for Using Multiple Cursors

Multiple cursors can be used to simultaneously modify occurrences of a word,
expression, symbol, etc. To enable it globally add `(global-evil-mc-mode 1)` to your `.spacemacs` file.

### 2.2 General Principles

1. Descriptions here are provided to supplement the [`evil-mc`
   documentation](https://github.com/gabesoft/evil-mc) which makes 
   sense if you have a foundation but may be somewhat terse for the novice.
   
2. You use `evil-mc` commands to make or manipulate multiple "fake" cursors. You
are then able to make modifications to text at all cursors at once in multiple
locations of the buffer.

3. Once created, fake cursors persist until you clear them (`grq`).

4. There are two sets of commands, those that create/remove cursors and those that
navigate among them.

5. Fake cursors are created in two ways: a) by matching text, or b) by manually
   selecting where the cursor should be.

### 2.3 Simple Case 1 - Matching

Using text matching we can create cursors on multiple lines. Let's say we have
this picnic list:

```
Ron: Ice and soda
Sally: Volleyball
Ron: Vollball nets
Ron: Sand
Ann: Adult beverages
Ron: Sunblock
```

Rob can't make it now we have to change his assignments to someone else.

1. Put your cursor on the first `Rob`.
2. In command mode type `C-n` (`evil-mc-make-cursor-and-goto-next-match`).
3. You should get another cursor on the _next_ match.
4. Again, type `C-n` which should give you another cursor on the third match.
5. At this point you can move and edit as appropriate (e.g., `b cw Rick`).
6. Type `ESC` to exit insert mode.
7. To clear your cursors, type `grq` (`evil-undo-all-cursors`).

### 2.4 Simple Case 2 - Columnar

Another common case for changing multiple lines is that you want to change a
column of text but there are no matching symbols.  In the example below, let's
say you want to change the `)` numbering to simply a `.`.  

```
1) Sample line A
2) Sample line B
3) Sample line C
```

If you put your cursor on `)` and use the `C-n` you get the message `Search
failed` because `evil` doesn't recognize the matching parenthesis. What we can
do in this case is use the `evil-mc-make-cursor-and-goto-next-line` function.
Rather than looking for match `evil` will simply move directly down one line.

1. Put your cursor on the first `)`.
2. In command mode type `grj` (`evil-mc-make-cursor-and-goto-next-line`).
3. You will get a new fake cursor directly below where you started. Type `grj`
   again and you will have your third cursor.
4. As before, you can make your edits here using the normal commands.
5. Type `ESC` to exit insert mode and type `grq` to clear the cursors.

### 2.5 Simple Case 3 - Movement Args

When running the cursor commands you can make use of normal `vim/spacemacs`
movement arguments.

```
1) Sample line A
2) Sample line B
3) Sample line C
```

1. As before, in command mode put your cursor on the first `)`.
2. Type `2grj`.
3. Edit as usual, `ESC` to exit insert mode, etc.

### 2.6 Simple Case 3 - Manually Setting Cursors 

In the last example let's say we have some word or symbol that isn't matching
really well or we're only dealing with a few lines.  In that case you might want
to manually place your fake cursors.  Let's say we want to instances below from
`appl` to `run`.

```groovy
def appl_start = "apple"
println "Application end: {appl_end}"
def (other, appl_and_exit) = [true,false]

```

1. Move your cursor to the `a` in `appl` in the first line.
2. Place a cursor using `grh` (`evil-mc-make-cursor-here`).
3. You have your first fake cursor but now it will want to chase the real cursor
   around while you place your other cursors so you need to pause it. Type `grs`
   (`evil-mc-pause-cursors`).
4. Now move to the `a` in `appl_end` and do another `grh`.
5. Move to the `a` in `appl_and_exit` and place your final fake cursor with `grh`.
6. Now resume cursors with `grr` (`evil-mc-resume-cursors`). 
7. Edit as usual, `ESC` to exit insert mode, etc. 

Once you get the idea, refer to the [`evil-mc`
documentation](https://github.com/gabesoft/evil-mc) for more details.

## Eyebrowse

#### Changing workspace

| Binding               | Description                        |
| --:                   | :--                                |
| `gT`                  | previous workspace                 |
| `SPC l w n`           | create or switch to workspace n    |
| `SPC l w TAB`         | last active workspace              |
| `SPC l w c`           | close current workspace            |
| `SPC l w <n or l>`    | next workspace                     |
| `SPC l w <N, p or h>` | previous workspace                 |
| `SPC l w r`           | set a tag to the current workspace |
| `SPC l w w`           | switched to tagged workspace       |

## Find/Replace

| Binding  | Description                                                                      |
| :--      | :--                                                                              |
| `Alt %`  | interactive find/replace within selected region, or from cursor point to end     |
| `y`      | do the replacement.                                                              |
| `n`      | skip                                                                             |
| `!`      | do this and all remaining replacements without asking.                           |
| `Ctrl+g` | cancel.                                                                          |
  
## Git

| Binding     | Description                                         |
| --:         | :--                                                 |
| `SPC g b`   | open a magit blame                                  |
| `SPC g B`   | quit magit blame                                    |
| `SPC g c`   | commit changes                                      |
| `SPC g C`   | checkout branches                                   |
| `SPC g d`   | show diff prompt                                    |
| `SPC g D`   | show diff against current head                      |
| `SPC g e`   | show ediff comparison                               |
| `SPC g E`   | show ediff against current head                     |
| `SPC g f`   | show fetch prompt                                   |
| `SPC g F`   | show pull prompt                                    |
| `SPC g H c` | clear highlights                                    |
| `SPC g H h` | highlight regions by age of commits                 |
| `SPC g H t` | highlight regions by last updated time              |
| `SPC g i`   | git init a given directory                          |
| `SPC g I`   | open helm-gitignore                                 |
| `SPC g l`   | open a magit log                                    |
| `SPC g L`   | display the log for a file                          |
| `SPC g P`   | show push prompt                                    |
| `SPC g s`   | open a magit status window                          |
| `SPC g S`   | stage current file                                  |
| `SPC g m`   | display the last commit message of the current line |
| `SPC g t`   | launch the git time machine                         |
| `SPC g U`   | unstage current file                                |
- Highlight by age of commit or last update time is provided by smeargle.
- Git time machine is provided by git-timemachine.
- Git last commit message per line is provided by git-messenger.

### 3.1 Magit

A well-featurend Spacemacs layer for managing Git repositories.

Add magit to `dotspacemacs-configuration-layers` in your `.spacemacs file`. Access it from spacemacs using `SPC f e d`

Magit can only work from a Git repository

#### From within a Git repo:

- `SPC g s` open magit for a git repo

#### Common commands
| Binding  | Description                                                        |
| :--      | :--                                                                |
| `$`      | open command output buffer                                         |
| `c c`    | open a commit message buffer                                       |
| `b b`    | checkout a branch                                                  |
| `b c`    | create a branch                                                    |
| `f f`    | fetch changes                                                      |
| `F u`    | pull tracked branch                                                |
| `-r`     | toggle rebase on pull                                              |
| `gr`     | refresh                                                            |
| `C-j`    | goto next magit section                                            |
| `C-k`    | goto previous magit section                                        |
| `l l`    | open log buffer                                                    |
| `o`      | revert item at point                                               |
| `P u`    | push to tracked branch                                             |
| `P m`    | push to matching branch (e.g., upstream/develop to origin/develop) |
| `q`      | quit                                                               |
| `s`      | on a file or hunk in a diff: stage the file or hunk                |
| `S`      | stage all                                                          |
| `x`      | discard changes                                                    |
| `+`      | on a hunk: increase hunk size                                      |
| `-`      | on a hunk: decrease hunk size                                      |
| `TAB`    | on a file: expand/collapse diff                                    |
| `u`      | on a staged file: unstage                                          |
| `U`      | unstage all staged files                                           |
| `v or V` | select multiple lines                                              |
| `z z`    | stash changes                                                      |

#### NOTE Staging lines

Magit allows you to stage specific lines by selecting them in a diff and hitting s to stage. Due to inconsistencies between Vim and Emacs editing styles, if you enter visual line state with V, you will stage one more line than intended. To work around this, you can use v instead (since Magit only stages whole lines, in any case).

### 3.2 Commit message editing buffer

When done editing, commit with `<leader>c` (`<leader>` defaults to `,` in spacemacs) or `C-c C-c`.
Discard the commit with `<leader>k`, or `C-c C-k`.

### 3.3 Interactive rebase buffer

| Binding                 | Description    |
| :--                     | :--            |
| `c` or `p`              | pick           |
| `e`                     | edit           |
| `f`                     | fixup          |
| `j`                     | go down        |
| `gj`                    | move line down |
| `k`                     | go up          |
| `gk`                    | move line up   |
| `d` or `x`	kill line |                |
| `r`                     | reword         |
| `s`                     | squash         |
| `u`                     | undo           |
| `y`                     | insert         |
| `!`                     | execute        |
        
### 3.4 Quick guide for recurring use cases in Magit

Amend a commit:
- `l l` to open log buffer
- `c a` on the commit you want to amend

Squash last commit:
- `l l` open log buffer
- `r e` on second to last commit, it opens the rebase buffer
- `j` put point on last commit
- `s` squash it

Force push a squashed commit:
in the status buffer you should see the new commit unpushed and the old commit unpulled
- `P -f P` for force a push (beware usually it is not recommended to rewrite the history of a public repository, but if you are sure that you are the only one to work on a repository it is ok - i.e. in your fork).
Add upstream remote (the parent repository you have forked):
- `M` open the remote popup
- `a` add a remote

Pull changes from upstream (the parent repository you have forked) and push:
- `F (-r) C-u F` then choose upstream or the name you gave to it
 - `(-r)`        toggle on rebase if needed
- `P P`          push the commit to origin

### 3.5 Git-Flow

magit-gitflow provides git-flow commands in its own magit menu.

- `%`	open magit-gitflow menu

### 3.6 Git time machine

git-timemachine allows to quickly browse the commits of the current buffer.

#### Enter git timemachine with `SPC g t` from the file you wish to explore

- `c`	show current commit
- `n`	show next commit
- `N`	show previous commit
- `p`	show previous commit
- `q`	leave micro-state and git timemachine
- `Y`	copy current commit hash


## Useful Vim key bindings

### movement

| Binding  | Description                                                      |
| :-:      | :--                                                              |
| `0`      | beginning of line                                                |
| `^`      | beginning of non-whitespace                                      |
| `$`      | end of line                                                      |
| `9j`     | move down 9 lines                                                |
| `w`      | move forward by word                                             |
| `b`      | move backward by word                                            |
| `gg`     | first line                                                       |
| `G`      | last line                                                        |
| `C-u`    | up half page                                                     |
| `C-d`    | down half page                                                   |
| `f/`     | move forward to first "/" character                              |
| `t/`     | move forward right before the first "/" character                |
| `;`      | repeat that command again                                        |
| `H`      | head of the screen                                               |
| `M`      | middle of the screen                                             |
| `L`      | last of the screen                                               |
| `}`      | move forward by paragraph or block                               |
| `{`      | move backwards by paragraph or block                             |
| `*`      | search for word under the cursor                                 |
| `n`      | search again forward                                             |
| `N`      | search again backwards                                           |
| `#`      | search backwards for word under cursor                           |
| `/`      | search forward                                                   |
| `?`      | search backward                                                  |
| `%`      | find matching brace, paren, etc                                  |
| `ma`     | mark a line in a file with marker "a"                            |
| ``a`     | after moving around, go back to the exact position of marker "a" |
| `'a`     | after moving around, go back to line of marker "a"               |
| `:marks` | view all the marks                                               |
| `''`     | go to the last place you were                                    |

### editing

| Binding | Description                                     |
| :-:     | :--                                             |
| `x`     | delete char under cursor                        |
| `X`     | delete char before cursor                       |
| `A`     | add to end of line                              |
| `I`     | insert at the beginning of the line             |
| `dd`    | delete line                                     |
| `D`     | delete from cursor to end of line               |
| `di'`   | delete text inside single quotes                |
| `yy`    | copy line                                       |
| `Y`     | copy from cursor to end of line                 |
| `p`     | paste after cursor                              |
| `P`     | paste before cursor                             |
| `o`     | add line below                                  |
| `O`     | add line above                                  |
| `.`     | repeat last comment                             |
| `r`     | replace character                               |
| `R`     | replace. (overwrite) (good for columns of text) |
| `J`     | join line (cursor can be anywhere on line)      |
| `cc`    | change line                                     |
| `C`     | change from cursor to end of line               |

#### Change text inside something, e.g.

| Binding | Description            |
| :-:     | :--                    |
| `cit`   | inside html tag        |
| `ci'`   | inside single quotes   |
| `ci{`   | inside curly brackets. |
| `ciw`   | inside word            |

