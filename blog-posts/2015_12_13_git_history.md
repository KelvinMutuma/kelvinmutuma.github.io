### **GIT HISTORY**

Today we are going at how to view the history of a git versioned project.


```
git log
```

This gives a listing of the commit history of a project

```
mutuma@bric gitlab-development-kit (master) $ git log
commit 1337d923a72a1053e0887ba98f546c7851089e8f
Merge: 07ca606 f4f7c58
Author: Jacob Vosmaer <contact@jacobvosmaer.nl>
Date:   Thu Nov 26 15:33:14 2015 +0000

    Merge branch 'fedora' into 'master'

    Fedora in install instructions



    See merge request !85

commit 07ca6060e55eef5e08f96af95be375ac2e5cac98
Merge: 35a669d d514e34
Author: Jacob Vosmaer <contact@jacobvosmaer.nl>
Date:   Tue Nov 24 16:57:19 2015 +0000

    Merge branch 'install-dependencies-from-package' into 'master'

    Install dependencies from package

    Some more improvements to the Vagrantfile and documentation.

:
```

You can press `q` to exit the prompt.

As you can see this returns a very large output and many not suffice for a quick check/investigation when you want to view a commit that was made a long time ago.

Now lets drill into this command further

#### One Line Histories

This gives us more control over what the log command displays.

1. ##### git log --pretty=oneline

```
mutuma@bric gitlab-development-kit (master) $ git log --pretty=oneline
1337d923a72a1053e0887ba98f546c7851089e8f Merge branch 'fedora' into 'master'
07ca6060e55eef5e08f96af95be375ac2e5cac98 Merge branch 'install-dependencies-from-package' into 'master'
f4f7c5833ddfbdd88c428cd40cc1fc8890fe871e Remove prerequisite
99bae88307ee957f6d755727c60449e6517b0510 Merge branch 'master' into fedora
35a669d971d4e681d44dffc2db3d2c4479384887 Merge branch 'disable-nfs-on-osx' into 'master'
d514e345a17fc4e2386dd181d1fb9dd7f5a9560f Update README to include Go PPA instructions for Ubuntu
b24771807efdd7c5a3da263cbbab6928de56a4e6 Install recent Go and RVM from packages
ee40b586180f8d207177d6076904d577b23d1417 Disable NFS on OS X
836de054e4f852eb0ad13d45bbb8d40e14068c52 Merge branch 'readme' into 'master'
796b0fe6bb031228d2d6a54706d4f799c29062e2 Users need to install the requirements for development-kit before starting foreman etc
d46963645e530ce36314eef2a4d2341fcb6a6202 Add fedora to the install instructions
51eb2b3a26ebf3289ab40ffbf5a4c1c6ed17f087 Add Fedora to install guide
e1410ae29333ccb88082bf3497d6a327d948fe9b Merge branch 'elaborate-on-port' into 'master'
da941a0707c1ed71ef5a1debbb50a03e47de5c5d elaborate on post-installation instructions
879da864564ff5d0b1f5728ba05970ae8c543f12 Merge branch 'master' into 'master'
f88070be0883b0b1d262ae841d7655b0819cc07c Fix-up items missed by !79 for #63
03db4599aaaa4ec9d4653da02e0070aa9d210e31 Merge branch 'master' into 'master'
90bbc5dc9021abd7b9cf87506def2fbfd308f4c2 Update table-of-contents.
```

2. #### Controlling Which Entries are Displayed

There are a lot of options for selecting which entries are displayed in the log. Play around with the following options:

`git log --pretty=oneline --max-count=2`: prints the last 2 commits
`git log --pretty=oneline --since='5 minutes ago'`: print all commits made in the last 5 minutes
`git log --pretty=oneline --since='5 days ago'`: print all commits made in the last 5 days
`git log --pretty=oneline --since='3 weeks ago'`: print all commits made in the last 3 weeks
`git log --pretty=oneline --until='5 minutes ago'`: print all commits made before 5 minutes ago
`git log --pretty=oneline --until='5 days ago'`: print all commits made before 5 days ago
`git log --pretty=oneline --until='3 weeks ago'`: print all commits made befire the last 3 weeks
`git log --pretty=oneline --author=<your name>`: print all commits made by the specified author/person
`git log --pretty=oneline --all`: print all commits

You can also specify `year` and `month` when using the  `--since` and `--until` time specifiers

3. #### Getting Fancy

`git log --all --pretty=format:'%h %cd %s (%an)' --since='7 weeks ago'`: Allow me to see all the commits made in the last 7 weeks with the abbreviated commit hash, commit date, time, timezone, commit message and author

Example:

