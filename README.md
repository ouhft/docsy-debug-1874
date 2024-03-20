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

... initial commit time.
