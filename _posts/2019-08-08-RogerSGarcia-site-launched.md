---
layout: post
title: "Git it, Don't Forget It !"
date: 2019-08-08
---

Getting started with Git? or if your familiar with working with Git, then you know it's always useful to bookmark or write down common Git commands. This tidbit is an effort to share (and as a reference for myself) common Git commands and some awesome resources I've come across so far.


![gitnotgithub](/images/gitnotgithub-200x400px.png){: .center-image }

Git is a version control tool, you install it locally (e.g <code>apt-get install git</code>) on computer if you don't have it already (<code>git --version</code>) and off you go. Github is a cloud-based hosting environment for Git projects along with additional features, such as branch protection rules!

<hr />

<h3 id="passing-a-copy--cvmat">Status, Branch, Checkout.</h3>
<p>Common if not the most common git commands likely to be used.</p>

<h3 id="passing-a-copy--cvmat"> <code class="highlighter-rouge">What's the situation</code>.</h3>
<pre class="sample"><code>$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add &lt;file&gt;..." to update what will be committed)
  (use "git checkout -- &lt;file&gt;..." to discard changes in working directory)

	<span class="redtext">modified:   _config.yml</span>
	<span class="redtext">modified:   css/custom.css</span>
	<span class="redtext">modified:   index.html</span>

Untracked files:
  (use "git add &lt;file&gt;..." to include in what will be committed)

	<span class="redtext">_posts/2019-08-04-RogerSGarcia-site-launched.md</span>


no changes added to commit (use "git add" and/or "git commit -a") </code></pre>


<h3> <code class="highlighter-rouge">Show me all branches</code>.</h3>
<pre class="sample"><code>$ git branch -a
<span class="yellowtext">* master</span>
  <span class ="redtext">rremotes/origin/HEAD</span> -> origin/master
  <spand class= "redtext">remotes/origin/master</spand></code></pre>



<h3> <code class="highlighter-rouge">Checkout a new local branch</code>.</h3>
In general, it is bad practice to always be pushing code to <code>master</code> branch, the great thing about git/github is that we can work on different hunks/issues of a project to then update the overall status of the project (or push) to <code>master</code>. I'm no exception so it's time I create a <code>dev</code> branch.
<pre class="sample"><code>$ git checkout -b dev
M _config.yml
M css/custom.css
M index.html
Switched to a new branch 'dev'
</code></pre>

<hr />
<h3 id="passing-a-copy--cvmat">Diff, Add, Commit, Push.</h3>

<h3> <code class="highlighter-rouge">What's change</code>.</h3>
<pre class="sample"><code>$ git diff _config.yml
diff --git a/_config.yml b/_config.yml
index 55f510a..27b9c67 100644
--- a/_config.yml
+++ b/_config.yml
@@ -4,6 +4,7 @@ name: Roger Garcia, Personal Website
 # Build settings
 markdown: kramdown
 permalink: /tidbits/:year/:month/:day/:title
<span class="yellowtext">+highlighter: rouge</span>

 collections:
   notes:
</code></pre>

<h3> <code class="highlighter-rouge">Add all tracked files</code>.</h3>
<p>Use <code>git add -u</code> or <code>git add -up</code> to interactively choose hunks which to add</p>

<pre class="sample"><code>$ git status
On branch dev
Changes to be committed:
  (use "git reset HEAD &lt;file&gt;..." to unstage)

  <span class="yellowtext">modified:   _config.yml</span>
  <span class="yellowtext">modified:   css/custom.css</span>
  <span class="yellowtext">modified:   index.html</span>

Untracked files:
  (use "git add &lt;file&gt;..." to include in what will be committed)

  <span class="redtext">_posts/2019-08-06-RogerSGarcia-site-launched.md
  git</span>
</code></pre>


<h3> <code class="highlighter-rouge">Commit changes</code>.</h3>
<pre class="sample"><code>$ git commit -m "initial commit" -m "updates to yaml file, css file and bio"
[dev b2ecb59] initial commit
 3 files changed, 30 insertions(+), 1 deletion(-)
</code></pre>


