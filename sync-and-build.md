# MkDocs Material
# Container image with MkDocs and squidfunks material theme. 
# 
# Below commands synchronize squidfunks repo with the local repo and merges it into my own repo. 
# Only important change here is the 'ENTRYPOINT' of squidfunks image
# This disables shell access when used in a GitLab runner.
# Furthermore support for plantuml is added

# Nice to have is automating the flow on a change in the original repository.

# Fix needed for external links

# One time to setup the "upstream"
# git remote -v
# git remote add upstream git@github.com:squidfunk/mkdocs-material.git
# git remote -v 
# origin    git@github.com:tIsGoud/mkdocs-material.git (fetch)
# origin    git@github.com:tIsGoud/mkdocs-material.git (push)
# upstream    git@github.com:squidfunk/mkdocs-material.git (fetch)
# upstream    git@github.com:squidfunk/mkdocs-material.git (push)

# Fetch the upstream repository. Commits to `master` will be stored in a local branch, `upstream/master`.
git fetch upstream

# Checkout your fork's local master branch
git checkout master

# Merge changes from the `upstream/master` into your local `master` branch. This brings your fork's master branch into sync with the upstream repository, without losing your local changes.
git merge upstream/master

# "Fetching and Merging" to deal with the fast-forward errors
git pull origin master

# Update your fork 
git push origin master

# Build this with (do note the '.' at the end of the line):
docker build -t tisgoud/mkdocs-material .

# Publish the image with
docker push tisgoud/mkdocs-material:latest
