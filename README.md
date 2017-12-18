[[<http://melpa.org/#/counsel-projectile>][![img](http://melpa.org/packages/counsel-projectile-badge.svg)]]


# Description

[Projectile](https://github.com/bbatsov/projectile) has native support for using [ivy](https://github.com/abo-abo/swiper) as its completion system. Counsel-projectile provides further ivy integration into projectile by taking advantage of ivy&rsquo;s support for selecting from a list of actions and applying an action without leaving the completion session. Concretely, counsel-projectile defines replacements for existing projectile commands as well as new commands that have no projectile counterparts. A minor mode is also provided that adds key bindings for all these commands on top of the projectile key bindings.


# News

-   <span class="timestamp-wrapper"><span class="timestamp">[2017-12-18 Mon] </span></span> New version `0.2`. If you are upgrading from `0.1`, please read [here](#upgrading) about important changes.
-   <span class="timestamp-wrapper"><span class="timestamp">[2016-04-12 Tue] </span></span> First version `0.1`.


# Installation

Install the package from [MELPA](https://melpa.org) or [el-get](https://github.com/dimitri/el-get), or clone this repository somewhere in your load path.


# Usage


<a id="start"></a>

## Getting started

To turn on counsel-projectile mode, either call the command `counsel-projectile-mode` or use the Customize interface to toggle on the variable `counsel-projectile-mode`. This will turn on projectile mode, thus enabling all projectile key bindings, and add the counsel-projectile key bindings on top of them.

The counsel-projectile key bindings either remap existing projectile commands to their counsel-projectile replacements (e.g. `C-c p f` now calls `counsel-projectile-find-file` instead of `projectile-find-file`) or bind keys to counsel-projectile commands that have no projectile counterparts (e.g. `C-c p SPC` calls the command `counsel-projectile`).

Calling the command `counsel-projectile-mode` once again or toggling off the variable `counsel-projectile-mode` disables the counsel-projectile key bindings and turns off projectile mode.

Note that if you turn on projectile mode but not counsel-projectile mode, the counsel-projectile commands can still be called with `M-x`, only the key bindings for these commands are not enabled.


## Summary of interactive commands

Replacements for existing commands:

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-left" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-left">Key binding</th>
<th scope="col" class="org-left">Command</th>
<th scope="col" class="org-left">Description</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-left">`C-c p p`</td>
<td class="org-left">`counsel-projectile-switch-project`</td>
<td class="org-left">Switch project</td>
</tr>


<tr>
<td class="org-left">`C-c p f`</td>
<td class="org-left">`counsel-projectile-find-file`</td>
<td class="org-left">Jump to a project file</td>
</tr>


<tr>
<td class="org-left">`C-c p d`</td>
<td class="org-left">`counsel-projectile-find-dir`</td>
<td class="org-left">Jump to a project directory</td>
</tr>


<tr>
<td class="org-left">`C-c p b`</td>
<td class="org-left">`counsel-projectile-switch-to-buffer`</td>
<td class="org-left">Jump to a project buffer</td>
</tr>


<tr>
<td class="org-left">`C-c p s g`</td>
<td class="org-left">`counsel-projectile-grep`</td>
<td class="org-left">Search project with grep</td>
</tr>


<tr>
<td class="org-left">`C-c p s s`</td>
<td class="org-left">`counsel-projectile-ag`</td>
<td class="org-left">Search project with ag</td>
</tr>
</tbody>
</table>

New commands:

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-left" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-left">Key binding</th>
<th scope="col" class="org-left">Command</th>
<th scope="col" class="org-left">Description</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-left">`C-c p SPC`</td>
<td class="org-left">`counsel-projectile`</td>
<td class="org-left">Jump to a project buffer or file, or switch project</td>
</tr>


<tr>
<td class="org-left">`C-c p s r`</td>
<td class="org-left">`counsel-projectile-rg`</td>
<td class="org-left">Search project with rg</td>
</tr>


<tr>
<td class="org-left">`C-c p O`</td>
<td class="org-left">`counsel-projectile-org-capture`</td>
<td class="org-left">Org-capture into project</td>
</tr>
</tbody>
</table>


## The `counsel-projectile` command

Default key binding: `C-c p SPC`.

This command lets you quickly jump to a project buffer or file. It uses ivy to display in the minibuffer a list of all project buffers as well as all project files that are not currently visited by a buffer. Buffers are fontified according to their major mode and files are fontified as &ldquo;virtual buffers&rdquo;, as in the command `ivy-switch-buffer`. As in all ivy commands, you can use `M-o` / `C-M-o` + `<key>` to select from a list of actions to apply (or `M-RET` / `C-M-REG` to apply the default action) to the selected candidate:

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-left">Key</th>
<th scope="col" class="org-left">Action</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-left">`o`</td>
<td class="org-left">Open buffer or file in current window (default action)</td>
</tr>


<tr>
<td class="org-left">`j`</td>
<td class="org-left">Open buffer or file in other window</td>
</tr>


<tr>
<td class="org-left">`x`</td>
<td class="org-left">Open file externally (does nothing for buffers)</td>
</tr>


<tr>
<td class="org-left">`r`</td>
<td class="org-left">Open file as root (does nothing for buffers)</td>
</tr>


<tr>
<td class="org-left">`m`</td>
<td class="org-left">Find file manually: call `counsel-find-file` from buffer or file&rsquo;s directory</td>
</tr>


<tr>
<td class="org-left">`p`</td>
<td class="org-left">Switch project: call `counsel-projectile-switch-project` (see below)</td>
</tr>
</tbody>
</table>

If not called inside a project, `counsel-projectile` first offers to select a project to switch to by calling `counsel-projectile-switch-project` (see below). Once you select a project and hit `RET`, it lets you jump to a buffer or file in this project as described above.


## `counsel-projectile-switch-project`

Default key binding: `C-c p p`.

This command is a replacement for `projectile-switch-project`. It adds the possibility to select from a list of switch-project actions to apply to the selected project:

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-left">Key</th>
<th scope="col" class="org-left">Action</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-left">`o`</td>
<td class="org-left">Jump to a project buffer or file: call `counsel-projectile` (default action; see above)</td>
</tr>


<tr>
<td class="org-left">`f`</td>
<td class="org-left">Jump to a project file: call `counsel-projectile-find-file` (see below)</td>
</tr>


<tr>
<td class="org-left">`d`</td>
<td class="org-left">Jump to a project directory: call `counsel-projectile-find-dir` (see below)</td>
</tr>


<tr>
<td class="org-left">`b`</td>
<td class="org-left">Jump to a project buffer: call `counsel-projectile-switch-to-buffer` (see below)</td>
</tr>


<tr>
<td class="org-left">`m`</td>
<td class="org-left">Find file manually: call `counsel-find-file` from the project root</td>
</tr>


<tr>
<td class="org-left">`S`</td>
<td class="org-left">Save all project buffers</td>
</tr>


<tr>
<td class="org-left">`k`</td>
<td class="org-left">Kill all project buffers</td>
</tr>


<tr>
<td class="org-left">`K`</td>
<td class="org-left">Remove project from the list of known projects</td>
</tr>


<tr>
<td class="org-left">`c`</td>
<td class="org-left">Run project compilation command</td>
</tr>


<tr>
<td class="org-left">`C`</td>
<td class="org-left">Run project configure command</td>
</tr>


<tr>
<td class="org-left">`E`</td>
<td class="org-left">Edit project directory-local variables</td>
</tr>


<tr>
<td class="org-left">`v`</td>
<td class="org-left">Open project in vc-dir / magit / monky</td>
</tr>


<tr>
<td class="org-left">`s g`</td>
<td class="org-left">Search project with grep: call `counsel-projectile-grep` (see below)</td>
</tr>


<tr>
<td class="org-left">`s s`</td>
<td class="org-left">Search project with ag: call `counsel-projectile-ag` (see below)</td>
</tr>


<tr>
<td class="org-left">`s r`</td>
<td class="org-left">Search project with rg: call `counsel-projectile-rg` (see below)</td>
</tr>


<tr>
<td class="org-left">`x s`</td>
<td class="org-left">Invoke shell from the project root</td>
</tr>


<tr>
<td class="org-left">`x e`</td>
<td class="org-left">Invoke eshell from the project root</td>
</tr>


<tr>
<td class="org-left">`x t`</td>
<td class="org-left">Invoke term from the project root</td>
</tr>


<tr>
<td class="org-left">`O`</td>
<td class="org-left">Org-capture into project: call `counsel-projectile-org-capture` (see below)</td>
</tr>
</tbody>
</table>


## `counsel-projectile-find-file`

Default key binding: `C-c p f`.

This command is a replacement for `projectile-find-file`. It displays a list of all project files and offers several actions:

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-left">Key</th>
<th scope="col" class="org-left">Action</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-left">`o`</td>
<td class="org-left">Open file in current window (default action)</td>
</tr>


<tr>
<td class="org-left">`j`</td>
<td class="org-left">Open file in other window</td>
</tr>


<tr>
<td class="org-left">`x`</td>
<td class="org-left">Open file externally (does nothing for buffers)</td>
</tr>


<tr>
<td class="org-left">`r`</td>
<td class="org-left">Open file as root (does nothing for buffers)</td>
</tr>


<tr>
<td class="org-left">`m`</td>
<td class="org-left">Find file manually: call `counsel-find-file` from file&rsquo;s directory</td>
</tr>


<tr>
<td class="org-left">`p`</td>
<td class="org-left">Switch project: call `counsel-projectile-switch-project` (see above)</td>
</tr>
</tbody>
</table>


## `counsel-projectile-find-dir`

Default key binding: `C-c p d`.

This command is a replacement for `projectile-find-dir`. It displays a list of all project directories and offers several actions:

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-left">Key</th>
<th scope="col" class="org-left">Action</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-left">`o`</td>
<td class="org-left">Open directory with `dired` in current window (default action)</td>
</tr>


<tr>
<td class="org-left">`j`</td>
<td class="org-left">Open director with `dired` in other window</td>
</tr>


<tr>
<td class="org-left">`m`</td>
<td class="org-left">Find file manually: call `counsel-find-file` from directory</td>
</tr>


<tr>
<td class="org-left">`p`</td>
<td class="org-left">Switch project: call `counsel-projectile-switch-project` (see above)</td>
</tr>
</tbody>
</table>


## `counsel-projectile-switch-to-buffer`

Default key binding: `C-c p b`.

This command is a replacement for `projectile-switch-to-buffer`. It displays a list of all project buffers and offers several actions:

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="org-left">Key</th>
<th scope="col" class="org-left">Action</th>
</tr>
</thead>

<tbody>
<tr>
<td class="org-left">`o`</td>
<td class="org-left">Open buffer in current window (default action)</td>
</tr>


<tr>
<td class="org-left">`j`</td>
<td class="org-left">Open buffer in other window</td>
</tr>


<tr>
<td class="org-left">`m`</td>
<td class="org-left">Find file manually: call `counsel-find-file` from buffer&rsquo;s directory</td>
</tr>


<tr>
<td class="org-left">`p`</td>
<td class="org-left">Switch project: call `counsel-projectile-switch-project` (see above)</td>
</tr>
</tbody>
</table>


## `counsel-projectile-grep`

Default key binding: `C-c p s g`.

This command is a replacement for `projectile-grep`. It searches all project files with `grep`, taking advantage of ivy&rsquo;s support for updating the list of candidates after each input (dynamic collections). Each canidate corresponds to a matching line in some project file, and there is only one action that opens that file at that line.


## `counsel-projectile-ag`

Default key binding: `C-c p s s`.

This command is a replacement for `projectile-ag`. It is similar to `counsel-projectile-grep` (see above) but uses `ag` (the silver searcher) instead of `grep`.


## `counsel-projectile-rg`

Default key binding: `C-c p s r`.

This command is similar to `counsel-projectile-grep` (see above) but uses `rg` (ripgrep) instead of `grep`.


## `counsel-projectile-org-capture`

Default key binding: `C-c p O`.

This command lets you capture something (a note, todo item&#x2026;) into the current project using org-mode&rsquo;s `org-capture`. Like `org-capture`, it first lets you select a capture template then file the newly captured information. By default, there is a single template storing the captured information into file \\&ldquo;notes.org\\&rdquo; in the project root directory, under headline `Tasks`.


# Configuration


## Enabling counsel-projectile mode when emacs starts

To automatically enable counsel-projectile mode when emacs starts, you can either use the Customize interface to toggle on the variable `counsel-projectile-mode`  and save your customization, or add `(counsel-projectile-mode)` to your init file.


<a id="config-action"></a>

## Customizing action lists

The lists of available actions (including the default action) for most of the commands above are stored in custom variables. If you set one of these variables, either through the Customize interface or directly with `setq`, the new value will be picked up the next time you invoke the correspodiding commmand.

The variable holding the action list for `command` is named `command-action`. The following action list variables are defined:

-   `counsel-projectile-action`
-   `counsel-projectile-switch-project-action`
-   `counsel-projectile-find-file-action`
-   `counsel-projectile-find-dir-action`
-   `counsel-projectile-switch-to-buffer-action`

For instance, the default value of `counsel-projectile-action` is:

    '(1
      ("o" counsel-projectile-action
       "current window")
      ("j" counsel-projectile-action-other-window
       "other window")
      ("x" counsel-projectile-action-file-extern
       "open file externally")
      ("r" counsel-projectile-action-file-root
       "open file as root")
      ("m" counsel-projectile-action-find-file-manually
       "find file manually")
      ("p" (lambda (_) (counsel-projectile-switch-project))
       "switch project"))

The first element is the index of the default action, and the remainig ones are the available actions (a key, an action function, and a name for each action). Thus the default action in this list is the first one (&ldquo;current window&rdquo;).

Extra actions can be added to these lists or, alternatively, can be set through ivy&rsquo;s `ivy-set-actions` mechanism. If you prefer setting all actions (except the default one) through this mechanism, you can set the action list variable to a single action (e.g. `counsel-projectile-action`) instead of a list.

Note that ivy only supports one-character keys for actions. Hence, for instance, it is not possible to directly set the keys `s g`, `s s`, and `s r` for the three project search commands in `projectile-switch-project-action`. Instead, the key `s` is set for a &ldquo;prefix&rdquo; action `counsel-projectile-switch-project-action-prefix-search` that reads a secondary one-character key and calls the corresponding search command as a &ldquo;sub-action&rdquo;. The list of available sub-actions is read from the variable `counsel-projectile-switch-project-action-prefix-search-sub-action`, which can be customized separately. This variable has the same format as an action list, except that the index is not present. Its default value is:

    '(("g" counsel-projectile-switch-project-action-grep
       "Search project with grep")
      ("s" counsel-projectile-switch-project-action-ag
       "Search project with ag")
      ("r" counsel-projectile-switch-project-action-rg
       "Search project with rg"))

The following sub-action variables are defined:

-   `counsel-projectile-switch-project-action-prefix-search-sub-action`
-   `counsel-projectile-switch-project-action-prefix-shell-sub-action`


## Setting `counsel-projectile-org-capture` templates

The available capture templates for `counsel-projectile-org-capture` are read from the variable `counsel-projectile-org-capture-templates`. This variable has the same format as the variable `org-capture-templates`, except that in all strings of in an entry’s target slot, all instances of `${root}` and `${name}` are replaced with the current project root and name, respectively.

The default value contains a single template, whose target is:

    (file+headline "${root}/notes.org}" "Tasks")

This points to headline `Tasks` in file `notes.org` in the
project root directory (one file per project).

Another example of a valid target is:

    (file+olp "~/notes.org" "${root}" "Tasks")

This points to outline path `<project-root>/Tasks` in file
`~/notes.org` (same file for all projects).

Templates contexts are read from the variable `counsel-projectile-org-capture-templates-contexts`, which has the same format as `capture-templates-contexts`


## Removing the current project or buffer from the list of candidates

By default, when calling `counsel-projectile-switch-project`, the current project (if any) is included in the candidates list and preselected. Similarly, when calling `counsel-projectile-switch-to-buffer`, the current buffer is included in the candidates list and preselected. If you prefer removing these elements from the candidate lists of these commands, you can set the variables `counsel-projectile-remove-current-project` and `counsel-projectile-remove-current-buffer` accordingly.


## Initial input for the project search commands

If you want some initial input to be inserted in the minibuffer every time you call `counsel-projectile-grep`, `counsel-projectile-ag`, or `counsel-projectile-rg`, you can customize the variables `counsel-projectile-grep-initial-input`, `counsel-projectile-ag-initial-input`, or `counsel-projectile-rg-initial-input` accordingly. Each of these variable, if non `nil`, should hold a Lisp expression whose evaluation yields the initial input string. If you use the Customize interface, some choices are proposed based on various versions of the `thing-at-point` function. Note that you can always insert the value of `(ivy-thing-at-point)` by hitting `M-n` in the minibuffer.


<a id="upgrading"></a>

# Upgrading from previous version (`0.1`)

If you are upgrading from version `0.1` to version `0.2`, please read below about important changes, some of which may require you to update your configuration.


## Key bindings

The commands `counsel-projectile-on`, `counsel-projectile-off` and `counsel-projectile-toggle` no longer exist. They are replaced by the counsel-projectile minor mode. You can toggle this mode either by calling the `counsel-projectile-mode` command. or by setting the `counsel-projectile-mode` variable throught the Customize interface. See [Getting started](#start) above for details.


## Action lists

The available actions for the various counsel-projectile commands are now customized differently:

-   The custom variable corresponding to `command` is now named `command-action`, not `command-actions`.
-   This variable now stores all the available actions, including the default action, not only the extra actions.
-   It also stores the index of the default action (it is a list whose first element is this index and whose remaining elements are the availabe actions).
-   This variable is now used as the value of the `:action` parameter for the command&rsquo;s `ivy-read` call. Hence if you set it outside the Customize interface, you no longer need to call `ivy-set-actions` afterwards. If you set extra actions through `ivy-set-actions`, they will not replace the variable&rsquo;s actions but will rather be added to them.

See [Customizing action lists](#config-action) above for details.

Also, in the default action lists, the keys set for some actions have changed, mainly for the `counsel-projectile-switch-project` command. Indeed, as new actions were added to this command, the corresponding list of keys was becoming somewhat inconsistent. The new keys replicate the default projectile key bindings (for instance, the aciton to save all project buffers is now called with the key `S`, mimicking the default key binding `C-c p S` for the command `projectile-save-project-buffers`). When an action calls a command that has no default projectile key binding, its key is chosen among those that are not bound by projectile by default.


## Minibuffer keymap

The minibuffer keymap `counsel-projectile-map` no longer exists. It was only used to bind a key (`M-SPC` by default) to the command `counsel-projectile-drop-to-switch-project` exiting the current command and calling `counsel-projectile-switch-project`. The same functionality is now implemented in a simpler way through an aciton that calls `counsel-projectile-switch-project`, whose key is `p` by default. Concretely, you should now hit `M-o p` instead of `M-SPC`.


# Contributors

Counsel-projectile is inspired by [helm-projectile](https://github.com/bbatsov/helm-projectile). Many thanks to [abo-abo](https://github.com/abo-abo) and [DamienCassou](https://github.com/DamienCassou) who encouraged and helped me to start this repository, as well as all contributors and users who have submitted issues and pull requests.

