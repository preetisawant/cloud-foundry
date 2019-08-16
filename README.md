# cloud-foundry

## Publishing to test.cloud.ibm.com

Everything in the `staging` branch is automatically published.

## Moving content updates from test.cloud.ibm.com to cloud.ibm.com

Our documentation repo for CFEE production documentation is here:
https://github.com/IBM-Bluemix-Docs/cloud-foundry

1. Check production repo for updates and try to make sure these update are also reflected in our test.cloud.ibm repo (here)

   In order to do this with diff/patch checkout both repos (this one / and production) and do a diff

    `diff -c IBMDocsProd/cloud-foundry/ IBMDocsTest/cloud-foundry/ | grep -v '^Only in' | grep -v '^Common sub' > test2prod_20190705.patch`
    
1. The diff will be applied to the first directory of the previous command via:

   `patch -p0 -i test2prod_20190705.patch`
   
1. Change directory into the directory that contains the patched files, create a new branch, checkout the branch and push it to github.com

   ```
   git branch test2prod_20190705.patch
   git checkout test2prod_20190705.patch
   git add .
   git commit -m "syncing changes from test2prod_20190705.patch"
   git push --set-upstream origin test2prod_20190705.patch
   ```
   
1. Create a PR in github.com and request review & merge.
