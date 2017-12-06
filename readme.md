<article class="markdown-body entry-content" itemprop="text"><h1><a href="#roles-permissions-laravel-rpl" aria-hidden="true" class="anchor" id="user-content-roles-permissions-laravel-rpl"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Roles Permissions Laravel (RPL)</h1>
<p>A stater kit with Roles and Permissions implementation on Laravel 5.4</p>
<h3><a href="#install" aria-hidden="true" class="anchor" id="user-content-install"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Install</h3>
<ol>
<li>To use it just clone the repo and composer install.</li>
<li>Set the database connection</li>
<li>To test the app run <code>php artisan db:seed</code>, our <a href="http://www.qcode.in/advance-interactive-database-seeding-in-laravel/" rel="nofollow">interactive seeder</a> will take care of everything.</li>
</ol>
<h3><a href="#add-a-new-resource" aria-hidden="true" class="anchor" id="user-content-add-a-new-resource"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Add a new Resource</h3>
<ol>
<li>Create desired resource by running</li>
</ol>
<div class="highlight highlight-source-shell"><pre><span class="pl-c"><span class="pl-c">#</span># Create Comment model with migration and resource controller</span>
php artisan make:model Comment -m -c --resource</pre></div>
<ol start="2">
<li>Register route for it.</li>
</ol>
<div class="highlight highlight-text-html-php"><pre><span class="pl-s1"><span class="pl-c1">Route</span><span class="pl-k">::</span>group( [<span class="pl-s"><span class="pl-pds">'</span>middleware<span class="pl-pds">'</span></span> <span class="pl-k">=&gt;</span> [<span class="pl-s"><span class="pl-pds">'</span>auth<span class="pl-pds">'</span></span>]], <span class="pl-k">function</span>() {</span>
<span class="pl-s1">    <span class="pl-k">...</span></span>
<span class="pl-s1">    <span class="pl-c1">Route</span><span class="pl-k">::</span>resource(<span class="pl-s"><span class="pl-pds">'</span>comments<span class="pl-pds">'</span></span>, <span class="pl-s"><span class="pl-pds">'</span>CommentController<span class="pl-pds">'</span></span>);</span>
<span class="pl-s1">});</span></pre></div>
<ol start="3">
<li>Now implement your controllers methods and use the <code>Authorizable</code> trait</li>
</ol>
<div class="highlight highlight-text-html-php"><pre><span class="pl-s1"><span class="pl-k">use</span> <span class="pl-c1">App\Authorizable</span>;</span>
<span class="pl-s1"></span>
<span class="pl-s1"><span class="pl-k">class</span> <span class="pl-en">CommentController</span> <span class="pl-k">extends</span> <span class="pl-e">Controller</span></span>
<span class="pl-s1">{</span>
<span class="pl-s1">    <span class="pl-k">use</span> <span class="pl-c1">Authorizable</span>;</span>
<span class="pl-s1">    <span class="pl-k">...</span></span></pre></div>
<ol start="4">
<li>Now add the permissions for this new <code>Comment</code> model.</li>
</ol>
<div class="highlight highlight-source-shell"><pre>php artisan auth:permission Comment</pre></div>
<p>That's it, you have added new resource controller which have full access control by laravel permissions.</p>
<h3><a href="#authpermission-command" aria-hidden="true" class="anchor" id="user-content-authpermission-command"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>auth:permission command</h3>
<p>This command can be user to add or remove permission for a given model</p>
<div class="highlight highlight-source-shell"><pre><span class="pl-c"><span class="pl-c">#</span># add permission</span>
php artisan auth:permission Comment

<span class="pl-c"><span class="pl-c">#</span># remove permissions</span>
php artisan auth:permission Comment --remove</pre></div>
<h3><a href="#author" aria-hidden="true" class="anchor" id="user-content-author"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>Author</h3>
<p>Created by Shyam Sasi T</p>
<h2><a href="#license" aria-hidden="true" class="anchor" id="user-content-license"><svg aria-hidden="true" class="octicon octicon-link" height="16" version="1.1" viewBox="0 0 16 16" width="16"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>License</h2>
<p><a href="http://opensource.org/licenses/MIT" rel="nofollow">MIT license</a>.</p>
</article>
