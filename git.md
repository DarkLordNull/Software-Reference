# Git

## Rebasing

To change the e-mail address and user name of all commits without otherwise changing the commits, use

    git rebase -i --root -x "git commit --amend --author 'NAME <EMAIL>' --no-edit"

If only the last `N` commits need to be changed, instead use

    git rebase -i HEAD~N -x "git commit --amend --author 'NAME <EMAIL>' --no-edit"

This changes all the commit hashes so a remote repository will appear to have two parallel histories -- one history with the old e-mail address(es) and name(s), and another history with the updated e-mail address/name. The old history would need to be deleted.

## Text Editor

If a text editor needs to be opened (such as during an interactive rebase), then git will use its configured text editor (which may not be the system's default text editor). To set git's text editor to the lightweight Git Nano use

    git config --global core.editor "nano"

One can also use Visual Studio Code by replacing `nano` with `code --wait`, though Visual Studio Code takes much longer to launch.

The difftool can be set most easily to, e.g. Visual Studio Code, by typing

    git config --global -e

to edit the git config file, then adding

    [diff]
        tool = default-difftool
    [difftool "default-difftool]
        cmd = code --wait --diff $LOCAL $REMOTE

to the git config file.
