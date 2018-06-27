---
title: RTC Example
date: 2018-06-22 18:58:14
tags: RTC
categories: RTC
---

Things to be used for CLI demo set SCM CLI env
```
setenv PATH <install_dir>/jazz/scmtools/eclipse:$PATH
```

Use help
```
scm help
scm help list
```

login
```
scm login -c -r  https://jazz07.abc.com:21443/jazz -u user@abc.com -n repo
```
<!--more-->
list streams 
```
scm list streams -r repo
```

list workspaces from all users
```
scm list workspaces -r repo
```

list workspaces of one user 
```
scm list workspaces -r repo -c user@abc.com
```

create workspace
```
scm create workspace -r repo -s "pmc_mainline" pmc_mainline_ws1
```

load workspace
```
scm load -r repo "pmc_mainline_ws1"
```

change a file locally
```
cd pmc/etc/
vi pmcstart.sh
```

show changes
```
scm status -C
```

show change history for a file
```
scm history pmcstart.sh 
```

diff from workspace
```
scm diff file pmcstart.sh
```

diff from stream
```
scm diff file pmcstart.sh stream "pmc_mainline"
```

diff from a specific changeset
```
scm diff file pmcstart.sh changeset 1623
```

diff from others workspace
```
scm diff file Makefile workspace "(tang) pmc_mainline WS"
```

checkin changes
```
scm checkin pmcstart.sh
```

add comment in a changeset
```
scm changeset comment 1701 "add a line in pmcstart.sh from CLI"
```

link a workitem with a changeset
```
scm changeset associate 1701 1159
```

deliver a changeset
```
scm deliver -c 1701
```

show last 5 change sets
```
scm list changesets -r repo -w pmc_mainline_ws1 -m 5
```

list changes in one change set
```
scm list changes 1701
```

unload workspace
```
scm workspace unload -D -r repo -w "pmc_mainline_ws1"
```

delete a workspace 
```
scm workspace delete -r repo "pmc_mainline_ws1"
```

logout 
```
scm logout -r repo
```

accept changes, accept all changes for one component
```
scm accept -C pmc
```

accept changes from a changesetscm 
```
scm accept -c 1701
```

View conflict 
```
scm status -C (view Outgoing and Incoming changes with "!" - conflict)
scm diff file <conflicted file> stream <target stream> (view conflicted diff)
```

Accept incoming change(with conflict)
```
scm accept <incoming changeset> -v -i  (view conflict in >>>> ==== <<<< format in sandbox)
scm status -C (view the "#" added in outgoing changeset) 
```

Resolve conflict, use workspace version:
```
scm resolve -c <conflicted file> 
```

use incoming version:
```
scm resolve -p <conflicted file> 
```

Manual merger use workspace version  (manually edit conflicted file by referencing  >>>> ==== <<<<)
```
scm checkin <conflicted file> -c <existing outgoing changeset> (add resolved changes to existing changeset)
scm resolve -c  <conflicted file>  (use workspace version to resolve the conflict)
scm status -C (view no conflict sign "!" or "#")
scm deliver -c <outgoing change set>
```

Change follow target
```
scm workspace change-target <current workspace> <target workspace>  (change workspace flow target)
scm workspace change-target "pmc_mainline_ws1"  "pmc_mainline_ws2"
```