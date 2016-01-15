* https://webkit.org/contributing-code/
* http://trac.webkit.org/wiki/UsingGitWithWebKit
* Some information of http://trac.webkit.org/wiki/QtWebKitContrib is still relevant

How I (annulen) do it now:

1. Create feature branch from master
2. Develop or cherry-pick patch implementing feature. Next steps expect that feature is implemented as exactly 1 commit on top of master.
3. Run Tools/Scripts/check-webkit-style, fix any errors it finds
4. Open new bug on https://bugs.webkit.org in WebKit product, choose proper component, use the same bug title as git commit title. Put in some description, e.g. description from git commit.
5. Tools/Scripts/prepare-ChangeLog -b <your new bug id> -g HEAD
6. Fix changes in ChangeLog files
7. Tools/Scripts/webkit-patch upload --request-commit -g HEAD

* In my setup upstream WebKit is cloned from git://git.webkit.org/WebKit.git, it is my "origin" remote. Master of annulen/webkit is periodically synced with upstream, but tends to be outdated. Mirrot at WebKit/webkit tends to lag behind git.webkit.org, but very slightly.
* If you are not sure in your patch and you need us to review it before upstream reviewers, at step 7 use

    Tools/Scripts/webkit-patch upload --no-review -g HEAD

Look at Tools/Scripts/webkit-patch --help and Tools/Scripts/webkit-patch help upload for more details