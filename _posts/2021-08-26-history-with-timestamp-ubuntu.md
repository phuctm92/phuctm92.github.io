---
title: "Command history with timestamp in Linux/Ubuntu"
date: 2021-08-26 8:00:00 +0700
categories: [Programming]
tags: [Ubuntu]
---
Display history with timestamp in Linux/Ubuntu
<!--more-->

By default, the `history` command will display output as follows:
```bash
1  cd
2  touch abc.text
3  mv abc.text def.text
4  rm def.text
5  history
```

## How to display timestamps of history in Bash
Define the environment variable named **HISTTIMEFORMAT**:

`HISTTIMEFORMAT="%d/%m/%y %T "`
- %d: Day
- %m: Month
- %y: Year
- %T: Time

Example:
```bash
HISTTIMEFORMAT="%d/%m/%y %T "
history
```
Sample output:
```bash
1  26/08/21 11:02:32 cd
2  26/08/21 11:02:32 touch abc.text
3  26/08/21 11:02:32 mv abc.text def.text
4  26/08/21 11:02:32 rm def.text
5  26/08/21 11:02:32 history
```

Or you can add directly to your `~/.bash_profile` file:
```bash
echo 'export HISTTIMEFORMAT="%d/%m/%y %T "' >> ~/.bash_profile
source ~/.bash_profile
history
```

## How to display timestamps of history in Zsh
In zsh, it's so easier with built-in commands:

Source: [https://github.com/ohmyzsh/ohmyzsh/blob/12669f29f0843b8b980dd137f150a74511f88842/lib/history.zsh](https://github.com/ohmyzsh/ohmyzsh/blob/12669f29f0843b8b980dd137f150a74511f88842/lib/history.zsh){:target="_blank"}

```bash
case ${HIST_STAMPS-} in
  "mm/dd/yyyy") alias history='omz_history -f' ;;
  "dd.mm.yyyy") alias history='omz_history -E' ;;
  "yyyy-mm-dd") alias history='omz_history -i' ;;
  "") alias history='omz_history' ;;
  *) alias history="omz_history -t '$HIST_STAMPS'" ;;
esac
```
Let's try these commands:
```bash
history -f
# 1  8/26/2021 11:02 cd
# 2  8/26/2021 11:02 touch abc.text

history -E
# 1  26.8.2021 11:02 cd
# 2  26.8.2021 11:02 touch abc.text

history -i
# 1  2021-08-26 11:02 cd
# 2  2021-08-26 11:02 touch abc.text
```
___
*“The earlier you start working on something, the earlier you will see results.”*
{: .text-center.text-success}
