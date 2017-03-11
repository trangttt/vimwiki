[#](#) Keys to remember 
- `C-c C-s` or `SPC m s`                 : insert calendar
- `t`                                    : trigger todo
- `C-- 1 C-c C-t`                        : TODO -> DONE for repeated task
- `C-c C-q`                              : adding tags
- `SPC f e R`                            : reload source file - file emacs Reload
-  `SPC m` = `,`
- `SPC a o l`                            : store link, `<leader> i l` : insert a link
- *Messages* buffer is for log for emacs
- `SPC T n`                              : Theme next
- 
# Org-mode as GTD
- `<leader>I`, `<leader>O`, `<leader>q` : Clock In, Clock Out, Cancel
- `org-dblock-update`                   : update clock
- `C-c C-c`         : update dynamic block
- Resolve idle time : k/K, s/S
- `C-c C-x C-d`     : Clock display
- `C-c C-x C-r`     : Clock report
- `<leader> :`      : set tags using predefined tag list in spacemacs
- `C-c C-q`         : set tags using tags defined in currently edited file
- `<leader> s`      : set calendar/scheduling http://orgmode.org/manual/Timestamps.html#Timestamps
- `<leadeR> d`      : set deadline
- Timestamp : 
  - `+<n>[d|m|y]`  : repeat 1 time after `n` unit times, must repeat exact the number of times it missed. Ex: paying rent. 
  - `.+<n>[d|m|y]` : repeat 1 time after `n` unit times, after DONE, set time to exactly `n` unit times later. Ex: changing batteries. If miss 3 times, still set deadline to `n` unit times later.
  - `++<n>[d|m|y]` : repeat 1 time after `n` unit times, stay exactly on the time, date in the future if set DONE. Ex: empty trash, having meals.
- Checkboxes:
  - `M-S-<RET>` : insert a new checkbox. Work only in Plain list.
# Org-mode project
# Handling links http://orgmode.org/manual/Handling-links.html
# Lisp
- Single quote ': preventing evaluating expression
- NULL value: `nil`
- Lisp expression ()
- Prefix operation. ( + 2 3 ) ( * 4 5  ) ( write 4 5 )
- Comparision. = /= > < >= <= 
- Conditionals.
  + `cond`:
           (cond ( test1 action1 )
              ( test2 action2 ))
  + `if`:
           (if ( test ) (action) (action))
- common funcs:
  + `setq`, `setq-default`: set value locally to buffer, globally
      (setq-default variable value)
  + 
# Getting things done (theory)
- General http://orgmode.org/worg/org-gtd-etc.html
- Checking tasks for a day 
- Org-mode as daily planner
- Org-mode as habit tracking
- Estimating day work
- Working the day, Using clock to track time spent for each task
- Reviewing the week
- habit tracking org-habits http://orgmode.org/worg/org-tutorials/tracking-habits.html http://orgmode.org/manual/Tracking-your-habits.html#Tracking-your-habits
- daily planner https://github.com/jwiegley/newartisans/blob/master/posts/2007-08-20-using-org-mode-as-a-day-planner.md
- Someday.org
- http://orgmode.org/worg/org-mac.html