<h3> <code class="highlighter-rouge">Push to remote branch</code>.</h3>
Since we haven't set upstream we can do it during the push
<pre class="sample"><code>$ git push -u origin dev
Counting objects: 6, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (6/6), done.
Writing objects: 100% (6/6), 768 bytes | 768.00 KiB/s, done.
Total 6 (delta 5), reused 0 (delta 0)
remote: Resolving deltas: 100% (5/5), completed with 5 local objects.
remote:
remote: Create a pull request for 'dev' on GitHub by visiting:
remote:      https://github.com/RogerSGarcia/RogerSGarcia.github.io/pull/new/dev
remote:
To github.com:RogerSGarcia/RogerSGarcia.github.io.git
 * [new branch]      dev -> dev
Branch 'dev' set up to track remote branch 'dev' from 'origin'.
</code></pre>


<h3> <code class="highlighter-rouge">Show me commits on current branch</code>.</h3>
<pre class="sample"><code>$ git log</code></pre>

<pre class = "sample"><code>$ git log --all --decorate --oneline --graph
* b2ecb59 (HEAD -> dev, origin/dev) initial commit
* 8fba3c1 (origin/master, origin/HEAD, master) cv and more
* 54b97ee content
* a263270 minor edits/changes
* 1680ef5 edits to content
* 3aa76b4 fixes for mobile-s
* 15a2f69 minor fixes
* 7e49da0 new tidbit post
* 5ec4c56 adding content
* a9d942f minor fixes
* 056cb95 navbar changes
* 6b7f452 navbar changes
* c8372fb navbar changes
* 0ccc577 Using Bootstrap with Jekyll
* 993c69c minor changes
* d4b3c3f adding about and cv
* 3756d6c layout for Jekyll
* 09a5894  adding css file
* 2a917b8 updating index.html
* e3a248c Hello World commit
* 1923a0c Initial commit
</code></pre>

<hr />

<h3>Merge </h3>
<p>Well, it's time I push to <code>master</code> my commits from <code>dev</code>, to do so there's this one part I always find myself looking up again and again just to double check!.</p>

<p>If I want changes from <code>dev</code> to go onto <code>master</code>, I want to be in the <code>master</code> branch before I merge. In other words, to determine merge direction go to branch that "knows" less and <code>merge</code> or bring that knowledge over there! and hope there's no conflicts (more on that later)</p>

<h3> <code class="highlighter-rouge">Pass on the knowledge by merging</code>.</h3>
<pre class="sample"><code>$ git checkout master</code></pre>

<hr />


<h3>Prune and Cleanup.</h3>
<p>Different variations of commands to prune/clean local branches.</p>

<h3> <code class="highlighter-rouge">Show me what branches can be pruned</code>.</h3>
<p>To actually remove, same command but remove <code>--dry-run</code></p>
<pre class="sample"><code>$ git remote prune origin --dry-run</code></pre>

<h3> <code class="highlighter-rouge">Synchronize local branches to remote</code>.</h3>
<p>At times, others on the team will update/merge branches and <code>git pull</code> won't remove those lagging local branches,
run the following command to list which are "gone": </p>

<pre class="sample"><code>$ git branch -vv | grep 'origin/.*: gone]' | awk '{print $1}' </code></pre>

<p>To actually remove, same command but pipe it to <code>git branch -d</code></p>

<pre class="sample"><code>$ git branch -vv | grep 'origin/.*: gone]' | awk '{print $1}' | xargs git branch -d </code></pre>

<hr />


<hr />

<h3>Awesome Resources</h3>

<div class="container">
   <h6 class="text-muted">What is it</h6>

  <dl class="row">
    <dt class="col-sm-3">Interactive Git Cheatsheet</dt>
    <dd class="col-sm-9"><a href="http://ndpsoftware.com/git-cheatsheet.html" class="btn btn-info" role="button">Link</a> to NDPSoftware</dd>
    <dt class="col-sm-3"></dt><dd class="col-sm-9"></dd>
    <dt class="col-sm-3">Visualize Git Commands</dt>
    <dd class="col-sm-9"><a href="https://git-school.github.io/visualizing-git/" class="btn btn-info" role="button">Link</a> to Git-School</dd>
  </dl>

</div>
