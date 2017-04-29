# Vim Skeleton Files
Skeleton files are a way to have a template instantiated upon opening a new file. For example, all C++ files might have a header like:

````
//
//  file.cpp
//  skeleton-files
//
//  Created by Illya Starikov on 04/28/17.
//  Copyright 2017. Illya Starikov. All rights reserved.
//
````

Well, skeleton files are a way to do that (the filename, directory, and date are auto-populated).

## Getting Started
To start using this directory, first clone the repository in your .vim repository (alternatively, `cd ~/.vim && git clone https://github.com/IllyaStarikov/skeleton-files.git`). In your .vimrc, add the following lines.

````
if has("autocmd")
    augroup templates
        autocmd BufNewFile main.* silent! execute '0r ~/.vim/skeleton-files/skeleton-main.'.expand("<afile>:e")
        autocmd BufNewFile *.* silent! execute '0r ~/.vim//skeleton.'.expand("<afile>:e")

        autocmd BufNewFile * %substitute#\[:VIM_EVAL:\]\(.\{-\}\)\[:END_EVAL:\]#\=eval(submatch(1))#ge
    augroup END
endif
````

## Creating New Skeleton File(s)
All skelton files have the same structure, with the extension determining which files are used. In the skeleton files directory, create a file called `skelton` with the extension you want.

Advanced auto-population (i.e. the directory, filename, or date) is created by Vim command evaluation. The syntax is `[:VIM_EVAL:]COMMAND[:END_EVAL:]`. The `VIM_EVAL` and `END_EVAL` are keywords to wrap around the command you want executed. The command is placed in the `COMMAND` field. Basic commands can be found [here](https://coderwall.com/p/adv71w/basic-vim-commands-for-getting-started).
