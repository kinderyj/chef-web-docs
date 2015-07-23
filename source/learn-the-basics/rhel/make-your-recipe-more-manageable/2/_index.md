## 2. Create a template

Now we'll move the home page to an external file. First, run this command to generate the HTML file for our home page.

```bash
# ~/chef-repo/cookbooks
$ chef generate template learn_chef_httpd index.html
```

The file <code class="file-path">index.html.erb</code> gets created under <code class="file-path">learn\_chef\_httpd/templates/default</code>.

```bash
# ~/chef-repo/cookbooks
$ tree
.
└── learn_chef_httpd
    ├── Berksfile
    ├── chefignore
    ├── metadata.rb
    ├── README.md
    ├── recipes
    │   └── default.rb
    └── templates
        └── default
            └── index.html.erb

4 directories, 6 files
```

The .erb extension simply means that the file can have placeholders. More on that later.

Now copy the contents of the HTML file from your recipe to the new HTML file, <code class="file-path">index.html.erb</code>.

```html
<!-- ~/chef-repo/cookbooks/learn_chef_httpd/templates/default/index.html.erb -->
<html>
  <body>
    <h1>hello world</h1>
  </body>
</html>
```