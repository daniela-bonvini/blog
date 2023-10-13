---
layout: ../../layouts/MarkdownPostLayout.astro
title: "Truncating branch name in agnoster theme with oh my zsh"
pubDate: 13/10/2023
description: "How to truncate branch name at tot characters in agnoster theme with oh my zsh framework for zsh shell"
image: "/blog.png"
author: "Daniela"
tags: ["oh my zsh", "zsh", "agnoster", "shell"]
---

Hi everybody! Today's post is more of a tip than a real long blog post but it's useful nonetheless.
Recently I've been using [zsh](https://www.zsh.org/) as shell instead of bash, as a lot of my colleagues suggested it and as with the normal bash sometimes it's difficult to understand at a glance in which branch you are, I decided to give it a try, hoping it would simplify my many branch checkouts.(PS: it also works seamlessly with VS Code).
After I installed it I of course downloaded [OhMyZsh](https://ohmyz.sh/), "a delightful, open source, community-driven framework for managing your Zsh configuration", which comes with some pre-configured colored theme.

After some days of usage, though, I really found inconvenient that when I had really long branch names, I couldn't easily see my git bash commands inside the VS Code terminal, which really bothered me. So I searched for a way to truncate the name to a certain number of characters and didn't find a solution for the theme I was using, Agnoster.
That's why I'm sharing this snippet of code with the world, so if someone else finds themselves in my same position, they won't have to search all around the internet no more.
So let's cut to the chase.

## Procedure

First, locate the file with name agnoster.zsh-theme. You can find it, and all the other themes files, in the folder ".oh-my-zsh/themes".
Once there open the corresponding file and then find the prompt_git() function and add this snippet after this line (local branch_name=${ref##refs/heads/}), for me it was at line 114.

(In this example the name will be truncated at 20 char total, 17 chars of branch name + 3 chars made up by "...", but of course you can change it to whatever better suits your needs)

```bash
<... other code before ...>

local branch_name=${ref##refs/heads/}
if [[ ${#branch_name} -gt 20 ]]; then
      branch_name=
"${branch_name:0:17}..."
fi

<... other code after ...>

```

With this modification, the branch name will be truncated to a maximum of 30 characters and will end with "..." if it exceeds that length.
Here's an example of the before and after the truncation:

### Before

<img title="before" alt="Zsh branch name not truncated" src="../src/images/zsh/before.png" width="550px">

### After

<img title="after" alt="Zsh branch name truncated" src="../src/images/zsh/after.png"  width="550px">

## Conclusion

So, there you go, now you have more colorful AND shorter branch branch names, win-win!
