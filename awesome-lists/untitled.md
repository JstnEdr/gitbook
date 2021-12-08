# Git

{% embed url="https://devconnected.com/how-to-clean-up-git-branches" %}

One liner to cleanup local branches: \
`git branch --merged | egrep -v "(^*|master|dev)" | xargs git branch -d`

``

``