```
mutuma@bric gitlab-development-kit (master) $ git log --all --pretty=format:'%h %cd %s (%an)' --since='3 weeks ago'
1337d92 Thu Nov 26 15:33:14 2015 +0000 Merge branch 'fedora' into 'master' (Jacob Vosmaer)
07ca606 Tue Nov 24 16:57:19 2015 +0000 Merge branch 'install-dependencies-from-package' into 'master' (Jacob Vosmaer)
f4f7c58 Tue Nov 24 15:36:20 2015 +0100 Remove prerequisite (Zeger-Jan van de Weg)
99bae88 Tue Nov 24 15:30:07 2015 +0100 Merge branch 'master' into fedora (Zeger-Jan van de Weg)
35a669d Tue Nov 24 12:10:01 2015 +0000 Merge branch 'disable-nfs-on-osx' into 'master' (Jacob Vosmaer)
```

By appending `--author=<author name>` to the command, you are able to distil to only the commits made by the user in that period

e.g.

```
mutuma@bric gitlab-development-kit (master) $ git log --all --pretty=format:'%h %cd %s (%an)' --since='3 weeks ago' --author="jacob"
1337d92 Thu Nov 26 15:33:14 2015 +0000 Merge branch 'fedora' into 'master' (Jacob Vosmaer)
07ca606 Tue Nov 24 16:57:19 2015 +0000 Merge branch 'install-dependencies-from-package' into 'master' (Jacob Vosmaer)
35a669d Tue Nov 24 12:10:01 2015 +0000 Merge branch 'disable-nfs-on-osx' into 'master' (Jacob Vosmaer)
```

4. **JIM WEIRICH'S history command**

`git log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short`

`%h`: abbreviated commit hash
`%ad`: author date
`%s`: commit message
`%d`: any decorations on that commit e.g. Branches, HEAD and tags
`%an`: author name
`--graph`: display the commit tree in ASCII graph layout
`--date=short`: keeps the date format nice and short

Example

```
mutuma@bric gitlab (fix-workhorse-upgrade-info) $ git log --pretty=format'%h %ad | %s%d [%an]' --graph --date=short
* formatd00d344 2015-12-08 | Remove the prepended v on GitLab Workhorse upgrade doc (HEAD -> fix-workhorse-upgrade-info, origin/fix-workhorse-upgrade-info) [Kelvin]
*   format792f2bb 2015-12-08 | Merge branch 'bump-gollum-version' into 'master' (origin/master, origin/HEAD, master) [Valery Sizov]
|\
| * formatf36fe92 2015-12-08 | Bump gollum-lib to 4.1.0 and fix dependency mismatch with rouge [Stan Hu]
* |   format51ed522 2015-12-08 | Merge branch 'serve_lfs_object' into 'master' [Douwe Maan]
|\ \
| * | format6245be0 2015-12-08 | All for you rubocop. [Marin Jankovski]
| * | formatea5b462 2015-12-08 | Stub the calls to disk and check what send_file returns. [Marin Jankovski]
| * | format9bf51ae 2015-12-08 | Fix specs caused by update of gitlab-test repo. [Marin Jankovski]
| * | formatbf17609 2015-12-07 | Rename blob helper, bump version of gitlab_git to 7.2.21. [Marin Jankovski]
| * | formate53b350 2015-12-07 | Add specs for showing lfs object in UI. [Marin Jankovski]
| * | formatb2c4675 2015-12-04 | Recursivity needed if a fork is a fork of a fork. [Marin Jankovski]
| * | formatb9a0f96 2015-12-04 | Don't show diffs for lfs pointers. [Marin Jankovski]
| * | formatea52a81 2015-12-03 | Move the file serving to Raw controller, add a few ifs to view. [Marin Jankovski]
| * | format0a081e7 2015-12-03 | If a user clicks on the LFS object, it should be served if the user has access to the object. [Marin Jankovski]
* | |   formatf5430e4 2015-12-08 | Merge branch 'rs-validators' into 'master' [Douwe Maan]
|\ \ \
| * | | format2379c8b 2015-12-07 | Inline Gitlab::Blacklist in NamespaceValidator [Robert Speicher]
| * | | format175f482 2015-12-07 | Add custom NamespaceNameValidator [Robert Speicher]
| * | | format9321d38 2015-12-07 | Add custom NamespaceValidator [Robert Speicher]
| * | | formatad6a771 2015-12-01 | Add custom LineCodeValidator [Robert Speicher]
| * | | format96e51a0 2015-12-01 | Minor EmailValidator refactor [Robert Speicher]
| * | | formate48391b 2015-12-01 | Add custom ColorValidator [Robert Speicher]
| * | | formatb3200c8 2015-12-01 | Move EmailValidator to app/validators [Robert Speicher]
| * | | formatd5ea934 2015-12-01 | Add custom UrlValidator [Robert Speicher]
* | | |   format1d605f6 2015-12-08 | Merge branch 'fix-merge-request-that-removes-submodule' into 'master' [Douwe Maan]
|\ \ \ \
| |_|_|/
|/| | |
| * | |   formatf7aafd8 2015-12-07 | Merge branch 'master' into fix-merge-request-that-removes-submodule [Douglas Barbosa Alexandre]
| |\ \ \
| * \ \ \   format7d836a0 2015-12-07 | Merge branch 'master' into fix-merge-request-that-removes-submodule [Douglas Barbosa Alexandre]
| |\ \ \ \
| * | | | | format12fdc13 2015-12-04 | Fix 500 error when creating a merge request that removes a submodule [Douglas Barbosa Alexandre]
* | | | | |   format7f90c8e 2015-12-08 | Merge branch 'gemfile_fix' into 'master' [Valery Sizov]
```

