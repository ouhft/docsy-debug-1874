# docsy-debug-1874

Test Site for diagnosing the issue in https://github.com/google/docsy/issues/1874

## Local setup steps

1.  `mkdir docsy-debug-1874` & `cd docsy-debug-1874/`
2.  `git clone https://github.com/ouhft/docsy-debug-1874.git ./docsy-debug-1874-repo` & `cd docsy-debug-1874-repo/`
    -   Create `.gitignore` and populate with minimal content
3.  `hugo new site docs`

    -   `Congratulations! Your new Hugo site was created in /Users/carl/Projects/github/ouhft/docsy-debug-1874/docsy-debug-1874-repo/docs.`

4.  `cd docs`
5.  `hugo mod init github.com/ouhft/docsy-debug-1874`
6.  `hugo mod get github.com/google/docsy@1929a65ccffb316006de9c0daaee631a7d8fc225`
7.  `mkdir -p content/en`
8.  Rename `hugo.toml` to `hugo.yaml`, then edit content to what is shown in current commit
9.  Run `hugo --cleanDestinationDir --gc --templateMetrics --logLevel debug` and store output into `/build.txt`

... initial commit time. Build successful

1.  Modify hugo.yaml to add module config
2.  Run `hugo --cleanDestinationDir --gc --templateMetrics --logLevel debug` and store output into `/build.txt`

... second commit. Build failed

1.  Add `package.json` to `/docs`
2.  Run `npm install`
3.  Run `hugo --cleanDestinationDir --gc --templateMetrics --logLevel debug` and store output into `/build.txt`

... third commit. Build successful

1.  Add `content/en/_index.md`
2.  Run `hugo --cleanDestinationDir --gc --templateMetrics --logLevel debug` and store output into `/build.txt`

Error has returned:
```
Error: error building site: render: failed to render pages: render of "taxonomy" failed: "/Users/carl/.local/share/hugo/modules/filecache/modules/pkg/mod/github.com/google/docsy@v0.9.2-0.20240315194958-1929a65ccffb/layouts/docs/list.html:12:5": execute of template failed: template: docs/list.html:12:5: executing "main" – File is nil; wrap it in if or with: {{ with partial "section-index.html" .>: error calling partial: "/Users/carl/.local/share/hugo/modules/filecache/modules/pkg/mod/github.com/google/docsy@v0.9.2-0.20240315194958-1929a65ccffb/layouts/partials/section-index.html:8:69": execute of template failed: template: partials/section-index.html:8:69: executing "partials/section-index.html" at <.File }}{{ .UniqueID }}{{ end }}
```

... fourth commit. Build failed

1.  Edit `_index.md`, remove the `cascade` frontmatter.
2.  Run `hugo --cleanDestinationDir --gc --templateMetrics --logLevel debug` and store output into `/build.txt`

This one fails on a more basic issue: `ERROR [en] REF_NOT_FOUND: Ref "/getting-started/migration.md": "/Users/carl/Projects/github/ouhft/docsy-debug-1874/docsy-debug-1874-repo/docs/content/en/_index.md:16:77": page not found`

... fifth commit. Build failed

1.  Edit `_index.md` to remove obvious issues with missing links. Add `type: docs` to frontmatter
2.  Run `hugo --cleanDestinationDir --gc --templateMetrics --logLevel debug` and store output into `/build.txt`

Also, `hugo server` tested to see the output. With the exception that the `readfile` shortcode isn't producing output (but if the path is changed, will produce an error!), the rest looks about right.

... sixth commit. Build successful