I always remove the `--date=short` part so that I am able to see the time the commit was made. 
I also usually append `--since=<specify period>` to get all commits made in a certain period in the fancy format.

Example:

```
git log --pretty=format'%h %ad | %s%d [%an]' --graph --since='4 weeks ago'
* formatd00d344 Tue Dec 8 18:23:30 2015 +0300 | Remove the prepended v on GitLab Workhorse upgrade doc (HEAD -> fix-workhorse-upgrade-info, origin/fix-workhorse-upgrade-info) [Kelvin]
*   format792f2bb Tue Dec 8 14:53:05 2015 +0000 | Merge branch 'bump-gollum-version' into 'master' (origin/master, origin/HEAD, master) [Valery Sizov]
|\
| * formatf36fe92 Tue Dec 8 04:43:17 2015 -0800 | Bump gollum-lib to 4.1.0 and fix dependency mismatch with rouge [Stan Hu]
* |   format51ed522 Tue Dec 8 14:19:52 2015 +0000 | Merge branch 'serve_lfs_object' into 'master' [Douwe Maan]
|\ \
| * | format6245be0 Tue Dec 8 14:00:15 2015 +0100 | All for you rubocop. [Marin Jankovski]
| * | formatea5b462 Tue Dec 8 13:33:12 2015 +0100 | Stub the calls to disk and check what send_file returns. [Marin Jankovski]
| * | format9bf51ae Tue Dec 8 10:58:15 2015 +0100 | Fix specs caused by update of gitlab-test repo. [Marin Jankovski]
| * | formatbf17609 Mon Dec 7 15:56:38 2015 +0100 | Rename blob helper, bump version of gitlab_git to 7.2.21. [Marin Jankovski]
| * | formate53b350 Mon Dec 7 15:03:50 2015 +0100 | Add specs for showing lfs object in UI. [Marin Jankovski]
| * | formatb2c4675 Fri Dec 4 12:32:13 2015 +0100 | Recursivity needed if a fork is a fork of a fork. [Marin Jankovski]
| * | formatb9a0f96 Fri Dec 4 12:01:08 2015 +0100 | Don't show diffs for lfs pointers. [Marin Jankovski]
| * | formatea52a81 Thu Dec 3 17:08:09 2015 +0100 | Move the file serving to Raw controller, add a few ifs to view. [Marin Jankovski]
| * | format0a081e7 Thu Dec 3 14:59:10 2015 +0100 | If a user clicks on the LFS object, it should be served if the user has access to the object. [Marin Jankovski]
* | |   formatf5430e4 Tue Dec 8 08:42:17 2015 +0000 | Merge branch 'rs-validators' into 'master' [Douwe Maan]
|\ \ \
| * | | format2379c8b Mon Dec 7 16:29:39 2015 -0500 | Inline Gitlab::Blacklist in NamespaceValidator [Robert Speicher]
| * | | format175f482 Mon Dec 7 16:17:24 2015 -0500 | Add custom NamespaceNameValidator [Robert Speicher]
| * | | format9321d38 Mon Dec 7 16:17:12 2015 -0500 | Add custom NamespaceValidator [Robert Speicher]
| * | | formatad6a771 Tue Dec 1 19:30:01 2015 -0500 | Add custom LineCodeValidator [Robert Speicher]
| * | | format96e51a0 Tue Dec 1 19:21:45 2015 -0500 | Minor EmailValidator refactor [Robert Speicher]
| * | | formate48391b Tue Dec 1 18:53:44 2015 -0500 | Add custom ColorValidator [Robert Speicher]
| * | | formatb3200c8 Tue Dec 1 18:46:00 2015 -0500 | Move EmailValidator to app/validators [Robert Speicher]
| * | | formatd5ea934 Tue Dec 1 18:45:36 2015 -0500 | Add custom UrlValidator [Robert Speicher]
* | | |   format1d605f6 Tue Dec 8 08:36:23 2015 +0000 | Merge branch 'fix-merge-request-that-removes-submodule' into 'master' [Douwe Maan]
* ```

### Other Tools

Both gitx (for Macs) and gitk (any platform) are useful in exploring log history.
